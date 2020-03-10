---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: Visual Studio 2013의 코드 편집 ASP.NET Web Forms Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 3473ad476fbbebc58e12586334b4600f57cf17ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513641"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a><span data-ttu-id="afea5-102">Visual Studio 2013의 코드 편집 ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="afea5-102">Code Editing ASP.NET Web Forms in Visual Studio 2013</span></span>

<span data-ttu-id="afea5-103">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="afea5-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="afea5-104">많은 ASP.NET Web Form 페이지에서 Visual Basic, C#또는 다른 언어로 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-104">In many ASP.NET Web Form pages, you write code in Visual Basic, C#, or another language.</span></span> <span data-ttu-id="afea5-105">Visual Studio의 코드 편집기는 오류를 방지 하는 동시에 코드를 신속 하 게 작성 하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-105">The code editor in Visual Studio can help you write code quickly while helping you avoid errors.</span></span> <span data-ttu-id="afea5-106">또한 편집기에서는 재사용 가능한 코드를 만들어 수행 해야 하는 작업의 양을 줄이는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-106">In addition, the editor provides ways for you to create reusable code to help reduce the amount of work you need to do.</span></span>

<span data-ttu-id="afea5-107">이 연습에서는 Visual Studio 코드 편집기의 다양 한 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-107">This walkthrough illustrates various features of the Visual Studio code editor.</span></span>

<span data-ttu-id="afea5-108">이 연습에서는 다음 작업을 수행하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-108">During this walkthrough, you will learn how to:</span></span>

- <span data-ttu-id="afea5-109">인라인 코딩 오류를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-109">Correct inline coding errors.</span></span>
- <span data-ttu-id="afea5-110">코드 리팩터링 및 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="afea5-110">Refactor and rename code.</span></span>
- <span data-ttu-id="afea5-111">변수 및 개체의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-111">Rename variables and objects.</span></span>
- <span data-ttu-id="afea5-112">코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-112">Insert code snippets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afea5-113">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="afea5-113">Prerequisites</span></span>

<span data-ttu-id="afea5-114">이 연습을 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="afea5-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="afea5-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="afea5-116">.NET Framework 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="afea5-117">Microsoft Visual Studio 2013 및 Microsoft Visual Studio Express 2013은이 자습서 시리즈 전체에서 Visual Studio 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="afea5-118">Visual Studio를 사용 하는 경우이 연습에서는 Visual Studio를 처음 시작할 때 **웹 개발** 설정 컬렉션을 선택 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="afea5-119">자세한 내용은 [방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="afea5-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="afea5-120">웹 응용 프로그램 프로젝트 및 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="afea5-120">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="afea5-121">이 연습 부분에서는 웹 응용 프로그램 프로젝트를 만들고 여기에 새 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-121">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="afea5-122">웹 응용 프로그램 프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="afea5-122">To create a Web application project</span></span>

1. <span data-ttu-id="afea5-123">Microsoft Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-123">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="afea5-124">**파일** 메뉴에서 **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-124">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="afea5-125">![파일 메뉴](code-editing-in-web-forms-pages/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="afea5-125">![File Menu](code-editing-in-web-forms-pages/_static/image1.png)</span></span>

    <span data-ttu-id="afea5-126">**새 프로젝트** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-126">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="afea5-127">왼쪽에 있는  **C# Visual** -&gt; **웹** 템플릿 그룹 &gt; -**템플릿을** 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-127">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="afea5-128">가운데 열에서 **ASP.NET 웹 애플리케이션** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-128">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="afea5-129">프로젝트 이름을 ***BasicWebApp*** 로 하 고 **확인** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-129">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="afea5-130">![새 프로젝트 대화 상자](code-editing-in-web-forms-pages/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="afea5-130">![New Project dialog box](code-editing-in-web-forms-pages/_static/image2.png)</span></span>
6. <span data-ttu-id="afea5-131">그런 다음 **Web Forms** 템플릿을 선택 하 고 **확인** 단추를 클릭 하 여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-131">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="afea5-132">![새 ASP.NET 프로젝트 대화 상자](code-editing-in-web-forms-pages/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="afea5-132">![New ASP.NET Project dialog box](code-editing-in-web-forms-pages/_static/image3.png)</span></span>  

    <span data-ttu-id="afea5-133">Visual Studio는 Web Forms 템플릿을 기반으로 하는 미리 작성 된 기능을 포함 하는 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-133">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span>

## <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="afea5-134">새 ASP.NET Web Forms 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="afea5-134">Creating a new ASP.NET Web Forms Page</span></span>

<span data-ttu-id="afea5-135">**ASP.NET 웹 응용 프로그램** 프로젝트 템플릿을 사용 하 여 새 Web Forms 응용 프로그램을 만드는 경우 Visual Studio는 *default.aspx*라는 ASP.NET 페이지 (Web Forms 페이지) 뿐만 아니라 다른 여러 파일 및 폴더도 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-135">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="afea5-136">*Default.aspx 페이지를* 웹 응용 프로그램의 홈 페이지로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-136">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="afea5-137">그러나이 연습에서는 새 페이지를 만들고 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-137">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="afea5-138">웹 응용 프로그램에 페이지를 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="afea5-138">To add a page to the Web application</span></span>

1. <span data-ttu-id="afea5-139">**솔루션 탐색기**에서 웹 응용 프로그램 이름을 마우스 오른쪽 단추로 클릭 하 고 (이 자습서에서는 응용 프로그램 이름이 **basicwebsite 사이트인**경우) **추가** -&gt; **새 항목**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-139">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="afea5-140">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-140">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="afea5-141">왼쪽의 **Visual C#**  -&gt; **웹** 템플릿 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-141">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="afea5-142">그런 다음 중간 목록에서 **Web Form** 을 선택 하 고 이름을 *firstwebpage .aspx*로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-142">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="afea5-143">![새 항목 추가 대화 상자](code-editing-in-web-forms-pages/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="afea5-143">![Add New Item dialog box](code-editing-in-web-forms-pages/_static/image4.png)</span></span>
3. <span data-ttu-id="afea5-144">**추가** 를 클릭 하 여 Web Forms 페이지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-144">Click **Add** to add the Web Forms page to your project.</span></span>  
 <span data-ttu-id="afea5-145">Visual Studio에서 새 페이지를 만들어 엽니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-145">Visual Studio creates the new page and opens it.</span></span>
4. <span data-ttu-id="afea5-146">그런 다음이 새 페이지를 기본 시작 페이지로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-146">Next, set this new page as the default startup page.</span></span> <span data-ttu-id="afea5-147">**솔루션 탐색기**에서 *firstwebpage 페이지 .aspx* 이라는 새 페이지를 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-147">In **Solution Explorer**, right-click the new page named *FirstWebPage.aspx* and select **Set As Start Page**.</span></span> <span data-ttu-id="afea5-148">다음에이 응용 프로그램을 실행 하 여 진행 상황을 테스트할 때 브라우저에이 새 페이지가 자동으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-148">The next time you run this application to test our progress, you will automatically see this new page in the browser.</span></span>

## <a name="correcting-inline-coding-errors"></a><span data-ttu-id="afea5-149">인라인 코딩 오류 수정</span><span class="sxs-lookup"><span data-stu-id="afea5-149">Correcting Inline Coding Errors</span></span>

<span data-ttu-id="afea5-150">Visual Studio의 코드 편집기를 사용 하면 코드를 작성할 때 오류를 방지할 수 있으며 오류가 발생 한 경우 코드 편집기에서 오류를 수정 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-150">The code editor in Visual Studio helps you to avoid errors as you write code, and if you have made an error, the code editor helps you to correct the error.</span></span> <span data-ttu-id="afea5-151">이 연습 부분에서는 편집기에서 오류 수정 기능을 설명 하는 코드 줄을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-151">In this part of the walkthrough, you will write a line of code that illustrate the error correction features in the editor.</span></span>

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a><span data-ttu-id="afea5-152">Visual Studio에서 간단한 코딩 오류를 해결 하려면</span><span class="sxs-lookup"><span data-stu-id="afea5-152">To correct simple coding errors in Visual Studio</span></span>

1. <span data-ttu-id="afea5-153">**디자인** 뷰에서 빈 페이지를 두 번 클릭 하 여 페이지에 대 한 **로드** 이벤트에 대 한 처리기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-153">In **Design** view, double-click the blank page to create a handler for the **Load** event for the page.</span></span>   
   <span data-ttu-id="afea5-154">일부 코드를 작성 하는 위치로만 이벤트 처리기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-154">You are using the event handler only as a place to write some code.</span></span>
2. <span data-ttu-id="afea5-155">처리기 내에 오류가 포함 된 다음 줄을 입력 하 **고 enter 키를 누릅니다.**</span><span class="sxs-lookup"><span data-stu-id="afea5-155">Inside the handler, type the following line that contains an error and press **ENTER**:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   <span data-ttu-id="afea5-156">**Enter**키를 누르면 코드 편집기는 문제가 있는 코드 영역에서 녹색 및 빨강 밑줄 (일반적으로 &quot;물결 무늬&quot; 줄)을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-156">When you press **ENTER**, the code editor places green and red underlines (commonly call &quot;squiggly&quot; lines) under areas of the code that have issues.</span></span> <span data-ttu-id="afea5-157">녹색 밑줄은 경고를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-157">A green underline indicates a warning.</span></span> <span data-ttu-id="afea5-158">빨간색 밑줄은 수정 해야 하는 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-158">A red underline indicates an error that you must fix.</span></span> 

    <span data-ttu-id="afea5-159">`myStr` 위에 마우스 포인터를 놓으면 경고에 대해 알려 주는 도구 설명을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-159">Hold the mouse pointer over `myStr` to see a tooltip that tells you about the warning.</span></span> <span data-ttu-id="afea5-160">또한 빨간색 밑줄 위에 마우스 포인터를 놓으면 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-160">Also, hold your mouse pointer over the red underline to see the error message.</span></span>

    <span data-ttu-id="afea5-161">다음 그림에서는 밑줄이 있는 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-161">The following image shows the code with the underlines.</span></span>

    <span data-ttu-id="afea5-162">![디자인 뷰의 환영 텍스트](code-editing-in-web-forms-pages/_static/image5.png "디자인 뷰의 환영 텍스트")</span><span class="sxs-lookup"><span data-stu-id="afea5-162">![Welcome text in Design view](code-editing-in-web-forms-pages/_static/image5.png "Welcome text in Design view")</span></span>  
   <span data-ttu-id="afea5-163">줄의 끝에 세미콜론 `;`을 추가 하 여 오류를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-163">The error must be fixed by adding a semicolon `;` to the end of the line.</span></span> <span data-ttu-id="afea5-164">이 경고는 `myStr` 변수를 아직 사용 하지 않았음을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-164">The warning simply notifies you that you haven't used the `myStr` variable yet.</span></span>  

    > [!NOTE] 
    > 
    > <span data-ttu-id="afea5-165">Visual Studio에서 **도구** -&gt; **옵션** -&gt; **글꼴 및 색**을 선택 하 여 현재 코드 서식 설정을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-165">You view your current code formatting settings in Visual Studio by selecting **Tools** -&gt; **Options** -&gt; **Fonts and Colors**.</span></span>

## <a name="refactoring-and-renaming"></a><span data-ttu-id="afea5-166">리팩터링 및 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="afea5-166">Refactoring and Renaming</span></span>

<span data-ttu-id="afea5-167">리팩터링은 기능을 유지 하면서 이해 하 고 유지 관리 하기 쉽도록 코드를 재구성 하는 소프트웨어 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-167">Refactoring is a software methodology that involves restructuring your code to make it easier to understand and to maintain, while preserving its functionality.</span></span> <span data-ttu-id="afea5-168">간단한 예제는 이벤트 처리기에서 코드를 작성 하 여 데이터베이스에서 데이터를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-168">A simple example might be that you write code in an event handler to get data from a database.</span></span> <span data-ttu-id="afea5-169">페이지를 개발할 때 다양 한 처리기에서 데이터에 액세스 해야 하는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-169">As you develop your page, you discover that you need to access the data from several different handlers.</span></span> <span data-ttu-id="afea5-170">따라서 페이지에서 데이터 액세스 메서드를 만들고 처리기의 메서드에 호출을 삽입 하 여 페이지의 코드를 리팩터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-170">Therefore, you refactor the page's code by creating a data-access method in the page and inserting calls to the method in the handlers.</span></span>

<span data-ttu-id="afea5-171">코드 편집기에는 다양 한 리팩터링 작업을 수행 하는 데 도움이 되는 도구가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-171">The code editor includes tools to help you perform various refactoring tasks.</span></span> <span data-ttu-id="afea5-172">이 연습에서는 변수의 이름을 바꾸고 메서드를 추출 하는 두 가지 리팩터링 기법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-172">In this walkthrough, you will work with two refactoring techniques: renaming variables and extracting methods.</span></span> <span data-ttu-id="afea5-173">기타 리팩터링 옵션으로는 필드 캡슐화, 지역 변수를 메서드 매개 변수로 승격, 메서드 매개 변수 관리 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-173">Other refactoring options include encapsulating fields, promoting local variables to method parameters, and managing method parameters.</span></span> <span data-ttu-id="afea5-174">이러한 리팩터링 옵션의 사용 가능 여부는 코드의 위치에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-174">The availability of these refactoring options depends on the location in the code.</span></span>

### <a name="refactoring-code"></a><span data-ttu-id="afea5-175">리팩터링 코드</span><span class="sxs-lookup"><span data-stu-id="afea5-175">Refactoring Code</span></span>

<span data-ttu-id="afea5-176">일반적인 리팩터링 시나리오는 메서드와 같이 다른 멤버 내에 있는 코드에서 메서드를 생성 (추출) 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-176">A common refactoring scenario is to create (extract) a method from code that is inside another member, such as a method.</span></span> <span data-ttu-id="afea5-177">이렇게 하면 원래 멤버의 크기가 줄어들고 추출 된 코드를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-177">This reduces the size of the original member and makes the extracted code reusable.</span></span>

<span data-ttu-id="afea5-178">이 연습 부분에서는 몇 가지 간단한 코드를 작성 한 다음 해당 코드에서 메서드를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-178">In this part of the walkthrough, you will write some simple code, and then extract a method from it.</span></span> <span data-ttu-id="afea5-179">리팩터링은에 대해 C#지원 되므로 프로그래밍 언어로를 사용 C# 하는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-179">Refactoring is supported for C#, so you will create a page that uses C# as its programming language.</span></span>

### <a name="to-extract-a-method-in-a-c-page"></a><span data-ttu-id="afea5-180">C# 페이지에서 메서드를 추출 하려면</span><span class="sxs-lookup"><span data-stu-id="afea5-180">To extract a method in a C# page</span></span>

1. <span data-ttu-id="afea5-181">**디자인** 뷰로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-181">Switch to **Design** view.</span></span>
2. <span data-ttu-id="afea5-182">**도구 상자**의 **표준** 탭에서 [단추](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) 컨트롤을 페이지로 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-182">In the **Toolbox**, from the **Standard** tab, drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page.</span></span>
3. <span data-ttu-id="afea5-183">**단추** 컨트롤을 두 번 클릭 하 여 [클릭](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) 이벤트에 대 한 처리기를 만든 후 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-183">Double-click the **Button** control to create a handler for its [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event, and then add the following highlighted code:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   <span data-ttu-id="afea5-184">이 코드는 **arraylist** 개체를 만들고 루프를 사용 하 여 값을 로드 한 다음 다른 루프를 사용 하 여 **arraylist** 개체의 내용을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-184">The code creates an **ArrayList** object, uses a loop to load it with values, and then uses another loop to display the contents of the **ArrayList** object.</span></span>
4. <span data-ttu-id="afea5-185">**Ctrl + F5** 키를 눌러 페이지를 실행 한 후 **단추** 를 클릭 하 여 다음 출력이 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-185">Press **CTRL+F5** to run the page, and then click the **button** to make sure that you see the following output:</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. <span data-ttu-id="afea5-186">코드 편집기로 돌아간 다음 이벤트 처리기에서 다음 줄을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-186">Return to the code editor, and then select the following lines in the event handler.</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. <span data-ttu-id="afea5-187">선택 항목을 마우스 오른쪽 단추로 클릭 하 고 **리팩터링**을 클릭 한 다음 **메서드 추출**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-187">Right-click the selection, click **Refactor**, and then choose **Extract Method**.</span></span> 

    <span data-ttu-id="afea5-188">**메서드 추출** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-188">The **Extract Method** dialog box appears.</span></span>
7. <span data-ttu-id="afea5-189">**새 메서드 이름** 상자에 **displayarray**를 입력 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-189">In the **New Method Name** box, type **DisplayArray**, and then click **OK**.</span></span> 

    <span data-ttu-id="afea5-190">코드 편집기는 `DisplayArray`이라는 새 메서드를 만들고 루프의 원래 위치에 있는 **클릭** 처리기에 새 메서드에 대 한 호출을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-190">The code editor creates a new method named `DisplayArray`, and puts a call to the new method in the **Click** handler where the loop was originally.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. <span data-ttu-id="afea5-191">**Ctrl + F5** 키를 눌러 페이지를 다시 실행 하 고 **단추**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-191">Press **CTRL+F5** to run the page again, and click the **button**.</span></span>

    <span data-ttu-id="afea5-192">페이지는 이전과 동일 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-192">The page functions the same as it did before.</span></span> <span data-ttu-id="afea5-193">이제 page 클래스의 어디에서 든 `DisplayArray` 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-193">The `DisplayArray` method can now be call from anywhere in the page class.</span></span>

## <a name="renaming-variables"></a><span data-ttu-id="afea5-194">변수 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="afea5-194">Renaming Variables</span></span>

<span data-ttu-id="afea5-195">변수 및 개체를 사용 하는 경우 코드에서 이미 참조 된 개체의 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-195">When you work with variables, as well as objects, you might want to rename them after they are already referenced in your code.</span></span> <span data-ttu-id="afea5-196">그러나 참조 중 하나의 이름을 바꾸지 않으면 변수와 개체의 이름을 바꾸면 코드가 중단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-196">However, renaming variables and objects can cause the code to break if you miss renaming one of the references.</span></span> <span data-ttu-id="afea5-197">따라서 리팩터링을 사용 하 여 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-197">Therefore, you can use refactoring to perform the renaming.</span></span>

### <a name="to-use-refactoring-to-rename-a-variable"></a><span data-ttu-id="afea5-198">리팩터링을 사용 하 여 변수 이름을 바꾸려면</span><span class="sxs-lookup"><span data-stu-id="afea5-198">To use refactoring to rename a variable</span></span>

1. <span data-ttu-id="afea5-199">**Click** 이벤트 처리기에서 다음 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-199">In the **Click** event handler, locate the following line:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. <span data-ttu-id="afea5-200">`alist`변수 이름을 마우스 오른쪽 단추로 클릭 하 고 **리팩터링**을 선택한 다음 **이름 바꾸기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-200">Right-click the variable name `alist`, choose **Refactor**, and then choose **Rename**.</span></span>

    <span data-ttu-id="afea5-201">**이름 바꾸기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-201">The **Rename** dialog box appears.</span></span>
3. <span data-ttu-id="afea5-202">**새 이름** 상자에 **ArrayList1** 을 입력 하 고 **참조 변경 내용 미리 보기** 확인란을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-202">In the **New name** box, type **ArrayList1** and make sure the **Preview reference changes** checkbox has been selected.</span></span> <span data-ttu-id="afea5-203">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-203">Then click **OK**.</span></span>

    <span data-ttu-id="afea5-204">**변경 내용 미리 보기** 대화 상자가 나타나고 이름을 바꿀 변수에 대 한 모든 참조를 포함 하는 트리가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-204">The **Preview Changes** dialog box appears, and displays a tree that contains all references to the variable that you are renaming.</span></span>
4. <span data-ttu-id="afea5-205">**적용** 을 클릭 하 여 **변경 내용 미리 보기** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-205">Click **Apply** to close the **Preview Changes** dialog box.</span></span>

    <span data-ttu-id="afea5-206">사용자가 선택한 인스턴스에 대해 구체적으로 참조 하는 변수는 이름이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-206">The variables that refer specifically to the instance that you selected are renamed.</span></span> <span data-ttu-id="afea5-207">그러나 다음 줄에 `alist` 변수는 이름이 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-207">Note, however, that the variable `alist` in the following line is not renamed.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    <span data-ttu-id="afea5-208">이 줄의 `alist` 변수는 이름을 바꾼 `alist` 변수의 값과 동일한 값을 나타내지 않으므로 이름이 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-208">The variable `alist` in this line is not renamed because it does not represent the same value as the variable `alist` that you renamed.</span></span> <span data-ttu-id="afea5-209">`DisplayArray` 선언에서 `alist` 변수는 해당 메서드에 대 한 지역 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-209">The variable `alist` in the `DisplayArray` declaration is a local variable for that method.</span></span> <span data-ttu-id="afea5-210">이는 리팩터링을 사용 하 여 변수 이름을 바꾸는 것은 단순히 편집기에서 찾기 및 바꾸기 작업을 수행 하는 것과는 다른 것을 보여 줍니다. 리팩터링은 작업 중인 변수의 의미 체계에 대 한 정보로 변수 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-210">This illustrates that using refactoring to rename variables is different than simply performing a find-and-replace action in the editor; refactoring renames variables with knowledge of the semantics of the variable that it is working with.</span></span>

## <a name="inserting-snippets"></a><span data-ttu-id="afea5-211">조각 삽입</span><span class="sxs-lookup"><span data-stu-id="afea5-211">Inserting Snippets</span></span>

<span data-ttu-id="afea5-212">Web Forms 개발자가 자주 수행 해야 하는 많은 코딩 태스크가 있기 때문에 코드 편집기는 코드 조각 라이브러리 또는 미리 작성 된 코드 블록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-212">Because there are many coding tasks that Web Forms developers frequently need to perform, the code editor provides a library of snippets, or blocks of prewritten code.</span></span> <span data-ttu-id="afea5-213">이러한 코드 조각을 페이지에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-213">You can insert these snippets into your page.</span></span>

<span data-ttu-id="afea5-214">Visual Studio에서 사용 하는 각 언어는 코드 조각을 삽입 하는 방법에 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-214">Each language that you use in Visual Studio has slight differences in the way you insert code snippets.</span></span> <span data-ttu-id="afea5-215">코드 조각을 삽입 하는 방법에 대 한 자세한 내용은 [Visual Basic IntelliSense 코드 조각](https://msdn.microsoft.com/library/18yz4be4.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="afea5-215">For information about inserting snippets, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx).</span></span> <span data-ttu-id="afea5-216">시각적 개체 C#에 코드 조각을 삽입 하는 방법에 대 한 자세한 내용은 [ C# 시각적 코드 조각](https://msdn.microsoft.com/library/z41h7fat.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="afea5-216">For information about inserting snippets in Visual C#, see [Visual C# Code Snippets](https://msdn.microsoft.com/library/z41h7fat.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="afea5-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="afea5-217">Next Steps</span></span>

<span data-ttu-id="afea5-218">이 연습에서는 코드에서 오류를 수정 하 고, 코드를 리팩터링 하 고, 변수 이름을 바꾸고, 코드 조각을 코드에 삽입 하기 위한 Visual Studio 2010 코드 편집기의 기본 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-218">This walkthrough has illustrated the basic features of the Visual Studio 2010 code editor for correcting errors in your code, refactoring code, renaming variables, and inserting code snippets into your code.</span></span> <span data-ttu-id="afea5-219">편집기의 추가 기능을 통해 응용 프로그램을 빠르고 쉽게 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-219">Additional features in the editor can make application development fast and easy.</span></span> <span data-ttu-id="afea5-220">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-220">For example, you might want to:</span></span>

- <span data-ttu-id="afea5-221">Intellisense의 기능 (예: IntelliSense 옵션 수정, 코드 조각 관리 및 온라인으로 코드 조각 검색)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="afea5-221">Learn more about the features of IntelliSense, such as modifying IntelliSense options, managing code snippets, and searching for code snippets online.</span></span> <span data-ttu-id="afea5-222">자세한 내용은 [IntelliSense 사용](https://msdn.microsoft.com/library/hcw1s69b.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afea5-222">For more information, see [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span></span>
- <span data-ttu-id="afea5-223">사용자 고유의 코드 조각을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="afea5-223">Learn how to create your own code snippets.</span></span> <span data-ttu-id="afea5-224">자세한 내용은 [IntelliSense 코드 조각 만들기 및 사용](https://msdn.microsoft.com/library/ms165392.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="afea5-224">For more information, see [Creating and Using IntelliSense Code Snippets](https://msdn.microsoft.com/library/ms165392.aspx)</span></span>
- <span data-ttu-id="afea5-225">코드 조각의 Visual Basic 특정 기능 (예: 코드 조각 사용자 지정 및 문제 해결)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="afea5-225">Learn more about the Visual Basic-specific features of IntelliSense code snippets, such as customizing the snippets and troubleshooting.</span></span> <span data-ttu-id="afea5-226">자세한 내용은 [Visual Basic IntelliSense 코드 조각](https://msdn.microsoft.com/library/18yz4be4.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="afea5-226">For more information, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx)</span></span>
- <span data-ttu-id="afea5-227">리팩터링, 코드 조각 C#등 IntelliSense의 특정 기능에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="afea5-227">Learn more about the C#-specific features of IntelliSense, such as refactoring and code snippets.</span></span> <span data-ttu-id="afea5-228">자세한 내용은 [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="afea5-228">For more information, see [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span></span>
