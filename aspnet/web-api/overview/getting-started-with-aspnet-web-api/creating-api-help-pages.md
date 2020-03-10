---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: ASP.NET Web API에 대 한 도움말 페이지 만들기-ASP.NET 4.x
author: MikeWasson
description: 이 자습서에서는 ASP.NET 4.x의 ASP.NET Web API에 대 한 도움말 페이지를 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448619"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="7cc71-103">ASP.NET Web API에 대 한 도움말 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="7cc71-103">Creating Help Pages for ASP.NET Web API</span></span>

<span data-ttu-id="7cc71-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7cc71-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7cc71-105">이 자습서에서는 ASP.NET 4.x의 ASP.NET Web API에 대 한 도움말 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-105">This tutorial with code shows how to create help pages for ASP.NET Web API in ASP.NET 4.x.</span></span>

<span data-ttu-id="7cc71-106">Web API를 만들 때 다른 개발자가 API를 호출 하는 방법을 알 수 있도록 도움말 페이지를 만드는 것이 유용한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-106">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="7cc71-107">모든 설명서를 수동으로 만들 수 있지만 최대한 자동 생성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-107">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span> <span data-ttu-id="7cc71-108">이 작업을 더 쉽게 수행 하기 위해 ASP.NET Web API는 런타임에 도움말 페이지를 자동으로 생성 하기 위한 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-108">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="7cc71-109">API 도움말 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="7cc71-109">Creating API Help Pages</span></span>

<span data-ttu-id="7cc71-110">[ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-110">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="7cc71-111">이 업데이트는 웹 API 프로젝트 템플릿에 도움말 페이지를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-111">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="7cc71-112">다음으로, 새 ASP.NET MVC 4 프로젝트를 만들고 웹 API 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-112">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="7cc71-113">프로젝트 템플릿은 `ValuesController`이라는 예제 API 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-113">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="7cc71-114">템플릿은 또한 API 도움말 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-114">The template also creates the API help pages.</span></span> <span data-ttu-id="7cc71-115">도움말 페이지의 모든 코드 파일은 프로젝트의 영역 폴더에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-115">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="7cc71-116">응용 프로그램을 실행할 때 홈 페이지에는 API 도움말 페이지에 대 한 링크가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-116">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="7cc71-117">홈 페이지에서 상대 경로는/Help.</span><span class="sxs-lookup"><span data-stu-id="7cc71-117">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="7cc71-118">이 링크를 누르면 API 요약 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-118">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="7cc71-119">이 페이지에 대 한 MVC 뷰는 Areas/HelpPage/Views/Help/Index. cshtml에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-119">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="7cc71-120">이 페이지를 편집 하 여 레이아웃, 소개, 제목, 스타일 등을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-120">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="7cc71-121">페이지의 주요 부분은 컨트롤러 별로 그룹화 된 Api의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-121">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="7cc71-122">Table 항목은 **Iapiexplorer** 인터페이스를 사용 하 여 동적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-122">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="7cc71-123">이 인터페이스에 대해서는 나중에 자세히 설명 합니다. 새 API 컨트롤러를 추가 하는 경우 테이블은 런타임에 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-123">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="7cc71-124">"API" 열에는 HTTP 메서드 및 상대 URI가 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-124">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="7cc71-125">"설명" 열에는 각 API에 대 한 설명서가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-125">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="7cc71-126">처음에는 설명서가 자리 표시자 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-126">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="7cc71-127">다음 섹션에서는 XML 주석에서 설명서를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-127">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="7cc71-128">각 API에는 예제 요청 및 응답 본문을 포함 하 여 보다 자세한 정보를 포함 하는 페이지에 대 한 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-128">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="7cc71-129">기존 프로젝트에 도움말 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="7cc71-129">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="7cc71-130">NuGet 패키지 관리자를 사용 하 여 기존 Web API 프로젝트에 도움말 페이지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-130">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="7cc71-131">이 옵션은 "Web API" 템플릿과 다른 프로젝트 템플릿에서 시작 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-131">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="7cc71-132">**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-132">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="7cc71-133">[패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 창에서 다음 명령 중 하나를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-133">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="7cc71-134">**C#** 응용 프로그램의 경우: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="7cc71-134">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="7cc71-135">**Visual Basic** 응용 프로그램의 경우: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="7cc71-135">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="7cc71-136">에 C# 는 두 개의 패키지가 있습니다. 하나는 Visual Basic입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-136">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="7cc71-137">프로젝트와 일치 하는 항목을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-137">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="7cc71-138">이 명령은 필요한 어셈블리를 설치 하 고 영역/도움말 페이지 폴더에 있는 도움말 페이지에 대 한 MVC 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-138">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="7cc71-139">도움말 페이지에 대 한 링크를 수동으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-139">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="7cc71-140">URI는/Help.</span><span class="sxs-lookup"><span data-stu-id="7cc71-140">The URI is /Help.</span></span> <span data-ttu-id="7cc71-141">Razor 뷰에서 링크를 만들려면 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-141">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="7cc71-142">또한 영역을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-142">Also, make sure to register areas.</span></span> <span data-ttu-id="7cc71-143">Global.asax 파일에서 다음 코드를 **응용 프로그램\_Start** 메서드에 추가 합니다 (아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="7cc71-143">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="7cc71-144">API 설명서 추가</span><span class="sxs-lookup"><span data-stu-id="7cc71-144">Adding API Documentation</span></span>

<span data-ttu-id="7cc71-145">기본적으로 도움말 페이지에는 설명서에 대 한 자리 표시자 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-145">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="7cc71-146">[XML 문서 주석을](https://msdn.microsoft.com/library/b2s063f7.aspx) 사용 하 여 설명서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-146">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="7cc71-147">이 기능을 사용 하도록 설정 하려면 파일 영역/도움말 페이지/앱\_Start/HelpPageConfig을 열고 다음 줄의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-147">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="7cc71-148">이제 XML 설명서를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-148">Now enable XML documentation.</span></span> <span data-ttu-id="7cc71-149">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-149">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="7cc71-150">**빌드** 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-150">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="7cc71-151">**출력**에서 **XML 문서 파일**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-151">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="7cc71-152">편집 상자에 "App\_Data/XmlDocument .xml"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-152">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="7cc71-153">그런 다음/Controllers/ValuesController.cs.에 정의 된 `ValuesController` API 컨트롤러에 대 한 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-153">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesController.cs.</span></span> <span data-ttu-id="7cc71-154">컨트롤러 메서드에 몇 가지 설명서 주석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-154">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="7cc71-155">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-155">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="7cc71-156">팁: 메서드 위의 줄에 캐럿을 배치 하 고 세 개의 슬래시를 입력 하면 Visual Studio에서 XML 요소를 자동으로 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-156">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="7cc71-157">그런 다음 공백을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-157">Then you can fill in the blanks.</span></span>

<span data-ttu-id="7cc71-158">이제 응용 프로그램을 빌드 및 실행 하 고 도움말 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-158">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="7cc71-159">설명서 문자열은 API 테이블에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-159">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="7cc71-160">도움말 페이지는 런타임에 XML 파일에서 문자열을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-160">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="7cc71-161">응용 프로그램을 배포할 때 XML 파일을 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-161">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="7cc71-162">내부적으로</span><span class="sxs-lookup"><span data-stu-id="7cc71-162">Under the Hood</span></span>

<span data-ttu-id="7cc71-163">도움말 페이지는 웹 API 프레임 워크의 일부인 **Apiexplorer** 클래스 위에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-163">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="7cc71-164">**Apiexplorer** 클래스는 도움말 페이지를 만들기 위한 원시 자료를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-164">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="7cc71-165">각 API에 대해 **Apiexplorer** 는 api를 설명 하는 **apiexplorer** 을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-165">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="7cc71-166">이러한 목적을 위해 "API"는 HTTP 메서드와 상대 URI의 조합으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-166">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="7cc71-167">예를 들어, 다음은 몇 가지 고유한 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-167">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="7cc71-168">/Api/제품 가져오기</span><span class="sxs-lookup"><span data-stu-id="7cc71-168">GET /api/Products</span></span>
- <span data-ttu-id="7cc71-169">/Api/Products/{id} 가져오기</span><span class="sxs-lookup"><span data-stu-id="7cc71-169">GET /api/Products/{id}</span></span>
- <span data-ttu-id="7cc71-170">게시/a n o/제품</span><span class="sxs-lookup"><span data-stu-id="7cc71-170">POST /api/Products</span></span>

<span data-ttu-id="7cc71-171">컨트롤러 작업에서 여러 HTTP 메서드를 지 원하는 경우 **Apiexplorer** 는 각 메서드를 고유한 API로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-171">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="7cc71-172">**Apiexplorer**에서 API를 숨기려면 **ApiExplorerSettings** 특성을 작업에 추가 하 고 *ignoreapi* 를 true로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-172">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="7cc71-173">컨트롤러에이 특성을 추가 하 여 전체 컨트롤러를 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-173">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="7cc71-174">ApiExplorer 클래스는 **Idocumentationprovider** 인터페이스에서 설명서 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-174">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="7cc71-175">앞서 살펴본 것 처럼 도움말 페이지 라이브러리는 XML 문서 문자열에서 설명서를 가져오는 **Idocumentationprovider** 를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-175">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="7cc71-176">코드는/Areas/HelpPage/XmlDocumentationProvider.cs.에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-176">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="7cc71-177">고유한 **Idocumentationprovider**를 작성 하 여 다른 원본에서 설명서를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-177">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="7cc71-178">연결 하려면 **HelpPageConfigurationExtensions** 에 정의 된 **Setdocumentationprovider** 확장 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-178">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="7cc71-179">**Apiexplorer** 는 자동으로 **Idocumentationprovider** 인터페이스를 호출 하 여 각 API에 대 한 설명서 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-179">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="7cc71-180">**Apidescription** 및 **ApiParameterDescription** 개체의 **설명서** 속성에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-180">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cc71-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7cc71-181">Next Steps</span></span>

<span data-ttu-id="7cc71-182">여기에 표시 된 도움말 페이지로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-182">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="7cc71-183">실제로 **Apiexplorer** 는 도움말 페이지를 만드는 것으로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-183">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="7cc71-184">Yao Huang 링크는 다음과 같은 몇 가지 유용한 블로그 게시물을 작성 하 여이에 대해 알아 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cc71-184">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="7cc71-185">ASP.NET Web API 도움말 페이지에 간단한 테스트 클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="7cc71-185">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="7cc71-186">ASP.NET Web API 도움말 페이지에서 자체 호스팅 서비스에 대해 작업 수행</span><span class="sxs-lookup"><span data-stu-id="7cc71-186">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="7cc71-187">ASP.NET Web API에 대 한 도움말 페이지 (또는 클라이언트)의 디자인 타임 생성</span><span class="sxs-lookup"><span data-stu-id="7cc71-187">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="7cc71-188">고급 도움말 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="7cc71-188">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
