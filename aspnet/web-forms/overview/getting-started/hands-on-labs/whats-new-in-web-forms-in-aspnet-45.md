---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: ASP.NET 4.5에서 Web Forms의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: ASP.NET Web Forms의 새 버전에는 데이터 작업 시 사용자 환경을 개선 하는 데 초점을 맞춘 많은 향상 된 기능이 도입 되었습니다. 이전 버전의에서 ...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 301af8ed877b58624e419c04f605c41f27dbdd0c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421925"
---
# <a name="whats-new-in-web-forms-in-aspnet-45"></a><span data-ttu-id="e2142-104">ASP.NET 4.5의 새로운 Web Forms 기능</span><span class="sxs-lookup"><span data-stu-id="e2142-104">What's New in Web Forms in ASP.NET 4.5</span></span>

<span data-ttu-id="e2142-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="e2142-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="e2142-106">ASP.NET Web Forms의 새 버전에는 데이터 작업 시 사용자 환경을 개선 하는 데 초점을 맞춘 많은 향상 된 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-106">The new version of ASP.NET Web Forms introduces a number of improvements focused on improving user experience when working with data.</span></span>
> 
> <span data-ttu-id="e2142-107">이전 버전의 Web Forms에서 데이터 바인딩을 사용 하 여 개체 멤버의 값을 내보낼 때 데이터 바인딩 식 Bind () 또는 Eval ()을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-107">In previous versions of Web Forms, when using data-binding to emit the value of an object member, you used the data-binding expressions Bind() or Eval().</span></span> <span data-ttu-id="e2142-108">새 버전의 ASP.NET에서는 새 ItemType 속성을 사용 하 여 컨트롤이 바인딩될 데이터 형식을 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-108">In the new version of ASP.NET, you are able to declare what type of data a control is going to be bound to by using a new ItemType property.</span></span> <span data-ttu-id="e2142-109">이 속성을 설정 하면 강력한 형식의 변수를 사용 하 여 Visual Studio 개발 환경 (예: IntelliSense, 멤버 탐색, 컴파일 시간 검사)의 모든 이점을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-109">Setting this property will enable you to use a strongly-typed variable to receive the full benefits of the Visual Studio development experience, such as IntelliSense, member navigation, and compile-time checking.</span></span>
> 
> <span data-ttu-id="e2142-110">데이터 바인딩된 컨트롤을 사용 하 여 데이터를 선택, 업데이트, 삭제 및 삽입 하는 사용자 지정 메서드를 직접 지정 하 여 페이지 컨트롤과 응용 프로그램 논리 간의 상호 작용을 간소화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-110">With the data-bound controls, you can now also specify your own custom methods for selecting, updating, deleting and inserting data, simplifying the interaction between the page controls and your application logic.</span></span> <span data-ttu-id="e2142-111">또한 ASP.NET에 모델 바인딩 기능이 추가 되었습니다. 즉, 페이지의 데이터를 메서드 형식 매개 변수에 직접 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-111">Additionally, model binding capabilities have been added to ASP.NET, which means you can map data from the page directly into method type parameters.</span></span>
> 
> <span data-ttu-id="e2142-112">최신 버전의 Web Forms에서 사용자 입력의 유효성을 검사 하는 것도 더 쉬워졌습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-112">Validating user input should also be easier with the latest version of Web Forms.</span></span> <span data-ttu-id="e2142-113">이제 **system.componentmodel** 네임 스페이스의 유효성 검사 특성을 사용 하 여 모델 클래스에 주석을 달고 모든 사이트 컨트롤이 해당 정보를 사용 하 여 사용자 입력의 유효성을 검사 하도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-113">You can now annotate your model classes with validation attributes from the **System.ComponentModel.DataAnnotations** namespace and request that all your site controls validate user input using that information.</span></span> <span data-ttu-id="e2142-114">Web Forms의 클라이언트 쪽 유효성 검사는 이제 jQuery와 통합 되어 클리너 클라이언트 쪽 코드와 방해가 되지 않는 JavaScript 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-114">Client-side validation in Web Forms is now integrated with jQuery, providing cleaner client-side code and unobtrusive JavaScript features.</span></span>
> 
> <span data-ttu-id="e2142-115">요청 유효성 검사 영역에서 응용 프로그램의 특정 부분에 대 한 요청 유효성 검사를 더 쉽게 끄거나 무효화 된 요청 데이터를 읽을 수 있도록 기능이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-115">In the request validation area, improvements have been made to make it easier to selectively turn off request validation for specific parts of your applications or read invalidated request data.</span></span>
> 
> <span data-ttu-id="e2142-116">HTML5의 새 기능을 활용 하기 위해 Web Forms 서버 컨트롤에 대 한 몇 가지 기능이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-116">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>
> 
> - <span data-ttu-id="e2142-117">TextBox 컨트롤의 TextMode 속성은 email, datetime 등의 새 HTML5 입력 형식을 지원 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-117">The TextMode property of the TextBox control has been updated to support the new HTML5 input types like email, datetime, and so on.</span></span>
> - <span data-ttu-id="e2142-118">이제 FileUpload 컨트롤은이 HTML5 기능을 지 원하는 브라우저에서 여러 파일 업로드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-118">The FileUpload control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
> - <span data-ttu-id="e2142-119">유효성 검사기 컨트롤은 이제 HTML5 입력 요소의 유효성 검사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-119">Validator controls now support validating HTML5 input elements.</span></span>
> - <span data-ttu-id="e2142-120">URL을 나타내는 특성이 있는 새 HTML5 요소는 이제 runat =&quot;server&quot;를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-120">New HTML5 elements that have attributes that represent a URL now support runat=&quot;server&quot;.</span></span> <span data-ttu-id="e2142-121">결과적으로 ~ 연산자와 같이 URL 경로에 ASP.NET 규칙을 사용 하 여 응용 프로그램 루트를 나타낼 수 있습니다. 예를 들어 &lt;video runat =&quot;server&quot; src =&quot;~/Myvideo.er&quot;&gt;&lt;).&gt;</span><span class="sxs-lookup"><span data-stu-id="e2142-121">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat=&quot;server&quot; src=&quot;~/myVideo.wmv&quot;&gt;&lt;/video&gt;).</span></span>
> - <span data-ttu-id="e2142-122">HTML5 입력 필드 게시를 지원 하도록 UpdatePanel 컨트롤이 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-122">The UpdatePanel control has been fixed to support posting HTML5 input fields.</span></span>
> 
> <span data-ttu-id="e2142-123">공식 ASP.NET 포털에서 ASP.NET WebForms 4.5: [ASP.NET 4.5 및 Visual Studio 2012의 새로운](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385) 기능에 대 한 추가 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-123">In the official ASP.NET portal you can find more examples of the new features in ASP.NET WebForms 4.5: [What's New in ASP.NET 4.5 and Visual Studio 2012](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)</span></span>
> 
> <span data-ttu-id="e2142-124">모든 샘플 코드와 코드 조각은 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-124">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="e2142-125">목표</span><span class="sxs-lookup"><span data-stu-id="e2142-125">Objectives</span></span>

<span data-ttu-id="e2142-126">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-126">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="e2142-127">강력한 형식의 데이터 바인딩 식 사용</span><span class="sxs-lookup"><span data-stu-id="e2142-127">Use strongly-typed data-binding expressions</span></span>
- <span data-ttu-id="e2142-128">Web Forms에서 새 모델 바인딩 기능 사용</span><span class="sxs-lookup"><span data-stu-id="e2142-128">Use new model binding features in Web Forms</span></span>
- <span data-ttu-id="e2142-129">값 공급자를 사용 하 여 페이지 데이터를 코드 숨김이 메서드에 매핑</span><span class="sxs-lookup"><span data-stu-id="e2142-129">Use value providers for mapping page data to code-behind methods</span></span>
- <span data-ttu-id="e2142-130">사용자 입력 유효성 검사에 대 한 데이터 주석 사용</span><span class="sxs-lookup"><span data-stu-id="e2142-130">Use Data Annotations for user input validation</span></span>
- <span data-ttu-id="e2142-131">Web Forms에서 jQuery에 대 한 클라이언트 쪽 유효성 검사를 사용 하지 않는 기능 활용</span><span class="sxs-lookup"><span data-stu-id="e2142-131">Take advantage of unobtrusive client-side validation with jQuery in Web Forms</span></span>
- <span data-ttu-id="e2142-132">세부적인 요청 유효성 검사 구현</span><span class="sxs-lookup"><span data-stu-id="e2142-132">Implement granular request validation</span></span>
- <span data-ttu-id="e2142-133">Web Forms에서 비동기 페이지 처리 구현</span><span class="sxs-lookup"><span data-stu-id="e2142-133">Implement asynchronous page processing in Web Forms</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="e2142-134">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="e2142-134">Prerequisites</span></span>

<span data-ttu-id="e2142-135">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-135">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="e2142-136">[웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="e2142-136">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="e2142-137">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="e2142-137">Setup</span></span>

<span data-ttu-id="e2142-138">**코드 조각 설치**</span><span class="sxs-lookup"><span data-stu-id="e2142-138">**Installing Code Snippets**</span></span>

<span data-ttu-id="e2142-139">편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-139">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="e2142-140">코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-140">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="e2142-141">Visual Studio Code 코드 조각에 대해 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [C: 코드 조각&quot;사용](#AppendixC) &quot;부록을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-141">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="e2142-142">실습</span><span class="sxs-lookup"><span data-stu-id="e2142-142">Exercises</span></span>

<span data-ttu-id="e2142-143">이 실습 랩에는 다음 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-143">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="e2142-144">연습 1: ASP.NET Web Forms의 모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="e2142-144">Exercise 1: Model Binding in ASP.NET Web Forms</span></span>](#Exercise1)
2. [<span data-ttu-id="e2142-145">연습 2: 데이터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e2142-145">Exercise 2: Data Validation</span></span>](#Exercise2)
3. [<span data-ttu-id="e2142-146">연습 3: ASP.NET의 비동기 페이지 처리 Web Forms</span><span class="sxs-lookup"><span data-stu-id="e2142-146">Exercise 3: Asynchronous Page Processing in ASP.NET Web Forms</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="e2142-147">각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-147">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="e2142-148">연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-148">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="e2142-149">이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="e2142-149">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a><span data-ttu-id="e2142-150">연습 1: ASP.NET Web Forms의 모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="e2142-150">Exercise 1: Model Binding in ASP.NET Web Forms</span></span>

<span data-ttu-id="e2142-151">ASP.NET Web Forms의 새 버전에는 데이터 작업 시 경험 향상에 중점을 둘 수 있는 여러 가지 향상 된 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-151">The new version of ASP.NET Web Forms introduces a number of enhancements focused on improving the experience when working with data.</span></span> <span data-ttu-id="e2142-152">이 연습에서는 강력한 형식의 데이터 컨트롤 및 모델 바인딩에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-152">Throughout this exercise, you will learn about strongly typed data-controls and model binding.</span></span>

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a><span data-ttu-id="e2142-153">작업 1-강력한 형식의 데이터 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="e2142-153">Task 1 - Using Strongly-Typed Data-Bindings</span></span>

<span data-ttu-id="e2142-154">이 작업에서는 ASP.NET 4.5에서 사용할 수 있는 강력한 형식의 새 바인딩을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-154">In this task, you will discover the new strongly-typed bindings available in ASP.NET 4.5.</span></span>

1. <span data-ttu-id="e2142-155">**원본/Ex1-ModelBinding/Begin/** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-155">Open the **Begin** solution located at **Source/Ex1-ModelBinding/Begin/** folder.</span></span>

   1. <span data-ttu-id="e2142-156">계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-156">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="e2142-157">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-157">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e2142-158">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-158">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="e2142-159">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-159">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e2142-160">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-160">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="e2142-161">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-161">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="e2142-162">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-162">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="e2142-163">**Customers .aspx** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-163">Open the **Customers.aspx** page.</span></span> <span data-ttu-id="e2142-164">주 컨트롤에 번호가 없는 목록을 삽입 하 고 각 고객을 나열 하는 데 repeater 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-164">Place an unnumbered list in the main control and include a repeater control inside for listing each customer.</span></span> <span data-ttu-id="e2142-165">다음 코드에 표시 된 것 처럼 repeater 이름을 **Customersrepeater** 로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-165">Set the repeater name to **customersRepeater** as shown in the following code.</span></span>

    <span data-ttu-id="e2142-166">이전 버전의 Web Forms에서 데이터 바인딩을 사용 하 여 데이터 바인딩된 개체의 멤버 값을 내보낼 경우 Eval 메서드에 대 한 호출과 함께 데이터 바인딩 식을 사용 하 여 멤버의 이름을 문자열로 전달 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-166">In previous versions of Web Forms, when using data-binding to emit the value of a member on an object you're data-binding to, you would use a data-binding expression, along with a call to the Eval method, passing in the name of the member as a string.</span></span>

    <span data-ttu-id="e2142-167">런타임에 이러한 Eval 호출은 현재 바인딩된 개체에 대 한 리플렉션을 사용 하 여 지정 된 이름의 멤버 값을 읽고 결과를 HTML로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-167">At runtime, these calls to Eval will use reflection against the currently bound object to read the value of the member with the given name, and display the result in the HTML.</span></span> <span data-ttu-id="e2142-168">이 접근 방식을 사용 하면 임의의 모양의 데이터에 대해 데이터를 매우 쉽게 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-168">This approach makes it very easy to data-bind against arbitrary, unshaped data.</span></span>

    <span data-ttu-id="e2142-169">아쉽게도 멤버 이름에 대 한 IntelliSense, 탐색 지원 (예: 정의로 이동) 및 컴파일 시간 검사를 비롯 하 여 Visual Studio의 다양 한 개발 시간 환경 기능이 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-169">Unfortunately, you lose many of the great development-time experience features in Visual Studio, including IntelliSense for member names, support for navigation (like Go To Definition), and compile-time checking.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. <span data-ttu-id="e2142-170">**Customers.aspx.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-170">Open the **Customers.aspx.cs** file.</span></span>
4. <span data-ttu-id="e2142-171">다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-171">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. <span data-ttu-id="e2142-172">**페이지\_Load** 메서드에서 repeater를 고객 목록으로 채우는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-172">In the **Page\_Load** method, add code to populate the repeater with the list of customers.</span></span>

    <span data-ttu-id="e2142-173">(코드 조각- *Web Forms 랩-Ex01-Customers 데이터 원본 바인딩*)</span><span class="sxs-lookup"><span data-stu-id="e2142-173">(Code Snippet - *Web Forms Lab - Ex01 - Bind Customers Data Source*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    <span data-ttu-id="e2142-174">솔루션은 CodeFirst와 함께 EntityFramework를 사용 하 여 데이터베이스를 만들고 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-174">The solution uses EntityFramework together with CodeFirst to create and access the database.</span></span> <span data-ttu-id="e2142-175">다음 코드에서 customersRepeater는 데이터베이스의 모든 고객을 반환 하는 구체화 된 쿼리에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-175">In the following code, the customersRepeater is bound to a materialized query that returns all the customers from the database.</span></span>
6. <span data-ttu-id="e2142-176">**F5** 키를 눌러 솔루션을 실행 하 고 **고객** 페이지로 이동 하 여 repeater의 동작을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-176">Press **F5** to run the solution and go to the **Customers** page to see the repeater in action.</span></span> <span data-ttu-id="e2142-177">솔루션이 CodeFirst를 사용 하는 경우 응용 프로그램을 실행할 때 데이터베이스가 생성 되 고 로컬 SQL Express 인스턴스에 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-177">As the solution is using CodeFirst, the database will be created and populated in your local SQL Express instance when running the application.</span></span>

    <span data-ttu-id="e2142-178">![Repeater를 사용 하 여 고객 나열](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "Repeater를 사용 하 여 고객 나열")</span><span class="sxs-lookup"><span data-stu-id="e2142-178">![Listing the customers with a repeater](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "Listing the customers with a repeater")</span></span>

    <span data-ttu-id="e2142-179">*Repeater를 사용 하 여 고객 나열*</span><span class="sxs-lookup"><span data-stu-id="e2142-179">*Listing the customers with a repeater*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-180">Visual Studio 2012에서 IIS Express는 기본 웹 개발 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-180">In Visual Studio 2012, IIS Express is the default Web development server.</span></span>
7. <span data-ttu-id="e2142-181">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-181">Close the browser and go back to Visual Studio.</span></span>
8. <span data-ttu-id="e2142-182">이제 강력한 형식의 바인딩을 사용 하도록 구현을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-182">Now replace the implementation to use strongly typed bindings.</span></span> <span data-ttu-id="e2142-183">**Customers** 페이지를 열고 repeater에서 새 **ItemType** 특성을 사용 하 여 **고객** 유형을 바인딩 유형으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-183">Open the **Customers.aspx** page and use the new **ItemType** attribute in the repeater to set the **Customer** type as the binding type.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    <span data-ttu-id="e2142-184">ItemType 속성을 사용 하면 컨트롤이 바인딩될 데이터 형식을 선언 하 고 데이터 바인딩된 컨트롤 내에서 강력한 형식의 바인딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-184">The ItemType property enables you to declare which type of data the control is going to be bound to and allows you to use strongly-typed binding inside the data-bound control.</span></span>
9. <span data-ttu-id="e2142-185">ItemTemplate 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-185">Replace the ItemTemplate content with the following code.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    <span data-ttu-id="e2142-186">위의 방법에서 한 가지 단점은 Eval () 및 Bind ()에 대 한 호출이 런타임에 바인딩되어 있으므로 속성 이름을 나타내는 문자열을 전달 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-186">One downside with the above approaches is that the calls to Eval() and Bind() are late-bound - meaning you pass strings to represent the property names.</span></span> <span data-ttu-id="e2142-187">즉, 멤버 이름에 대 한 Intellisense, 코드 탐색 지원 (예: 정의로 이동) 및 컴파일 시간 검사 지원 기능이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-187">This means you don't get Intellisense for the member names, support for code navigation (like Go To Definition), nor compile-time checking support.</span></span>

    <span data-ttu-id="e2142-188">ItemType 속성을 설정 하면 데이터 바인딩 식의 범위에서 **item** 및 **binditem**이라는 두 개의 새 형식화 된 변수가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-188">Setting the ItemType property causes two new typed variables to be generated in the scope of the data-binding expressions: **Item** and **BindItem**.</span></span> <span data-ttu-id="e2142-189">데이터 바인딩 식에서 이러한 강력한 형식의 변수를 사용 하 여 Visual Studio 개발 환경에 대 한 모든 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-189">You can use these strongly typed variables in the data-binding expressions and get the full benefits of the Visual Studio development experience.</span></span>

    <span data-ttu-id="e2142-190">식에 사용 되는 &quot;&quot;는 보안 문제를 방지 하기 위해 출력을 자동으로 HTML 인코딩합니다 (예 **:** 사이트 간 스크립팅 공격).</span><span class="sxs-lookup"><span data-stu-id="e2142-190">The &quot;**:** &quot; used in the expression will automatically HTML-encode the output to avoid security issues (for example, cross-site scripting attacks).</span></span> <span data-ttu-id="e2142-191">이 표기법은 응답 작성을 위해 .NET 4부터 사용할 수 있었지만 이제는 데이터 바인딩 식 에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-191">This notation was available since .NET 4 for response writing, but now is also available in data-binding expressions.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-192">항목 멤버는 단방향 바인딩에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-192">The Item member works for one-way binding.</span></span> <span data-ttu-id="e2142-193">양방향 바인딩을 수행 하려면 **Binditem** 멤버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-193">If you want to perform two-way binding use the **BindItem** member.</span></span>

    <span data-ttu-id="e2142-194">![강력한 형식의 바인딩에서 IntelliSense 지원](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "강력한 형식의 바인딩에서 IntelliSense 지원")</span><span class="sxs-lookup"><span data-stu-id="e2142-194">![IntelliSense support in strongly-typed binding](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "IntelliSense support in strongly-typed binding")</span></span>

    <span data-ttu-id="e2142-195">*강력한 형식의 바인딩에서 IntelliSense 지원*</span><span class="sxs-lookup"><span data-stu-id="e2142-195">*IntelliSense support in strongly-typed binding*</span></span>
10. <span data-ttu-id="e2142-196">**F5** 키를 눌러 솔루션을 실행 하 고 고객 페이지로 이동 하 여 변경 내용이 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-196">Press **F5** to run the solution and go to the Customers page to make sure the changes work as expected.</span></span>

    <span data-ttu-id="e2142-197">![고객 세부 정보 나열](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "고객 세부 정보 나열")</span><span class="sxs-lookup"><span data-stu-id="e2142-197">![Listing customer details](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "Listing customer details")</span></span>

    <span data-ttu-id="e2142-198">*고객 세부 정보 나열*</span><span class="sxs-lookup"><span data-stu-id="e2142-198">*Listing customer details*</span></span>
11. <span data-ttu-id="e2142-199">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-199">Close the browser and go back to Visual Studio.</span></span>

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a><span data-ttu-id="e2142-200">작업 2-Web Forms의 모델 바인딩 소개</span><span class="sxs-lookup"><span data-stu-id="e2142-200">Task 2 - Introducing Model Binding in Web Forms</span></span>

<span data-ttu-id="e2142-201">이전 버전의 ASP.NET Web Forms에서 데이터를 검색 하 고 업데이트 하는 양방향 데이터 바인딩을 수행 하려는 경우에는 데이터 원본 개체를 사용 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-201">In previous versions of ASP.NET Web Forms, when you wanted to perform two-way data-binding, both retrieving and updating data, you needed to use a Data Source object.</span></span> <span data-ttu-id="e2142-202">개체 데이터 원본, SQL 데이터 원본, LINQ 데이터 원본 등이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-202">This could be an Object Data Source, a SQL Data Source, a LINQ Data Source and so on.</span></span> <span data-ttu-id="e2142-203">그러나 시나리오에서 데이터를 처리 하는 사용자 지정 코드를 필요로 하는 경우에는 개체 데이터 소스를 사용 해야 하는데 약간의 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-203">However if your scenario required custom code for handling the data, you needed to use the Object Data Source and this brought some drawbacks.</span></span> <span data-ttu-id="e2142-204">예를 들어 복합 형식을 피하고 유효성 검사 논리를 실행할 때 예외를 처리 해야 하는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-204">For example, you needed to avoid complex types and you needed to handle exceptions when executing validation logic.</span></span>

<span data-ttu-id="e2142-205">새 버전의 ASP.NET Web Forms 데이터 바인딩된 컨트롤은 모델 바인딩을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-205">In the new version of ASP.NET Web Forms the data-bound controls support model binding.</span></span> <span data-ttu-id="e2142-206">즉, 데이터 바인딩된 컨트롤에서 직접 select, update, insert 및 delete 메서드를 지정 하 여 코드 숨김이 나 다른 클래스에서 논리를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-206">This means that you can specify select, update, insert and delete methods directly in the data-bound control to call logic from your code-behind file or from another class.</span></span>

<span data-ttu-id="e2142-207">이에 대해 자세히 알아보려면 GridView를 사용 하 여 새 **SelectMethod** 특성을 사용 하는 제품 범주를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-207">To learn about this, you will use a GridView to list the product categories using the new **SelectMethod** attribute.</span></span> <span data-ttu-id="e2142-208">이 특성을 사용 하면 GridView 데이터를 검색 하는 메서드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-208">This attribute enables you to specify a method for retrieving the GridView data.</span></span>

1. <span data-ttu-id="e2142-209">**Products .aspx** 페이지를 열고 **GridView**를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-209">Open the **Products.aspx** page and include a **GridView**.</span></span> <span data-ttu-id="e2142-210">강력한 형식의 바인딩을 사용 하 고 정렬과 페이징을 사용 하도록 설정 하려면 아래와 같이 GridView를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-210">Configure the GridView as shown below to use strongly-typed bindings and enable sorting and paging.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. <span data-ttu-id="e2142-211">새 **SelectMethod** 특성을 사용 하 여 **getcategories** 메서드를 호출 하 여 데이터를 선택 하도록 GridView를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-211">Use the new **SelectMethod** attribute to configure the GridView to call a **GetCategories** method to select the data.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. <span data-ttu-id="e2142-212">**Products.aspx.cs** 코드 숨김으로 파일을 열고 다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-212">Open the **Products.aspx.cs** code-behind file and add the following using statements.</span></span>

    <span data-ttu-id="e2142-213">(코드 조각- *Web Forms Ex01*)</span><span class="sxs-lookup"><span data-stu-id="e2142-213">(Code Snippet - *Web Forms Lab - Ex01 - Namespaces*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. <span data-ttu-id="e2142-214">**Products** 클래스에서 private 멤버를 추가 하 고 **ProductsContext**의 새 인스턴스를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-214">Add a private member in the **Products** class and assign a new instance of **ProductsContext**.</span></span> <span data-ttu-id="e2142-215">이 속성은 데이터베이스에 연결할 수 있도록 하는 Entity Framework 데이터 컨텍스트를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-215">This property will store the Entity Framework data context that enables you to connect to the database.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. <span data-ttu-id="e2142-216">LINQ를 사용 하 여 범주 목록을 검색 하는 **Getcategories** 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-216">Create a **GetCategories** method to retrieve the list of categories using LINQ.</span></span> <span data-ttu-id="e2142-217">GridView가 각 범주에 대 한 제품의 양을 표시할 수 있도록 **products** 속성이 쿼리에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-217">The query will include the **Products** property so the GridView can show the amount of products for each category.</span></span> <span data-ttu-id="e2142-218">메서드는 나중에 페이지 수명 주기에서 실행할 쿼리를 나타내는 원시 IQueryable 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-218">Notice that the method returns a raw IQueryable object that represent the query to be executed later on the page lifecycle.</span></span>

    <span data-ttu-id="e2142-219">(코드 조각- *Web Forms Lab-Ex01-GetCategories*)</span><span class="sxs-lookup"><span data-stu-id="e2142-219">(Code Snippet - *Web Forms Lab - Ex01 - GetCategories*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="e2142-220">이전 버전의 ASP.NET Web Forms에서는 사용자 지정 코드를 작성 하 고 필요한 모든 매개 변수를 수신 하는 데 필요한 개체 데이터 소스 컨텍스트 내에서 고유한 리포지토리 논리를 사용 하 여 정렬 및 페이징을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-220">In previous versions of ASP.NET Web Forms, enabling sorting and paging using your own repository logic within an Object Data Source context, required to write your own custom code and receive all the necessary parameters.</span></span> <span data-ttu-id="e2142-221">이제 데이터 바인딩 메서드에서 IQueryable을 반환할 수 있으며이는 실행 되는 쿼리를 나타내므로 ASP.NET는 적절 한 정렬 및 페이징 매개 변수를 추가 하기 위해 쿼리를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-221">Now, as the data-binding methods can return IQueryable and this represents a query still to be executed, ASP.NET can take care of modifying the query to add the proper sorting and paging parameters.</span></span>
6. <span data-ttu-id="e2142-222">**F5** 키를 눌러 사이트 디버깅을 시작 하 고 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-222">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="e2142-223">GridView가 GetCategories 메서드에 의해 반환 된 범주로 채워지는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-223">You should see that the GridView is populated with the categories returned by the GetCategories method.</span></span>

    <span data-ttu-id="e2142-224">![모델 바인딩을 사용 하 여 GridView 채우기](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "모델 바인딩을 사용 하 여 GridView 채우기")</span><span class="sxs-lookup"><span data-stu-id="e2142-224">![Populating a GridView using model binding](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "Populating a GridView using model binding")</span></span>

    <span data-ttu-id="e2142-225">*모델 바인딩을 사용 하 여 GridView 채우기*</span><span class="sxs-lookup"><span data-stu-id="e2142-225">*Populating a GridView using model binding*</span></span>
7. <span data-ttu-id="e2142-226">+**SHIFT** 키를 누르고 **f5** 키를 눌러 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-226">Press **SHIFT**+**F5** Stop debugging.</span></span>

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a><span data-ttu-id="e2142-227">작업 3-모델 바인딩의 값 공급자</span><span class="sxs-lookup"><span data-stu-id="e2142-227">Task 3 - Value Providers in Model Binding</span></span>

<span data-ttu-id="e2142-228">모델 바인딩을 사용 하면 데이터 바인딩된 컨트롤에서 직접 데이터를 사용 하는 사용자 지정 메서드를 지정할 수 있을 뿐만 아니라 페이지의 데이터를 이러한 메서드의 매개 변수에 매핑할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-228">Model binding not only enables you to specify custom methods to work with your data directly in the data-bound control, but also allows you to map data from the page into parameters from these methods.</span></span> <span data-ttu-id="e2142-229">메서드 매개 변수에서 값 공급자 특성을 사용 하 여 값의 데이터 원본을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-229">On the method parameter, you can use value provider attributes to specify the value's data source.</span></span> <span data-ttu-id="e2142-230">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-230">For example:</span></span>

- <span data-ttu-id="e2142-231">페이지의 컨트롤</span><span class="sxs-lookup"><span data-stu-id="e2142-231">Controls on the page</span></span>
- <span data-ttu-id="e2142-232">쿼리 문자열 값</span><span class="sxs-lookup"><span data-stu-id="e2142-232">Query string values</span></span>
- <span data-ttu-id="e2142-233">데이터 보기</span><span class="sxs-lookup"><span data-stu-id="e2142-233">View data</span></span>
- <span data-ttu-id="e2142-234">세션 상태</span><span class="sxs-lookup"><span data-stu-id="e2142-234">Session state</span></span>
- <span data-ttu-id="e2142-235">쿠키</span><span class="sxs-lookup"><span data-stu-id="e2142-235">Cookies</span></span>
- <span data-ttu-id="e2142-236">게시 된 양식 데이터</span><span class="sxs-lookup"><span data-stu-id="e2142-236">Posted form data</span></span>
- <span data-ttu-id="e2142-237">상태 보기</span><span class="sxs-lookup"><span data-stu-id="e2142-237">View state</span></span>
- <span data-ttu-id="e2142-238">사용자 지정 값 공급자도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-238">Custom value providers are supported as well</span></span>

<span data-ttu-id="e2142-239">ASP.NET MVC 4를 사용 하는 경우 모델 바인딩 지원이 유사 하다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-239">If you have used ASP.NET MVC 4, you will notice the model binding support is similar.</span></span> <span data-ttu-id="e2142-240">실제로 이러한 기능은 ASP.NET MVC에서 가져온 후 Web Forms에서 사용할 수 있도록 **system.web** 어셈블리로 이동 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-240">Indeed, these features were taken from ASP.NET MVC and moved into the **System.Web** assembly to be able to use them on Web Forms as well.</span></span>

<span data-ttu-id="e2142-241">이 태스크에서는 모델 바인딩을 사용 하 여 필터 매개 변수를 수신 하는 각 범주에 대 한 제품의 양에 따라 결과를 필터링 하도록 GridView를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-241">In this task, you will update the GridView to filter its results by the amount of products for each category, receiving the filter parameter with model binding.</span></span>

1. <span data-ttu-id="e2142-242">**Products .aspx** 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-242">Go back to the **Products.aspx** page.</span></span>
2. <span data-ttu-id="e2142-243">GridView 위쪽에서 **레이블과** **ComboBox** 를 추가 하 여 아래와 같이 각 범주의 제품 수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-243">At the top of the GridView, add a **Label** and a **ComboBox** to select the number of products for each category as shown below.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. <span data-ttu-id="e2142-244">선택한 수의 제품을 포함 하는 범주가 없으면 메시지를 표시 하도록 GridView에 **emptydatatemplate이** 를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-244">Add an **EmptyDataTemplate** to the GridView to show a message when there are no categories with the selected number of products.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. <span data-ttu-id="e2142-245">**Products.aspx.cs** 코드 숨김으로 열고 다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-245">Open the **Products.aspx.cs** code-behind and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. <span data-ttu-id="e2142-246">**Getcategories** 메서드를 수정 하 여 정수 **minProductsCount** 인수를 받고 반환 된 결과를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-246">Modify the **GetCategories** method to receive an integer **minProductsCount** argument and filter the returned results.</span></span> <span data-ttu-id="e2142-247">이렇게 하려면 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-247">To do this, replace the method with the following code.</span></span>

    <span data-ttu-id="e2142-248">(코드 조각- *Web Forms Lab-Ex01-GetCategories 2*)</span><span class="sxs-lookup"><span data-stu-id="e2142-248">(Code Snippet - *Web Forms Lab - Ex01 - GetCategories 2*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    <span data-ttu-id="e2142-249">**MinProductsCount** 인수의 New **[Control]** 특성은 페이지의 컨트롤을 사용 하 여 해당 값을 채워야 한다는 것을 ASP.NET에 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-249">The new **[Control]** attribute on the **minProductsCount** argument will let ASP.NET know its value must be populated using a control in the page.</span></span> <span data-ttu-id="e2142-250">ASP.NET는 인수 이름 (minProductsCount)과 일치 하는 모든 컨트롤을 검색 하 고 필요한 매핑과 변환을 수행 하 여 매개 변수를 컨트롤 값으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-250">ASP.NET will look for any control matching the name of the argument (minProductsCount) and perform the necessary mapping and conversion to fill the parameter with the control value.</span></span>

    <span data-ttu-id="e2142-251">또는 특성은 값을 가져올 컨트롤을 지정할 수 있는 오버 로드 된 생성자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-251">Alternatively, the attribute provides an overloaded constructor that enables you to specify the control from where to get the value.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-252">데이터 바인딩 기능의 목표 중 하나는 페이지 상호 작용을 위해 작성 해야 하는 코드의 양을 줄이는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-252">One goal of the data-binding features is to reduce the amount of code that needs to be written for page interaction.</span></span> <span data-ttu-id="e2142-253">[Control] 값 공급자 외에 다른 모델 바인딩 공급자를 메서드 매개 변수에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-253">Apart from the [Control] value provider, you can use other model-binding providers in your method parameters.</span></span> <span data-ttu-id="e2142-254">그 중 일부는 작업 소개에 나열 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-254">Some of them are listed in the task introduction.</span></span>
6. <span data-ttu-id="e2142-255">**F5** 키를 눌러 사이트 디버깅을 시작 하 고 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-255">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="e2142-256">드롭다운 목록에서 여러 제품을 선택 하 여 이제 GridView가 업데이트 되는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-256">Select a number of products in the drop-down list and notice how the GridView is now updated.</span></span>

    <span data-ttu-id="e2142-257">![드롭다운 목록 값으로 GridView 필터링](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "드롭다운 목록 값으로 GridView 필터링")</span><span class="sxs-lookup"><span data-stu-id="e2142-257">![Filtering the GridView with a drop-down list value](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "Filtering the GridView with a drop-down list value")</span></span>

    <span data-ttu-id="e2142-258">*드롭다운 목록 값으로 GridView 필터링*</span><span class="sxs-lookup"><span data-stu-id="e2142-258">*Filtering the GridView with a drop-down list value*</span></span>
7. <span data-ttu-id="e2142-259">디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-259">Stop debugging.</span></span>

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a><span data-ttu-id="e2142-260">작업 4-모델 바인딩을 사용 하 여 필터링</span><span class="sxs-lookup"><span data-stu-id="e2142-260">Task 4 - Using Model Binding for Filtering</span></span>

<span data-ttu-id="e2142-261">이 태스크에서는 선택한 범주 내의 제품을 표시 하는 두 번째 자식 GridView를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-261">In this task, you will add a second, child GridView to show the products within the selected category.</span></span>

1. <span data-ttu-id="e2142-262">**Products .aspx** 페이지를 열고 범주 GridView를 업데이트 하 여 선택 단추를 자동 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-262">Open the **Products.aspx** page and update the categories GridView to auto-generate the Select button.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. <span data-ttu-id="e2142-263">맨 아래에 **productsGrid** 라는 두 번째 **GridView** 를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-263">Add a second **GridView** named **productsGrid** at the bottom.</span></span> <span data-ttu-id="e2142-264">**ItemType** 을 **WebDataKeyNames**, to **ProductId** 로 설정 하 고, **SelectMethod** 를 **getproducts**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-264">Set the **ItemType** to **WebFormsLab.Model.Product**, the **DataKeyNames** to **ProductId** and the **SelectMethod** to **GetProducts**.</span></span> <span data-ttu-id="e2142-265">**AutoGenerateColumns** 을 **false** 로 설정 하 고 ProductId, ProductName, Description 및 UnitPrice 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-265">Set **AutoGenerateColumns** to **false** and add the columns for ProductId, ProductName, Description and UnitPrice.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. <span data-ttu-id="e2142-266">**Products.aspx.cs** 코드 숨겨진 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-266">Open the **Products.aspx.cs** code-behind file.</span></span> <span data-ttu-id="e2142-267">**Getproducts** 메서드를 구현 하 여 범주 GridView에서 범주 ID를 받고 제품을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-267">Implement the **GetProducts** method to receive the category ID from the category GridView and filter the products.</span></span> <span data-ttu-id="e2142-268">모델 바인딩에서는 **범주 표에서**선택 된 행을 사용 하 여 매개 변수 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-268">Model binding will set the parameter value using the selected row in the **categoriesGrid**.</span></span> <span data-ttu-id="e2142-269">인수 이름과 컨트롤 이름이 일치 하지 않으므로 컨트롤 값 공급자의 컨트롤 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-269">Since the argument name and control name do not match, you should specify the name of the control in the Control value provider.</span></span>

    <span data-ttu-id="e2142-270">(코드 조각- *Web Forms 랩-Ex01-GetProducts*)</span><span class="sxs-lookup"><span data-stu-id="e2142-270">(Code Snippet - *Web Forms Lab - Ex01 - GetProducts*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="e2142-271">이러한 방법을 사용 하면 이러한 메서드를 보다 쉽게 단위 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-271">This approach makes it easier to unit test these methods.</span></span> <span data-ttu-id="e2142-272">Web Forms 실행 되 고 있지 않은 단위 테스트 컨텍스트에서 [컨트롤] 특성은 특정 작업을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-272">On a unit test context, where Web Forms is not executing, the [Control] attribute will not perform any specific action.</span></span>
4. <span data-ttu-id="e2142-273">**Products .aspx** 페이지를 열고 products GridView를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-273">Open the **Products.aspx** page and locate the products GridView.</span></span> <span data-ttu-id="e2142-274">Products GridView를 업데이트 하 여 선택한 제품을 편집 하기 위한 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-274">Update the products GridView to show a link for editing the selected product.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. <span data-ttu-id="e2142-275">**제품 세부 정보 .aspx** 페이지 코드 숨김으로 열고 **selectproduct** 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-275">Open the **ProductDetails.aspx** page code-behind and replace the **SelectProduct** method with the following code.</span></span>

    <span data-ttu-id="e2142-276">(코드 조각- *Web Forms Lab-Ex01-SelectProduct 메서드*)</span><span class="sxs-lookup"><span data-stu-id="e2142-276">(Code Snippet - *Web Forms Lab - Ex01 - SelectProduct Method*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="e2142-277">**[QueryString]** 특성은 쿼리 문자열의 productId 매개 변수에서 메서드 매개 변수를 채우는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-277">Notice that the **[QueryString]** attribute is used to fill the method parameter from a productId parameter in the query string.</span></span>
6. <span data-ttu-id="e2142-278">**F5** 키를 눌러 사이트 디버깅을 시작 하 고 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-278">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="e2142-279">범주 GridView에서 범주를 선택 하 고 products GridView가 업데이트 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-279">Select any category from the categories GridView and notice that the products GridView is updated.</span></span>

    <span data-ttu-id="e2142-280">![선택한 범주의 제품 표시](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "선택한 범주의 제품 표시")</span><span class="sxs-lookup"><span data-stu-id="e2142-280">![Showing products from the selected category](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "Showing products from the selected category")</span></span>

    <span data-ttu-id="e2142-281">*선택한 범주의 제품 표시*</span><span class="sxs-lookup"><span data-stu-id="e2142-281">*Showing products from the selected category*</span></span>
7. <span data-ttu-id="e2142-282">제품에 대 한 **보기** 링크를 클릭 하 여 제품 세부 정보 .aspx 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-282">Click the **View** link on a product to open the ProductDetails.aspx page.</span></span>

    <span data-ttu-id="e2142-283">페이지에서 쿼리 문자열의 productId 매개 변수를 사용 하 여 SelectMethod를 사용 하 여 제품을 검색 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-283">Notice that the page is retrieving the product with the SelectMethod using the productId parameter from the query string.</span></span>

    <span data-ttu-id="e2142-284">![제품 정보 보기](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "제품 정보 보기")</span><span class="sxs-lookup"><span data-stu-id="e2142-284">![Viewing the product details](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "Viewing the product details")</span></span>

    <span data-ttu-id="e2142-285">*제품 정보 보기*</span><span class="sxs-lookup"><span data-stu-id="e2142-285">*Viewing the product details*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-286">HTML 설명을 입력 하는 기능은 다음 연습에서 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-286">The ability to type an HTML description will be implemented in the next exercise.</span></span>

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a><span data-ttu-id="e2142-287">작업 5-업데이트 작업에 모델 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="e2142-287">Task 5 - Using Model Binding for Update Operations</span></span>

<span data-ttu-id="e2142-288">이전 태스크에서는 주로 데이터를 선택 하기 위해 모델 바인딩을 사용 했습니다 .이 태스크에서는 업데이트 작업에서 모델 바인딩을 사용 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-288">In the previous task, you have used model binding mainly for selecting data, in this task you will learn how to use model binding in update operations.</span></span>

<span data-ttu-id="e2142-289">범주 GridView를 업데이트 하면 사용자가 범주를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-289">You will update the categories GridView to let the user update categories.</span></span>

1. <span data-ttu-id="e2142-290">**Products .aspx** 페이지를 열고 항목 GridView를 업데이트 하 여 편집 단추를 자동 생성 하 고 새 **UpdateMethod** 특성을 사용 하 여 **UpdateCategory** 메서드를 지정 하 여 선택한 항목을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-290">Open the **Products.aspx** page and update the categories GridView to auto-generate the Edit button and use the new **UpdateMethod** attribute to specify an **UpdateCategory** method to update the selected item.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    <span data-ttu-id="e2142-291">GridView의 DataKeyNames 특성은 모델 바인딩된 개체를 고유 하 게 식별 하는 멤버 이며, 따라서 update 메서드가 적어도 받아야 하는 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-291">The DataKeyNames attribute in the GridView define which are the members that uniquely identify the model-bound object and therefore, which are the parameters the update method should at least receive.</span></span>
2. <span data-ttu-id="e2142-292">**Products.aspx.cs** 코드 숨겨진 파일을 열고 **UpdateCategory** 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-292">Open the **Products.aspx.cs** code-behind file and implement the **UpdateCategory** method.</span></span> <span data-ttu-id="e2142-293">메서드는 현재 범주를 로드 하 고 GridView에서 값을 채운 다음 범주를 업데이트 하기 위해 범주 ID를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-293">The method should receive the category ID to load the current category, populate the values from the GridView and then update the category.</span></span>

    <span data-ttu-id="e2142-294">(코드 조각- *Web Forms 랩-Ex01-UpdateCategory*)</span><span class="sxs-lookup"><span data-stu-id="e2142-294">(Code Snippet - *Web Forms Lab - Ex01 - UpdateCategory*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    <span data-ttu-id="e2142-295">Page 클래스의 새 **TryUpdateModel** 메서드는 페이지에 있는 컨트롤의 값을 사용 하 여 모델 개체를 채우는 역할을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-295">The new **TryUpdateModel** method in the Page class is responsible of populating the model object using the values from the controls in the page.</span></span> <span data-ttu-id="e2142-296">이 경우 편집 중인 현재 GridView 행에서 업데이트 된 값을 **category** 개체로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-296">In this case, it will replace the updated values from the current GridView row being edited into the **category** object.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-297">다음 연습에서는 개체를 편집할 때 사용자가 입력 한 데이터의 유효성을 검사 하는 데 사용 되는 ModelState. IsValid를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-297">The next exercise will explain the usage of the ModelState.IsValid for validating the data entered by the user when editing the object.</span></span>
3. <span data-ttu-id="e2142-298">사이트를 실행 하 고 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-298">Run the site and go to the Products page.</span></span> <span data-ttu-id="e2142-299">범주를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-299">Edit a category.</span></span> <span data-ttu-id="e2142-300">새 이름을 입력 한 다음 **업데이트** 를 클릭 하 여 변경 내용을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-300">Type a new name and then click **Update** to persist the changes.</span></span>

    <span data-ttu-id="e2142-301">![범주 편집](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "범주 편집")</span><span class="sxs-lookup"><span data-stu-id="e2142-301">![Editing categories](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "Editing categories")</span></span>

    <span data-ttu-id="e2142-302">*범주 편집*</span><span class="sxs-lookup"><span data-stu-id="e2142-302">*Editing categories*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a><span data-ttu-id="e2142-303">연습 2: 데이터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e2142-303">Exercise 2: Data Validation</span></span>

<span data-ttu-id="e2142-304">이 연습에서는 ASP.NET 4.5의 새로운 데이터 유효성 검사 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-304">In this exercise, you will learn about the new data validation features in ASP.NET 4.5.</span></span> <span data-ttu-id="e2142-305">Web Forms에서 사용자가 제공 하지 않는 새 유효성 검사 기능을 체크 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-305">You will check out the new unobtrusive validation features in Web Forms.</span></span> <span data-ttu-id="e2142-306">사용자 입력 유효성 검사를 위해 응용 프로그램 모델 클래스에서 데이터 주석을 사용 하 고, 마지막으로 페이지의 개별 컨트롤에 대 한 요청 유효성 검사를 설정 하거나 해제 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-306">You will use data annotations in the application model classes for user input validation, and finally, you will learn how to turn on or off request validation to individual controls in a page.</span></span>

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a><span data-ttu-id="e2142-307">작업 1-유효성 검사를 하지 않음</span><span class="sxs-lookup"><span data-stu-id="e2142-307">Task 1 - Unobtrusive Validation</span></span>

<span data-ttu-id="e2142-308">유효성 검사기를 포함 하는 복잡 한 데이터를 포함 하는 양식은 페이지에서 너무 많은 JavaScript 코드를 생성 하 여 코드의 약 60%를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-308">Forms with complex data including validators tend to generate too much JavaScript code in the page, which can represent about 60% of the code.</span></span> <span data-ttu-id="e2142-309">비 표시 유효성 검사를 사용 하도록 설정 하면 HTML 코드가 깔끔하고 tidier 보입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-309">With unobtrusive validation enabled, your HTML code will look cleaner and tidier.</span></span>

<span data-ttu-id="e2142-310">이 섹션에서는 ASP.NET에서 두 구성에 의해 생성 된 HTML 코드를 비교 하는 데 방해가 되는 유효성 검사를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-310">In this section, you will enable unobtrusive validation in ASP.NET to compare the HTML code generated by both configurations.</span></span>

1. <span data-ttu-id="e2142-311">**Visual Studio 2012** 을 열고이 랩의 **Source\ex2-validation\begin** 폴더에 있는 **begin** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-311">Open **Visual Studio 2012** and open the **Begin** solution located in the **Source\Ex2-Validation\Begin** folder of this lab.</span></span> <span data-ttu-id="e2142-312">또는 이전 연습에서 기존 솔루션에 대 한 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-312">Alternatively, you can continue working on your existing solution from the previous exercise.</span></span>

   1. <span data-ttu-id="e2142-313">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-313">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="e2142-314">이렇게 하려면 솔루션 탐색기에서 **Webformslab** 프로젝트 **NuGet 패키지 관리**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-314">To do this, in the Solution Explorer, click the **WebFormsLab** project **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e2142-315">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-315">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="e2142-316">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-316">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e2142-317">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-317">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="e2142-318">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-318">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="e2142-319">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-319">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="e2142-320">**F5** 키를 눌러 웹 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-320">Press **F5** to start the web application.</span></span> <span data-ttu-id="e2142-321">고객 페이지로 이동 하 여 **새 고객 추가** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-321">Go to the Customers page and click the **Add a New Customer** link.</span></span>
3. <span data-ttu-id="e2142-322">브라우저 페이지를 마우스 오른쪽 단추로 클릭 하 고 **소스 보기** 옵션을 선택 하 여 응용 프로그램에서 생성 된 HTML 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-322">Right-click on the browser page, and select **View Source** option to open the HTML code generated by the application.</span></span>

    <span data-ttu-id="e2142-323">![페이지 HTML 코드 표시](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "페이지 HTML 코드 표시")</span><span class="sxs-lookup"><span data-stu-id="e2142-323">![Showing the page HTML code](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "Showing the page HTML code")</span></span>

    <span data-ttu-id="e2142-324">*페이지 HTML 코드 표시*</span><span class="sxs-lookup"><span data-stu-id="e2142-324">*Showing the page HTML code*</span></span>
4. <span data-ttu-id="e2142-325">페이지 소스 코드를 스크롤하고 ASP.NET에서 유효성 검사를 수행 하 고 오류 목록을 표시 하기 위해 페이지에 JavaScript 코드 및 데이터 유효성 검사기를 삽입 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-325">Scroll through the page source code and notice that ASP.NET has injected JavaScript code and data validators in the page to perform the validations and show the error list.</span></span>

    <span data-ttu-id="e2142-326">![CustomerDetails 페이지의 유효성 검사 JavaScript 코드](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "CustomerDetails 페이지의 유효성 검사 JavaScript 코드")</span><span class="sxs-lookup"><span data-stu-id="e2142-326">![Validation JavaScript code in CustomerDetails page](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "Validation JavaScript code in CustomerDetails page")</span></span>

    <span data-ttu-id="e2142-327">*CustomerDetails 페이지의 유효성 검사 JavaScript 코드*</span><span class="sxs-lookup"><span data-stu-id="e2142-327">*Validation JavaScript code in CustomerDetails page*</span></span>
5. <span data-ttu-id="e2142-328">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-328">Close the browser and go back to Visual Studio.</span></span>
6. <span data-ttu-id="e2142-329">이제는 조심 스럽게 유효성 검사를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-329">Now you will enable unobtrusive validation.</span></span> <span data-ttu-id="e2142-330">**Web.config** 를 열고 **AppSettings** 섹션에서 **validationsettings: UnobtrusiveValidationMode** key를 찾습니다 **.**</span><span class="sxs-lookup"><span data-stu-id="e2142-330">Open **Web.Config** and locate **ValidationSettings:UnobtrusiveValidationMode** key in the **AppSettings** section **.**</span></span> <span data-ttu-id="e2142-331">키 값을 **WebForms**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-331">Set the key value to **WebForms**.</span></span>

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > <span data-ttu-id="e2142-332">일부 페이지에 대해서만 &quot;없는 유효성 검사를 사용 하려는 경우에는이 속성을 **페이지\_로드**&quot; 이벤트에서 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-332">You can also set this property in the &quot;**Page\_Load**&quot; event in case you want to enable Unobtrusive Validation only for some pages.</span></span>
7. <span data-ttu-id="e2142-333">**Customerdetails .aspx** 를 열고 **F5** 키를 눌러 웹 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-333">Open **CustomerDetails.aspx** and press **F5** to start the Web application.</span></span>
8. <span data-ttu-id="e2142-334">F12 키를 눌러 IE 개발자 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-334">Press the F12 key to open the IE developer tools.</span></span> <span data-ttu-id="e2142-335">개발자 도구가 열리면 스크립트 탭을 선택 합니다. 메뉴에서 **Customerdetails .aspx** 를 선택 하 고 페이지에서 jQuery를 실행 하는 데 필요한 스크립트가 로컬 사이트에서 브라우저에 로드 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-335">Once the developer tools is open, select the script tab. Select **CustomerDetails.aspx** from the menu and take note that the scripts required to run jQuery on the page have been loaded into the browser from the local site.</span></span>

    <span data-ttu-id="e2142-336">![로컬 IIS 서버에서 직접 jQuery JavaScript 파일 로드](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "로컬 IIS 서버에서 직접 jQuery JavaScript 파일 로드")</span><span class="sxs-lookup"><span data-stu-id="e2142-336">![Loading the jQuery JavaScript files directly from the local IIS server](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "Loading the jQuery JavaScript files directly from the local IIS server")</span></span>

    <span data-ttu-id="e2142-337">*로컬 IIS 서버에서 직접 jQuery JavaScript 파일 로드*</span><span class="sxs-lookup"><span data-stu-id="e2142-337">*Loading the jQuery JavaScript files directly from the local IIS server*</span></span>
9. <span data-ttu-id="e2142-338">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-338">Close the browser to return to Visual Studio.</span></span> <span data-ttu-id="e2142-339">**사이트 마스터** 파일을 다시 열고 **ScriptManager**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-339">Open the **Site.Master** file again and locate the **ScriptManager**.</span></span> <span data-ttu-id="e2142-340">값 **True**를 사용 하 여 **enablecdn** 속성 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-340">Add the attribute **EnableCdn** property with the value **True**.</span></span> <span data-ttu-id="e2142-341">그러면 jQuery가 로컬 사이트의 URL이 아닌 온라인 URL에서 강제로 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-341">This will force jQuery to be loaded from the online URL, not from the local site's URL.</span></span>
10. <span data-ttu-id="e2142-342">Visual Studio에서 **Customerdetails** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-342">Open **CustomerDetails.aspx** in Visual Studio.</span></span> <span data-ttu-id="e2142-343">F5 키를 눌러 사이트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-343">Press the F5 key to run the site.</span></span> <span data-ttu-id="e2142-344">Internet Explorer가 열리면 F12 키를 눌러 개발자 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-344">Once Internet Explorer opens, press the F12 key to open the developer tools.</span></span> <span data-ttu-id="e2142-345">**스크립트** 탭을 선택 하 고 드롭다운 목록을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-345">Select the **Script** tab, and then take a look at the drop-down list.</span></span> <span data-ttu-id="e2142-346">JQuery JavaScript 파일은 더 이상 로컬 사이트에서 로드 되지 않고 온라인 jQuery CDN에서 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-346">Note the jQuery JavaScript files are no longer being loaded from the local site, but rather from the online jQuery CDN.</span></span>

    <span data-ttu-id="e2142-347">![CDN에서 jQuery JavaScript 파일 로드](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "CDN에서 jQuery JavaScript 파일 로드")</span><span class="sxs-lookup"><span data-stu-id="e2142-347">![Loading the jQuery JavaScript files from the CDN](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "Loading the jQuery JavaScript files from the CDN")</span></span>

    <span data-ttu-id="e2142-348">*CDN에서 jQuery JavaScript 파일 로드*</span><span class="sxs-lookup"><span data-stu-id="e2142-348">*Loading the jQuery JavaScript files from the CDN*</span></span>
11. <span data-ttu-id="e2142-349">브라우저에서 소스 보기 옵션을 사용 하 여 HTML 페이지 소스 코드를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-349">Open the HTML page source code again using the View source option in the browser.</span></span> <span data-ttu-id="e2142-350">ASP.NET 유효성 검사를 사용 하도록 설정 하면 삽입 된 JavaScript 코드가 데이터 \*특성으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-350">Notice that by enabling the unobtrusive validation ASP.NET has replaced the injected JavaScript code with data- \*attributes.</span></span>

    <span data-ttu-id="e2142-351">![조심 스럽게 유효성 검사 코드](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "조심 스럽게 유효성 검사 코드")</span><span class="sxs-lookup"><span data-stu-id="e2142-351">![Unobtrusive validation code](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "Unobtrusive validation code")</span></span>

    <span data-ttu-id="e2142-352">*조심 스럽게 유효성 검사 코드*</span><span class="sxs-lookup"><span data-stu-id="e2142-352">*Unobtrusive validation code*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-353">이 예제에서는 데이터 주석이 있는 유효성 검사 요약이 몇 가지 HTML 및 JavaScript 선 으로만 간소화 되었다는 것을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-353">In this example, you saw how a validation summary with Data annotations was simplified to only a few HTML and JavaScript lines.</span></span> <span data-ttu-id="e2142-354">이전에는 유효성을 검사 하지 않고 더 많은 유효성 검사 컨트롤을 추가 하면 JavaScript 유효성 검사 코드가 커집니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-354">Previously, without unobtrusive validation, the more validation controls you add, the bigger your JavaScript validation code will grow.</span></span>

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a><span data-ttu-id="e2142-355">작업 2-데이터 주석을 사용 하 여 모델 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e2142-355">Task 2 - Validating the Model with Data Annotations</span></span>

<span data-ttu-id="e2142-356">ASP.NET 4.5에는 Web Forms에 대 한 데이터 주석 유효성 검사가 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-356">ASP.NET 4.5 introduces data annotations validation for Web Forms.</span></span> <span data-ttu-id="e2142-357">각 입력에 유효성 검사 컨트롤을 사용 하는 대신 이제 모델 클래스에서 제약 조건을 정의 하 고 모든 웹 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-357">Instead of having a validation control on each input, you can now define constraints in your model classes and use them across all your web application.</span></span> <span data-ttu-id="e2142-358">이 섹션에서는 새 고객 폼의 유효성을 검사 하기 위해 데이터 주석을 사용 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-358">In this section, you will learn how to use data annotations for validating a new/edit customer form.</span></span>

1. <span data-ttu-id="e2142-359">**Customerdetail .aspx** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-359">Open **CustomerDetail.aspx** page.</span></span> <span data-ttu-id="e2142-360">**EditItemTemplate** 및 **InsertItemTemplate** 섹션의 customer first name 및 Second Name은 requiredfieldvalidator 컨트롤을 사용 하 여 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-360">Notice that the customer first name and second name in the **EditItemTemplate** and **InsertItemTemplate** sections are validated using a RequiredFieldValidator controls.</span></span> <span data-ttu-id="e2142-361">각 유효성 검사기는 특정 조건에 연결 되므로 검사할 조건으로 많은 유효성 검사기를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-361">Each validator is associated to a particular condition, so you need to include as many validators as conditions to check.</span></span>
2. <span data-ttu-id="e2142-362">고객 모델 클래스의 유효성을 검사 하는 데이터 주석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-362">Add data annotations to validate the Customer model class.</span></span> <span data-ttu-id="e2142-363">**Model** 폴더에서 **Customer.cs** 클래스를 열고 데이터 주석 특성을 사용 하 여 각 속성을 *데코 레이트* 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-363">Open **Customer.cs** class in the **Model** folder and *decorate* each property using data annotation attributes.</span></span>

    <span data-ttu-id="e2142-364">(코드 조각- *Web Forms 랩-Ex02-데이터 주석*)</span><span class="sxs-lookup"><span data-stu-id="e2142-364">(Code Snippet - *Web Forms Lab - Ex02 - Data Annotations*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > <span data-ttu-id="e2142-365">.NET Framework 4.5에서 기존 데이터 주석 컬렉션을 확장 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-365">.NET Framework 4.5 has extended the existing data annotation collection.</span></span> <span data-ttu-id="e2142-366">다음은 사용할 수 있는 데이터 주석 중 일부입니다. [크레딧카드], [Phone], [EmailAddress], [Range], [Compare], [Url], [FileExtensions], [Required], [Key], [RegularExpression].</span><span class="sxs-lookup"><span data-stu-id="e2142-366">These are some of the data annotations you can use: [CreditCard], [Phone], [EmailAddress], [Range], [Compare], [Url], [FileExtensions], [Required], [Key], [RegularExpression].</span></span>
    > 
    > <span data-ttu-id="e2142-367">몇 가지 사용 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-367">Some usage examples:</span></span>
    > 
    > [Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > <span data-ttu-id="e2142-369">각 특성 내에서 고유한 오류 메시지를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-369">You can also define your own error messages within each attribute.</span></span>
3. <span data-ttu-id="e2142-370">**Customerdetails .aspx** 를 열고 FormView 컨트롤의 EditItemTemplate 및 InsertItemTemplate 섹션에서 first 및 last 이름 필드에 대 한 모든 RequiredFieldValidators 검사기를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-370">Open **CustomerDetails.aspx** and remove all the RequiredFieldValidators for the first and last name fields in the in EditItemTemplate and InsertItemTemplate sections of the FormView control.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > <span data-ttu-id="e2142-371">데이터 주석을 사용할 경우의 이점 중 하나는 유효성 검사 논리가 응용 프로그램 페이지에서 중복 되지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-371">One advantage of using data annotations is that validation logic is not duplicated in your application pages.</span></span> <span data-ttu-id="e2142-372">모델에서 한 번 정의 하 고 데이터를 조작 하는 모든 응용 프로그램 페이지에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-372">You define it once in the model, and use it across all the application pages that manipulate data.</span></span>
4. <span data-ttu-id="e2142-373">**Customerdetails .aspx** 코드를 열고 SaveCustomer 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-373">Open **CustomerDetails.aspx** code-behind and locate the SaveCustomer method.</span></span> <span data-ttu-id="e2142-374">이 메서드는 새 고객을 삽입 하 고 FormView 컨트롤 값에서 Customer 매개 변수를 받을 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-374">This method is called when inserting a new customer and receives the Customer parameter from the FormView control values.</span></span> <span data-ttu-id="e2142-375">페이지 컨트롤과 매개 변수 개체 간의 매핑이 발생 하면 ASP.NET는 모든 데이터 주석 특성에 대해 모델 유효성 검사를 실행 하 고 발생 한 오류 (있는 경우)를 사용 하 여 ModelState 사전을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-375">When the mapping between the page controls and the parameter object occurs, ASP.NET will execute the model validation against all the data annotation attributes and fill the ModelState dictionary with the errors encountered, if any.</span></span>

    <span data-ttu-id="e2142-376">ModelState. IsValid는 유효성 검사를 수행한 후 모델의 모든 필드가 유효한 경우에만 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-376">The ModelState.IsValid will only return true if all the fields on your model are valid after performing the validation.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. <span data-ttu-id="e2142-377">CustomerDetails 페이지의 끝에 **ValidationSummary** 컨트롤을 추가 하 여 모델 오류 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-377">Add a **ValidationSummary** control at the end of the CustomerDetails page to show the list of model errors.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    <span data-ttu-id="e2142-378">**Showmodelstateerrors** 는 ValidationSummary 컨트롤의 새 속성으로, **true**로 설정 된 경우 컨트롤은 modelstate 사전에서 오류를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-378">The **ShowModelStateErrors** is a new property on the ValidationSummary control that when set to **true**, the control will show the errors from the ModelState dictionary.</span></span> <span data-ttu-id="e2142-379">이러한 오류는 데이터 주석 유효성 검사에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-379">These errors come from the data annotations validation.</span></span>
6. <span data-ttu-id="e2142-380">**F5** 키를 눌러 웹 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-380">Press **F5** to run the Web application.</span></span> <span data-ttu-id="e2142-381">일부 잘못 된 값으로 양식을 완료 하 고 **저장** 을 클릭 하 여 유효성 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-381">Complete the form with some erroneous values and click **Save** to execute validation.</span></span> <span data-ttu-id="e2142-382">아래쪽에서 오류 요약을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-382">Notice the error summary at the bottom.</span></span>

    <span data-ttu-id="e2142-383">![데이터 주석을 사용한 유효성 검사](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "데이터 주석을 사용한 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="e2142-383">![Validation with Data Annotations](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "Validation with Data Annotations")</span></span>

    <span data-ttu-id="e2142-384">*데이터 주석을 사용한 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="e2142-384">*Validation with Data Annotations*</span></span>

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a><span data-ttu-id="e2142-385">작업 3-ModelState를 사용 하 여 사용자 지정 데이터베이스 오류 처리</span><span class="sxs-lookup"><span data-stu-id="e2142-385">Task 3 - Handling Custom Database Errors with ModelState</span></span>

<span data-ttu-id="e2142-386">이전 버전의 Web Forms에서 너무 긴 문자열 또는 고유 키 위반과 같은 데이터베이스 오류를 처리 하려면 리포지토리 코드에서 예외를 throw 한 다음 코드 숨김으로 예외를 처리 하 여 오류를 표시 하는 것이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-386">In previous version of Web Forms, handling database errors such as a too long string or a unique key violation could involve throwing exceptions in your repository code and then handling the exceptions on your code-behind to display an error.</span></span> <span data-ttu-id="e2142-387">비교적 간단한 작업을 수행 하려면 많은 양의 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-387">A great amount of code is required to do something relatively simple.</span></span>

<span data-ttu-id="e2142-388">Web Forms 4.5에서는 ModelState 개체를 사용 하 여 모델 또는 데이터베이스에서 페이지의 오류를 일관 된 방식으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-388">In Web Forms 4.5, the ModelState object can be used to display the errors on the page, either from your model or from the database, in a consistent manner.</span></span>

<span data-ttu-id="e2142-389">이 태스크에서는 데이터베이스 예외를 올바르게 처리 하 고 ModelState 개체를 사용 하 여 사용자에 게 적절 한 메시지를 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-389">In this task, you will add code to properly handle database exceptions and show the appropriate message to the user using the ModelState object.</span></span>

1. <span data-ttu-id="e2142-390">응용 프로그램이 계속 실행 되는 동안 중복 된 값을 사용 하 여 범주 이름을 업데이트 해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-390">While the application is still running, try to update the name of a category using a duplicated value.</span></span>

    <span data-ttu-id="e2142-391">![중복 된 이름의 범주 업데이트](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "중복 된 이름의 범주 업데이트")</span><span class="sxs-lookup"><span data-stu-id="e2142-391">![Updating a category with a duplicated name](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "Updating a category with a duplicated name")</span></span>

    <span data-ttu-id="e2142-392">*중복 된 이름의 범주 업데이트*</span><span class="sxs-lookup"><span data-stu-id="e2142-392">*Updating a category with a duplicated name*</span></span>

    <span data-ttu-id="e2142-393">**범주** 열의 &quot;unique&quot; 제약 조건으로 인해 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-393">Notice that an exception is thrown due to the &quot;unique&quot; constraint of the **CategoryName** column.</span></span>

    <span data-ttu-id="e2142-394">![중복 된 범주 이름에 대 한 예외](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "중복 된 범주 이름에 대 한 예외")</span><span class="sxs-lookup"><span data-stu-id="e2142-394">![Exception for duplicated category names](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "Exception for duplicated category names")</span></span>

    <span data-ttu-id="e2142-395">*중복 된 범주 이름에 대 한 예외*</span><span class="sxs-lookup"><span data-stu-id="e2142-395">*Exception for duplicated category names*</span></span>
2. <span data-ttu-id="e2142-396">디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-396">Stop debugging.</span></span> <span data-ttu-id="e2142-397">**Products.aspx.cs** 코드 파일에서 **UpdateCategory** 메서드를 업데이트 하 여 db에서 throw 된 예외를 처리 합니다. SaveChanges () 메서드를 호출 하 고 **Modelstate** 개체에 오류를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-397">In the **Products.aspx.cs** code-behind file, update the **UpdateCategory** method to handle the exceptions thrown by the db.SaveChanges() method call and add an error to the **ModelState** object.</span></span>

    <span data-ttu-id="e2142-398">새 **TryUpdateModel** 메서드는 사용자가 제공 하는 양식 데이터를 사용 하 여 데이터베이스에서 검색 된 category 개체를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-398">The new **TryUpdateModel** method updates the category object retrieved from the database using the form data provided by the user.</span></span>

    <span data-ttu-id="e2142-399">(코드 조각- *Web Forms Lab-Ex02-UpdateCategory 처리 오류*)</span><span class="sxs-lookup"><span data-stu-id="e2142-399">(Code Snippet - *Web Forms Lab - Ex02 - UpdateCategory Handle Errors*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > <span data-ttu-id="e2142-400">이상적으로는 DbUpdateException의 원인을 파악 하 고 근본 원인이 고유 키 제약 조건에 위반 되는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-400">Ideally, you would have to identify the cause of the DbUpdateException and check if the root cause is the violation of a unique key constraint.</span></span>
3. <span data-ttu-id="e2142-401">**Products .aspx** 를 열고 범주 GridView 아래에 **ValidationSummary** 컨트롤을 추가 하 여 모델 오류 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-401">Open **Products.aspx** and add a **ValidationSummary** control below the categories GridView to show the list of model errors.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. <span data-ttu-id="e2142-402">사이트를 실행 하 고 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-402">Run the site and go to the Products page.</span></span> <span data-ttu-id="e2142-403">중복 된 값을 사용 하 여 범주 이름을 업데이트 해 보세요.</span><span class="sxs-lookup"><span data-stu-id="e2142-403">Try to update the name of a category using an duplicated value.</span></span>

    <span data-ttu-id="e2142-404">예외가 처리 되 고 오류 메시지가 **ValidationSummary** 컨트롤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-404">Notice that the exception was handled and the error message appears in the **ValidationSummary** control.</span></span>

    <span data-ttu-id="e2142-405">![중복 된 범주 오류](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "중복 된 범주 오류")</span><span class="sxs-lookup"><span data-stu-id="e2142-405">![Duplicated category error](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "Duplicated category error")</span></span>

    <span data-ttu-id="e2142-406">*중복 된 범주 오류*</span><span class="sxs-lookup"><span data-stu-id="e2142-406">*Duplicated category error*</span></span>

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a><span data-ttu-id="e2142-407">작업 4-ASP.NET Web Forms 4.5에서 유효성 검사 요청</span><span class="sxs-lookup"><span data-stu-id="e2142-407">Task 4 - Request Validation in ASP.NET Web Forms 4.5</span></span>

<span data-ttu-id="e2142-408">ASP.NET의 요청 유효성 검사 기능은 XSS (사이트 간 스크립팅) 공격에 대해 특정 수준의 기본 보호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-408">The request validation feature in ASP.NET provides a certain level of default protection against cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="e2142-409">이전 버전의 ASP.NET에서는 요청 유효성 검사를 기본적으로 사용 하도록 설정 했으며 전체 페이지에 대해서만 사용 하지 않도록 설정할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-409">In previous versions of ASP.NET, request validation was enabled by default and could only be disabled for an entire page.</span></span> <span data-ttu-id="e2142-410">ASP.NET Web Forms 새 버전을 사용 하 여 이제 단일 컨트롤에 대 한 요청 유효성 검사를 사용 하지 않도록 설정 하거나, 지연 된 요청 유효성 검사를 수행 하거나, 유효성 검사 되지 않은 요청 데이터에 액세스할 수 있습니다 (이렇게 하려면 주의 해야 함).</span><span class="sxs-lookup"><span data-stu-id="e2142-410">With the new version of ASP.NET Web Forms you can now disable the request validation for a single control, perform lazy request validation or access un-validated request data (be careful if you do so!).</span></span>

1. <span data-ttu-id="e2142-411">**Ctrl + F5** 키를 눌러 디버깅 하지 않고 사이트를 시작 하 고 제품 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-411">Press **Ctrl+F5** to start the site without debugging and go to the Products page.</span></span> <span data-ttu-id="e2142-412">범주를 선택한 다음 제품의 **편집** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-412">Select a category and then click the **Edit** link on any of the products.</span></span>
2. <span data-ttu-id="e2142-413">잠재적으로 위험한 콘텐츠를 포함 하는 설명을 입력 합니다 (예를 들어 HTML 태그 포함).</span><span class="sxs-lookup"><span data-stu-id="e2142-413">Type a description containing potentially dangerous content, for instance including HTML tags.</span></span> <span data-ttu-id="e2142-414">요청 유효성 검사로 인해 throw 되는 예외를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-414">Take notice of the exception thrown due to the request validation.</span></span>

    <span data-ttu-id="e2142-415">![잠재적으로 위험한 콘텐츠가 있는 제품 편집](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "잠재적으로 위험한 콘텐츠가 있는 제품 편집")</span><span class="sxs-lookup"><span data-stu-id="e2142-415">![Editing a product with potentially dangerous content](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "Editing a product with potentially dangerous content")</span></span>

    <span data-ttu-id="e2142-416">*잠재적으로 위험한 콘텐츠가 있는 제품 편집*</span><span class="sxs-lookup"><span data-stu-id="e2142-416">*Editing a product with potentially dangerous content*</span></span>

    <span data-ttu-id="e2142-417">![요청 유효성 검사로 인해 예외가 발생 했습니다.](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "요청 유효성 검사로 인해 예외가 발생 했습니다.")</span><span class="sxs-lookup"><span data-stu-id="e2142-417">![Exception thrown due to request validation](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "Exception thrown due to request validation")</span></span>

    <span data-ttu-id="e2142-418">*요청 유효성 검사로 인해 예외가 발생 했습니다.*</span><span class="sxs-lookup"><span data-stu-id="e2142-418">*Exception thrown due to request validation*</span></span>
3. <span data-ttu-id="e2142-419">페이지를 닫고 Visual Studio에서 **SHIFT + f** 5를 눌러 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-419">Close the page and, in Visual Studio, press **SHIFT+F5** to stop debugging.</span></span>
4. <span data-ttu-id="e2142-420">**제품 세부 정보 .aspx** 페이지를 열고 **설명** 텍스트 상자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-420">Open the **ProductDetails.aspx** page and locate the **Description** TextBox.</span></span>
5. <span data-ttu-id="e2142-421">새 **ValidateRequestMode** 속성을 텍스트 상자에 추가 하 고 해당 값을 **사용 안 함**으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-421">Add the new **ValidateRequestMode** property to the TextBox and set its value to **Disabled**.</span></span>

    <span data-ttu-id="e2142-422">새 **ValidateRequestMode** 특성을 사용 하면 각 컨트롤에서 요청 유효성 검사 세부적으로을 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-422">The new **ValidateRequestMode** attribute allows you to disable the request validation granularly on each control.</span></span> <span data-ttu-id="e2142-423">HTML 코드를 받을 수 있지만 페이지의 나머지 부분에 대해 유효성 검사가 작동 하는 것을 유지 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-423">This is useful when you want to use an input that may receive HTML code, but want to keep the validation working for the rest of the page.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. <span data-ttu-id="e2142-424">**F5** 키를 눌러 웹 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-424">Press **F5** to run the web application.</span></span> <span data-ttu-id="e2142-425">제품 편집 페이지를 다시 열고 HTML 태그를 포함 한 제품 설명을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-425">Open the edit product page again and complete a product description including HTML tags.</span></span> <span data-ttu-id="e2142-426">이제 설명에 HTML 콘텐츠를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-426">Notice that you can now add HTML content to the description.</span></span>

    <span data-ttu-id="e2142-427">![제품 설명에 대 한 요청 유효성 검사를 사용 하지 않습니다.](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "제품 설명에 대 한 요청 유효성 검사를 사용 하지 않습니다.")</span><span class="sxs-lookup"><span data-stu-id="e2142-427">![Request validation disabled for the product description](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "Request validation disabled for the product description")</span></span>

    <span data-ttu-id="e2142-428">*제품 설명에 대 한 요청 유효성 검사를 사용 하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="e2142-428">*Request validation disabled for the product description*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-429">프로덕션 응용 프로그램에서는 사용자가 입력 한 HTML 코드를 삭제 하 여 안전한 HTML 태그만 입력 되도록 해야 합니다. 예를 들어 &lt;스크립트&gt; 태그는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-429">In a production application, you should sanitize the HTML code entered by the user to make sure only safe HTML tags are entered (for example, there are no &lt;script&gt; tags).</span></span> <span data-ttu-id="e2142-430">이를 위해 [Microsoft 웹 보호 라이브러리](https://www.nuget.org/packages/AntiXSS)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-430">To do this, you can use [Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS).</span></span>
7. <span data-ttu-id="e2142-431">제품을 다시 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-431">Edit the product again.</span></span> <span data-ttu-id="e2142-432">이름 필드에 HTML 코드를 입력 하 고 **저장**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-432">Type HTML code in the Name field and click **Save**.</span></span> <span data-ttu-id="e2142-433">요청 유효성 검사는 설명 필드에 대해서만 사용할 수 있으며, 나머지 필드는 잠재적으로 위험한 콘텐츠에 대해 유효성 검사를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-433">Notice that Request Validation is only disabled for the Description field and the rest of the fields re still validated against the potentially dangerous content.</span></span>

    <span data-ttu-id="e2142-434">![나머지 필드에서 요청 유효성 검사 사용](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "나머지 필드에서 요청 유효성 검사 사용")</span><span class="sxs-lookup"><span data-stu-id="e2142-434">![Request validation enabled in the rest of the fields](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "Request validation enabled in the rest of the fields")</span></span>

    <span data-ttu-id="e2142-435">*나머지 필드에서 요청 유효성 검사 사용*</span><span class="sxs-lookup"><span data-stu-id="e2142-435">*Request validation enabled in the rest of the fields*</span></span>

    <span data-ttu-id="e2142-436">ASP.NET Web Forms 4.5은 요청 유효성 검사를 지연 수행 하기 위한 새 요청 유효성 검사 모드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-436">ASP.NET Web Forms 4.5 includes a new request validation mode to perform request validation lazily.</span></span> <span data-ttu-id="e2142-437">요청 유효성 검사 모드를 **4.5**로 설정 하 고 코드 조각이 *&quot;&quot;요청*에 액세스 하는 경우 ASP.NET 4.5의 요청 유효성 검사는 폼 컬렉션의 특정 요소에 대 한 요청 유효성 검사만 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-437">With the request validation mode set to **4.5**, if a piece of code accesses *Request.Form[&quot;key&quot;]*, ASP.NET 4.5's request validation will only trigger request validation for that specific element in the form collection.</span></span>

    <span data-ttu-id="e2142-438">또한 ASP.NET 4.5에는 이제 Microsoft의 XSS 라이브러리 v 4.0의 핵심 인코딩 루틴이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-438">Additionally, ASP.NET 4.5 now includes core encoding routines from the Microsoft Anti-XSS Library v4.0.</span></span> <span data-ttu-id="e2142-439">XSS 방지 인코딩 루틴은 새 Antixssencoder 사용할 **네임 스페이스에 있는 새** 형식에 의해 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-439">The Anti-XSS encoding routines are implemented by the new *AntiXssEncoder* type found in the new **System.Web.Security.AntiXss** namespace.</span></span> <span data-ttu-id="e2142-440">*Antixssencoder 사용할*를 사용 하도록 구성 된 **encoderType** 매개 변수를 사용 하면 ASP.NET 내의 모든 출력 인코딩이 자동으로 새 인코딩 루틴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-440">With the **encoderType** parameter configured to use *AntiXssEncoder*, all output encoding within ASP.NET automatically uses the new encoding routines.</span></span>
8. <span data-ttu-id="e2142-441">ASP.NET 4.5 요청 유효성 검사는 데이터 요청에 대 한 유효성 검사 되지 않은 액세스도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-441">ASP.NET 4.5 request validation also supports un-validated access to request data.</span></span> <span data-ttu-id="e2142-442">ASP.NET 4.5는 **유효성 검사**라는 **HttpRequest** 개체에 새 컬렉션 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-442">ASP.NET 4.5 adds a new collection property to the **HttpRequest** object called **Unvalidated**.</span></span> <span data-ttu-id="e2142-443">HttpRequest로 이동 하면 폼, QueryStrings, 쿠키, Url 등을 비롯 한 요청 데이터의 모든 일반적인 부분에 액세스할 수 있습니다 **.**</span><span class="sxs-lookup"><span data-stu-id="e2142-443">When you navigate into **HttpRequest.Unvalidated** you have access to all of the common pieces of request data, including Forms, QueryStrings, Cookies, URLs, and so on.</span></span>

    <span data-ttu-id="e2142-444">![유효성 검사 개체](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "유효성 검사 개체")</span><span class="sxs-lookup"><span data-stu-id="e2142-444">![Request.Unvalidated object](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request.Unvalidated object")</span></span>

    <span data-ttu-id="e2142-445">*유효성 검사 개체*</span><span class="sxs-lookup"><span data-stu-id="e2142-445">*Request.Unvalidated object*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-446">**HttpRequest. 유효성 검사 속성은 주의 해 서 사용 하세요.**</span><span class="sxs-lookup"><span data-stu-id="e2142-446">**Please use the HttpRequest.Unvalidated property with caution!**</span></span> <span data-ttu-id="e2142-447">원시 요청 데이터에 대 한 사용자 지정 유효성 검사를 신중 하 게 수행 하 여 위험한 텍스트가 라운드트립 하 고 확실 하지 않은 고객에 게 다시 렌더링 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-447">Make sure you carefully perform custom validation on the raw request data to ensure that dangerous text is not round-tripped and rendered back to unsuspecting customers!</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a><span data-ttu-id="e2142-448">연습 3: ASP.NET의 비동기 페이지 처리 Web Forms</span><span class="sxs-lookup"><span data-stu-id="e2142-448">Exercise 3: Asynchronous Page Processing in ASP.NET Web Forms</span></span>

<span data-ttu-id="e2142-449">이 연습에서는 ASP.NET Web Forms의 새로운 비동기 페이지 처리 기능에 대해 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-449">In this exercise, you will be introduced to the new asynchronous page processing features in ASP.NET Web Forms.</span></span>

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a><span data-ttu-id="e2142-450">작업 1-제품 세부 정보 페이지를 업데이트 하 여 이미지 업로드 및 표시</span><span class="sxs-lookup"><span data-stu-id="e2142-450">Task 1 - Updating the Product Details Page to Upload and Show Images</span></span>

<span data-ttu-id="e2142-451">이 작업에서는 제품 세부 정보 페이지를 업데이트 하 여 사용자가 제품에 대 한 이미지 URL을 지정 하 고이를 읽기 전용 보기에 표시할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-451">In this task, you will update the product details page to allow the user to specify an image URL for the product and display it in the read-only view.</span></span> <span data-ttu-id="e2142-452">지정 된 이미지를 동기적으로 다운로드 하 여 로컬 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-452">You will create a local copy of the specified image by downloading it synchronously.</span></span> <span data-ttu-id="e2142-453">다음 태스크에서는이 구현을 업데이트 하 여 비동기 방식으로 작동 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-453">In the next task, you will update this implementation to make it work asynchronously.</span></span>

1. <span data-ttu-id="e2142-454">**Visual Studio 2012** 을 열고이 랩의 폴더에서 **Source\ex3-async\begin** 에 있는 **시작** 솔루션을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-454">Open **Visual Studio 2012** and load the **Begin** solution located in **Source\Ex3-Async\Begin** from this lab's folder.</span></span> <span data-ttu-id="e2142-455">또는 이전 연습에서 기존 솔루션에 대 한 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-455">Alternatively, you can continue working on your existing solution from the previous exercises.</span></span>

   1. <span data-ttu-id="e2142-456">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-456">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="e2142-457">이렇게 하려면 솔루션 탐색기에서 **Webformslab** 프로젝트를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-457">To do this, in the Solution Explorer, click the **WebFormsLab** project and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e2142-458">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-458">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="e2142-459">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-459">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e2142-460">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-460">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="e2142-461">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-461">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="e2142-462">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-462">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="e2142-463">제품 **세부 정보 .aspx** 페이지 소스를 열고 FormView의 ItemTemplate에 필드를 추가 하 여 제품 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-463">Open the **ProductDetails.aspx** page source and add a field in the FormView's ItemTemplate to show the product image.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. <span data-ttu-id="e2142-464">필드를 추가 하 여 FormView의 EditTemplate에서 이미지 URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-464">Add a field to specify the image URL in the FormView's EditTemplate.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. <span data-ttu-id="e2142-465">**ProductDetails.aspx.cs** 코드 숨겨진 파일을 열고 다음 네임 스페이스 지시문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-465">Open the **ProductDetails.aspx.cs** code-behind file and add the following namespace directives.</span></span>

    <span data-ttu-id="e2142-466">(코드 조각- *Web Forms Ex03*)</span><span class="sxs-lookup"><span data-stu-id="e2142-466">(Code Snippet - *Web Forms Lab - Ex03 - Namespaces*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. <span data-ttu-id="e2142-467">로컬 **이미지** 폴더에 원격 이미지를 저장 하는 **UpdateProductImage** 메서드를 만들고 새 이미지 위치 값을 사용 하 여 product 엔터티를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-467">Create an **UpdateProductImage** method to store remote images in the local **Images** folder and update the product entity with the new image location value.</span></span>

    <span data-ttu-id="e2142-468">(코드 조각- *Web Forms 랩-Ex03-UpdateProductImage*)</span><span class="sxs-lookup"><span data-stu-id="e2142-468">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. <span data-ttu-id="e2142-469">**UpdateProductImage** 메서드를 호출 하도록 **updateproduct** 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-469">Update the **UpdateProduct** method to call the **UpdateProductImage** method.</span></span>

    <span data-ttu-id="e2142-470">(코드 조각- *Web Forms Lab-Ex03-UpdateProductImage Call*)</span><span class="sxs-lookup"><span data-stu-id="e2142-470">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage Call*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. <span data-ttu-id="e2142-471">응용 프로그램을 실행 하 고 제품에 대 한 이미지를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-471">Run the application and try to upload an image for a product.</span></span> <span data-ttu-id="e2142-472">예를 들어 Office 클립 예술에서 다음 이미지 URL을 사용할 수 있습니다. [ [http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)</span><span class="sxs-lookup"><span data-stu-id="e2142-472">For example, you can use the following image URL from Office Clip Arts: [[http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)</span></span>

    <span data-ttu-id="e2142-473">![제품에 대 한 이미지 설정](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "제품에 대 한 이미지 설정")</span><span class="sxs-lookup"><span data-stu-id="e2142-473">![Setting an image for a product](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "Setting an image for a product")</span></span>

    <span data-ttu-id="e2142-474">*제품에 대 한 이미지 설정*</span><span class="sxs-lookup"><span data-stu-id="e2142-474">*Setting an image for a product*</span></span>

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a><span data-ttu-id="e2142-475">작업 2-제품 세부 정보 페이지에 비동기 처리 추가</span><span class="sxs-lookup"><span data-stu-id="e2142-475">Task 2 - Adding Asynchronous Processing to the Product Details Page</span></span>

<span data-ttu-id="e2142-476">이 작업에서는 제품 세부 정보 페이지를 업데이트 하 여 비동기 방식으로 작동 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-476">In this task, you will update the product details page to make it work asynchronously.</span></span> <span data-ttu-id="e2142-477">ASP.NET 4.5 비동기 페이지 처리를 사용 하 여 장기 실행 작업 (이미지 다운로드 프로세스)을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-477">You will enhance a long running task - the image download process - by using ASP.NET 4.5 asynchronous page processing.</span></span>

<span data-ttu-id="e2142-478">웹 응용 프로그램의 비동기 메서드를 사용 하 여 ASP.NET 스레드 풀을 사용 하는 방법을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-478">Asynchronous methods in web applications can be used to optimize the way ASP.NET thread pools are used.</span></span> <span data-ttu-id="e2142-479">ASP.NET의 스레드 풀에는 요청에 참여 하기 위한 스레드 수가 제한 되어 있기 때문에 모든 스레드가 사용 중이면 ASP.NET가 새 요청을 거부 하 고 응용 프로그램 오류 메시지를 전송 하 여 사이트를 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-479">In ASP.NET there are a limited number of threads in the thread pool for attending requests, thus, when all the threads are busy, ASP.NET starts to reject new requests, sends application error messages and makes your site unavailable.</span></span>

<span data-ttu-id="e2142-480">웹 사이트에서 시간이 오래 걸리는 작업은 할당 된 스레드를 오랫동안 사용 하기 때문에 비동기 프로그래밍에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-480">Time-consuming operations on your web site are great candidates for asynchronous programming because they occupy the assigned thread for a long time.</span></span> <span data-ttu-id="e2142-481">여기에는 장기 실행 요청, 데이터베이스를 쿼리하거나 외부 웹 서버에 액세스 하는 경우와 같이 오프 라인 작업을 필요로 하는 다양 한 요소 및 페이지가 있는 페이지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-481">This includes long running requests, pages with lots of different elements and pages that require offline operations, such querying a database or accessing an external web server.</span></span> <span data-ttu-id="e2142-482">이러한 작업에 비동기 메서드를 사용 하는 경우 페이지가 처리 되는 동안 스레드가 해제 되 고 스레드 풀로 반환 되 고 새 페이지 요청에 참석 하는 데 사용 될 수 있다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-482">The advantage is that if you use asynchronous methods for these operations, while the page is processing, the thread is freed and returned to the thread pool and can be used to attend to a new page request.</span></span> <span data-ttu-id="e2142-483">즉, 페이지는 스레드 풀의 한 스레드에서 처리를 시작 하 고 비동기 처리가 완료 된 후 다른 스레드에서 처리를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-483">This means, the page will start processing in one thread from the thread pool and might complete processing in a different one, after the async processing completes.</span></span>

1. <span data-ttu-id="e2142-484">**제품 세부 정보 .aspx** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-484">Open the **ProductDetails.aspx** page.</span></span> <span data-ttu-id="e2142-485">**Page** 요소에 **Async** 특성을 추가 하 고 **true**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-485">Add the **Async** attribute in the **Page** element and set it to **true**.</span></span> <span data-ttu-id="e2142-486">이 특성은 IHttpAsyncHandler 인터페이스를 구현 하도록 ASP.NET에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-486">This attribute tells ASP.NET to implement the IHttpAsyncHandler interface.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. <span data-ttu-id="e2142-487">페이지 아래쪽에 레이블을 추가 하 여 페이지를 실행 하는 스레드에 대 한 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-487">Add a Label at the bottom of the page to show the details of the threads running the page.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. <span data-ttu-id="e2142-488">**ProductDetails.aspx.cs** 를 열고 다음 네임 스페이스 지시문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-488">Open up **ProductDetails.aspx.cs** and add the following namespace directives.</span></span>

    <span data-ttu-id="e2142-489">(코드 조각- *Web Forms Ex03-네임 스페이스 2*)</span><span class="sxs-lookup"><span data-stu-id="e2142-489">(Code Snippet - *Web Forms Lab - Ex03 - Namespaces 2*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. <span data-ttu-id="e2142-490">**UpdateProductImage** 메서드를 수정 하 여 비동기 작업으로 이미지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-490">Modify the **UpdateProductImage** method to download the image with an asynchronous task.</span></span> <span data-ttu-id="e2142-491">**WebClient** **DownloadFile** 메서드를 **DownloadFileTaskAsync** 메서드로 바꾸고 **wait** 키워드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-491">You will replace the **WebClient** **DownloadFile** method with the **DownloadFileTaskAsync** method and include the **await** keyword.</span></span>

    <span data-ttu-id="e2142-492">(코드 조각- *Web Forms Lab-Ex03-UpdateProductImage Async*)</span><span class="sxs-lookup"><span data-stu-id="e2142-492">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage Async*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    <span data-ttu-id="e2142-493">RegisterAsyncTask는 다른 스레드에서 실행할 새 페이지 비동기 작업을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-493">The RegisterAsyncTask registers a new page asynchronous task to be executed in a different thread.</span></span> <span data-ttu-id="e2142-494">실행할 태스크 (t)를 사용 하 여 람다 식을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-494">It receives a lambda expression with the Task (t) to be executed.</span></span> <span data-ttu-id="e2142-495">**DownloadFileTaskAsync** 메서드의 **wait** 키워드는 메서드 나머지를 **DownloadFileTaskAsync** 메서드가 완료 된 후 비동기식으로 호출 되는 콜백으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-495">The **await** keyword in the **DownloadFileTaskAsync** method converts the remainder of the method into a callback that is invoked asynchronously after the **DownloadFileTaskAsync** method has completed.</span></span> <span data-ttu-id="e2142-496">ASP.NET는 모든 HTTP 요청 원래 값을 자동으로 유지 하 여 메서드 실행을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-496">ASP.NET will resume the execution of the method by automatically maintaining all the HTTP request original values.</span></span> <span data-ttu-id="e2142-497">.NET 4.5의 새로운 비동기 프로그래밍 모델을 사용 하면 동기 코드와 매우 비슷한 비동기 코드를 작성 하 고 컴파일러에서 콜백 함수 또는 연속 코드의 복잡 한 문제를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-497">The new asynchronous programming model in .NET 4.5 enables you to write asynchronous code that looks very much like synchronous code, and let the compiler handle the complications of callback functions or continuation code.</span></span>
    > [!NOTE]
    > <span data-ttu-id="e2142-498">RegisterAsyncTask 및 PageAsyncTask은 .NET 2.0부터 이미 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-498">RegisterAsyncTask and PageAsyncTask were already available since .NET 2.0.</span></span> <span data-ttu-id="e2142-499">Wait 키워드는 .NET 4.5 비동기 프로그래밍 모델에서 새로 사용 되며 .NET WebClient 개체의 새 TaskAsync 메서드와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-499">The await keyword is new from the .NET 4.5 asynchronous programming model and can be used together with the new TaskAsync methods from the .NET WebClient object.</span></span>
5. <span data-ttu-id="e2142-500">코드가 시작 되 고 실행이 완료 된 스레드를 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-500">Add code to display the threads on which the code started and finished executing.</span></span> <span data-ttu-id="e2142-501">이렇게 하려면 **UpdateProductImage** 메서드를 다음 코드로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-501">To do this, update the **UpdateProductImage** method with the following code.</span></span>

    <span data-ttu-id="e2142-502">(코드 조각- *Web Forms 랩-Ex03-스레드 표시*)</span><span class="sxs-lookup"><span data-stu-id="e2142-502">(Code Snippet - *Web Forms Lab - Ex03 - Show threads*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. <span data-ttu-id="e2142-503">**웹 사이트의 web.config 파일을** 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-503">Open the web site's **Web.config** file.</span></span> <span data-ttu-id="e2142-504">다음 appSetting 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-504">Add the following appSetting variable.</span></span>

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. <span data-ttu-id="e2142-505">**F5** 키를 눌러 응용 프로그램을 실행 하 고 제품에 대 한 이미지를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-505">Press **F5** to run the application and upload an image for the product.</span></span> <span data-ttu-id="e2142-506">코드가 시작 되 고 완료 된 스레드 ID가 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-506">Notice the threads ID where the code started and finished may be different.</span></span> <span data-ttu-id="e2142-507">비동기 작업은 ASP.NET 스레드 풀에서 별도의 스레드에서 실행 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-507">This is because asynchronous tasks run on a separate thread from ASP.NET thread pool.</span></span> <span data-ttu-id="e2142-508">태스크가 완료 되 면 ASP.NET는 작업을 다시 큐에 넣고 사용 가능한 스레드를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-508">When the task completes, ASP.NET puts the task back in the queue and assigns any of the available threads.</span></span>

    <span data-ttu-id="e2142-509">![비동기적으로 이미지 다운로드](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "비동기적으로 이미지 다운로드")</span><span class="sxs-lookup"><span data-stu-id="e2142-509">![Downloading an image asynchronously](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "Downloading an image asynchronously")</span></span>

    <span data-ttu-id="e2142-510">*비동기적으로 이미지 다운로드*</span><span class="sxs-lookup"><span data-stu-id="e2142-510">*Downloading an image asynchronously*</span></span>

> [!NOTE]
> <span data-ttu-id="e2142-511">또한 [부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)를 따라 Azure에이 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-511">Additionally, you can deploy this application to Azure following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="e2142-512">요약</span><span class="sxs-lookup"><span data-stu-id="e2142-512">Summary</span></span>

<span data-ttu-id="e2142-513">이 실습 랩에서는 다음 개념에 대해 설명 하 고 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-513">In this hands-on lab, the following concepts have been addressed and demonstrated:</span></span>

- <span data-ttu-id="e2142-514">강력한 형식의 데이터 바인딩 식 사용</span><span class="sxs-lookup"><span data-stu-id="e2142-514">Use strongly-typed data-binding expressions</span></span>
- <span data-ttu-id="e2142-515">Web Forms에서 새 모델 바인딩 기능 사용</span><span class="sxs-lookup"><span data-stu-id="e2142-515">Use new model binding features in Web Forms</span></span>
- <span data-ttu-id="e2142-516">값 공급자를 사용 하 여 페이지 데이터를 코드 숨김이 메서드에 매핑</span><span class="sxs-lookup"><span data-stu-id="e2142-516">Use value providers for mapping page data to code-behind methods</span></span>
- <span data-ttu-id="e2142-517">사용자 입력 유효성 검사에 대 한 데이터 주석 사용</span><span class="sxs-lookup"><span data-stu-id="e2142-517">Use Data Annotations for user input validation</span></span>
- <span data-ttu-id="e2142-518">Web Forms에서 jQuery에 대 한 클라이언트 쪽 유효성 검사를 사용 하지 않는 기능 활용</span><span class="sxs-lookup"><span data-stu-id="e2142-518">Take advantage of unobtrusive client-side validation with jQuery in Web Forms</span></span>
- <span data-ttu-id="e2142-519">세부적인 요청 유효성 검사 구현</span><span class="sxs-lookup"><span data-stu-id="e2142-519">Implement granular request validation</span></span>
- <span data-ttu-id="e2142-520">Web Forms에서 비동기 페이지 처리 구현</span><span class="sxs-lookup"><span data-stu-id="e2142-520">Implement asynchronous page processing in Web Forms</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="e2142-521">부록 A: 웹에 대 한 Visual Studio Express 2012 설치</span><span class="sxs-lookup"><span data-stu-id="e2142-521">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="e2142-522">**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-522">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="e2142-523">다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-523">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="e2142-524">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-524">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="e2142-525">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> 제품 &quot;검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-525">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="e2142-526">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-526">Click on **Install Now**.</span></span> <span data-ttu-id="e2142-527">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-527">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="e2142-528">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-528">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="e2142-529">![Visual Studio Express 설치](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="e2142-529">![Install Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="e2142-530">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="e2142-530">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="e2142-531">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-531">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    <span data-ttu-id="e2142-533">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="e2142-533">*Accepting the license terms*</span></span>
5. <span data-ttu-id="e2142-534">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-534">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    <span data-ttu-id="e2142-536">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="e2142-536">*Installation progress*</span></span>
6. <span data-ttu-id="e2142-537">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-537">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    <span data-ttu-id="e2142-539">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="e2142-539">*Installation completed*</span></span>
7. <span data-ttu-id="e2142-540">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-540">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="e2142-541">웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-541">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    <span data-ttu-id="e2142-543">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="e2142-543">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="e2142-544">부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="e2142-544">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="e2142-545">이 부록에서는 azure Portal에서 새 웹 사이트를 만들고 랩에 따라 얻은 응용 프로그램을 게시 하 여 Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-545">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="e2142-546">작업 1-Azure 포털에서 새 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="e2142-546">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="e2142-547">[Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-547">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-548">Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 다음 트래픽이 증가 함에 따라 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-548">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="e2142-549">[여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-549">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="e2142-550">![Windows Azure Portal에 로그온 합니다.](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Windows Azure Portal에 로그온 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2142-550">![Log on to Windows Azure portal](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="e2142-551">*포털 로그온*</span><span class="sxs-lookup"><span data-stu-id="e2142-551">*Log on to the Portal*</span></span>
2. <span data-ttu-id="e2142-552">명령 모음에서 **새로 만들기** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-552">Click **New** on the command bar.</span></span>

    <span data-ttu-id="e2142-553">![새 웹 사이트 만들기](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="e2142-553">![Creating a new Web Site](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="e2142-554">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="e2142-554">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="e2142-555">**Compute** | **웹 사이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-555">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="e2142-556">그런 다음 **빠른 생성** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-556">Then select **Quick Create** option.</span></span> <span data-ttu-id="e2142-557">새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-557">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-558">Azure는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-558">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="e2142-559">빠른 생성 옵션을 사용 하면 포털 외부에서 완료 된 웹 응용 프로그램을 Azure에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-559">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="e2142-560">데이터베이스를 설정 하는 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-560">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="e2142-561">![빠른 생성을 사용 하 여 새 웹 사이트 만들기](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="e2142-561">![Creating a new Web Site using Quick Create](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="e2142-562">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="e2142-562">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="e2142-563">새 **웹 사이트가** 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-563">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="e2142-564">웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-564">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="e2142-565">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-565">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="e2142-566">![새 웹 사이트로 이동](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "새 웹 사이트로 이동")</span><span class="sxs-lookup"><span data-stu-id="e2142-566">![Browsing to the new web site](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="e2142-567">*새 웹 사이트로 이동*</span><span class="sxs-lookup"><span data-stu-id="e2142-567">*Browsing to the new web site*</span></span>

    <span data-ttu-id="e2142-568">![웹 사이트 실행 중](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "웹 사이트 실행 중")</span><span class="sxs-lookup"><span data-stu-id="e2142-568">![Web site running](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "Web site running")</span></span>

    <span data-ttu-id="e2142-569">*웹 사이트 실행 중*</span><span class="sxs-lookup"><span data-stu-id="e2142-569">*Web site running*</span></span>
6. <span data-ttu-id="e2142-570">포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-570">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="e2142-571">![웹 사이트 관리 페이지 열기](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="e2142-571">![Opening the web site management pages](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="e2142-572">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="e2142-572">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="e2142-573">**대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-573">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-574">*게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Azure에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-574">The *publish profile* contains all of the information required to publish a web application to Azure for each enabled publication method.</span></span> <span data-ttu-id="e2142-575">게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-575">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="e2142-576">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 Azure에 웹 응용 프로그램을 게시 하기 위해 이러한 프로그램의 구성을 자동화 하는 게시 프로필 읽기를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-576">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="e2142-577">![웹 사이트 게시 프로필을 다운로드 하는 중](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "웹 사이트 게시 프로필을 다운로드 하는 중")</span><span class="sxs-lookup"><span data-stu-id="e2142-577">![Downloading the web site publish profile](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="e2142-578">*웹 사이트 게시 프로필을 다운로드 하는 중*</span><span class="sxs-lookup"><span data-stu-id="e2142-578">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="e2142-579">알려진 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-579">Download the publish profile file to a known location.</span></span> <span data-ttu-id="e2142-580">이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Azure에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-580">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="e2142-581">![게시 프로필 파일을 저장 하는 중](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "게시 프로필을 저장 하는 중")</span><span class="sxs-lookup"><span data-stu-id="e2142-581">![Saving the publish profile file](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "Saving the publish profile")</span></span>

    <span data-ttu-id="e2142-582">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="e2142-582">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="e2142-583">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="e2142-583">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="e2142-584">응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-584">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="e2142-585">SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-585">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="e2142-586">응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-586">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="e2142-587">Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL database** | **Servers** | **서버 대시보드**.</span><span class="sxs-lookup"><span data-stu-id="e2142-587">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="e2142-588">만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-588">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="e2142-589">다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-589">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="e2142-590">이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="e2142-590">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="e2142-591">![SQL Database 서버 대시보드](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="e2142-591">![SQL Database Server Dashboard](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="e2142-592">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="e2142-592">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="e2142-593">다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-593">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="e2142-594">이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-594">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) button.</span></span>

    ![클라이언트 IP 주소를 추가 하는 중](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    <span data-ttu-id="e2142-596">*클라이언트 IP 주소를 추가 하는 중*</span><span class="sxs-lookup"><span data-stu-id="e2142-596">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="e2142-597">**클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-597">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 내용 확인](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    <span data-ttu-id="e2142-599">*변경 내용 확인*</span><span class="sxs-lookup"><span data-stu-id="e2142-599">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="e2142-600">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="e2142-600">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="e2142-601">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-601">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="e2142-602">**솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-602">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="e2142-603">![응용 프로그램 게시](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="e2142-603">![Publishing the Application](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "Publishing the Application")</span></span>

    <span data-ttu-id="e2142-604">*웹 사이트 게시*</span><span class="sxs-lookup"><span data-stu-id="e2142-604">*Publishing the web site*</span></span>
2. <span data-ttu-id="e2142-605">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-605">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="e2142-606">![게시 프로필을 가져오는 중](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "게시 프로필을 가져오는 중")</span><span class="sxs-lookup"><span data-stu-id="e2142-606">![Importing the publish profile](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "Importing the publish profile")</span></span>

    <span data-ttu-id="e2142-607">*게시 프로필을 가져오는 중*</span><span class="sxs-lookup"><span data-stu-id="e2142-607">*Importing publish profile*</span></span>
3. <span data-ttu-id="e2142-608">**연결 유효성 검사**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-608">Click **Validate Connection**.</span></span> <span data-ttu-id="e2142-609">유효성 검사가 완료 되 면 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-609">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2142-610">유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-610">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="e2142-611">![연결 유효성 검사](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="e2142-611">![Validating connection](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "Validating connection")</span></span>

    <span data-ttu-id="e2142-612">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="e2142-612">*Validating connection*</span></span>
4. <span data-ttu-id="e2142-613">**설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-613">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="e2142-614">![웹 배포 구성](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="e2142-614">![Web deploy configuration](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web deploy configuration")</span></span>

    <span data-ttu-id="e2142-615">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="e2142-615">*Web deploy configuration*</span></span>
5. <span data-ttu-id="e2142-616">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-616">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="e2142-617">**서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-617">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="e2142-618">**사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-618">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="e2142-619">**암호** 에 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-619">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="e2142-620">새 데이터베이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-620">Type a new database name.</span></span>

     <span data-ttu-id="e2142-621">![대상 연결 문자열 구성](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="e2142-621">![Configuring destination connection string](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="e2142-622">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="e2142-622">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="e2142-623">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-623">Then click **OK**.</span></span> <span data-ttu-id="e2142-624">데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-624">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="e2142-625">![데이터베이스 만들기](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="e2142-625">![Creating the database](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "Creating the database string")</span></span>

    <span data-ttu-id="e2142-626">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="e2142-626">*Creating the database*</span></span>
7. <span data-ttu-id="e2142-627">Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-627">The connection string you will use to connect to SQL Database in Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="e2142-628">그런 후 **Next** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-628">Then click **Next**.</span></span>

    <span data-ttu-id="e2142-629">![SQL Database를 가리키는 연결 문자열](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "SQL Database를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="e2142-629">![Connection string pointing to SQL Database](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="e2142-630">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="e2142-630">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="e2142-631">**미리 보기** 페이지에서 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-631">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="e2142-632">![웹 응용 프로그램 게시](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="e2142-632">![Publishing the web application](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "Publishing the web application")</span></span>

    <span data-ttu-id="e2142-633">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="e2142-633">*Publishing the web application*</span></span>
9. <span data-ttu-id="e2142-634">게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-634">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="e2142-635">부록 C: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="e2142-635">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="e2142-636">코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-636">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="e2142-637">랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-637">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="e2142-638">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")</span><span class="sxs-lookup"><span data-stu-id="e2142-638">![Using Visual Studio code snippets to insert code into your project](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="e2142-639">*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*</span><span class="sxs-lookup"><span data-stu-id="e2142-639">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="e2142-640">***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***</span><span class="sxs-lookup"><span data-stu-id="e2142-640">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="e2142-641">코드를 삽입할 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-641">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="e2142-642">조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-642">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="e2142-643">IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-643">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="e2142-644">올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-644">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="e2142-645">Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-645">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="e2142-646">![코드 조각 이름 입력 시작](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "코드 조각 이름 입력 시작")</span><span class="sxs-lookup"><span data-stu-id="e2142-646">![Start typing the snippet name](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "Start typing the snippet name")</span></span>

<span data-ttu-id="e2142-647">*코드 조각 이름 입력 시작*</span><span class="sxs-lookup"><span data-stu-id="e2142-647">*Start typing the snippet name*</span></span>

<span data-ttu-id="e2142-648">![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2142-648">![Press Tab to select the highlighted snippet](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="e2142-649">*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2142-649">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="e2142-650">![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="e2142-650">![Press Tab again and the snippet will expand](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="e2142-651">*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="e2142-651">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="e2142-652">***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1).</span><span class="sxs-lookup"><span data-stu-id="e2142-652">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="e2142-653">코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-653">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="e2142-654">코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-654">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="e2142-655">목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2142-655">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="e2142-656">![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2142-656">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="e2142-657">*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2142-657">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="e2142-658">![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2142-658">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="e2142-659">*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2142-659">*Pick the relevant snippet from the list, by clicking on it*</span></span>
