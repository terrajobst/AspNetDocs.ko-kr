---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: ASP.NET Web Forms에서 Visual Studio 2012에 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 페이지 검사기은 통합 브라우저를 사용 하는 웹 개발 도구입니다. 통합 브라우저에서 요소를 선택 하 고 페이지 검사기 ...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464945"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a><span data-ttu-id="c002b-104">ASP.NET Web Forms에서 Visual Studio 2012용 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="c002b-104">Using Page Inspector for Visual Studio 2012 in ASP.NET Web Forms</span></span>

<span data-ttu-id="c002b-105">사람, Tim Am마나트 n</span><span class="sxs-lookup"><span data-stu-id="c002b-105">by Tim Ammann</span></span>

> <span data-ttu-id="c002b-106">Visual Studio 2012 페이지 검사기은 통합 브라우저를 사용 하는 웹 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-106">Page Inspector for Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="c002b-107">통합 브라우저에서 요소를 선택 하 고 페이지 검사기 요소의 원본 및 CSS를 즉시 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="c002b-108">응용 프로그램의 모든 페이지를 찾아보고, 렌더링 된 태그의 소스를 빠르게 찾고, Visual Studio 환경 내에서 브라우저 도구를 바로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-108">You can browse any page in your application, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> <span data-ttu-id="c002b-109">이 자습서에서는 검사 모드을 사용 하도록 설정한 다음 웹 프로젝트 내에서 CSS 규칙과 텍스트를 빠르게 찾고 편집 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-109">This tutorial shows how to enable Inspection Mode and then quickly locate and edit CSS rules and text within your web project.</span></span> <span data-ttu-id="c002b-110">이 자습서에서는 Web Forms 응용 프로그램 프로젝트를 사용 하지만 웹 사이트 프로젝트 및 [MVC](https://go.microsoft.com/?linkid=9802002) 응용 프로그램에 페이지 검사기를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-110">The tutorial uses a Web Forms Application Project, but you can also use Page Inspector for Web Site projects and [MVC](https://go.microsoft.com/?linkid=9802002) applications.</span></span>
> 
> <span data-ttu-id="c002b-111">이 자습서에는 다음과 같은 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-111">The tutorial has the following sections:</span></span>
> 
> [<span data-ttu-id="c002b-112">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c002b-112">Prerequisites</span></span>](#_1_prerequisites)
> 
> [<span data-ttu-id="c002b-113">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c002b-113">Create a Web Application</span></span>](#_2_creating_a)
> 
> [<span data-ttu-id="c002b-114">페이지 검사기를 사용 하 여 응용 프로그램 보기</span><span class="sxs-lookup"><span data-stu-id="c002b-114">Use Page Inspector to View the Application</span></span>](#_3_using_page)
> 
> [<span data-ttu-id="c002b-115">검사 모드 사용</span><span class="sxs-lookup"><span data-stu-id="c002b-115">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> 
> [<span data-ttu-id="c002b-116">페이지 검사기를 사용 하 여 태그 변경</span><span class="sxs-lookup"><span data-stu-id="c002b-116">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> 
> [<span data-ttu-id="c002b-117">검사 모드 및 HTML 창</span><span class="sxs-lookup"><span data-stu-id="c002b-117">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> 
> [<span data-ttu-id="c002b-118">스타일 창에서 CSS 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="c002b-118">Preview CSS Changes in the Styles Window</span></span>](#_7_previewing_css)
> 
> [<span data-ttu-id="c002b-119">CSS 자동 동기화</span><span class="sxs-lookup"><span data-stu-id="c002b-119">CSS Auto Sync</span></span>](#css_auto_sync)
> 
> [<span data-ttu-id="c002b-120">CSS 색 선택 사용</span><span class="sxs-lookup"><span data-stu-id="c002b-120">Using the CSS Color Picker</span></span>](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="c002b-121">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c002b-121">Prerequisites</span></span>

- <span data-ttu-id="c002b-122">웹 용 [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) 또는 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/downloads#express-web)</span><span class="sxs-lookup"><span data-stu-id="c002b-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="c002b-123">최신 버전의 페이지 검사기을 다운로드 하려면 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=255386) 를 사용 하 여 Azure SDK for .net 2.0을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-123">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="c002b-124">페이지 검사기 Microsoft Web 개발자 도구와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-124">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="c002b-125">최신 버전은 1.3입니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-125">The latest version is 1.3.</span></span> <span data-ttu-id="c002b-126">보유 한 버전을 확인 하려면 Visual Studio를 실행 하 고 **도움말** 메뉴에서 **정보 Microsoft Visual Studio** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-126">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="c002b-127">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c002b-127">Create a Web Application</span></span>

<span data-ttu-id="c002b-128">먼저 페이지 검사기 사용할 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-128">First, you will create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="c002b-129">Visual Studio에서 **파일** &gt; **새 프로젝트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-129">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="c002b-130">왼쪽에서 **시각적 C#개체** 를 확장 하 고 **웹**을 선택한 다음 **ASP.NET Web Forms 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-130">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET Web Forms Application**.</span></span>

![새 Web Forms 응용 프로그램](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

<span data-ttu-id="c002b-132">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-132">Click **OK**.</span></span>

<span data-ttu-id="c002b-133">응용 프로그램이 **소스** 뷰에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-133">The application opens in **Source** view.</span></span>

![소스 뷰의 새 Web Forms 응용 프로그램](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

<span data-ttu-id="c002b-135">이제 작업할 응용 프로그램이 있으므로 페이지 검사기를 사용 하 여 검사 하 고 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-135">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a><span data-ttu-id="c002b-136">페이지 검사기를 사용 하 여 응용 프로그램 보기</span><span class="sxs-lookup"><span data-stu-id="c002b-136">Use Page Inspector to View the Application</span></span>

<span data-ttu-id="c002b-137">다음에는 페이지 검사기를 사용 하 여 응용 프로그램을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-137">Next, you will view the application with Page Inspector.</span></span> <span data-ttu-id="c002b-138">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **페이지 검사기에서 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-138">In **Solution Explorer**, right click the project, and then choose **View in Page Inspector**.</span></span>

![페이지 검사기에서 보기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

<span data-ttu-id="c002b-140">기본적으로 페이지 검사기 처음 시작 하는 경우 Visual Studio 환경의 왼쪽에 좁은 창으로 도킹 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-140">By default, when Page Inspector launches for the first time, it is docked as a narrow window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="c002b-141">왼쪽에 도킹 된 상태로 두고 사용자에 게 친숙 한 너비로 설정 하거나 위쪽, 아래쪽 또는 오른쪽의 도구 영역 중 하나에 도킹 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-141">Leave it docked on the left side and set it to a width that is comfortable for you, or dock it in one of the tool areas on the top, bottom, or right:</span></span>

![페이지 검사기 도킹 위치](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

<span data-ttu-id="c002b-143">페이지 검사기 창의 도킹을 해제 하는 경우 Visual Studio 외부 또는 두 번째 모니터 (있는 경우)에도 놓을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-143">If you undock the Page Inspector window, you can place it outside Visual Studio, or even on a second monitor if you have one.</span></span> <span data-ttu-id="c002b-144">그러나 페이지 검사기 창이 도킹 해제 될 때 페이지 검사기와 Visual Studio 사이에서 ALT + TAB을 실행 하려면 **도구** &gt; **옵션** &gt; **환경** &gt; **탭 및 창**으로 이동 하 고, **탭 웰**에서 **부동 도구 창**이라는 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-144">However, in order to ALT+TAB between Page Inspector and Visual Studio when the Page Inspector window is undocked, go to **Tools** &gt; **Options** &gt; **Environment** &gt; **Tabs and Windows**, and under **Tab Well**, clear the check box called **Floating tool windows always stay on top of the main window**:</span></span>

![부동 도구 창 확인란의 선택을 취소 하 고 Visual Studio와 도킹 되지 않은 페이지 검사기 창 사이에서 ALT + TAB을 선택 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

<span data-ttu-id="c002b-146">페이지 검사기 창의 위쪽 창에는 브라우저 창의 현재 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-146">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="c002b-147">아래쪽 창에는 왼쪽의 HTML 태그에 페이지가 표시 되 고 오른쪽에는 페이지의 다양 한 측면을 검사할 수 있는 탭이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-147">The bottom pane shows the page in HTML markup on the left, and some tabs on the right that let you inspect different aspects of the page.</span></span> <span data-ttu-id="c002b-148">아래쪽 창은 Internet Explorer의 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478) 와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-148">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span> <span data-ttu-id="c002b-149">그러나 개발자 도구와 달리 Visual Studio 내에서 페이지 검사기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-149">(However, unlike the developer tools, you can use Page Inspector right within Visual Studio.)</span></span>

![페이지 검사기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

<span data-ttu-id="c002b-151">이 자습서에서는 응용 프로그램을 신속 하 게 탐색 하 고 변경 하는 데 도움이 되는 페이지 검사기 브라우저 창과 **HTML** 및 **스타일** 탭을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-151">In this tutorial, you will use the Page Inspector browser pane, and the **HTML** and **Styles** tabs to help you rapidly navigate and make changes to the application.</span></span>

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a><span data-ttu-id="c002b-152">검사 모드 사용</span><span class="sxs-lookup"><span data-stu-id="c002b-152">Enable Inspection Mode</span></span>

<span data-ttu-id="c002b-153">다음으로 페이지 검사기 검사 모드 작동 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-153">Next, you will see how Page Inspector's Inspection Mode works.</span></span> <span data-ttu-id="c002b-154">페이지 검사기 창에서 **검사** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-154">In the Page Inspector window, click the **Inspect** button.</span></span>

![요소 검사](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

<span data-ttu-id="c002b-156">작동 중인 검사 모드를 확인 하려면 페이지 검사기 브라우저 창 내에서 페이지의 다른 부분으로 마우스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-156">To see inspection mode in action, move your mouse over different parts of the page within the Page Inspector browser window.</span></span> <span data-ttu-id="c002b-157">이렇게 하면 마우스 포인터가 큼 더하기 기호로 바뀌고 아래 요소가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-157">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Div를 마우스로 가리킵니다. 콘텐츠-래퍼](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

<span data-ttu-id="c002b-159">마우스 포인터를 이동할 때 다음 사항에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c002b-159">As you move the mouse pointer, note that</span></span>

- <span data-ttu-id="c002b-160">**소스** 뷰의 콘텐츠가 변경 되어 페이지에서 선택한 요소에 해당 하는 태그가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-160">The content in **Source** view changes to show the markup corresponding to the selected element on the page.</span></span> <span data-ttu-id="c002b-161">관련 태그가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-161">The relevant markup is highlighted.</span></span> <span data-ttu-id="c002b-162">소스가 다른 파일에 있는 경우 해당 파일은 관련 태그가 강조 표시 된 소스 뷰에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-162">If the source is in another file, that file is opened in Source view with the relevant markup highlighted.</span></span>

- <span data-ttu-id="c002b-163">페이지 검사기의 **HTML** 탭에 표시 되는 마크업도 페이지에서 선택한 요소에 해당 하는로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-163">The markup displayed in the **HTML** tab in Page Inspector also changes to correspond to the selected element on the page.</span></span> <span data-ttu-id="c002b-164">**HTML** 탭에서 관련 태그에 대해 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-164">In the **HTML** tab, the relevant markup is outlined.</span></span>

- <span data-ttu-id="c002b-165">**스타일** 탭에는 현재 선택 영역과 관련 된 CSS 규칙이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-165">The **Styles** tab shows the CSS rules relevant to the current selection.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="c002b-166">페이지 검사기를 사용 하 여 태그 변경</span><span class="sxs-lookup"><span data-stu-id="c002b-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="c002b-167">이제 페이지 검사기를 사용 하 여 위치가 즉시 명확 하지 않을 수 있는 태그 또는 텍스트를 찾고 변경 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-167">Now you will see how you can use Page Inspector to find and make changes to markup or text whose location might not be immediately obvious.</span></span>

<span data-ttu-id="c002b-168">페이지 검사기를 검사 모드에 넣고 홈 페이지의 아래쪽으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-168">Put Page Inspector in Inspection Mode and then scroll to the bottom of the home page.</span></span>

<span data-ttu-id="c002b-169">바닥글 영역을 입력 하는 즉시 페이지 검사기 다른 탭의 오른쪽에 있는 임시 탭의 **원본** 뷰에서 *사이트 .master* 레이아웃 파일을 열고 선택한 마스터 페이지의 섹션을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-169">As soon as you enter the footer area, Page Inspector opens the *Site.Master* layout file in **Source** view in a temporary tab to the right of the other tabs and highlights the section of the master page that you have selected.</span></span> <span data-ttu-id="c002b-170">이 항목에서는 처음에 열었던 것과 다른 파일에서 실제로 제공 될 수 있는 페이지에서 콘텐츠를 찾고 표시할 수 페이지 검사기 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-170">This shows you how Page Inspector can find and display content on a page that might actually come from a different file than the one you originally opened.</span></span>

![검사 모드에서 바닥글 강조 표시](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

<span data-ttu-id="c002b-172">페이지 검사기 브라우저 창에서 저작권 <a id="a"> </a>표시를 사용 하 여 줄 위로 마우스 포인터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-172">In the Page Inspector browser window, move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span>

<span data-ttu-id="c002b-173">*Site.master* 페이지에서 해당 줄이 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-173">In the *Site.Master* page, the corresponding line is highlighted.</span></span>

![바닥글 저작권 선이 강조 표시 됨](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

<span data-ttu-id="c002b-175">*사이트 마스터* 파일의 줄 끝에 일부 텍스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-175">Add some text to the end of the line in the *Site.Master* file.</span></span>

<span data-ttu-id="c002b-176">&lt;p&gt;&amp;복사 &lt;%: DateTime. Year%&gt;-My ASP.NET Application 암석 지.&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="c002b-176">&lt;p&gt;&amp;copy; &lt;%: DateTime.Now.Year %&gt; - My ASP.NET Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="c002b-177">이제 Ctrl + Alt + Enter를 누르거나 업데이트 표시줄을 클릭 하 여 페이지 검사기 브라우저 창에 결과를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-177">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![내 ASP.NET 응용 프로그램 돌!](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

<span data-ttu-id="c002b-179">바닥글은 default.aspx 페이지에 있었지만 마스터 레이아웃 페이지에 표시 되는 것으로 확인 했을 수 있습니다. *이 페이지에서* 이를 찾을 페이지 검사기.</span><span class="sxs-lookup"><span data-stu-id="c002b-179">You might have thought that the footer was on the *Default.aspx* page, but it turned out to be in the master layout page, and Page Inspector found it for you.</span></span>

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="c002b-180">검사 모드 및 HTML 창</span><span class="sxs-lookup"><span data-stu-id="c002b-180">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="c002b-181">다음으로 HTML 창 및이 창에서 요소를 매핑하는 방법에 대해 간략히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-181">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="c002b-182">검사 모드에 페이지 검사기을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-182">Put Page Inspector in Inspection Mode.</span></span>

![요소 검사](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

<span data-ttu-id="c002b-184">"여기에 로고가 있습니다." 라는 페이지의 위쪽 부분을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-184">Click the top part of the page that says "your logo here".</span></span> <span data-ttu-id="c002b-185">특정 요소를 자세히 검사 하 고 있으므로 마우스 포인터를 이동할 때 브라우저 창에 표시 되는 내용이 더 이상 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="c002b-186">이제 마우스 포인터를 **HTML** 창으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="c002b-187">마우스 포인터를 움직이면 페이지 검사기 **HTML** 창에서 요소를 윤곽선으로 표시 하 고 브라우저 창에서 해당 요소를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 창](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

<span data-ttu-id="c002b-189">이전 처럼 페이지 검사기 임시 탭에서 *site.master* 파일을 엽니다. 사이트. 마스터 탭을 클릭 하면 &lt;헤더&gt; 섹션에서 해당 태그가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-189">As before, Page Inspector opens the *Site.Master* file for you in a temporary tab. Click the Site.Master tab, and the corresponding markup is highlighted in the &lt;header&gt; section:</span></span>

![강조 표시 된 태그](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="c002b-191">스타일 창에서 CSS 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="c002b-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="c002b-192">다음으로 페이지 검사기 **스타일** 창을 사용 하 여 CSS에 대 한 변경 내용을 미리 볼 수 있는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-192">Next, you will see how you can use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="c002b-193">**검사** 단추를 클릭 하 여 검사 모드 페이지 검사기을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-193">Click the **Inspect** button to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="c002b-194">페이지 검사기 브라우저 창에서 **div. 콘텐츠-래퍼** 레이블이 나타날 때까지 마우스 포인터를 "홈 페이지" 섹션으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![요소 가리키기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

<span data-ttu-id="c002b-196">Div. 콘텐츠-래퍼 섹션 내에서 한 번 클릭 한 다음 마우스 포인터를 **스타일** 창으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="c002b-197">주요. 콘텐츠-래퍼 클래스 선택기에서 배경색 속성의 확인란을 선택 취소 하 고 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-197">Under the .featured .content-wrapper class selector, clear and select the checkbox for the background-color property.</span></span>

![배경색 지우기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

<span data-ttu-id="c002b-199">페이지 검사기 브라우저 창에서 변경 내용이 즉시 미리 보기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-199">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="c002b-200">확인란을 다시 선택 하 고 속성 값을 두 번 클릭 한 다음 `red`로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-200">Select the checkbox again, then double-click the property value and change it to `red`.</span></span> <span data-ttu-id="c002b-201">변경 내용이 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-201">The change shows immediately:</span></span>

![빨강 배경색](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

<span data-ttu-id="c002b-203">스타일 **창을 사용** 하면 스타일 시트 자체에 변경 내용을 커밋하기 전에 CSS 변경을 쉽게 테스트 하 고 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-203">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="c002b-204">CSS Auto Sync</span><span class="sxs-lookup"><span data-stu-id="c002b-204">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="c002b-205">이 기능을 사용 하려면 1.3 버전의 페이지 검사기 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-205">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="c002b-206">CSS 자동 동기화 기능을 사용 하면 CSS 파일을 직접 편집 하 고 페이지 검사기 브라우저에서 즉시 변경 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-206">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="c002b-207">**검사** 를 클릭 하 여 검사 모드에 페이지 검사기을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-207">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="c002b-208">페이지 검사기 브라우저에서 ' 홈 페이지 ' 섹션 위로 마우스 포인터를 이동 합니다. **콘텐츠-래퍼** 레이블이 나타날 때까지 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-208">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="c002b-209">한 번 클릭 하 여이 요소를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-209">Click once to select this element.</span></span>

<span data-ttu-id="c002b-210">**스타일** 창에는이 요소에 대 한 모든 CSS 규칙이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-210">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="c002b-211">아래로 스크롤하여, 주요. 콘텐츠-래퍼 클래스 선택기를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-211">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="c002b-212">"주요. 콘텐츠-래퍼"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-212">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="c002b-213">페이지 검사기이 스타일 (.css)을 정의 하는 CSS 파일을 열고 해당 CSS 스타일을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-213">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![CSS 파일](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

<span data-ttu-id="c002b-215">이제 `background-color`의 값을 "red"로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-215">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="c002b-216">변경 내용은 페이지 검사기 브라우저에 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-216">The change appears immediately in the Page Inspector browser.</span></span>

![페이지 검사기 브라우저](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a><span data-ttu-id="c002b-218">CSS 색 선택 사용</span><span class="sxs-lookup"><span data-stu-id="c002b-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="c002b-219">다음으로 페이지 검사기를 사용 하 여 기본 응용 프로그램에서 강조 표시 된 텍스트에 대 한 CSS를 빠르게 찾고 변경 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-219">Next, you'll learn how to use Page Inspector to quickly find and change the CSS for highlighted text in the default application.</span></span> <span data-ttu-id="c002b-220">이 예제에서는 파란색 강조 표시와 다른 색으로 변경 하는 것을 원하지 않기로 결정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-220">In this example, you've decided that you don't like the blue highlighting and want to change it to another color.</span></span>

<span data-ttu-id="c002b-221">**검사** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-221">Click the **Inspect** button.</span></span>

![요소 검사](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

<span data-ttu-id="c002b-223">페이지 검사기 브라우저 창에서 강조 표시 된 "비디오, 자습서 및 샘플" 텍스트 위로 마우스 포인터를 이동 하 여 CSS "표시" 레이블이 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-223">In the Page Inspector browser window, move the mouse pointer over the highlighted "videos, tutorials, and samples" text so that the CSS "mark" label appears.</span></span>

![Mark 요소 가리키기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

<span data-ttu-id="c002b-225">텍스트를 클릭 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-225">Click the text to select it.</span></span> <span data-ttu-id="c002b-226">해당 CSS 표시 선택기는 **스타일** 창의 아래쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-226">The corresponding CSS mark selector appears at the bottom of the **Styles** window.</span></span>

![스타일 창의 표시 선택기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

<span data-ttu-id="c002b-228">표시 선택기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-228">Click the mark selector.</span></span> <span data-ttu-id="c002b-229">그러면 웹 응용 프로그램에 대 한 *사이트 .css* 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-229">This opens the *Site.css* file for the web application.</span></span> <span data-ttu-id="c002b-230">사이트 .css 탭을 클릭 하면 선택기의 해당 CSS가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-230">Click the Site.css tab, and the corresponding CSS for the selector is highlighted:</span></span>

![스타일 시트의 표시 선택기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

<span data-ttu-id="c002b-232">배경 색 속성을 사용 하 여 줄을 선택 하 고 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-232">Select and remove the line with the background-color property.</span></span>

<span data-ttu-id="c002b-233">이제 새 Visual Studio 2012 CSS 색 선택기를 사용 하 여 배경색 **표시** 속성의 새 색을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-233">You will now use the new Visual Studio 2012 CSS color picker to choose a new color for the **mark** background-color property.</span></span>

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a><span data-ttu-id="c002b-234">Visual Studio 2012 CSS 색 선택 사용</span><span class="sxs-lookup"><span data-stu-id="c002b-234">Using the Visual Studio 2012 CSS Color Picker</span></span>

<span data-ttu-id="c002b-235">Visual Studio 2012의 CSS 편집기에는 색을 쉽게 선택 하 고 삽입할 수 있는 색 선택이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-235">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="c002b-236">간단한 색 막대와 "팝업" 선택기를 통해 더욱 세밀 하 게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-236">It has a simple color bar and a "pop-down" picker that offers finer control.</span></span>

<span data-ttu-id="c002b-237">색 선택기는 색의 표준 색상표를 포함 하 고, 표준 색 이름, 해시 코드, RGB, RGBA, HSL 및 HSLA 색을 지원 하며, 문서에서 가장 최근에 사용한 색의 목록을 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-237">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="c002b-238">배경 색 속성이 있었던 줄에서 "bc"를 입력 하 고 아래쪽 화살표를 한 번 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-238">On the line where the background-color property was, type "bc" and press the down arrow once.</span></span>

<span data-ttu-id="c002b-239">하이픈으로 구분 된 속성 (예: "배경색")에서 각 단어의 첫 번째 문자를 입력 하면 IntelliSense는 일치 하는 속성만 표시 하도록 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-239">When you type the first character of each word in a hyphen-separated property like "background-color", IntelliSense filters the list for you to show only the properties that match:</span></span>

![Intellisense 필터링 된 값](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

<span data-ttu-id="c002b-241">이제 콜론을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-241">Now type a colon.</span></span> <span data-ttu-id="c002b-242">이렇게 하면 전체 배경색 속성 이름이 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-242">When you do, the full background-color property name is inserted.</span></span> <span data-ttu-id="c002b-243">**#** 또는 **rgb (** 를 입력 합니다. 그러면 색 선택 막대가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-243">Type **#** or **rgb(**, and the color picker bar appears:</span></span>

![CSS 색 선택 막대입니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

<span data-ttu-id="c002b-245">색 선택 막대가 어떻게 작동 하는지 확인 하려면 마우스 포인터로 색을 클릭 하거나 아래쪽 화살표 키를 누른 다음 왼쪽 및 오른쪽 화살표 키를 사용 하 여 색을 트래버스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-245">To see how the color picker bar works, click its colors with the mouse pointer, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="c002b-246">색을 방문할 때 배경 색 속성에 해당 하는 값을 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-246">When you visit a color, the corresponding value for the background-color property is previewed:</span></span>

![배경 색 속성 값 미리 보기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

<span data-ttu-id="c002b-248">이 시점에서 Enter 키를 눌러 값을 선택 하 고 세미콜론 (;) CSS 항목을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-248">At this point, you could press Enter to select the value and then a semicolon (;) to complete the CSS entry.</span></span> <span data-ttu-id="c002b-249">지금은 색 선택 팝업이 작동 하는 방식을 확인할 수 있도록 다음 섹션으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-249">For now, go on to the next section so that you can see how the color picker pop-down works.</span></span>

#### <a name="using-the-color-picker-pop-down"></a><span data-ttu-id="c002b-250">색 선택 팝업 사용</span><span class="sxs-lookup"><span data-stu-id="c002b-250">Using the Color Picker Pop-Down</span></span>

<span data-ttu-id="c002b-251">색 막대에 원하는 정확한 색이 없으면 색 선택 팝업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-251">When the color bar doesn't have the exact color that you're looking for, you can use the color picker pop-down.</span></span>

<span data-ttu-id="c002b-252">이를 열려면 색 막대의 오른쪽 끝에 있는 이중 갈매기형 펼침 단추를 클릭 하거나 키보드에서 아래쪽 화살표를 한 번 또는 두 번 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-252">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 색 선택 팝업](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

<span data-ttu-id="c002b-254">오른쪽의 세로 막대에서 색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-254">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="c002b-255">이렇게 하면 주 창에 해당 색의 그라데이션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-255">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="c002b-256">Enter 키를 눌러 세로 막대에서 색을 직접 선택 하거나 주 창에서 아무 점이 나 클릭 하 여 더 높은 정밀도로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-256">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="c002b-257">사용 하려는 컴퓨터 화면에 색이 있는 경우 (Visual Studio 사용자 인터페이스 내부에 있을 필요가 없음) 오른쪽 아래에 있는 스 포 이트 도구를 사용 하 여 해당 값을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-257">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="c002b-258">색 선택 아래쪽의 슬라이더를 움직여 색의 불투명도를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-258">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="c002b-259">이렇게 하면 RGBA 형식이 불투명을 나타낼 수 있기 때문에 색 값이 RGBA 값으로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-259">Doing so changes color values to RGBA values because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="c002b-260">색을 선택한 후 Enter 키를 누른 후 세미콜론을 입력 하 여 *사이트 .css* 파일의 배경색 항목을 완성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-260">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="c002b-261">페이지 검사기 업데이트 표시줄</span><span class="sxs-lookup"><span data-stu-id="c002b-261">The Page Inspector Update Bar</span></span>

<span data-ttu-id="c002b-262">페이지 검사기는 *사이트 .css* 파일 (또는 응용 프로그램의 모든 파일)에 대 한 변경 내용을 즉시 검색 하 고 업데이트 표시줄에 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-262">Page Inspector immediately detects the change to the *Site.css* file (or to any file in the application) and displays an alert in an update bar.</span></span>

![업데이트 표시줄](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

<span data-ttu-id="c002b-264">모든 파일을 저장 하 고 페이지 검사기 브라우저를 새로 고치려면 Ctrl + Alt + Enter를 누르거나 업데이트 표시줄을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-264">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="c002b-265">강조 표시 색의 변경 내용이 브라우저에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-265">The change in the highlight color appears in the browser:</span></span>

![강조 색이 변경 됨](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a><span data-ttu-id="c002b-267">Visual Studio 환경 내에서 바로 페이지 검사기 브라우저를 새로 고쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-267">Notice that you conveniently refreshed the Page Inspector browser right from within the Visual Studio environment.</span></span> <span data-ttu-id="c002b-268">외부 브라우저 대신 페이지 검사기를 사용 하면 웹 응용 프로그램을 개발할 때 편집기를 그대로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c002b-268">Using Page Inspector instead of an external browser lets you stay in the editor when you develop your web applications.</span></span>

## <a name="see-also"></a><span data-ttu-id="c002b-269">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c002b-269">See Also</span></span>

<span data-ttu-id="c002b-270">[페이지 검사기 소개](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 비디오)</span><span class="sxs-lookup"><span data-stu-id="c002b-270">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 video)</span></span>

<span data-ttu-id="c002b-271">[페이지 검사기 오류 메시지](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="c002b-271">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
