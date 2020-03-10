---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Visual Studio를 사용 하 여 프로그래밍 ASP.NET 웹 페이지 (Razor) | Microsoft Docs
author: Rick-Anderson
description: 이 부록은 Visual Studio 2010 또는 Visual Web Developer 2010 Express를 사용 하 여 Razor 구문 ASP.NET 웹 페이지를 프로그래밍 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514295"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="299fc-103">Visual Studio를 사용 하 여 프로그래밍 ASP.NET 웹 페이지 (Razor)</span><span class="sxs-lookup"><span data-stu-id="299fc-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="299fc-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="299fc-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="299fc-105">이 문서에서는 Visual Studio 또는 Visual Web Developer Express를 사용 하 여 Razor (ASP.NET 웹 페이지) 웹 사이트를 프로그래밍 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="299fc-106">학습할 내용</span><span class="sxs-lookup"><span data-stu-id="299fc-106">What you'll learn</span></span>
>
> - <span data-ttu-id="299fc-107">Visual Studio 버전에서 ASP.NET 웹 페이지 작업을 수행 하기 위해 필요한 항목 (있는 경우)입니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="299fc-108">Visual Web Developer 2010 Express에 ASP.NET 웹 페이지에 대 한 지원을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="299fc-109">Visual Studio의 기능을 사용 하 여 IntelliSense 및 디버거를 비롯 한 ASP.NET Razor 페이지로 작업 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="299fc-110">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="299fc-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="299fc-111">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="299fc-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="299fc-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="299fc-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="299fc-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="299fc-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="299fc-114">이 자습서는 ASP.NET 웹 페이지 2, Visual Studio 2012, Visual Studio 2010 및 WebMatrix 2에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="299fc-115">WebMatrix 또는 다른 많은 코드 편집기를 사용 하 여 Razor 구문 ASP.NET 웹 페이지를 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="299fc-116">모든 기능을 갖춘 IDE (통합 개발 환경) 인 Microsoft Visual Studio를 사용 하 여 웹 사이트 뿐만 아니라 여러 유형의 응용 프로그램을 만들 수 있는 강력한 도구 집합을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="299fc-117">ASP.NET Razor 페이지로 작업 하려면 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="299fc-118">ASP.NET Razor 웹 페이지를 사용 하 여 프로그래밍 하기 위해 Visual Studio에서 제공 하는 두 가지 특히 유용한 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="299fc-119">*IntelliSense*.</span><span class="sxs-lookup"><span data-stu-id="299fc-119">*IntelliSense*.</span></span> <span data-ttu-id="299fc-120">Visual Studio에 기본 제공 되는 IntelliSense 기능은 WebMatrix에서 IntelliSense 보다 더 포괄적입니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="299fc-121">*디버거*.</span><span class="sxs-lookup"><span data-stu-id="299fc-121">*Debugger*.</span></span> <span data-ttu-id="299fc-122">디버거를 사용 하면 실행 중인 프로그램을 중지 하 고, 변수를 검사 하 고, 코드를 한 줄씩 단계별로 실행 하 여 코드 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="299fc-123">서로 다른 버전의 ASP.NET 웹 페이지에서 Visual Studio 사용</span><span class="sxs-lookup"><span data-stu-id="299fc-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="299fc-124">Visual Studio 2017에서 ASP.NET 웹 앱을 개발 하려면 **ASP.NET 및 웹 개발** 워크 로드를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="299fc-125">Visual Studio 2012 및 Visual Studio 2013에는 ASP.NET 웹 페이지에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="299fc-126">ASP.NET 웹 페이지를 지원 하기 위해 필요한 패키지는 Visual Studio를 설치할 때 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="299fc-127">Visual Studio 2010는 기본적으로 ASP.NET 웹 페이지에 대 한 지원을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="299fc-128">Visual Studio 2010에서 ASP.NET 웹 페이지를 사용 하려면 ASP.NET MVC 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="299fc-129">ASP.NET 웹 페이지 2를 다운로드 하려면 ASP.NET MVC 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="299fc-130">다음 표에는 여러 버전의 Visual Studio에서 ASP.NET 웹 페이지에 대 한 지원이 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="299fc-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="299fc-131">Visual Studio 2010</span></span> | <span data-ttu-id="299fc-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="299fc-132">Visual Studio 2012</span></span> | <span data-ttu-id="299fc-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="299fc-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="299fc-134">**ASP.NET 웹 페이지 2**</span><span class="sxs-lookup"><span data-stu-id="299fc-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="299fc-135">ASP.NET MVC 4 설치</span><span class="sxs-lookup"><span data-stu-id="299fc-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="299fc-136">들어</span><span class="sxs-lookup"><span data-stu-id="299fc-136">(Included)</span></span> | <span data-ttu-id="299fc-137">들어</span><span class="sxs-lookup"><span data-stu-id="299fc-137">(Included)</span></span> |
| <span data-ttu-id="299fc-138">**ASP.NET 웹 페이지 3**</span><span class="sxs-lookup"><span data-stu-id="299fc-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="299fc-139">NuGet을 통해 ASP.NET 웹 페이지 3으로 업데이트</span><span class="sxs-lookup"><span data-stu-id="299fc-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="299fc-140">들어</span><span class="sxs-lookup"><span data-stu-id="299fc-140">(Included)</span></span> |

<span data-ttu-id="299fc-141">Visual Studio 2010을 사용 하려면 [Visual studio 2010에서 ASP.NET 웹 페이지에 대 한 지원 설치](#vs2010support)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="299fc-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="299fc-142">WebMatrix에서 Visual Studio 시작</span><span class="sxs-lookup"><span data-stu-id="299fc-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="299fc-143">WebMatrix에서 프로젝트를 시작 하 고 Visual Studio로 전환 하려는 경우 WebMatrix는 Visual Studio에서 프로젝트를 쉽게 열 수 있는 단추를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="299fc-144">이 단추를 사용 하려면 컴퓨터에 Visual Studio가 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="299fc-145">다음 이미지는 WebMatrix의 단추를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-145">The following image shows the button in WebMatrix.</span></span>

![Visual Studio 시작](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="299fc-147">단추를 클릭 하면 Visual Studio에서 프로젝트가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="299fc-148">문제 없이 WebMatrix와 Visual Studio 간을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="299fc-149">다른 환경에서 파일이 변경 된 경우 알림이 표시 되며, 최신 변경 내용을 가져오려면 다시 로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="299fc-150">Visual Studio에서 ASP.NET Razor 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="299fc-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="299fc-151">Visual Studio에서 ASP.NET Razor 웹 사이트를 만들려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="299fc-152">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="299fc-153">**파일** 메뉴에서 **새 웹 사이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-153">In the **File** menu, click **New Web Site**.</span></span>

    ![새 웹 사이트 만들기](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="299fc-155">**새 웹 사이트** 대화 상자에서 사용할 언어 (시각적 개체 C# 또는 Visual Basic)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="299fc-156">**ASP.NET 웹 사이트 (Razor)** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![razor 사이트](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="299fc-158">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-158">Click **OK**.</span></span>

<span data-ttu-id="299fc-159">새 프로젝트가 존재 하 고 시작 하는 데 도움이 되는 몇 가지 기본 웹 페이지로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="299fc-160">IntelliSense 사용</span><span class="sxs-lookup"><span data-stu-id="299fc-160">Using IntelliSense</span></span>

<span data-ttu-id="299fc-161">이제 사이트를 만들었으므로 Visual Studio에서 IntelliSense가 작동 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="299fc-162">방금 만든 웹 사이트에서 *기본. cshtml* 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="299fc-163">페이지의 `<h3>` 태그 뒤에 `@ServerInfo.` (점 포함)를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="299fc-164">IntelliSense는 드롭다운 목록에서 `ServerInfo` 도우미에 사용할 수 있는 메서드를 표시 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![메서드가](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="299fc-166">목록에서 `GetHtml` 메서드를 선택 하 고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="299fc-167">IntelliSense는 메서드를 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="299fc-168">의 C#모든 메서드와 마찬가지로 메서드 뒤에 `()` 문자를 추가 해야 합니다. `GetHtml` 메서드의 완성 된 코드는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="299fc-169">Ctrl + F5 키를 눌러 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="299fc-170">브라우저에 표시 되는 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-170">This is what the page looks like when displayed in a browser:</span></span>

    ![브라우저의 기본 페이지](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="299fc-172">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="299fc-173">디버거 사용</span><span class="sxs-lookup"><span data-stu-id="299fc-173">Using the Debugger</span></span>

1. <span data-ttu-id="299fc-174">*기본 cshtml* 페이지의 맨 위에서 `Page.Title`로 시작 하는 줄 뒤에 다음 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="299fc-175">코드 왼쪽 편집기의 회색 여백에서 *중단점*을 추가 하기 위해이 새 줄 옆에 있는 다음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="299fc-176">중단점은 해당 지점에서 프로그램의 실행을 중지 하 고 있는지 확인할 수 있도록 디버거에 알리는 마커입니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![중단점 설정](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="299fc-178">`ServerInfo.GetHtml` 메서드에 대 한 호출을 제거 하 고 그 자리에 `@myTime` 변수에 대 한 호출을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="299fc-179">이 호출은 새 코드 줄에서 반환 된 현재 시간 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="299fc-180">F5 키를 눌러 디버거에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="299fc-181">설정 하는 중단점에서 페이지가 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="299fc-182">다음 이미지는 편집기에서 중단점 (노란색)이 있는 페이지의 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![디버그 중단점](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="299fc-184">디버그 도구 모음에서 한 **단계씩** 코드 실행 단추를 클릭 하거나 F11 키를 눌러 다음 코드 줄을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="299fc-185">이 단추를 클릭할 때마다 실행을 다음 코드 줄로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![한 단계씩 코드 실행 단추](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="299fc-187">마우스 포인터를 잡고 **지역** 및 **호출 스택** 창에 표시 된 값을 검사 하 여 `myTime` 변수의 값을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="299fc-188">Visual Studio에서 변수의 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-188">Visual Studio display the value of the variable.</span></span>

    ![시간 값 표시](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="299fc-190">변수 검사를 완료 하 고 코드를 단계별로 실행 하는 경우 F5 키를 눌러 각 줄에서 중지 하지 않고 페이지를 계속 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="299fc-191">모든 코드의 단계별 실행을 완료 하면 브라우저에 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="299fc-192">디버거에 대 한 자세한 내용 및 Visual Studio에서 코드를 디버깅 하는 방법에 대 한 자세한 내용은 [연습: Visual Web Developer에서 웹 페이지 디버깅](https://msdn.microsoft.com/library/z9e7w6cs.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="299fc-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="299fc-193">Visual Studio에서 ASP.NET MVC 프로젝트에서 Razor 사용</span><span class="sxs-lookup"><span data-stu-id="299fc-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="299fc-194">이 Razor 구문는 ASP.NET MVC 프로젝트 에서도 광범위 하 게 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="299fc-195">MVC는 동적 웹 사이트를 빌드하는 강력한 패턴 기반 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="299fc-196">ASP.NET 웹 페이지 사이트를 유지 관리 하기 어려운 경우 ASP.NET MVC 응용 프로그램으로 변환 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="299fc-197">MVC 응용 프로그램을 만드는 방법에 대 한 예제는 [ASP.NET MVC 5 시작](../../../mvc/overview/getting-started/introduction/getting-started.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="299fc-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="299fc-198">Visual Studio 2010의 ASP.NET 웹 페이지에 대 한 지원 설치</span><span class="sxs-lookup"><span data-stu-id="299fc-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="299fc-199">이 섹션에서는 visual Web Developer Express 2010 및 Visual Studio 용 ASP.NET 웹 페이지 도구를 설치 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="299fc-200">웹 플랫폼 설치 관리자가 아직 없는 경우 다음 URL에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="299fc-201">웹 플랫폼 설치 관리자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="299fc-202">**제품** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-202">Click the **Products** tab.</span></span>

    ![WebPI 제품 탭](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="299fc-204">**ASP.NET MVC 4** (ASP.NET 웹 페이지 2)를 검색 한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="299fc-205">이러한 제품에는 ASP.NET Razor 웹 사이트를 빌드하기 위한 Visual Studio 도구가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 설치 옵션](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="299fc-207">설치 **를 클릭 하** 여 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="299fc-207">Click **Install** to complete the installation.</span></span>
