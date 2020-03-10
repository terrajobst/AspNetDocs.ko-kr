---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Visual Studio 2012에서 제공 되는 ASP.NET 및 웹 개발의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 새 버전의 Visual Studio에는 웹 기술을 사용 하는 경우 환경 및 성능을 개선 하는 데 초점을 맞춘 많은 향상 된 기능이 도입 되었습니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422099"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a><span data-ttu-id="f0b4d-103">Visual Studio 2012의 새로운 ASP.NET 및 웹 개발 기능</span><span class="sxs-lookup"><span data-stu-id="f0b4d-103">What's New in ASP.NET and Web Development in Visual Studio 2012</span></span>

<span data-ttu-id="f0b4d-104">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="f0b4d-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="f0b4d-105">새 버전의 Visual Studio에는 웹 기술로 작업할 때 경험 및 성능을 개선 하는 데 초점을 맞춘 많은 향상 된 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-105">The new version of Visual Studio introduces a number of enhancements focused on improving the experience and performance when working with Web technologies.</span></span> <span data-ttu-id="f0b4d-106">CSS, JavaScript 및 HTML 용 Visual Studio 편집기는 IntelliSense 및 자동 들여쓰기와 같은 대부분의 주문형 코드 지원 기능을 포함 하도록 완전히 개선 된 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-106">Visual Studio Editors for CSS, JavaScript and HTML have been completely revamped to include many of the most in-demand code aids, such as IntelliSense and automatic indentation.</span></span> <span data-ttu-id="f0b4d-107">이제 성능, 묶음 및 축소 기능이 기본 제공 기능으로 통합 되어 페이지 로드 시간을 쉽게 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-107">Regarding performance, bundling and minification are now integrated as built-in features to easily reduce page load time.</span></span>
> 
> <span data-ttu-id="f0b4d-108">Visual Studio를 사용 하면 최신 웹 사이트 기술로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-108">Visual Studio enables you to work with the latest website technologies.</span></span> <span data-ttu-id="f0b4d-109">브라우저 간 CSS3 코드 조각을 사용 하 여 새 HTML5 요소와 기능을 활용 하면서 클라이언트 플랫폼에 관계 없이 사이트가 작동 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-109">You can use cross-browser CSS3 Snippets to make sure your site works regardless of the client platform while also taking advantage of the new HTML5 elements and features.</span></span>
> 
> <span data-ttu-id="f0b4d-110">이 Visual Studio 버전에서는 JavaScript 코드를 작성 하 고 프로 파일링 하는 것이 더 쉬워졌습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-110">Writing and profiling JavaScript code should be easier with this Visual Studio version.</span></span> <span data-ttu-id="f0b4d-111">IntelliSense 목록, 통합 XML 설명서 및 탐색 기능을 이제 JavaScript 코드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-111">IntelliSense lists, integrated XML documentation and navigation features are now available for JavaScript code.</span></span> <span data-ttu-id="f0b4d-112">이제 JavaScript 카탈로그를 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-112">You now have the JavaScript catalog at your fingertips.</span></span> <span data-ttu-id="f0b4d-113">또한 스크립트를 사용 하 여 ECMAScript5 준수를 확인 하 고 초기 단계에서 구문 오류를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-113">Additionally, you can check ECMAScript5 compliance with your scripts and detect syntax errors at an early stage.</span></span>
> 
> <span data-ttu-id="f0b4d-114">마지막으로,이 Visual Studio 버전은 기본 제공 묶음 및 축소를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-114">Last but not least, this Visual Studio version implements built-in bundling and minification.</span></span> <span data-ttu-id="f0b4d-115">사이트를 더 빠르게 수행 하도록 스크립트 파일 및 스타일 시트를 압축 하 고 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-115">Your script files and style sheets will be packed and compressed so that the site performs faster.</span></span>
> 
> <span data-ttu-id="f0b4d-116">이 랩에서는 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 사항을 적용 하 여 앞에서 설명한 향상 된 기능 및 새로운 기능을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="f0b4d-117">모든 샘플 코드와 코드 조각은 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-117">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="f0b4d-118">목표</span><span class="sxs-lookup"><span data-stu-id="f0b4d-118">Objectives</span></span>

<span data-ttu-id="f0b4d-119">이 연습에서는 다음을 수행 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-119">In this hands on lab, you will learn how to:</span></span>

- <span data-ttu-id="f0b4d-120">CSS 편집기의 새로운 기능 및 향상 된 기능 사용</span><span class="sxs-lookup"><span data-stu-id="f0b4d-120">Use the new features and improvements in the CSS editor</span></span>
- <span data-ttu-id="f0b4d-121">HTML 편집기의 새로운 기능 및 향상 된 기능 사용</span><span class="sxs-lookup"><span data-stu-id="f0b4d-121">Use the new features and improvements in the HTML editor</span></span>
- <span data-ttu-id="f0b4d-122">JavaScript 편집기의 새로운 기능 및 향상 된 기능 사용</span><span class="sxs-lookup"><span data-stu-id="f0b4d-122">Use the new features and improvements in the JavaScript editor</span></span>
- <span data-ttu-id="f0b4d-123">묶음 및 축소 구성 및 사용</span><span class="sxs-lookup"><span data-stu-id="f0b4d-123">Configure and use bundling and minification</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="f0b4d-124">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="f0b4d-124">Prerequisites</span></span>

- <span data-ttu-id="f0b4d-125">[웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="f0b4d-125">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="f0b4d-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (설치 스크립트의 경우-windows 8 및 windows Server 2008 r 2에 이미 설치 됨)</span><span class="sxs-lookup"><span data-stu-id="f0b4d-126">[Windows PowerShell](https://support.microsoft.com/kb/968930/) (for setup scripts - already installed on Windows 8 and Windows Server 2008 R2)</span></span>
- <span data-ttu-id="f0b4d-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) 또는 HTML5 호환 브라우저</span><span class="sxs-lookup"><span data-stu-id="f0b4d-127">[Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) - or an HTML5 compliant browser</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="f0b4d-128">실습</span><span class="sxs-lookup"><span data-stu-id="f0b4d-128">Exercises</span></span>

<span data-ttu-id="f0b4d-129">이 실습 랩에서는 다음 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-129">This hands on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="f0b4d-130">연습 1: CSS 편집기의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f0b4d-130">Exercise 1: What's New in the CSS Editor</span></span>](#Exercise1)
2. [<span data-ttu-id="f0b4d-131">연습 2: HTML 편집기의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f0b4d-131">Exercise 2: What's New in the HTML Editor</span></span>](#Exercise2)
3. [<span data-ttu-id="f0b4d-132">연습 3: JavaScript 편집기의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f0b4d-132">Exercise 3: What's New in the JavaScript Editor</span></span>](#Exercise3)
4. [<span data-ttu-id="f0b4d-133">연습 4: 묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="f0b4d-133">Exercise 4: Bundling and Minification</span></span>](#Exercise4)

<span data-ttu-id="f0b4d-134">이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="f0b4d-134">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a><span data-ttu-id="f0b4d-135">연습 1: CSS 편집기의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f0b4d-135">Exercise 1: What's New in the CSS Editor</span></span>

<span data-ttu-id="f0b4d-136">웹 개발자는 CSS 편집과 관련 된 많은 문제에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-136">Web developers should be familiar with many of the difficulties related to CSS editing.</span></span> <span data-ttu-id="f0b4d-137">CSS 스타일의 가장 큰 문제 중 하나는 브라우저 간 호환성입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-137">One of the biggest issues of CSS styling is cross-browser compatibility.</span></span> <span data-ttu-id="f0b4d-138">사이트에 스타일을 적용 한 후에는 다른 브라우저나 장치에서 열 때 다르게 표시 되는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-138">It often happens that, after applying styles to your site, you notice that it looks different if you open it in another browser or device.</span></span> <span data-ttu-id="f0b4d-139">따라서 이러한 시각적 문제를 해결 하는 데 상당한 시간을 할애 하 여 한 브라우저에서 작업을 수행 하는 경우 다른 브라우저에서 분리 될 수 있다는 점을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-139">Therefore, you may spend a considerable time on fixing those visual issues to realize that, when you finally make it work in one browser, it is broken in the others.</span></span>

<span data-ttu-id="f0b4d-140">이제 Visual Studio에는 개발자가 CSS 스타일 시트를 효과적으로 액세스, 작업 및 구성 하는 데 도움이 되는 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-140">Visual Studio now includes features that help developers access, work and organize CSS style sheets effectively.</span></span> <span data-ttu-id="f0b4d-141">이 연습을 진행 하는 동안에는 유효한 조직과 버전의 새로운 기능 뿐만 아니라 브라우저 간 호환성을 위한 CSS3 코드 조각이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-141">Throughout this exercise, you will meet the new features for an effective organization and edition, as well as the CSS3 Code Snippets for cross-browser compatibility.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a><span data-ttu-id="f0b4d-142">작업 1-새 편집기 기능</span><span class="sxs-lookup"><span data-stu-id="f0b4d-142">Task 1 - New Editor Features</span></span>

<span data-ttu-id="f0b4d-143">이 태스크에서는 CSS 편집기의 새 기능을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-143">In this task, you will discover the new features of the CSS Editor.</span></span> <span data-ttu-id="f0b4d-144">이 새로운 편집기는 새로운 스마트 들여쓰기, 향상 된 코드 주석 및 향상 된 IntelliSense 목록을 활용 하 여 생산성을 높이는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-144">This new editor will help you increase your productivity by taking advantage of the new smart indentation, the improved code comments and the enhanced IntelliSense list.</span></span>

1. <span data-ttu-id="f0b4d-145">**Visual Studio** 를 시작 하 고이 랩의 **Source\WhatsNewASPNET** 폴더에 있는 **WhatsNewASPNET** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-145">Start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="f0b4d-146">솔루션 탐색기에서 **스타일** 폴더 아래에 있는 **사이트 .css** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-146">In Solution Explorer, open the **Site.css** file located under the **Styles** folder.</span></span> <span data-ttu-id="f0b4d-147">**텍스트 편집기** 도구가 도구 모음에 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-147">Make sure the **Text Editor** tools are visible on the toolbar.</span></span> <span data-ttu-id="f0b4d-148">이렇게 하려면 | **도구 모음** **보기** 메뉴 옵션을 선택 하 고 **텍스트 편집기** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-148">To do that, select the **View** | **Toolbars** menu option, and check the **Text Editor** options.</span></span> <span data-ttu-id="f0b4d-149">이 새 버전을 사용 하는 경우 **주석** 단추![(주석 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png))와 주석 **제거** 단추 (![주석 제거 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png))도 CSS 편집기에 대해 사용 하도록 설정 된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-149">You will notice that, since this new version, the **Comment** button (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png) ) and the **Uncomment** button (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png) ) are also enabled for the CSS editor.</span></span>

    <span data-ttu-id="f0b4d-150">![편집기 및 CSS 도구 사용](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "편집기 및 CSS 도구 사용")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-150">![Enabling Editor and CSS Tools](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Enabling Editor and CSS Tools")</span></span>

    <span data-ttu-id="f0b4d-151">*편집기 및 CSS 도구 사용*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-151">*Enabling Editor and CSS Tools*</span></span>
3. <span data-ttu-id="f0b4d-152">코드를 스크롤하고 CSS 클래스 정의를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-152">Scroll the code and select any CSS class definition.</span></span> <span data-ttu-id="f0b4d-153">\*\*주석 (![** 주석 단추](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)) 단추를 클릭 하 여 선택한 줄을 주석 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-153">Click the **Comment** (![comment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png) ) button to comment the selected lines.</span></span> <span data-ttu-id="f0b4d-154">그런 다음 **주석 처리 제거** (![](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) 제거) 단추를 클릭 하 여 변경 내용을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-154">Then, click the **Uncomment** (![uncomment-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png) ) button to undo the changes.</span></span>
4. <span data-ttu-id="f0b4d-155">**축소** (![](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) 축소)를 클릭 하 고 텍스트의 왼쪽 여백에 있는 확장 (![](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png)) 단추를 **확장** 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-155">Click the **Collapse** (![collapse](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) ) and **Expand** (![expand](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png) ) buttons located on the left margin of the text.</span></span> <span data-ttu-id="f0b4d-156">이제 사용 하지 않는 스타일을 더 이상 사용 하지 않는 스타일을 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-156">Notice that you can now hide the styles you don't use to have a cleaner view.</span></span>

    <span data-ttu-id="f0b4d-157">![CSS 클래스 축소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "CSS 클래스 축소")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-157">![Collapsing CSS classes](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "Collapsing CSS classes")</span></span>

    <span data-ttu-id="f0b4d-158">*CSS 클래스 축소*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-158">*Collapsing CSS classes*</span></span>
5. <span data-ttu-id="f0b4d-159">스마트 들여쓰기 기능이 사용 되도록 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-159">Make sure that the smart indentation feature is enabled.</span></span> <span data-ttu-id="f0b4d-160">**도구** | **옵션** 메뉴 옵션을 선택한 다음 화면의 왼쪽 창에서 **텍스트 편집기** | **CSS** | **서식 지정** 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-160">Select the **Tools** | **Options** menu option, and then select the **Text Editor** | **CSS** | **Formatting** page in the left pane of the screen.</span></span> <span data-ttu-id="f0b4d-161">**계층적 들여쓰기** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-161">Check the **Hierarchical indentation** option.</span></span>

    <span data-ttu-id="f0b4d-162">![계층적 들여쓰기 사용](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "계층적 들여쓰기 사용")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-162">![Enabling hierarchical indentation](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Enabling hierarchical indentation")</span></span>

    <span data-ttu-id="f0b4d-163">*계층적 들여쓰기 사용*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-163">*Enabling hierarchical indentation*</span></span>
6. <span data-ttu-id="f0b4d-164">주 클래스 정의 (main)를 찾아 div 요소에 스타일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-164">Locate the main class definition (.main) and append a style to the div elements.</span></span> <span data-ttu-id="f0b4d-165">코드가 자동으로 정렬 되어 사용자가 부모 클래스를 한눈에 찾을 수 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-165">You will notice that the code aligns automatically, helping users to find the parent classes at a glance.</span></span>

    <span data-ttu-id="f0b4d-166">CSS</span><span class="sxs-lookup"><span data-stu-id="f0b4d-166">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    <span data-ttu-id="f0b4d-167">![CSS의 계층적 맞춤](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS의 계층적 맞춤")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-167">![Hierarchical alignment in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "Hierarchical alignment in CSS")</span></span>

    <span data-ttu-id="f0b4d-168">*CSS의 계층적 맞춤*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-168">*Hierarchical alignment in CSS*</span></span>
7. <span data-ttu-id="f0b4d-169">**Main div** 클래스 내에서 **border** 의 끝에 있는 커서를 찾고 **enter** 키를 눌러 IntelliSense 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-169">Inside **.main div** class, locate the cursor at the end of **border: 0px;** and press **Enter** to display the IntelliSense list.</span></span> <span data-ttu-id="f0b4d-170">**Top** 입력을 시작 하 고 입력할 때 목록이 필터링 되는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-170">Start typing **top** and notice how the list is filtered as you type.</span></span> <span data-ttu-id="f0b4d-171">이 목록에는 word의 모든 부분에서 **위쪽** 을 포함 하는 요소가 표시 됩니다 (이전 버전의 Visual Studio에서이 목록은 용어로 *시작* 하는 항목을 기준으로 필터링 됨).</span><span class="sxs-lookup"><span data-stu-id="f0b4d-171">The list will display the elements that contain **top** at any part of the word (In prior versions of Visual Studio, the list is filtered by the items that *begin* with the term).</span></span>

    <span data-ttu-id="f0b4d-172">![CSS의 향상 된 IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS의 향상 된 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-172">![IntelliSense enhancements in CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "IntelliSense enhancements in CSS")</span></span>

    <span data-ttu-id="f0b4d-173">*CSS의 향상 된 IntelliSense*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-173">*IntelliSense enhancements in CSS*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a><span data-ttu-id="f0b4d-174">작업 2-색 선택</span><span class="sxs-lookup"><span data-stu-id="f0b4d-174">Task 2 - The Color Picker</span></span>

<span data-ttu-id="f0b4d-175">이 작업에서는 Visual Studio IntelliSense에 통합 된 새 CSS 색 선택을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-175">In this task, you will discover the new CSS Color Picker integrated into Visual Studio IntelliSense.</span></span>

1. <span data-ttu-id="f0b4d-176">**사이트 .css** 에서 헤더 클래스 정의 (. header)를 찾은 다음 **해당 코드 줄** 에서 &quot;:&quot;와 &quot;#&quot; 문자 사이의 **배경 색** 특성 옆에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-176">In **Site.css,** locate the header class definition (.header) and place the cursor next to **background-color** attribute, between the &quot;:&quot; and &quot;#&quot; characters on that line of code **.**</span></span>

    <span data-ttu-id="f0b4d-177">![커서 찾기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "커서 찾기")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-177">![Locating the cursor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "Locating the cursor")</span></span>

    <span data-ttu-id="f0b4d-178">*커서 찾기*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-178">*Locating the cursor*</span></span>
2. <span data-ttu-id="f0b4d-179">**콜론** (:)을 삭제 합니다. 다시 작성 하 여 색 선택기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-179">Delete the **colon** (:) and write it again to display the color picker.</span></span> <span data-ttu-id="f0b4d-180">표시 되는 첫 번째 색은 사이트의 가장 자주 발생 하는 색입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-180">Notice that the first colors you will see are the most frequent colors of your site.</span></span> <span data-ttu-id="f0b4d-181">흰색을 클릭 하면 해당 HTML 색 코드 (#fff)가 스타일 시트의 현재 색 코드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-181">If you click the white color, its HTML color code (#fff) will replace the current color code in the stylesheet.</span></span>

    <span data-ttu-id="f0b4d-182">![색 선택](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "색 선택")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-182">![Color picker](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Color picker")</span></span>

    <span data-ttu-id="f0b4d-183">*색 선택*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-183">*Color picker*</span></span>
3. <span data-ttu-id="f0b4d-184">색 선택에서 **확장**![(com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)) 단추를 눌러 색 그라데이션을 표시 한 다음 그라데이션 커서를 끌어 다른 색을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-184">Press the **Expand** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png) ) button on the color picker to display the color gradient, and then drag the gradient cursor to select a different color.</span></span> <span data-ttu-id="f0b4d-185">그런 다음 **스 포 이트** 단추를 클릭 하 고 화면에서 색을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-185">After that, click the **Eyedropper** button and select any color from the screen.</span></span> <span data-ttu-id="f0b4d-186">커서를 이동 하는 동안에는 배경 색 값이 동적으로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-186">Notice that background color value changes dynamically while you move the cursor.</span></span>

    <span data-ttu-id="f0b4d-187">![색 선택 그라데이션](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "색 선택 그라데이션")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-187">![Color picker gradient](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Color picker gradient")</span></span>

    <span data-ttu-id="f0b4d-188">*색 선택 그라데이션*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-188">*Color picker gradient*</span></span>
4. <span data-ttu-id="f0b4d-189">**불투명도** 슬라이더에서 선택기를 막대의 가운데로 이동 하 여 불투명도를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-189">In the **Opacity** slider, move the selector to the center of the bar to reduce the opacity.</span></span> <span data-ttu-id="f0b4d-190">이제 배경 색 값이 RGBA로 크기를 변경 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-190">Notice that background-color value now changes its scale to RGBA.</span></span>

    <span data-ttu-id="f0b4d-191">![색 선택 불투명도](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "색 선택 불투명도")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-191">![Color picker Opacity](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Color picker Opacity")</span></span>

    <span data-ttu-id="f0b4d-192">*색 선택 불투명도*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-192">*Color picker Opacity*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0b4d-193">CSS3의 RGBA (빨강, 녹색, 파랑, 알파) 색 정의를 사용 하면 단일 항목에 대 한 색 불투명도 값을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-193">The RGBA (Red, Green, Blue, Alpha) color definition in CSS3 enables you to define the color opacity value for a single item.</span></span> <span data-ttu-id="f0b4d-194">**불투명** 과 달리, RGBA 색 **-** 유사한 CSS 특성도 최신 브라우저와 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-194">Unlike **opacity -** a similar CSS attribute **-** RGBA colors are also compatible with the latest browsers.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a><span data-ttu-id="f0b4d-195">작업 3-CSS 호환 코드 조각</span><span class="sxs-lookup"><span data-stu-id="f0b4d-195">Task 3 - CSS Compatible Code Snippets</span></span>

<span data-ttu-id="f0b4d-196">이 작업에서는 브라우저 간 호환 CSS3 코드 조각을 사용 하 여 웹 사이트에서 일부 기능을 구현 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-196">In this task, you will learn how to use cross-browser compatible CSS3 snippets in order to implement some features in your website.</span></span>

1. <span data-ttu-id="f0b4d-197">**사이트 .css** 파일에서 **헤더** css 클래스 정의 (. header)를 찾고 커서를 **/\*테두리 반경\*/** 자리 표시자에 배치 하 여 새 조각을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-197">In the **Site.css** file, locate the **header** CSS class definition (.header) and place the cursor below the **/\*border radius\*/** placeholder to add a new snippet.</span></span> <span data-ttu-id="f0b4d-198">**Enter** 키를 눌러 IntelliSense 목록을 표시 하 고 **radius** 를 입력 하 여 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-198">Press **Enter** to display the IntelliSense list and type **radius** to filter the list.</span></span> <span data-ttu-id="f0b4d-199">두 번 클릭 하 여 목록에서 **테두리-반경** 옵션을 선택한 다음 **tab** 키를 눌러 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-199">Select the **border-radius** option from the list with a double click, and then press the **TAB** key to insert the snippet.</span></span> <span data-ttu-id="f0b4d-200">그런 다음 반경 크기를 픽셀 단위로 입력 하 고 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-200">Then, type a radius size in pixels and press **Enter**.</span></span> <span data-ttu-id="f0b4d-201">예를 들어 **15px**를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-201">For instance, type **15px**.</span></span>

    <span data-ttu-id="f0b4d-202">이 코드 조각에서 추가 된 CSS3 특성은 Mozilla 및 WebKit 기반 브라우저를 포함 하 여 대부분의 HTML5 규정 준수 브라우저에서 둥근 테두리를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-202">The CSS3 attributes added by the snippet will render rounded borders in most HTML5 compliance browsers, including Mozilla and WebKit-based browsers.</span></span>

    <span data-ttu-id="f0b4d-203">![테두리-반지름 코드 조각 사용](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "테두리-반지름 코드 조각 사용")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-203">![Using a border-radius snippet](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Using a border-radius snippet")</span></span>

    <span data-ttu-id="f0b4d-204">*테두리-반지름 코드 조각 사용*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-204">*Using a border-radius snippet*</span></span>
2. <span data-ttu-id="f0b4d-205">페이지 스타일 (페이지)에 같은 **테두리** 조각을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-205">Apply the same **border** snippets in the page style (.page).</span></span>

    <span data-ttu-id="f0b4d-206">CSS</span><span class="sxs-lookup"><span data-stu-id="f0b4d-206">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. <span data-ttu-id="f0b4d-207">**F5** 키를 눌러 솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-207">Press **F5** to run the solution.</span></span> <span data-ttu-id="f0b4d-208">이제 각 페이지의 테두리가 둥근 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-208">Notice that each page now has rounded borders.</span></span>

    <span data-ttu-id="f0b4d-209">![모퉁이가 둥근 모퉁이](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "모퉁이가 둥근 모퉁이")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-209">![Rounded corners](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Rounded corners")</span></span>

    <span data-ttu-id="f0b4d-210">*모퉁이가 둥근 모퉁이*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-210">*Rounded corners*</span></span>
4. <span data-ttu-id="f0b4d-211">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-211">Close the browser and return to Visual Studio.</span></span>
5. <span data-ttu-id="f0b4d-212">**Styles** 폴더 아래에 있는 **사용자 지정 .css** 파일을 열고 **div. images ul imimg** 클래스 정의에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-212">Open the **Custom.css** file located under the **Styles** folder and place the cursor inside **div.images ul li img** class definition.</span></span>
6. <span data-ttu-id="f0b4d-213">Enter 키를 눌러 IntelliSense 목록을 표시 하 고 **box-shadow** 를 입력 한 다음 **tab** 키를 두 번 눌러 클래스 정의 내부에 기본 그림자 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-213">Press enter to display the IntelliSense list, type **box-shadow** and press the **TAB** key twice to insert the default shadow code snippet inside the class definition.</span></span> <span data-ttu-id="f0b4d-214">그림자 값을 **10px 10px 5px #888**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-214">Set the shadow values to **10px 10px 5px #888**.</span></span> <span data-ttu-id="f0b4d-215">그런 다음 **border-radius** 를 입력 하 고 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-215">Then, type **border-radius** and insert the code snippet.</span></span> <span data-ttu-id="f0b4d-216">반경 크기를 설정 하려면 **15px** 를 입력 하 **고 enter 키를 누릅니다.**</span><span class="sxs-lookup"><span data-stu-id="f0b4d-216">Type **15px** to set radius size and press **ENTER**.</span></span>

    <span data-ttu-id="f0b4d-217">![그림자가 있는 둥근 모퉁이](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "그림자가 있는 둥근 모퉁이")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-217">![Rounded corners with shadow](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Rounded corners with shadow")</span></span>

    <span data-ttu-id="f0b4d-218">*그림자가 있는 둥근 모퉁이*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-218">*Rounded corners with shadow*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0b4d-219">지금은 Mozilla 및 Webkit (Chrome, Safari, Konkeror) 브라우저를 지원 하기 위해 해당 접두사 (moz, webkit, o)를 사용 하 여 섀도 특성이 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-219">At this moment, the shadow attribute is inserted with the corresponding prefix (moz, webkit, o) to support Mozilla and Webkit (Chrome, Safari, Konkeror) browsers.</span></span>
7. <span data-ttu-id="f0b4d-220">새 클래스 div를 만듭니다 **. 이미지 ul li img: div를 마우스로 가리키면** **ul li img** 클래스 정의가 중괄호 안에 커서를 놓습니다 **.**</span><span class="sxs-lookup"><span data-stu-id="f0b4d-220">Create a new class **div.images ul li img:hover** below the **div.images ul li img** class definition and place the cursor inside the brackets **.**</span></span>

    <span data-ttu-id="f0b4d-221">CSS</span><span class="sxs-lookup"><span data-stu-id="f0b4d-221">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. <span data-ttu-id="f0b4d-222">Transform **을 입력 하** 고 **tab** 키를 두 번 눌러 변환 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-222">Type **transform** and press the **TAB** key twice in order to insert the transform snippet.</span></span> <span data-ttu-id="f0b4d-223">그런 다음 **회전 (-15deg)** 을 입력 하 여 이미지를 가리킬 때 회전 각도 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-223">Then, enter **rotate(-15deg)** to change the rotation angle value when images are hovered.</span></span>

    <span data-ttu-id="f0b4d-224">CSS</span><span class="sxs-lookup"><span data-stu-id="f0b4d-224">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. <span data-ttu-id="f0b4d-225">**F5** 키를 눌러 솔루션을 실행 하 고 CSS3 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-225">Press **F5** to run the solution and browse to the CSS3 page.</span></span> <span data-ttu-id="f0b4d-226">이미지에 모퉁이가 둥근 모퉁이 및 상자 그림자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-226">Notice that the images have rounded corners and box shadows.</span></span> <span data-ttu-id="f0b4d-227">이미지 위로 마우스를 가져가면 회전을 시청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-227">Hover the mouse over the images and watch them rotate.</span></span>

    <span data-ttu-id="f0b4d-228">![이미지를 회전 하는 조각 변환](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "이미지를 회전 하는 조각 변환")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-228">![Transform snippet rotating an image](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Transform snippet rotating an image")</span></span>

    <span data-ttu-id="f0b4d-229">*이미지를 회전 하는 조각 변환*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-229">*Transform snippet rotating an image*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0b4d-230">Internet Explorer 10을 사용 하 고 그림자를 볼 수 없는 경우 문서 모드가 IE10 표준으로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-230">If you are using Internet Explorer 10 and cannot see the shadows, make sure the document mode is set to IE10 standards.</span></span> <span data-ttu-id="f0b4d-231">**F12** 키를 눌러 Internet Explorer 개발자 도구를 열고 **문서 모드** 를 클릭 하 여 IE10 표준으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-231">Press **F12** to open Internet Explorer developer tools and click **Document Mode** to change to IE10 standards.</span></span>

    ![about-us](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a><span data-ttu-id="f0b4d-233">연습 2: HTML 편집기의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f0b4d-233">Exercise 2: What's New in the HTML Editor</span></span>

<span data-ttu-id="f0b4d-234">Visual Studio에는 향상 된 HTML 편집기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-234">Visual Studio has an improved HTML editor.</span></span> <span data-ttu-id="f0b4d-235">이 버전에 포함 된 향상 된 기능 중 일부는 HTML 문서, HTML5 조각, HTML 시작 및 끝 태그 일치 및 HTML 유효성 검사에서 스마트 들여쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-235">Some of the enhancements included in this version are smart indentation in HTML documents, HTML5 snippets, HTML start and end tag matching, and HTML validation.</span></span> <span data-ttu-id="f0b4d-236">이 연습을 수행 하는 동안 웹 사이트 태그에서 작업 하는 경우 이러한 변경 내용이 능숙를 어떻게 개선 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-236">Throughout this exercise, you will see how these changes improve your fluency when working in the website markup.</span></span>

<span data-ttu-id="f0b4d-237">CSS 편집기와 마찬가지로 HTML 편집기도 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-237">Like the CSS editor, the HTML editor was also improved.</span></span> <span data-ttu-id="f0b4d-238">이러한 향상 된 기능 중 대부분은 웹 개발자의 작업을 용이 하 게 하는 작은 규모입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-238">Most of these improvements are small ones that make the Web developer's life easier.</span></span> <span data-ttu-id="f0b4d-239">HTML 문서 DOCTYPE을 대상으로 하는 편집 및 유효성 검사를 수행할 때 HTML5, 스마트 들여쓰기, 일치 하는 시작 및 끝 태그에 대 한 추가 코드 조각 같은 항목은 이러한 향상 된 기능 중 일부입니다</span><span class="sxs-lookup"><span data-stu-id="f0b4d-239">Things like more code snippets for HTML5, smart indentation, matching start and end tags when editing and validation targeting the HTML document DOCTYPE are some of these improvements.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a><span data-ttu-id="f0b4d-240">작업 1-향상 된 DOCTYPE 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="f0b4d-240">Task 1 - Improved DOCTYPE Validation</span></span>

<span data-ttu-id="f0b4d-241">이제 HTML 편집기는 마스터 페이지에 정의 되어 있는 경우에도 페이지의 DOCTYPE을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-241">The HTML editor now has the ability to check the DOCTYPE of your page, even though the definition might be in the master page.</span></span> <span data-ttu-id="f0b4d-242">페이지의 DOCTYPE에 따라 HTML 편집기는 올바른 규칙 집합을 사용 하 여 유효성을 검사 하 고 DOCTYPE 요소를 고려 하 여 IntelliSense 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-242">Depending on the DOCTYPE of your page, the HTML editor will validate with the correct set of rules and will filter the IntelliSense list considering the DOCTYPE elements.</span></span>

<span data-ttu-id="f0b4d-243">이 태스크에서는 페이지의 DOCTYPE을 변경 하 여 HTML 편집기 동작을 적절 하 게 변경 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-243">In this task, you will change the DOCTYPE of a page to see how the HTML editor behavior changes accordingly.</span></span>

1. <span data-ttu-id="f0b4d-244">아직 열지 않은 경우 **Visual Studio** 를 시작 하 고이 랩의 **Source\WhatsNewASPNET** 폴더에 있는 **WhatsNewASPNET** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-244">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="f0b4d-245">**사이트 마스터** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-245">Open the **Site.Master** page.</span></span>
3. <span data-ttu-id="f0b4d-246">유효성 검사 도구 모음에 대 한 대상 스키마를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-246">Notice the Target Schema for Validation Toolbar.</span></span> <span data-ttu-id="f0b4d-247">HTML 편집기의 동작 (유효성 검사, IntelliSense 등)이 선택한 Doctype에 맞게 올바르게 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-247">The way the HTML editor behaves (Validation, IntelliSense, etc.) will properly change to fit the Doctype selected.</span></span>

    <span data-ttu-id="f0b4d-248">![HTML 소스 편집 도구 모음에서 Doctype 사용](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "HTML 소스 편집 도구 모음에서 Doctype 사용")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-248">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="f0b4d-249">*HTML 소스 편집 도구 모음에서 Doctype 사용*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-249">*Use Doctype in HTML Source Editing toolbar*</span></span>
4. <span data-ttu-id="f0b4d-250">대상 스키마를 HTML 4.01로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-250">Change the Target Schema to HTML 4.01.</span></span>

    <span data-ttu-id="f0b4d-251">![HTML 소스 편집 도구 모음의 Doctype 변경](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "HTML 소스 편집 도구 모음의 Doctype 변경")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-251">![Changing Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "Changing Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="f0b4d-252">*HTML 소스 편집 도구 모음의 Doctype 변경*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-252">*Changing Doctype in HTML Source Editing toolbar*</span></span>
5. <span data-ttu-id="f0b4d-253">**Body** 요소 아래에 커서를 놓고 HTML5 요소의 이름 (예: **비디오**)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-253">Place the cursor under the **body** element, and start typing the name of an HTML5 element (for example, **video**).</span></span> <span data-ttu-id="f0b4d-254">IntelliSense 목록에서 요소를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-254">Notice that the element is not available in the IntelliSense list.</span></span>

    <span data-ttu-id="f0b4d-255">![나열 되지 않은 HTML5 요소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "나열 되지 않은 HTML5 요소")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-255">![HTML5 elements not listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 elements not listed")</span></span>

    <span data-ttu-id="f0b4d-256">*나열 되지 않은 HTML5 요소*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-256">*HTML5 elements not listed*</span></span>
6. <span data-ttu-id="f0b4d-257">유효성 검사 도구 모음의 대상 스키마에 대 한 변경 내용을 취소 하 고 드롭다운 목록에서 DOCTYPE: XHTML5를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-257">Undo the changes to the Target Schema for Validation Toolbar, picking DOCTYPE: XHTML5 from the dropdown list.</span></span>

    <span data-ttu-id="f0b4d-258">![HTML 소스 편집 도구 모음에서 Doctype 사용](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "HTML 소스 편집 도구 모음에서 Doctype 사용")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-258">![Use Doctype in HTML Source Editing toolbar](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "Use Doctype in HTML Source Editing toolbar")</span></span>

    <span data-ttu-id="f0b4d-259">*HTML 원본 편집 도구 모음의 Doctype 다시 설정*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-259">*Reset Doctype in HTML Source Editing toolbar*</span></span>
7. <span data-ttu-id="f0b4d-260">**Body** 요소 아래에 커서를 놓고 HTML5 요소를 다시 입력 하기 시작 합니다 (예: **비디오**).</span><span class="sxs-lookup"><span data-stu-id="f0b4d-260">Place the cursor under the **body** element and start typing an HTML5 element again (For example, like **video**).</span></span> <span data-ttu-id="f0b4d-261">이제는 HTML5 요소를 IntelliSense 목록에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-261">Notice that the HTML5 elements are now available in the IntelliSense list.</span></span>

    <span data-ttu-id="f0b4d-262">![표시 되는 HTML5 요소](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "표시 되는 HTML5 요소")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-262">![HTML5 elements being listed](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "HTML5 elements being listed")</span></span>

    <span data-ttu-id="f0b4d-263">*표시 되는 HTML5 요소*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-263">*HTML5 elements being listed*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a><span data-ttu-id="f0b4d-264">작업 2-시작/끝 태그 자동 업데이트</span><span class="sxs-lookup"><span data-stu-id="f0b4d-264">Task 2 - Start/End Tags Automatic Update</span></span>

<span data-ttu-id="f0b4d-265">이제 Visual Studio는 편집 중인 요소의 HTML 여는 태그 또는 닫는 태그를 서로 일치 하도록 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-265">Visual Studio now updates the HTML opening or closing tags of the element that you are editing to match each other.</span></span> <span data-ttu-id="f0b4d-266">이 새로운 기능을 통해 HTML 태그를 편집할 때 생산성을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-266">This new feature will improve your productivity when editing HTML tags.</span></span>

1. <span data-ttu-id="f0b4d-267">**Default.aspx 페이지에서** 제목이 있는 **H3** 요소를 추가 합니다 (예: Visual Studio 2012 암석 지 어!).</span><span class="sxs-lookup"><span data-stu-id="f0b4d-267">On the **Default.aspx** page, add an **H3** element with a title (for example, Visual Studio 2012 Rocks!).</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. <span data-ttu-id="f0b4d-268">**H3** 태그를 변경 하 고 **H2** 또는 **H1을 입력 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f0b4d-268">Change the **H3** tag and type **H2** or **H1.**</span></span>

    <span data-ttu-id="f0b4d-269">끝 태그가 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-269">Notice that the end tag automatically updates.</span></span> <span data-ttu-id="f0b4d-270">또한 끝 태그를 수정 하 여 시작 태그가 그에 따라 업데이트 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-270">You can also modify the end tag to see that the start tag updates accordingly too.</span></span>

    <span data-ttu-id="f0b4d-271">![끝 태그의 자동 업데이트](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "끝 태그의 자동 업데이트")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-271">![Automatic update of the end tag](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Automatic update of the end tag")</span></span>

    <span data-ttu-id="f0b4d-272">*끝 태그의 자동 업데이트*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-272">*Automatic update of the end tag*</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a><span data-ttu-id="f0b4d-273">작업 3-새 HTML5 코드 조각</span><span class="sxs-lookup"><span data-stu-id="f0b4d-273">Task 3 - New HTML5 Code Snippets</span></span>

<span data-ttu-id="f0b4d-274">이제 Visual Studio에는 여러 HTML5 코드 조각이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-274">Visual Studio now includes several HTML5 code snippets.</span></span> <span data-ttu-id="f0b4d-275">이 작업에서는 다음 코드 조각 중 일부를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-275">In this task, you will use some of these snippets.</span></span>

1. <span data-ttu-id="f0b4d-276">이름이 **audio** 인 새 폴더를 웹 사이트 폴더의 루트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-276">Add a new folder named **audio** to the root of the web site folder.</span></span> <span data-ttu-id="f0b4d-277">Windows 탐색기를 열고 오디오 파일을 **WhatsNewASPNET** 솔루션의 **audio** 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-277">Open Windows Explorer and copy any audio file into the **audio** folder of the **WhatsNewASPNET.sln** solution.</span></span>
2. <span data-ttu-id="f0b4d-278">**Default.aspx 페이지에서** Web11 암석 지에서 커서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-278">In the **Default.aspx** page, locate the cursor under the Web11 Rocks!!</span></span> <span data-ttu-id="f0b4d-279">헤더.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-279">Header.</span></span> <span data-ttu-id="f0b4d-280">**Audio** 를 입력 하 고 tab 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-280">Type **audio** and press the TAB key.</span></span>

    <span data-ttu-id="f0b4d-281">새 HTML 편집기에는 HTML5 콘텐츠에 대 한 코드 조각이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-281">The new HTML editor includes code snippets for HTML5 content.</span></span> <span data-ttu-id="f0b4d-282">HTML5 코드 조각을 사용 하도록 설정 하려면 적절 한 DOCTYPE 정의를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-282">Remember to use the proper DOCTYPE definition to enable the HTML5 snippets.</span></span>

    <span data-ttu-id="f0b4d-283">![HTML5 코드 조각 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "HTML5 코드 조각 삽입")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-283">![Inserting HTML5 Code Snippets](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "Inserting HTML5 Code Snippets")</span></span>

    <span data-ttu-id="f0b4d-284">*HTML5 코드 조각 삽입*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-284">*Inserting HTML5 Code Snippets*</span></span>
3. <span data-ttu-id="f0b4d-285">기존 오디오 파일을 가리키도록 오디오 소스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-285">Update the audio source to point to an existing audio file.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > <span data-ttu-id="f0b4d-286">오디오 파일을 솔루션에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-286">You will need to add the audio file to the solution.</span></span>
4. <span data-ttu-id="f0b4d-287">**F5** 키를 눌러 사이트를 실행 하 고 오디오를 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-287">Press **F5** to run the site and play the audio.</span></span>

    <span data-ttu-id="f0b4d-288">![오디오 컨트롤 실행](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "오디오 컨트롤 실행")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-288">![Running the audio control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Running the audio control")</span></span>

    <span data-ttu-id="f0b4d-289">*오디오 컨트롤 실행*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-289">*Running the audio control*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0b4d-290">비디오, 그림 등 Visual Studio에 포함 된 추가 코드 조각을 사용해 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-290">You can also try more snippets included in Visual Studio, such as video, figure, etc.</span></span>
5. <span data-ttu-id="f0b4d-291">이제 페이지의 일부에 컨트롤을 삽입 해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-291">Now, try to insert a control in some part of the page.</span></span> <span data-ttu-id="f0b4d-292">예를 들어 **GridView** 컨트롤을 삽입 하려고 하지만 **&lt;눈금선를** 입력 하는 대신 **&lt;GV**를 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-292">For example, try to insert a **GridView** control, but instead of typing **&lt;Gri,** start typing **&lt;GV**.</span></span> <span data-ttu-id="f0b4d-293">IntelliSense 목록에 **asp: GridView** 컨트롤이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-293">Notice that the IntelliSense list shows the **asp:GridView** control.</span></span>

    <span data-ttu-id="f0b4d-294">HTML 편집기의 IntelliSense는 이제 부분 일치 (용어를 포함 하는 모든 요소 검색) 뿐만 아니라 부분 일치 검색을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-294">IntelliSense in the HTML Editor now provides title-casing search, as well as partial matching (retrieving all elements that contains the term).</span></span>

    <span data-ttu-id="f0b4d-295">![IntelliSense 목록을 사용 하 여 GridView 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "IntelliSense 목록을 사용 하 여 GridView 삽입")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-295">![Inserting a GridView with IntelliSense lists](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "Inserting a GridView with IntelliSense lists")</span></span>

    <span data-ttu-id="f0b4d-296">*IntelliSense 목록을 사용 하 여 GridView 삽입*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-296">*Inserting a GridView with IntelliSense lists*</span></span>

    <span data-ttu-id="f0b4d-297">**&lt;grid** 를 입력 하면 용어와 일치 하는 항목이 모두 표시 되지만 Visual Studio에서 **gridview** 컨트롤을 제안 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-297">If you type **&lt;grid** you will get all the items that match the term, but Visual Studio will suggest the **gridview** control:</span></span>

    <span data-ttu-id="f0b4d-298">![IntelliSense 목록과 부분 일치를 사용 하 여 GridView 삽입](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "IntelliSense 목록과 부분 일치를 사용 하 여 GridView 삽입")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-298">![Inserting a GridView with IntelliSense lists and partial matching](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "Inserting a GridView with IntelliSense lists and partial matching")</span></span>

    <span data-ttu-id="f0b4d-299">*IntelliSense 목록과 부분 일치를 사용 하 여 GridView 삽입*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-299">*Inserting a GridView with IntelliSense lists and partial matching*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a><span data-ttu-id="f0b4d-300">작업 4-HTML 편집기 스마트 태그</span><span class="sxs-lookup"><span data-stu-id="f0b4d-300">Task 4 - HTML Editor Smart Tags</span></span>

<span data-ttu-id="f0b4d-301">HTML 편집기의 또 다른 개선 사항은 스마트 태그 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-301">Another improvement in the HTML Editor is the Smart Tags feature.</span></span> <span data-ttu-id="f0b4d-302">스마트 태그를 사용 하면 컨트롤 단위로 일반적인 개발 작업 또는 반복적인 개발 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-302">Smart tags make it easy to perform common or repetitive development tasks on a per-control basis.</span></span> <span data-ttu-id="f0b4d-303">Html 디자이너에서는이 기능을 이미 사용할 수 있었지만 HTML 편집기에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-303">This feature was already available in the HTML Designer, but not in the HTML Editor.</span></span>

1. <span data-ttu-id="f0b4d-304">**Site.master** 를 열고 **asp: Menu** 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-304">Open **Site.Master** and locate the **asp:Menu** element.</span></span> <span data-ttu-id="f0b4d-305">시작 태그에 커서를 놓고 요소의 아래쪽에 작은 문자 모양이 표시 되는지 확인 하 고 클릭 하 여 스마트 작업 메뉴를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-305">Place the cursor on the start tag and notice that the small glyph displayed at the bottom of the element - click it to open the smart tasks menu.</span></span> <span data-ttu-id="f0b4d-306">메뉴 컨트롤과 관련 된 일부 작업에 빠르게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-306">Notice that you have quick access to some tasks related to the Menu control.</span></span>

    <span data-ttu-id="f0b4d-307">![메뉴 컨트롤에 대 한 스마트 작업](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "메뉴 컨트롤에 대 한 스마트 작업")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-307">![Smart tasks for the Menu control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Smart tasks for the Menu control")</span></span>

    <span data-ttu-id="f0b4d-308">*메뉴 컨트롤에 대 한 스마트 작업*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-308">*Smart tasks for the Menu control*</span></span>

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a><span data-ttu-id="f0b4d-309">작업 5-스마트 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="f0b4d-309">Task 5 - Smart Indentation</span></span>

<span data-ttu-id="f0b4d-310">HTML의 모범 사례 중 하나는 코드를 읽을 수 있도록 중첩 된 요소를 들여쓰는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-310">One of the best practices in HTML is indenting the nested elements to keep the code readable.</span></span> <span data-ttu-id="f0b4d-311">Visual Studio 2012에서는 코드를 작성 하는 동안 편집기에서 요소를 자동으로 들여씁니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-311">In Visual Studio 2012, you will notice that the editor automatically indents the elements while you are writing the code.</span></span>

> [!NOTE]
> <span data-ttu-id="f0b4d-312">이전 버전의 Visual Studio에서는 스마트 들여쓰기가 XML 편집기에서 사용할 수 있지만 HTML 편집기에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-312">In previous version of Visual Studio, smart indentation was available in the XML editor but not in the HTML editor.</span></span>

1. <span data-ttu-id="f0b4d-313">HTML 편집기의 들여쓰기 구성이 스마트 들여쓰기로 설정 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-313">Make sure that the Indenting configuration on the HTML Editor is set to Smart Indentation.</span></span> <span data-ttu-id="f0b4d-314">이렇게 하려면 도구를 선택 합니다. **| 옵션** 메뉴 옵션을 선택 하 고 **텍스트 편집기를 선택 합니다. HTML |** 화면의 왼쪽 창에 있는 탭 페이지</span><span class="sxs-lookup"><span data-stu-id="f0b4d-314">To do that, select the **Tools | Options** menu option and then select the **Text Editor | HTML | Tabs** page in the left pane of the screen.</span></span> <span data-ttu-id="f0b4d-315">스마트 들여쓰기 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-315">Select the Smart indentation option.</span></span>

    <span data-ttu-id="f0b4d-316">![HTML 편집기 설정](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML 편집기 설정")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-316">![HTML Editor settings](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML Editor settings")</span></span>

    <span data-ttu-id="f0b4d-317">*HTML 편집기 설정*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-317">*HTML Editor settings*</span></span>
2. <span data-ttu-id="f0b4d-318">**Default.aspx 페이지에서** audio 요소 아래의 모든 콘텐츠를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-318">On the **Default.aspx** page, remove all the content under the audio element.</span></span>
3. <span data-ttu-id="f0b4d-319">열린 **오디오** 요소의 끝에 커서를 놓고 **enter 키**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-319">Place the cursor at the end of the opening **audio** element and hit **ENTER**.</span></span>

    <span data-ttu-id="f0b4d-320">커서의 새 위치에는 추가 들여쓰기 수준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-320">Notice that the new position of cursor has an additional indentation level.</span></span>

    <span data-ttu-id="f0b4d-321">![HTML 편집기의 스마트 들여쓰기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "HTML 편집기의 스마트 들여쓰기")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-321">![Smart indentation in the HTML Editor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "Smart indentation in the HTML Editor")</span></span>

    <span data-ttu-id="f0b4d-322">*HTML 편집기의 스마트 들여쓰기*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-322">*Smart indentation in the HTML Editor*</span></span>
4. <span data-ttu-id="f0b4d-323">제거한 콘텐츠를 사용 하 여 audio 태그를 복원 하거나 변경 내용을 저장 하지 않고 default.aspx를 닫습니다 **.**</span><span class="sxs-lookup"><span data-stu-id="f0b4d-323">Restore the audio tag with the content you have removed, or close **Default.aspx** without saving the changes.</span></span>

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a><span data-ttu-id="f0b4d-324">작업 6-사용자 정의 컨트롤로 추출</span><span class="sxs-lookup"><span data-stu-id="f0b4d-324">Task 6 - Extract to User Control</span></span>

<span data-ttu-id="f0b4d-325">코드의 일부를 함수로 추출 하는 것과 같이 Visual Studio에 포함 된 리팩터링 도구는 향상 된 기능을 활용 하 고 기존 코드를 리팩터링할 수 있는 훌륭한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-325">The Refactoring tools included in Visual Studio, such as extracting a portion of code to a function, are great features that facilitate the improvement and the refactoring the existing code.</span></span> <span data-ttu-id="f0b4d-326">ASP.NET 페이지에 해당 하는는 사용자 정의 컨트롤에 대 한 HTML 코드를 추출 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-326">The counterpart for ASP.NET pages would be the extraction of HTML code to a User Control.</span></span> <span data-ttu-id="f0b4d-327">수동으로 작업을 수행 하는 경우 새 사용자 정의 컨트롤을 만들고, 코드 섹션을 사용자 컨트롤로 이동 하 고, 사용자 정의 컨트롤에 대 한 태그 접두사를 등록 하 고, 마지막으로 페이지에서 사용자 정의 컨트롤을 인스턴스화하는 것과 같은 여러 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-327">Doing it manually would involve several steps, like creating a new User Control, moving the code section to the User Control, registering a tag prefix for the User Control, and, finally, instantiating the User Control on the pages.</span></span> <span data-ttu-id="f0b4d-328">이제 새 *사용자 정의 컨트롤로 추출* 도구가 자동으로 이러한 단계를 모두 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-328">Now, the new *Extract to User Control* tool automatically performs all those steps for you.</span></span>

<span data-ttu-id="f0b4d-329">이 태스크에서는 새 사용자 정의 컨트롤을 사용 하 여 새 사용자 정의 컨트롤 컨텍스트 작업을 사용 하 여 선택한 코드에서 새 사용자 정의 컨트롤을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-329">In this task, you will use the new Extract to User Control contextual operation to generate a new user control from the selected code.</span></span>

1. <span data-ttu-id="f0b4d-330">**Default.aspx 페이지에서** **H2** 및 **audio** 요소를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-330">On the **Default.aspx** page, select the **H2** and **audio** elements.</span></span>
2. <span data-ttu-id="f0b4d-331">마우스 오른쪽 단추를 클릭 하 고 **사용자 정의 컨트롤로 추출을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-331">Right click and select **Extract to User Control**.</span></span>

    <span data-ttu-id="f0b4d-332">![사용자 정의 컨트롤로 추출 메뉴 옵션](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "사용자 정의 컨트롤로 추출 메뉴 옵션")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-332">![Extract to User Control menu option](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Extract to User Control menu option")</span></span>

    <span data-ttu-id="f0b4d-333">*사용자 정의 컨트롤로 추출 메뉴 옵션*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-333">*Extract to User Control menu option*</span></span>
3. <span data-ttu-id="f0b4d-334">새 사용자 정의 컨트롤의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-334">Type a name for the new user control.</span></span> <span data-ttu-id="f0b4d-335">예를 들어, **주크박스**를 클릭 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-335">For instance, **Jukebox.ascx**, and then click **OK**.</span></span>

    <span data-ttu-id="f0b4d-336">![추출한 사용자 정의 컨트롤 저장](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "추출한 사용자 정의 컨트롤 저장")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-336">![Saving the extracted user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Saving the extracted user control")</span></span>

    <span data-ttu-id="f0b4d-337">*추출한 사용자 정의 컨트롤 저장*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-337">*Saving the extracted user control*</span></span>
4. <span data-ttu-id="f0b4d-338">선택한 코드를 사용자 정의 컨트롤로 추출 하 고 선택한 코드의 원래 위치가 새 사용자 정의 컨트롤의 인스턴스로 대체 되었음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-338">Notice that the selected code was extracted to a user control and the original location of the selected code was replaced with an instance of the new user control.</span></span>

    <span data-ttu-id="f0b4d-339">![새 사용자 정의 컨트롤을 사용 하도록 페이지가 자동으로 업데이트 됩니다.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "새 사용자 정의 컨트롤을 사용 하도록 페이지가 자동으로 업데이트 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-339">![Page automatically updated to use the new user control](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Page automatically updated to use the new user control")</span></span>

    <span data-ttu-id="f0b4d-340">*새 사용자 정의 컨트롤을 사용 하도록 페이지가 자동으로 업데이트 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-340">*Page automatically updated to use the new user control*</span></span>
5. <span data-ttu-id="f0b4d-341">**F5** 키를 눌러 페이지를 실행 하 고 컨트롤이 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-341">Press **F5** to run the page and verify that the control works.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a><span data-ttu-id="f0b4d-342">연습 3: JavaScript 편집기의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f0b4d-342">Exercise 3: What's New in the JavaScript Editor</span></span>

<span data-ttu-id="f0b4d-343">JavaScript 코드를 작성 하거나 편집 하는 작업은 간단한 작업이 아닙니다. 특히 응용 프로그램 크기가 증가 하기 시작 하 고 긴 파일 및 수백 개의 함수를 처리 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-343">Writing or editing JavaScript code is not an easy task, especially when your application starts to grow in size and you find yourself dealing with long files and hundreds of functions.</span></span> <span data-ttu-id="f0b4d-344">스크립트 개발자는 일반적으로 코드 가독성을 유지 하 고 여러 파일을 탐색 하기 위해 몇 가지 추가 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-344">Script developers usually have to do some extra work to maintain code legibility and navigate across files.</span></span> <span data-ttu-id="f0b4d-345">JQuery와 같은 JavaScript 라이브러리를 포함 하 여 스크립트 탐색은 코드 길이 때문에 챌린지 자체가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-345">With the inclusion of JavaScript libraries like jQuery, script navigation has become a challenge itself because of the code length.</span></span>

<span data-ttu-id="f0b4d-346">Visual Studio는 코드 모드에 액세스 하 고 구성할 수 있도록 하 여 JavaScript 편집기를 갱신 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-346">Visual Studio has renewed the JavaScript editor with the promise to make the code mode accessible and organized.</span></span> <span data-ttu-id="f0b4d-347">또는 VB 편집기에 C# 이미 있던 많은 Visual Studio 기능이 JavaScript 편집기에서 구현 됩니다. 정의로 이동, 자동 들여쓰기, 설명서 및 작성 중에 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-347">Many Visual Studio features that already existed in C# or VB editors are now implemented in the JavaScript editor: Go To Definition, automatic indentation, documentation and validation when you are writing.</span></span> <span data-ttu-id="f0b4d-348">갱신 된 IntelliSense 목록에서 JavaScript 함수 카탈로그를 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-348">With the renewed IntelliSense list you will have the JavaScript function catalog at your fingertips.</span></span>

<span data-ttu-id="f0b4d-349">이 연습에서는 JavaScript 편집기의 새로운 기능 및 향상 된 기능 중 일부를 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-349">In this exercise, you will learn some of the new features and improvements of JavaScript editor.</span></span> <span data-ttu-id="f0b4d-350">샘플 파일을 탐색 하 고 Visual Studio 2012 내에서 JavaScript 프로그래밍의 효율성을 높일 수 있는 새로운 특성을 각각 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-350">You will browse sample files and discover each of the new characteristics that will make your JavaScript programming more efficient within Visual Studio 2012.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a><span data-ttu-id="f0b4d-351">작업 1-JavaScript 편집기의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f0b4d-351">Task 1 - JavaScript Editor New Features</span></span>

<span data-ttu-id="f0b4d-352">이 작업에서는 코드를 구성 하 고 더 나은 사용자 환경을 제공 하는 데 초점을 맞춘 새로운 JavaScript 편집기 기능 중 일부를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-352">This task will introduce you to some of the new JavaScript editor features, which focus on organizing your code and bringing a better user experience.</span></span>

1. <span data-ttu-id="f0b4d-353">아직 열지 않은 경우 **Visual Studio** 를 시작 하 고이 랩의 **Source\WhatsNewASPNET** 폴더에 있는 **WhatsNewASPNET** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-353">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="f0b4d-354">**F5** 키를 눌러 응용 프로그램을 실행 한 다음 탐색 모음에서 JavaScript 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-354">Press **F5** to run the application, then click the JavaScript link in the navigation bar.</span></span> <span data-ttu-id="f0b4d-355">페이지를 여러 번 새로 고치고 카운터가 증가 하는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-355">Refresh the page several times and check how the counter increments.</span></span>

    <span data-ttu-id="f0b4d-356">![페이지 카운터](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "페이지 카운터")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-356">![Page counter](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Page counter")</span></span>

    <span data-ttu-id="f0b4d-357">*페이지 카운터*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-357">*Page counter*</span></span>
3. <span data-ttu-id="f0b4d-358">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-358">Close the browser and go back to Visual Studio.</span></span>
4. <span data-ttu-id="f0b4d-359">**JavaScript .aspx** 페이지를 열고 아래에 표시 된 **&lt;스크립트&gt;** 블록을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-359">Open the **JavaScript.aspx** page and locate the **&lt;script&gt;** block (shown below).</span></span>

    <span data-ttu-id="f0b4d-360">다음 코드는 HTML5 로컬 저장소를 사용 하 여 현재 사용자가 페이지를 방문한 횟수를 저장 하는 *Pageloadcount* 변수를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-360">The following code uses HTML5 local storage to store a *pageLoadCount* variable that stores the number of times the page has been visited by the current user.</span></span> <span data-ttu-id="f0b4d-361">로컬 저장소는 HTML5 표준에 도입 된 클라이언트 쪽 키-값 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-361">Local Storage is a client-side key-value database introduced with the HTML5 standard.</span></span> <span data-ttu-id="f0b4d-362">데이터는 사용자의 브라우저 내에서 로컬 컴퓨터에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-362">The data is saved on the local machine, inside the user's browser.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="f0b4d-363">다음 단계를 진행 하기 전에 DOCTYPE이 XHTML5로 설정 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-363">Ensure the DOCTYPE is set to XHTML5 before proceeding with the next steps.</span></span>
5. <span data-ttu-id="f0b4d-364">코드를 편집 하 고 JavaScript 용 IntelliSense는 로컬 저장소와 같은 HTML5 기능과 내부 메서드를 포함 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-364">Edit the code and notice that IntelliSense for JavaScript includes HTML5 features, like local storage, and their inner methods.</span></span>

    <span data-ttu-id="f0b4d-365">![JavaScript의 HTML5 JavaScript 기능](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "JavaScript의 HTML5 JavaScript 기능")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-365">![HTML5 JavaScript features in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "HTML5 JavaScript features in JavaScript")</span></span>

    <span data-ttu-id="f0b4d-366">*JavaScript의 HTML5 JavaScript 기능*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-366">*HTML5 JavaScript features in JavaScript*</span></span>
6. <span data-ttu-id="f0b4d-367">스크립팅 코드에서 여는 대괄호 ( **{** )를 클릭 하면 대괄호가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-367">Click any opening bracket (**{**) from the scripting code and notice that the brackets are highlighted.</span></span>

    <span data-ttu-id="f0b4d-368">![대괄호가 강조 표시 됩니다.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "대괄호가 강조 표시 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-368">![Brackets are highlighted](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Brackets are highlighted")</span></span>

    <span data-ttu-id="f0b4d-369">*대괄호가 강조 표시 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-369">*Brackets are highlighted*</span></span>
7. <span data-ttu-id="f0b4d-370">**Testautoalign ()** 함수의 주석 처리를 제거 합니다 (3 개의 줄을 선택 하 고 **CTRL** + **K**를 사용할 수 있음). **CTRL** + **U**)를 누르고 함수 코드 내에서 커서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-370">Uncomment the function **testAutoAlign()** (select the three lines and you can use **CTRL** + **K**; **CTRL** + **U**) and locate the cursor inside the function code.</span></span> <span data-ttu-id="f0b4d-371">Enter 키를 눌러 두 번째 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-371">Press enter to append a second line.</span></span> <span data-ttu-id="f0b4d-372">이제 코드가 **정렬** 되 고 **자동으로 들여쓰기**됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-372">Notice that the code is now **aligned** and **auto-indented**.</span></span>

    <span data-ttu-id="f0b4d-373">![JavaScript 코드가 자동으로 정렬 됨](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript 코드가 자동으로 정렬 됨")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-373">![JavaScript code is auto aligned](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript code is auto aligned")</span></span>

    <span data-ttu-id="f0b4d-374">*JavaScript 코드가 자동으로 정렬 됨*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-374">*JavaScript code is auto aligned*</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a><span data-ttu-id="f0b4d-375">작업 2-JavaScript 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="f0b4d-375">Task 2 - Validating JavaScript</span></span>

<span data-ttu-id="f0b4d-376">이 작업에서는 ECMAScript5 표준에 대 한 새 JavaScript 유효성 검사를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-376">In this task, you will discover the new JavaScript validation for the ECMAScript5 standard.</span></span> <span data-ttu-id="f0b4d-377">이 기능을 통해 호환 되는 JavaScript 코드를 작성 하는 데 도움이 되지만 사이트 배포 이전에는 스크립팅 문제가 방지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-377">This feature will help you to write compliant JavaScript code, while preventing scripting issues before site deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="f0b4d-378">Visual studio 2010은 ECMAStript3 준수를 구현 했지만 Visual studio 2012은 ECMAScript5 규정 준수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-378">Visual Studio 2010 implemented ECMAStript3 compliance, while Visual Studio 2012 provides ECMAScript5 compliance.</span></span>

1. <span data-ttu-id="f0b4d-379">**Scripts\custom** 프로젝트 폴더 아래에 있는 **ECMA5script5** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-379">Open **ECMA5script5.js** located under the **Scripts\custom** project folder.</span></span> <span data-ttu-id="f0b4d-380">이제 ECMAScript5 표준에 대 한 유효성 검사를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-380">You will now test validation for ECMAScript5 standard.</span></span>

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    <span data-ttu-id="f0b4d-381">파일의 첫 번째 줄에서 **엄격한** &quot; 방향을 사용 하 &quot;를 체크 아웃할 수 있습니다. 그러면 ECMAScript5 **strict 모드**를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-381">You can check out the &quot; **use strict** &quot; direction in the first line of the file, which enables ECMAScript5 **strict mode**.</span></span> <span data-ttu-id="f0b4d-382">이 모드는 이전 버전의 모호성을 명확 하 게 하는 언어의 하위 집합으로 구성 되며 getter 및 setter와 같은 몇 가지 새로운 기능, JSON에 대 한 라이브러리 지원 및 개체 속성에 대 한 보다 완전 한 반사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-382">This mode consists in a subset of the language that clarifies ambiguities from the past edition, and adds some new features, such as getters and setters, library support for JSON, and more complete reflection on object properties.</span></span>
2. <span data-ttu-id="f0b4d-383">아직 열지 않은 경우 **오류 목록** 열기 (**보기** 메뉴 | **오류 목록**).</span><span class="sxs-lookup"><span data-stu-id="f0b4d-383">Open the **Error List** if not already opened (**View** menu | **Error List**).</span></span> <span data-ttu-id="f0b4d-384">**함수** 선언에는 밑줄이 그어집니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-384">Notice the **function** declaration is underlined.</span></span> <span data-ttu-id="f0b4d-385">이는 ECMA5 표준 함수를 언어 구조 안에 중첩할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-385">This is because in ECMA5 standard functions cannot be nested inside language structures.</span></span> <span data-ttu-id="f0b4d-386">아래 오류 목록에 경고 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-386">In the error list below you will see the warning details.</span></span>

    <span data-ttu-id="f0b4d-387">![JavaScript 유효성 검사 오류 메시지](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript 유효성 검사 오류 메시지")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-387">![JavaScript validation error message](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript validation error message")</span></span>

    <span data-ttu-id="f0b4d-388">*JavaScript 유효성 검사 오류 메시지*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-388">*JavaScript validation error message*</span></span>
3. <span data-ttu-id="f0b4d-389">**엄격한&quot;방향을 사용 하&quot;** 를 주석으로 처리 하 고 오류가 사라지지만 경고는 남아 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-389">Comment out the **&quot;use strict&quot;** direction and notice that errors disappear, but the warnings remain.</span></span>
4. <span data-ttu-id="f0b4d-390">파일의 마지막 줄에서 **&quot;테스트&quot;** 와 같은 문자열을 작성 합니다 (따옴표를 포함 하 여 문자열 임을 나타냄).</span><span class="sxs-lookup"><span data-stu-id="f0b4d-390">In the last line of the file, write any string like **&quot;test&quot;** (include the quotation marks to indicate it is as string).</span></span> <span data-ttu-id="f0b4d-391">문자열 옆에 마침표를 쓰고 IntelliSense 목록을 표시 한 다음 **trim** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-391">Write a period next to the string to display the IntelliSense list, and select the **trim** option.</span></span>

    <span data-ttu-id="f0b4d-392">ECMAScript5 standard에서 문자열 값 및 변수에는 trim, 대문자, 검색 및 바꾸기와 같은 문자열 메서드도 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-392">In ECMAScript5 standard, string values and variables also have string methods defined, like trim, uppercase, search and replace.</span></span>

    <span data-ttu-id="f0b4d-393">![JavaScript의 IntelliSense 목록](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript의 IntelliSense 목록")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-393">![IntelliSense list in JavaScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "IntelliSense list in JavaScript")</span></span>

    <span data-ttu-id="f0b4d-394">*JavaScript의 IntelliSense 목록*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-394">*IntelliSense list in JavaScript*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a><span data-ttu-id="f0b4d-395">작업 3-JavaScript에 대 한 XML 문서</span><span class="sxs-lookup"><span data-stu-id="f0b4d-395">Task 3 - XML Documentation for JavaScript</span></span>

<span data-ttu-id="f0b4d-396">이 작업에서는 JavaScript에서 XML 문서에 대 한 Visual Studio 기능을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-396">In this task, you will explore Visual Studio features for XML documentation in JavaScript.</span></span> <span data-ttu-id="f0b4d-397">이제 JavaScript IntelliSense 목록에 각 함수의 XML 문서가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-397">You will see the JavaScript IntelliSense list now shows the XML documentation of each function.</span></span> <span data-ttu-id="f0b4d-398">또한 JavaScript에서 탐색 기능을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-398">Additionally, you will discover the navigation feature in JavaScript.</span></span>

1. <span data-ttu-id="f0b4d-399">**스크립트/사용자 지정** 프로젝트 폴더에 있는 **xmldoc 주석의** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-399">Open **XMLDoc.js** file located in **Scripts/custom** project folder.</span></span> <span data-ttu-id="f0b4d-400">이 파일에는 각 JavaScript 함수에 대 한 XML 문서가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-400">This file contains XML documentation on each of the JavaScript functions.</span></span>

    <span data-ttu-id="f0b4d-401">![IntelliSense에 통합 되는 JavaScript XML 문서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "IntelliSense에 통합 되는 JavaScript XML 문서")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-401">![JavaScript XML documentation integrated to IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "JavaScript XML documentation integrated to IntelliSense")</span></span>

    <span data-ttu-id="f0b4d-402">*IntelliSense에 통합 되는 JavaScript XML 문서*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-402">*JavaScript XML documentation integrated to IntelliSense*</span></span>
2. <span data-ttu-id="f0b4d-403">**Xmldoc 주석의** 파일의 **add** 함수 아래에 **test**라는 새 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-403">Below **add** function in **XMLDoc.js** file, create a new function named **test**.</span></span>
3. <span data-ttu-id="f0b4d-404">**테스트** 함수에서 두 개의 매개 변수를 받는 **곱하기** 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-404">In the **test** function, call the **multiply** function that receives two parameters.</span></span> <span data-ttu-id="f0b4d-405">도구 설명 상자는 **곱하기** 함수 설명서를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-405">Notice the tooltip box is showing the **multiply** function documentation.</span></span>

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    <span data-ttu-id="f0b4d-406">![JavaScript 함수에 대 한 XML 문서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript 함수에 대 한 XML 문서")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-406">![XML documentation for JavaScript functions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "XML documentation for JavaScript functions")</span></span>

    <span data-ttu-id="f0b4d-407">*JavaScript 함수에 대 한 XML 문서*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-407">*XML documentation for JavaScript functions*</span></span>
4. <span data-ttu-id="f0b4d-408">함수 호출 문을 완료 하 고 *점을* 입력 하 여 반환 된 값에 대 한 IntelliSense 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-408">Complete the function call statement and type a *dot* to open the IntelliSense list on the returned value.</span></span> <span data-ttu-id="f0b4d-409">Visual Studio는 설명서에서 **반환** 값을 검색 하 여 값을 숫자로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-409">Notice that Visual Studio is detecting the **return** value in the documentation, treating the value as a number.</span></span>

    <span data-ttu-id="f0b4d-410">![반환 형식에 대 한 XML 문서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "반환 형식에 대 한 XML 문서")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-410">![XML documentation for return types](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "XML documentation for return types")</span></span>

    <span data-ttu-id="f0b4d-411">*반환 형식에 대 한 XML 문서*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-411">*XML documentation for return types*</span></span>
5. <span data-ttu-id="f0b4d-412">이제 함수 추가에 대 한 호출을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-412">Now, insert a call to add function.</span></span> <span data-ttu-id="f0b4d-413">JavaScript 편집기는 이제 함수 오버 로드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-413">Notice that the JavaScript editor now supports function overloads.</span></span> <span data-ttu-id="f0b4d-414">함수 이름을 작성 하면 설명서에 지정 된 사용 가능한 오버 로드를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-414">When you write a function name, you will be able to select any of the available overloads specified in the documentation.</span></span>

    <span data-ttu-id="f0b4d-415">![오버 로드에 대 한 XML 문서](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "오버 로드에 대 한 XML 문서")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-415">![XML documentation for overloads](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "XML documentation for overloads")</span></span>

    <span data-ttu-id="f0b4d-416">*오버 로드에 대 한 XML 문서*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-416">*XML documentation for overloads*</span></span>
6. <span data-ttu-id="f0b4d-417">**GotoDefinition** 파일을 열고 **$ () .html ()** 함수 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-417">Open **GotoDefinition.js** file and locate the **$().html()** function call.</span></span> <span data-ttu-id="f0b4d-418">**Html**에서 커서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-418">Locate the cursor on **html**.</span></span>
7. <span data-ttu-id="f0b4d-419">**F12** 키를 누르고 정의로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-419">Press **F12** and navigate to the definition.</span></span> <span data-ttu-id="f0b4d-420">이제 **찾기** 도구를 사용 하지 않고 JavaScript 코드를 액세스 하 고 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-420">Notice you can now access and browse your JavaScript code without using the **Find** tool.</span></span>
8. <span data-ttu-id="f0b4d-421">코드 파일의 맨 아래에 있는 서명 블록 앞에서 jQuery 명령의 커서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-421">Locate the cursor on the jQuery instruction prior to the signature block at the bottom of the code file.</span></span> <span data-ttu-id="f0b4d-422">**F12**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-422">Press **F12**.</span></span> <span data-ttu-id="f0b4d-423">JQuery 라이브러리 파일로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-423">You will navigate to the jQuery library file.</span></span> <span data-ttu-id="f0b4d-424">**F12**키를 사용 하 여 jQuery 파일을 탐색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-424">Notice you can also navigate across the jQuery files using **F12**.</span></span>

    <span data-ttu-id="f0b4d-425">![JQuery 정의로 이동](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "JQuery 정의로 이동")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-425">![Navigating to jQuery definitions](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "Navigating to jQuery definitions")</span></span>

    <span data-ttu-id="f0b4d-426">*JQuery 정의로 이동*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-426">*Navigating to jQuery definitions*</span></span>

> [!NOTE]
> <span data-ttu-id="f0b4d-427">GotoDefinition에 파일을 저장 하기 전에 구문 오류가 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-427">Make sure that GotoDefinition.js has no syntax errors before saving the file.</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a><span data-ttu-id="f0b4d-428">연습 4: 묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="f0b4d-428">Exercise 4: Bundling and Minification</span></span>

<span data-ttu-id="f0b4d-429">웹 사이트에 JavaScript 또는 CSS 파일이 둘 이상 포함 되는 횟수는 몇 개입니까?</span><span class="sxs-lookup"><span data-stu-id="f0b4d-429">How many times do your websites include more than one JavaScript or CSS file?</span></span> <span data-ttu-id="f0b4d-430">이는 번들 및 축소를 사용 하 여 파일 크기를 줄이고 사이트를 더 빠르게 수행 하는 데 도움이 되는 매우 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-430">This is a very common scenario where bundling and minification can help to reduce the file size and make the site perform faster.</span></span> <span data-ttu-id="f0b4d-431">ASP.NET 4.5의 새로운 번들 기능은 JS 또는 CSS 파일 집합을 단일 요소로 압축 하 고, 콘텐츠를 축소 하 여 크기를 줄입니다 (즉, 필요 하지 않은 빈 공간 제거, 주석 제거, 식별자 감소).</span><span class="sxs-lookup"><span data-stu-id="f0b4d-431">The new bundling feature in ASP.NET 4.5 packs a set of JS or CSS files into a single element, and reduces its size by minifying the content ( i.e. removing not required blank spaces, removing comments, reducing identifiers ).</span></span>

<span data-ttu-id="f0b4d-432">ASP.NET 4.5의 묶음 및 축소는 런타임에 수행 되어 사용자 에이전트 (예: IE, Mozilla 등)를 식별할 수 있습니다. 따라서 사용자 브라우저를 대상으로 지정 하 여 압축을 향상 시킵니다 (예: Mozilla 관련 된 콘텐츠 제거). 요청이 IE에서 제공 되는 경우).</span><span class="sxs-lookup"><span data-stu-id="f0b4d-432">Bundling and minification in ASP.NET 4.5 is performed at runtime, so that the process can identify the user agent (for example IE, Mozilla, etc), and thus, improve the compression by targeting the user browser (for instance, removing stuff that is Mozilla specific when the request comes from IE).</span></span>

<span data-ttu-id="f0b4d-433">이 연습에서는 ASP.NET 4.5에서 다양 한 종류의 묶음 및 축소를 사용 하도록 설정 하 고 사용 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-433">In this exercise, you will learn how to enable and use the different types of bundling and minification in ASP.NET 4.5.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a><span data-ttu-id="f0b4d-434">작업 1-NuGet에서 번들 및 축소 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="f0b4d-434">Task 1 - Installing the Bundling and Minification Package from NuGet</span></span>

1. <span data-ttu-id="f0b4d-435">아직 열지 않은 경우 **Visual Studio** 를 시작 하 고이 랩의 **Source\WhatsNewASPNET** 폴더에 있는 **WhatsNewASPNET** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-435">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="f0b4d-436">NuGet 패키지 관리자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-436">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="f0b4d-437">이렇게 하려면 **다른 Windows** | **패키지 관리자 콘솔** | 메뉴 **뷰** 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-437">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>

    <span data-ttu-id="f0b4d-438">![패키지 관리자 file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole 열기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "패키지 관리자 콘솔 열기")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-438">![Opening the package manager file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Opening the package manager console")</span></span>

    <span data-ttu-id="f0b4d-439">*패키지 관리자 콘솔 열기*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-439">*Opening the package manager console*</span></span>
3. <span data-ttu-id="f0b4d-440">**패키지 관리자 콘솔** 에서 **설치 패키지** 를 입력 하 고 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-440">In the **Package Manager Console,** type **Install-Package Microsoft.Web.Optimization** and press **ENTER**.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a><span data-ttu-id="f0b4d-441">작업 2-기본 번들</span><span class="sxs-lookup"><span data-stu-id="f0b4d-441">Task 2 - Default Bundles</span></span>

<span data-ttu-id="f0b4d-442">묶음 및 축소를 사용 하는 가장 간단한 방법은 기본 번들을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-442">The simplest way to use bundling and minification is to enable the default bundles.</span></span> <span data-ttu-id="f0b4d-443">이 메서드는 규칙을 사용 하 여 폴더의 JS 및 CSS 파일에 대해 제공 된 버전과 표시 되지 않은 버전을 참조할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-443">This method uses conventions to let you reference the bundled and minified version for the JS and CSS files in a folder.</span></span>

<span data-ttu-id="f0b4d-444">이 태스크에서는 함께 제공 된 JS 및 CSS 파일을 사용 하도록 설정 하 고 참조 하 고 결과 출력을 확인 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-444">In this task, you will learn how to enable and reference the bundled and minified JS and CSS files and view the resulting output.</span></span>

1. <span data-ttu-id="f0b4d-445">아직 열지 않은 경우 **Visual Studio** 를 시작 하 고이 랩의 **Source\WhatsNewASPNET** 폴더에 있는 **WhatsNewASPNET** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-445">If not already opened, start **Visual Studio** and open the **WhatsNewASPNET.sln** solution located in the **Source\WhatsNewASPNET** folder of this lab.</span></span>
2. <span data-ttu-id="f0b4d-446">**솔루션 탐색기**에서 **scripts\custom** 및 **scripts\custom** 폴더 **스타일**을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-446">In the **Solution Explorer**, expand the **Styles**, **Scripts\custom** and **Scripts\bundle** folders.</span></span>

    <span data-ttu-id="f0b4d-447">응용 프로그램에서 둘 이상의 CSS 및 JS 파일을 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-447">Notice that the application is using more than one CSS and JS file.</span></span>

    <span data-ttu-id="f0b4d-448">![응용 프로그램의 여러 스타일 시트 및 JavaScript 파일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "응용 프로그램의 여러 스타일 시트 및 JavaScript 파일")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-448">![Multiple Stylesheets and JavaScript files in the application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Multiple Stylesheets and JavaScript files in the application")</span></span>

    <span data-ttu-id="f0b4d-449">*응용 프로그램의 여러 스타일 시트 및 JavaScript 파일*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-449">*Multiple Stylesheets and JavaScript files in the application*</span></span>
3. <span data-ttu-id="f0b4d-450">**Global.asax.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-450">Open the **Global.asax.cs** file.</span></span>

    <span data-ttu-id="f0b4d-451">새 **Microsoft** 네임 스페이스는 파일의 시작 부분에서 주석으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-451">Notice that the new **Microsoft.Web.Optimization** namespace is commented out at the beginning of the file.</span></span> <span data-ttu-id="f0b4d-452">Using 지시문의 주석 처리를 제거 하 여 묶음 및 축소 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-452">Uncomment the using directive to include the bundling and minification features.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. <span data-ttu-id="f0b4d-453">**응용 프로그램\_Start** 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-453">Locate the **Application\_Start** method.</span></span>

    <span data-ttu-id="f0b4d-454">이 메서드에서는 아래 코드 조각과 같이 EnableDefaultBundles 호출의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-454">In this method, uncomment the EnableDefaultBundles call as shown in the snippet below.</span></span> <span data-ttu-id="f0b4d-455">이렇게 하면 해당 폴더에 대 한 경로를 사용 하 여 폴더에 있는 CSS 파일의 번들 컬렉션을 참조할 수 있으며 &quot;CSS&quot; 또는 &quot;JS&quot; 접미사를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-455">This enables us to reference a bundled collection of CSS files in a folder by using the path to that folder, plus the &quot;CSS&quot; or the &quot;JS&quot; suffix.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. <span data-ttu-id="f0b4d-456">**최적화 .aspx** 파일을 열고 **헤드 콘텐츠의**콘텐츠 컨트롤을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-456">Open the **Optimization.aspx** file and locate the content control for **HeadContent**.</span></span>

    <span data-ttu-id="f0b4d-457">CSS 파일 및 JS 파일에는 참조 된 단일 태그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-457">Notice the CSS files and the JS files have a single referenced tag.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > <span data-ttu-id="f0b4d-458">이 코드는 데모용입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-458">This code is for demo purposes.</span></span> <span data-ttu-id="f0b4d-459">이상적으로는 사이트 .Master 파일에서 번들을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-459">Ideally, you will reference the bundles in the Site.Master file.</span></span> <span data-ttu-id="f0b4d-460">이 샘플 코드에서는 일부 번들 파일이 Site.master 파일에 의해 참조 되는 것을 확인 하 여 마지막 참조를 중복 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-460">In this sample code, you will find that some of the bundled files are also being referenced by the Site.Master file, making this last reference redundant.</span></span>
6. <span data-ttu-id="f0b4d-461">링크는 **href** 특성의 묶음 규칙을 사용 하 여 각각 Styles 및 Scripts\custom 폴더에서 모든 CSS 또는 JS 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-461">Notice that the links are using the bundling conventions in the **href** attribute to get all the CSS or JS files from the Styles and Scripts\custom folder respectively.</span></span>

    <span data-ttu-id="f0b4d-462">아래 표시 된 것 처럼 **스크립트/사용자 지정/js** 경로를 사용 하 여 **스크립트/사용자 지정** 폴더 내의 모든 JS 파일을 번들로 묶어 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-462">You can use the path **Scripts/custom/JS** as shown below to bundle and minify all the JS files inside a **Scripts/custom** folder.</span></span> <span data-ttu-id="f0b4d-463">기본 번들의 기본 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-463">This is the default behavior with the default bundles.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. <span data-ttu-id="f0b4d-464">**Styles\Site.css** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-464">Open the **Styles\Site.css** file.</span></span>

    <span data-ttu-id="f0b4d-465">원래 CSS 파일에는 들여쓰기 된 코드, 공백 및 파일을 확장 하는 주석이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-465">Notice that the original CSS file contains indented code, blank spaces and comments that enlarge the file.</span></span> <span data-ttu-id="f0b4d-466">(또한 JavaScript 파일에는 공백 및 주석이 포함 되어 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="f0b4d-466">(Also the JavaScript file contains blank spaces and comments).</span></span>

    <span data-ttu-id="f0b4d-467">![Scripts 폴더의 원본 CSS 파일 중 하나](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Scripts 폴더의 원본 CSS 파일 중 하나")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-467">![One of the original CSS files in the Scripts folder](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "One of the original CSS files in the Scripts folder")</span></span>

    <span data-ttu-id="f0b4d-468">*Scripts 폴더의 원본 CSS 파일 중 하나*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-468">*One of the original CSS files in the Scripts folder*</span></span>
8. <span data-ttu-id="f0b4d-469">**F5** 키를 눌러 응용 프로그램을 실행 하 고 **최적화** 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-469">Press **F5** to run the application and navigate to the **Optimization** page.</span></span>
9. <span data-ttu-id="f0b4d-470">**CSS 번들** 링크를 클릭 하 여 파일을 다운로드 하 고 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-470">Click on the **CSS Bundle** link to download and open the file.</span></span>

    <span data-ttu-id="f0b4d-471">함께 제공 되는 파일을 체크 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-471">Check out the minified bundled file.</span></span> <span data-ttu-id="f0b4d-472">모든 공백, 주석 및 들여쓰기 문자가 제거 되어 더 작은 파일을 생성 하는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-472">You will notice that all the blank spaces, comments and indentation characters have been removed, generating a smaller file.</span></span>

    <span data-ttu-id="f0b4d-473">![번들로 제공 되는 CSS 파일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "번들로 제공 되는 CSS 파일")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-473">![Bundled CSS files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Bundled CSS files")</span></span>

    <span data-ttu-id="f0b4d-474">*번들로 제공 되는 CSS 파일*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-474">*Bundled CSS files*</span></span>
10. <span data-ttu-id="f0b4d-475">이제 **JS 번들** 링크를 클릭 하 여 JavaScript 번들 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-475">Now click the **JS Bundle** link to open the JavaScript bundled file.</span></span> <span data-ttu-id="f0b4d-476">탐색기 경고는 무시 해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-476">You can safely disregard the explorer warning.</span></span> <span data-ttu-id="f0b4d-477">**사용자 지정** 폴더 아래의 JavaScript 파일도 번들로 표시 되 고 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-477">Notice the JavaScript files under the **custom** folder are also bundled and minified.</span></span>

    <span data-ttu-id="f0b4d-478">![번들로 제공 되는 JavaScript 파일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "번들로 제공 되는 JavaScript 파일")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-478">![Bundled JavaScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Bundled JavaScript files")</span></span>

    <span data-ttu-id="f0b4d-479">*번들로 제공 되는 JavaScript 파일*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-479">*Bundled JavaScript files*</span></span>

    <span data-ttu-id="f0b4d-480">이전 ASP.NET 버전에서는 CSS 또는 JS 파일에 대해 압축을 사용 하는 것이 훨씬 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-480">Enabling compression for CSS or JS files was much more complicated in previous ASP.NET version.</span></span> <span data-ttu-id="f0b4d-481">이제 *global.asax* 파일에 한 줄을 추가 하 여 번들을 사용 하도록 설정한 다음 사이트에서 번들로 제공 되는 파일을 참조 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-481">Now, as you have seen, you just need to add one line in the *Global.asax* file to enable bundling, and then reference the bundled files from your site.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a><span data-ttu-id="f0b4d-482">작업 3-정적 번들</span><span class="sxs-lookup"><span data-stu-id="f0b4d-482">Task 3 - Static Bundles</span></span>

<span data-ttu-id="f0b4d-483">정적 번들 방식을 사용 하면 사용할 파일 집합, 참조 및 사용 되는 축소 메서드를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-483">The static bundle approach allows you to customize the set of files to bundle, the reference and the minification method that will be used.</span></span>

<span data-ttu-id="f0b4d-484">이 작업에서는 번들로 지정 된 특정 파일 집합을 정의 하도록 정적 번들을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-484">In this task, you will configure a static bundle to define a specific set of files to bundle and minify.</span></span>

1. <span data-ttu-id="f0b4d-485">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-485">Close the browser.</span></span>
2. <span data-ttu-id="f0b4d-486">**Global.asax.cs** 파일을 열고 **응용 프로그램\_Start** 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-486">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
3. <span data-ttu-id="f0b4d-487">아래 코드에 표시 된 것 처럼 정적 번들 코드의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-487">Uncomment the static bundle code as shown in the code below.</span></span>

    <span data-ttu-id="f0b4d-488">&quot; **~/Staticbundle**&quot; 가상 경로를 사용 하 여 참조 되는 정적 번들을 정의 하 고 **AddFile** 메서드를 사용 하 여 지정 된 모든 파일의 축소에 **JsMinify** 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-488">You are defining a static bundle that will be referenced with the &quot;**~/StaticBundle**&quot; virtual path and use **JsMinify** for minification of all the specified files with the **AddFile** method.</span></span> <span data-ttu-id="f0b4d-489">마지막으로 **bundletable.enableoptimization** 에 정적 번들을 추가 하 고 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-489">Finally, you are adding the static bundle to the **BundleTable** and enabling it.</span></span>

    <span data-ttu-id="f0b4d-490">파일이 동일한 위치에 있지 않은 것을 알 수 있습니다. 이는 기본 묶음의 또 다른 장점입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-490">Notice that the files are not located in the same place; this is another advantage over the default bundling.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. <span data-ttu-id="f0b4d-491">**최적화 .aspx** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-491">Open the **Optimization.aspx** file.</span></span>

    <span data-ttu-id="f0b4d-492">**정적 JS 번들** 에 대 한 링크는 Global.asax.cs 파일에서 정적 번들을 구성할 때 선언 된 경로를 사용 하 고 있습니다. **/staticbundle**.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-492">Notice that the link to **Static JS Bundle** is using the path you have declared when you configured the static bundle in the Global.asax.cs file: **/StaticBundle**.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. <span data-ttu-id="f0b4d-493">**F5** 키를 눌러 응용 프로그램을 실행 한 다음 **최적화** 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-493">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
6. <span data-ttu-id="f0b4d-494">**정적 JS 번들** 링크를 클릭 하 여 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-494">Click on the **Static JS Bundle** link to open the file.</span></span>

    <span data-ttu-id="f0b4d-495">함께 제공 된 모든 JavaScript 파일의 출력은 고정 번들 파일에서 구성 된 모든 JavaScript 파일의 출력으로, &quot;/StaticBundle&quot;경로 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-495">Notice that the minified bundled JavaScript file is the output for all the JavaScript files configured in the static bundle file under the path &quot;/StaticBundle&quot;.</span></span>

    <span data-ttu-id="f0b4d-496">![정적 JavaScript 파일 번들](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "정적 JavaScript 파일 번들")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-496">![Static JavaScript files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Static JavaScript files bundle")</span></span>

    <span data-ttu-id="f0b4d-497">*정적 JavaScript 파일 번들*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-497">*Static JavaScript files bundle*</span></span>
7. <span data-ttu-id="f0b4d-498">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-498">Close the browser and return to Visual Studio.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a><span data-ttu-id="f0b4d-499">작업 4-동적 폴더 번들</span><span class="sxs-lookup"><span data-stu-id="f0b4d-499">Task 4 - Dynamic Folder Bundles</span></span>

<span data-ttu-id="f0b4d-500">이 작업에서는 동적 폴더 번들을 구성 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-500">In this task, you will learn how to configure dynamic folder bundles.</span></span> <span data-ttu-id="f0b4d-501">동적 번들의 기능은 정적 JavaScript와 JavaScript로 컴파일되는 언어의 다른 파일을 포함할 수 있으므로 번들이 실행 되기 전에 약간의 처리가 필요 하다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-501">The power of dynamic bundling is that you can include static JavaScript, as well as other files in languages that compiles into JavaScript, and thus, require some processing before the bundling is executed.</span></span>

<span data-ttu-id="f0b4d-502">이 예제에서는 **Dynamicfolderbundle** 클래스를 사용 하 여 CofeeScript로 작성 된 파일에 대 한 동적 번들을 만드는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-502">In this example, you will learn how to use the **DynamicFolderBundle** class to create a dynamic bundle for files written in CofeeScript.</span></span> <span data-ttu-id="f0b4d-503">CofeeScript는 javascript로 컴파일되고 javascript 코드를 작성 하는 간단한 구문을 제공 하 여 JavaScript의 간결 하 고 가독성이 향상 되는 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-503">CofeeScript is a programming language that compiles into JavaScript and provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability.</span></span>

1. <span data-ttu-id="f0b4d-504">**Global.asax.cs** 파일을 열고 **응용 프로그램\_Start** 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-504">Open the **Global.asax.cs** file and locate the **Application\_Start** method.</span></span>
2. <span data-ttu-id="f0b4d-505">아래 코드에 표시 된 것 처럼 동적 번들 코드의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-505">Uncomment the dynamic bundle code as shown in the code below.</span></span>

    <span data-ttu-id="f0b4d-506">&quot; **. 커피**&quot; 확장 (CoffeeScript 파일)을 사용 하 여 파일에만 적용 되는 **CoffeeMinify** 사용자 지정 축소 프로세서를 사용 하는 동적 폴더 번들을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-506">You are defining a dynamic folder bundle that will use the **CoffeeMinify** custom minification processor that will only apply to the files with the &quot;**.coffee**&quot; extension (CoffeeScript files).</span></span> <span data-ttu-id="f0b4d-507">검색 패턴을 사용 하 여 폴더 내에서 묶을 파일을 선택할 수 있습니다 (예: '\*. 커피 ').</span><span class="sxs-lookup"><span data-stu-id="f0b4d-507">Notice that you can use a search pattern to select the files to bundle within a folder, like '\*.coffee'.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. <span data-ttu-id="f0b4d-508">NuGet 패키지 관리자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-508">Open the NuGet Package Manager Console.</span></span> <span data-ttu-id="f0b4d-509">이렇게 하려면 **다른 Windows** | **패키지 관리자 콘솔** | 메뉴 **뷰** 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-509">To do this, use the menu **View** | **Other Windows** | **Package Manager Console**.</span></span>
4. <span data-ttu-id="f0b4d-510">**패키지 관리자 콘솔** 에서 **Install CoffeeSharp** **을 입력 하 고 enter 키를**누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-510">In the **Package Manager Console,** type **Install-Package CoffeeSharp** and press **ENTER**.</span></span>
5. <span data-ttu-id="f0b4d-511">**솔루션 탐색기** 창에서 **모든 파일 표시** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-511">Click the **Show All Files** button in the **Solution Explorer** window</span></span>

    <span data-ttu-id="f0b4d-512">![모든 파일 표시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "모든 파일 표시")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-512">![Showing all files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Showing all files")</span></span>

    <span data-ttu-id="f0b4d-513">*모든 파일 표시*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-513">*Showing all files*</span></span>
6. <span data-ttu-id="f0b4d-514">**솔루션 탐색기** 에서 **CoffeeMinify.cs** 파일을 마우스 오른쪽 단추로 클릭 하 고 **프로젝트에 포함** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-514">Right click the **CoffeeMinify.cs** file in the **Solution Explorer** and select **Include in Project**</span></span>

    <span data-ttu-id="f0b4d-515">![프로젝트에 CoffeeMinify.cs 파일 포함](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "프로젝트에 CoffeeMinify.cs 파일 포함")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-515">![Include the CoffeeMinify.cs file in the project](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "Include the CoffeeMinify.cs file in the project")</span></span>

    <span data-ttu-id="f0b4d-516">*프로젝트에 CoffeeMinify.cs 파일 포함*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-516">*Include the CoffeeMinify.cs file in the project*</span></span>
7. <span data-ttu-id="f0b4d-517">**CoffeeMinify.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-517">Open the **CoffeeMinify.cs** file.</span></span>

    <span data-ttu-id="f0b4d-518">이 클래스는 CoffeeScript 코드 컴파일에서 생성 된 JavaScript 출력을 JsMinify에서 미니로 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-518">This class inherits from JsMinify to minify the JavaScript output resulting from the CoffeeScript code compilation.</span></span> <span data-ttu-id="f0b4d-519">CoffeeScript 컴파일러를 호출 하 여 JavaScript 코드를 먼저 생성 한 다음 JsMinify 메서드로 보내 결과 코드를 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-519">It calls the CoffeeScript compiler to generate the JavaScript code first, and then it sends it to the JsMinify.Process method to minify the resulting code.</span></span>

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. <span data-ttu-id="f0b4d-520">**Scripts/번들** 폴더에서 **Script1** 및 **Script2** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-520">Open the **Script1.coffee** and **Script2.coffee** files from the **Scripts/bundle** folder.</span></span>

    <span data-ttu-id="f0b4d-521">이러한 파일에는 CoffeeMinify 클래스를 사용 하 여 번들을 수행 하는 동안 컴파일될 CoffeScript 코드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-521">These files will include the CoffeScript code to be compiled while performing the bundling with the CoffeeMinify class.</span></span>

    <span data-ttu-id="f0b4d-522">간단한 설명을 위해 제공 된 CoffeeScript 파일은 CoffeeScript 샘플 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-522">For simplicity purposes, the CoffeeScript files provided are only including CoffeeScript sample code.</span></span> <span data-ttu-id="f0b4d-523">주석은 JsMinify 프로세스에 의해 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-523">The comments are excluded by the JsMinify process.</span></span>

    <span data-ttu-id="f0b4d-524">![CoffeeScript 파일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript 파일")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-524">![CoffeeScript files](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript files")</span></span>

    <span data-ttu-id="f0b4d-525">*CoffeeScript 파일*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-525">*CoffeeScript files*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0b4d-526">[CofeeScript](https://github.com/jashkenas/coffeescript/) 는 javascript 코드를 작성 하는 간단한 구문을 제공 하 여 javascript의 간결 하 고 가독성이 향상 되 고 배열 이해 및 패턴 일치와 같은 다른 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-526">[CofeeScript](https://github.com/jashkenas/coffeescript/) provides a simpler syntax for writing JavaScript code, enhancing JavaScript's brevity and readability, as well as adding other features like array comprehension and pattern matching.</span></span>
9. <span data-ttu-id="f0b4d-527">**최적화 .aspx** 파일을 열고 번들 링크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-527">Open the **Optimization.aspx** file and locate the bundle links.</span></span>

    <span data-ttu-id="f0b4d-528">**동적 JS 번들** 에 대 한 링크는 동적 폴더 번들에 대해 구성한 **/coffee** 접미사를 사용 하 여 **스크립트/번들** 폴더를 참조 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-528">Notice that the link to **Dynamic JS Bundle** is referencing the **Scripts/bundle** folder by using the **/Coffee** suffix you configured for the dynamic folder bundle.</span></span>

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. <span data-ttu-id="f0b4d-529">**F5** 키를 눌러 응용 프로그램을 실행 한 다음 **최적화** 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-529">Press **F5** to run the application, and then navigate to the **Optimization** page.</span></span>
11. <span data-ttu-id="f0b4d-530">**동적 JS 번들** 링크를 클릭 하 여 생성 된 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-530">Click on the **Dynamic JS Bundle** link to open the generated file.</span></span>

    <span data-ttu-id="f0b4d-531">이 번들에 포함 된 콘텐츠는 커피 파일만 포함 하 고 있습니다 **.**</span><span class="sxs-lookup"><span data-stu-id="f0b4d-531">Notice that the content that was included in this bundle only contains **.coffee** files.</span></span> <span data-ttu-id="f0b4d-532">CoffeeScript 코드를 JavaScript로 컴파일 했 고 주석 처리 된 줄이 제거 되었음을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-532">You can also see that the CoffeeScript code was compiled to JavaScript and the commented-out lines has been removed.</span></span>

    <span data-ttu-id="f0b4d-533">![동적 JS 파일 번들](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "동적 JS 파일 번들")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-533">![Dynamic JS files bundle](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Dynamic JS files bundle")</span></span>

    <span data-ttu-id="f0b4d-534">*동적 JS 파일 번들*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-534">*Dynamic JS files bundle*</span></span>

> [!NOTE]
> <span data-ttu-id="f0b4d-535">또한 [부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)를 수행 하는 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-535">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="f0b4d-536">요약</span><span class="sxs-lookup"><span data-stu-id="f0b4d-536">Summary</span></span>

<span data-ttu-id="f0b4d-537">이 랩을 통해 Visual Studio 2012에서 ASP.NET 및 웹 개발의 새로운 기능 및 Visual Studio 2012의 다양 한 향상 된 기능을 활용 하는 방법을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-537">This lab helps you to understand what New in ASP.NET and Web Development in Visual Studio 2012 is and how to take advantage of the variety of enhancements in Visual Studio 2012.</span></span>

<span data-ttu-id="f0b4d-538">이 실습 실습을 완료 하면 Visual Studio 2012 편집기에서 CSS, JavaScript 및 HTML에 대 한 새로운 기능 및 향상 된 기능을 사용 하는 방법을 학습 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-538">By completing this Hands-On Lab, you have learnt how to use the new features and improvements in Visual Studio 2012 Editors for CSS, JavaScript and HTML.</span></span> <span data-ttu-id="f0b4d-539">또한 Visual Studio 2012에서 기본 제공 번들 및 축소를 구현 하는 방법도 학습 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-539">In addition, you have learnt how Visual Studio 2012 implements built-in bundling and minification.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="f0b4d-540">부록 A: 웹에 대 한 Visual Studio Express 2012 설치</span><span class="sxs-lookup"><span data-stu-id="f0b4d-540">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="f0b4d-541">**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-541">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="f0b4d-542">다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-542">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="f0b4d-543">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-543">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="f0b4d-544">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-544">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="f0b4d-545">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-545">Click on **Install Now**.</span></span> <span data-ttu-id="f0b4d-546">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-546">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="f0b4d-547">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-547">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="f0b4d-548">![Visual Studio Express 설치](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-548">![Install Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="f0b4d-549">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-549">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="f0b4d-550">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-550">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    <span data-ttu-id="f0b4d-552">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-552">*Accepting the license terms*</span></span>
5. <span data-ttu-id="f0b4d-553">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-553">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    <span data-ttu-id="f0b4d-555">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-555">*Installation progress*</span></span>
6. <span data-ttu-id="f0b4d-556">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-556">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    <span data-ttu-id="f0b4d-558">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-558">*Installation completed*</span></span>
7. <span data-ttu-id="f0b4d-559">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-559">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="f0b4d-560">웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-560">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    <span data-ttu-id="f0b4d-562">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-562">*VS Express for Web tile*</span></span>

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f0b4d-563">부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="f0b4d-563">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="f0b4d-564">이 부록에서는 windows azure 관리 포털에서 새 웹 사이트를 만들고 랩에 따라 가져온 응용 프로그램을 게시 하 여 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-564">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="f0b4d-565">작업 1-Windows Azure 포털에서 새 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="f0b4d-565">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="f0b4d-566">[Windows Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-566">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0b4d-567">Windows Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 후 트래픽 증가에 따라 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-567">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="f0b4d-568">[여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-568">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="f0b4d-569">![Windows Azure Portal에 로그온 합니다.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Windows Azure Portal에 로그온 합니다.")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-569">![Log on to Windows Azure portal](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="f0b4d-570">*Windows Azure 관리 포털에 로그온 합니다.*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-570">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="f0b4d-571">명령 모음에서 **새로 만들기** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-571">Click **New** on the command bar.</span></span>

    <span data-ttu-id="f0b4d-572">![새 웹 사이트 만들기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-572">![Creating a new Web Site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="f0b4d-573">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-573">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="f0b4d-574">**Compute** | **웹 사이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-574">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="f0b4d-575">그런 다음 **빠른 생성** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-575">Then select **Quick Create** option.</span></span> <span data-ttu-id="f0b4d-576">새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-576">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0b4d-577">Microsoft Azure 웹 사이트는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-577">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="f0b4d-578">빠른 생성 옵션을 사용 하면 포털 외부에서 Windows Azure 웹 사이트에 완료 된 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-578">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="f0b4d-579">데이터베이스를 설정 하는 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-579">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="f0b4d-580">![빠른 생성을 사용 하 여 새 웹 사이트 만들기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-580">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="f0b4d-581">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-581">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="f0b4d-582">새 **웹 사이트가** 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-582">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="f0b4d-583">웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-583">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="f0b4d-584">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-584">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="f0b4d-585">![새 웹 사이트로 이동](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "새 웹 사이트로 이동")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-585">![Browsing to the new web site](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="f0b4d-586">*새 웹 사이트로 이동*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-586">*Browsing to the new web site*</span></span>

    <span data-ttu-id="f0b4d-587">![웹 사이트 실행 중](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "웹 사이트 실행 중")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-587">![Web site running](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Web site running")</span></span>

    <span data-ttu-id="f0b4d-588">*웹 사이트 실행 중*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-588">*Web site running*</span></span>
6. <span data-ttu-id="f0b4d-589">포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-589">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="f0b4d-590">![웹 사이트 관리 페이지 열기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-590">![Opening the web site management pages](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="f0b4d-591">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-591">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="f0b4d-592">**대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-592">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0b4d-593">*게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-593">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="f0b4d-594">게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-594">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="f0b4d-595">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 게시 프로필 읽기를 지원 하 여 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하기 위해 이러한 프로그램의 구성을 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-595">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="f0b4d-596">![웹 사이트 게시 프로필을 다운로드 하는 중](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "웹 사이트 게시 프로필을 다운로드 하는 중")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-596">![Downloading the web site publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="f0b4d-597">*웹 사이트 게시 프로필을 다운로드 하는 중*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-597">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="f0b4d-598">알려진 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-598">Download the publish profile file to a known location.</span></span> <span data-ttu-id="f0b4d-599">이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-599">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="f0b4d-600">![게시 프로필 파일을 저장 하는 중](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "게시 프로필을 저장 하는 중")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-600">![Saving the publish profile file](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Saving the publish profile")</span></span>

    <span data-ttu-id="f0b4d-601">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-601">*Saving the publish profile file*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="f0b4d-602">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="f0b4d-602">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="f0b4d-603">응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-603">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="f0b4d-604">SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-604">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="f0b4d-605">응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-605">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="f0b4d-606">Microsoft Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL 데이터베이스** | **서버** | **서버의 대시보드**.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-606">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="f0b4d-607">만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-607">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="f0b4d-608">다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-608">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="f0b4d-609">이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-609">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="f0b4d-610">![SQL Database 서버 대시보드](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-610">![SQL Database Server Dashboard](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="f0b4d-611">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-611">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="f0b4d-612">다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-612">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="f0b4d-613">이렇게 하려면 **구성**을 클릭 하 고 **현재 클라이언트 IP 주소** 에서 ip 주소를 선택한 후 **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-613">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes.</span></span> <span data-ttu-id="f0b4d-614">규칙의 이름을 입력 하 고 ![-](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png)---------------------------</span><span class="sxs-lookup"><span data-stu-id="f0b4d-614">Enter a name for the rule and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) button.</span></span>

    ![클라이언트 IP 주소를 추가 하는 중](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    <span data-ttu-id="f0b4d-616">*클라이언트 IP 주소를 추가 하는 중*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-616">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="f0b4d-617">**클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-617">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 내용 확인](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    <span data-ttu-id="f0b4d-619">*변경 내용 확인*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-619">*Confirm Changes*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f0b4d-620">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="f0b4d-620">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="f0b4d-621">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-621">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="f0b4d-622">**솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-622">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="f0b4d-623">![응용 프로그램 게시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-623">![Publishing the Application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Publishing the Application")</span></span>

    <span data-ttu-id="f0b4d-624">*웹 사이트 게시*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-624">*Publishing the web site*</span></span>
2. <span data-ttu-id="f0b4d-625">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-625">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="f0b4d-626">![게시 프로필을 가져오는 중](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "게시 프로필을 가져오는 중")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-626">![Importing the publish profile](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Importing the publish profile")</span></span>

    <span data-ttu-id="f0b4d-627">*게시 프로필을 가져오는 중*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-627">*Importing publish profile*</span></span>
3. <span data-ttu-id="f0b4d-628">**연결 유효성 검사**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-628">Click **Validate Connection**.</span></span> <span data-ttu-id="f0b4d-629">유효성 검사가 완료 되 면 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-629">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0b4d-630">유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-630">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="f0b4d-631">![연결 유효성 검사](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-631">![Validating connection](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Validating connection")</span></span>

    <span data-ttu-id="f0b4d-632">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-632">*Validating connection*</span></span>
4. <span data-ttu-id="f0b4d-633">**설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-633">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="f0b4d-634">![웹 배포 구성](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-634">![Web deploy configuration](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web deploy configuration")</span></span>

    <span data-ttu-id="f0b4d-635">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-635">*Web deploy configuration*</span></span>
5. <span data-ttu-id="f0b4d-636">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-636">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="f0b4d-637">**서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-637">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="f0b4d-638">**사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-638">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="f0b4d-639">**암호** 에 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-639">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="f0b4d-640">새 데이터베이스 이름 (예: *MVC4SampleDB*)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-640">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="f0b4d-641">![대상 연결 문자열 구성](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-641">![Configuring destination connection string](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="f0b4d-642">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-642">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="f0b4d-643">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-643">Then click **OK**.</span></span> <span data-ttu-id="f0b4d-644">데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-644">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="f0b4d-645">![데이터베이스 만들기](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-645">![Creating the database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Creating the database string")</span></span>

    <span data-ttu-id="f0b4d-646">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-646">*Creating the database*</span></span>
7. <span data-ttu-id="f0b4d-647">Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-647">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="f0b4d-648">그런 후 **Next** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-648">Then click **Next**.</span></span>

    <span data-ttu-id="f0b4d-649">![SQL Database를 가리키는 연결 문자열](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "SQL Database를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-649">![Connection string pointing to SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="f0b4d-650">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-650">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="f0b4d-651">**미리 보기** 페이지에서 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-651">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="f0b4d-652">![웹 응용 프로그램 게시](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-652">![Publishing the web application](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Publishing the web application")</span></span>

    <span data-ttu-id="f0b4d-653">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-653">*Publishing the web application*</span></span>
9. <span data-ttu-id="f0b4d-654">게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0b4d-654">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="f0b4d-655">![Windows Azure에 게시 된 응용 프로그램](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Windows Azure에 게시 된 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="f0b4d-655">![Application published to Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="f0b4d-656">*Windows Azure에 게시 된 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="f0b4d-656">*Application published to Windows Azure*</span></span>
