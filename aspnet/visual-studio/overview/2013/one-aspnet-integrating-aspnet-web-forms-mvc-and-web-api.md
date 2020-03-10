---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: '실습: One ASP.NET: ASP.NET Web Forms, MVC 및 Web API 통합 | Microsoft Docs'
author: rick-anderson
description: ASP.NET는 MVC, Web API 등의 전문 기술을 사용 하 여 웹 사이트, 앱 및 서비스를 빌드하기 위한 프레임 워크입니다. 확장 ASP.NET h ...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505457"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a><span data-ttu-id="094a2-104">실습: One ASP.NET: ASP.NET Web Forms, MVC 및 Web API 통합</span><span class="sxs-lookup"><span data-stu-id="094a2-104">Hands On Lab: One ASP.NET: Integrating ASP.NET Web Forms, MVC and Web API</span></span>

<span data-ttu-id="094a2-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="094a2-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="094a2-106">웹 캠프 교육 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="094a2-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="094a2-107">ASP.NET는 MVC, Web API 등의 전문 기술을 사용 하 여 웹 사이트, 앱 및 서비스를 빌드하기 위한 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-107">ASP.NET is a framework for building Web sites, apps and services using specialized technologies such as MVC, Web API and others.</span></span> <span data-ttu-id="094a2-108">확장 ASP.NET이 생성 된 후에는 이러한 기술이 통합 되어야 하 **는 것으로 나타났습니다.**</span><span class="sxs-lookup"><span data-stu-id="094a2-108">With the expansion ASP.NET has seen since its creation and the expressed need to have these technologies integrated, there have been recent efforts in working towards **One ASP.NET**.</span></span>
> 
> <span data-ttu-id="094a2-109">Visual Studio 2013에는 응용 프로그램을 빌드하고 한 프로젝트의 모든 ASP.NET 기술을 사용할 수 있도록 하는 통합 프로젝트 시스템이 새로 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-109">Visual Studio 2013 introduces a new unified project system which lets you build an application and use all the ASP.NET technologies in one project.</span></span> <span data-ttu-id="094a2-110">이 기능을 사용 하면 프로젝트를 시작할 때 한 기술을 선택 하 여 함께 사용할 필요가 없으며, 대신 한 프로젝트 내에서 여러 ASP.NET 프레임 워크를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-110">This feature eliminates the need to pick one technology at the start of a project and stick with it, and instead encourages the use of multiple ASP.NET frameworks within one project.</span></span>
> 
> <span data-ttu-id="094a2-111">모든 샘플 코드와 코드 조각은 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-111">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="094a2-112">개요</span><span class="sxs-lookup"><span data-stu-id="094a2-112">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="094a2-113">목표</span><span class="sxs-lookup"><span data-stu-id="094a2-113">Objectives</span></span>

<span data-ttu-id="094a2-114">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-114">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="094a2-115">ASP.NET 프로젝트 형식 **하나** 를 기반으로 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-115">Create a Web site based on the **One ASP.NET** project type</span></span>
- <span data-ttu-id="094a2-116">동일한 프로젝트에서 **MVC** 및 **Web API** 와 같은 다른 **ASP.NET** 프레임 워크 사용</span><span class="sxs-lookup"><span data-stu-id="094a2-116">Use different **ASP.NET** frameworks like **MVC** and **Web API** in the same project</span></span>
- <span data-ttu-id="094a2-117">**ASP.NET** 응용 프로그램의 주요 구성 요소를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-117">Identify the main components of an **ASP.NET** application</span></span>
- <span data-ttu-id="094a2-118">**ASP.NET 스 캐 폴딩** 프레임 워크를 활용 하 여 모델 클래스를 기반으로 CRUD 작업을 수행 하는 컨트롤러 및 뷰를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-118">Take advantage of the **ASP.NET Scaffolding** framework to automatically create Controllers and Views to perform CRUD operations based on your model classes</span></span>
- <span data-ttu-id="094a2-119">각 작업에 적합 한 도구를 사용 하 여 컴퓨터 및 사람이 읽을 수 있는 형식으로 동일한 정보 집합을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-119">Expose the same set of information in machine- and human-readable formats using the right tool for each job</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="094a2-120">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="094a2-120">Prerequisites</span></span>

<span data-ttu-id="094a2-121">이 실습 실습을 완료 하려면 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-121">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="094a2-122">[웹 이상의 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="094a2-122">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="094a2-123">Visual Studio 2013 업데이트 1</span><span class="sxs-lookup"><span data-stu-id="094a2-123">Visual Studio 2013 Update 1</span></span>](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="094a2-124">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="094a2-124">Setup</span></span>

<span data-ttu-id="094a2-125">이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-125">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="094a2-126">Windows 탐색기를 열고 랩의 **원본** 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-126">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="094a2-127">**Setup.exe** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행** 을 선택 하 여 환경을 구성 하는 설치 프로세스를 시작 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-127">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="094a2-128">사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-128">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="094a2-129">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 확인 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-129">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="094a2-130">코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="094a2-130">Using the Code Snippets</span></span>

<span data-ttu-id="094a2-131">랩 문서 전체에서 코드 블록을 삽입 하 라는 지침이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-131">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="094a2-132">사용자 편의를 위해이 코드의 대부분은 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio Code 코드 조각으로 제공 되며,이를 수동으로 추가 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-132">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="094a2-133">각 연습에는 각 연습을 서로 독립적으로 수행할 수 있는 연습 **시작** 폴더에 있는 시작 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-133">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="094a2-134">연습 중에 추가 된 코드 조각은 이러한 시작 솔루션에서 누락 되었으며, 연습을 완료할 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-134">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="094a2-135">연습에 대 한 소스 코드 내에서 해당 연습의 단계를 완료 하 여 생성 된 코드를 포함 하는 Visual Studio 솔루션을 포함 하는 **끝** 폴더를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-135">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="094a2-136">이 실습 랩을 통해 작업할 때 추가 도움이 필요한 경우 이러한 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-136">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="094a2-137">실습</span><span class="sxs-lookup"><span data-stu-id="094a2-137">Exercises</span></span>

<span data-ttu-id="094a2-138">이 실습 랩에는 다음 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-138">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="094a2-139">새 Web Forms 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-139">Creating a New Web Forms Project</span></span>](#Exercise1)
2. [<span data-ttu-id="094a2-140">스 캐 폴딩을 사용 하 여 MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-140">Creating an MVC Controller Using Scaffolding</span></span>](#Exercise2)
3. [<span data-ttu-id="094a2-141">스 캐 폴딩을 사용 하 여 Web API 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-141">Creating a Web API Controller Using Scaffolding</span></span>](#Exercise3)

<span data-ttu-id="094a2-142">이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="094a2-142">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="094a2-143">Visual Studio를 처음 시작 하는 경우 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-143">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="094a2-144">미리 정의 된 각 컬렉션은 특정 개발 스타일에 맞게 디자인 되 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-144">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="094a2-145">이 실습의 절차에서는 **일반 개발 설정** 컬렉션을 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-145">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="094a2-146">개발 환경에 대해 다른 설정 컬렉션을 선택 하는 경우 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-146">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a><span data-ttu-id="094a2-147">연습 1: 새 Web Forms 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-147">Exercise 1: Creating a New Web Forms Project</span></span>

<span data-ttu-id="094a2-148">이 연습에서는 **하나의 ASP.NET** 통합 프로젝트 환경을 사용 하 여 Visual Studio 2013에 새 Web Forms 사이트를 만듭니다 .이를 통해 동일한 응용 프로그램에서 WEB FORMS, MVC 및 Web API 구성 요소를 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-148">In this exercise you will create a new Web Forms site in Visual Studio 2013 using the **One ASP.NET** unified project experience, which will allow you to easily integrate Web Forms, MVC and Web API components in the same application.</span></span> <span data-ttu-id="094a2-149">그런 다음 생성 된 솔루션을 탐색 하 고 파트를 식별 하 고 마지막으로 웹 사이트를 작동 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-149">You will then explore the generated solution and identify its parts, and finally you will see the Web site in action.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a><span data-ttu-id="094a2-150">작업 1-하나의 ASP.NET 환경을 사용 하 여 새 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-150">Task 1 – Creating a New Site Using the One ASP.NET Experience</span></span>

<span data-ttu-id="094a2-151">이 작업에서는 Visual Studio에서 ASP.NET 프로젝트 형식 **하나** 를 기반으로 새 웹 사이트 만들기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-151">In this task you will start creating a new Web site in Visual Studio based on the **One ASP.NET** project type.</span></span> <span data-ttu-id="094a2-152">**한 ASP.NET** 는 모든 ASP.NET 기술을 통합 하 고 원하는 대로 혼합 하 고 일치 시킬 수 있는 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-152">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="094a2-153">그런 다음 응용 프로그램 내에서 나란히 있는 Web Forms, MVC 및 Web API의 여러 구성 요소를 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-153">You will then recognize the different components of Web Forms, MVC and Web API that live side by side within your application.</span></span>

1. <span data-ttu-id="094a2-154">**웹에 대해 Visual Studio Express 2013** 을 열고 파일을 선택 합니다. **| 새 프로젝트** ... 새 솔루션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-154">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    ![새 프로젝트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    <span data-ttu-id="094a2-156">*새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="094a2-156">*Creating a New Project*</span></span>
2. <span data-ttu-id="094a2-157">**새 프로젝트** 대화 상자의 시각적 개체  **C# 에서 ASP.NET 웹 응용 프로그램을 선택 합니다. 웹** 탭을 선택 하 고 **.NET Framework 4.5** 을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-157">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab, and make sure **.NET Framework 4.5** is selected.</span></span> <span data-ttu-id="094a2-158">프로젝트 이름을 *MyHybridSite*로, **위치** 를 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-158">Name the project *MyHybridSite*, choose a **Location** and click **OK**.</span></span>

    ![새 ASP.NET 웹 응용 프로그램 프로젝트](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    <span data-ttu-id="094a2-160">*새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="094a2-160">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="094a2-161">**새 ASP.NET 프로젝트** 대화 상자에서 **Web Forms** 템플릿을 선택 하 고 **MVC** 및 **Web API** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-161">In the **New ASP.NET Project** dialog box, select the **Web Forms** template and select the **MVC** and **Web API** options.</span></span> <span data-ttu-id="094a2-162">또한 **인증** 옵션이 **개별 사용자 계정**으로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-162">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="094a2-163">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-163">Click **OK** to continue.</span></span>

    ![Web API 및 MVC 구성 요소를 포함 하 여 Web Forms 템플릿을 사용 하 여 새 프로젝트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    <span data-ttu-id="094a2-165">*Web API 및 MVC 구성 요소를 포함 하 여 Web Forms 템플릿을 사용 하 여 새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="094a2-165">*Creating a new project with the Web Forms template, including Web API and MVC components*</span></span>
4. <span data-ttu-id="094a2-166">이제 생성 된 솔루션의 구조를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-166">You can now explore the structure of the generated solution.</span></span>

    ![생성 된 솔루션 살펴보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    <span data-ttu-id="094a2-168">*생성 된 솔루션 살펴보기*</span><span class="sxs-lookup"><span data-stu-id="094a2-168">*Exploring the generated solution*</span></span>

    1. <span data-ttu-id="094a2-169">**계정:** 이 폴더에는 응용 프로그램의 사용자 계정을 등록 하 고, 로그인 하 고, 관리할 웹 폼 페이지가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-169">**Account:** This folder contains the Web Form pages to register, log in to and manage the application's user accounts.</span></span> <span data-ttu-id="094a2-170">이 폴더는 Web Forms 프로젝트 템플릿을 구성 하는 동안 **개별 사용자 계정** 인증 옵션을 선택한 경우에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-170">This folder is added when the **Individual User Accounts** authentication option is selected during the configuration of the Web Forms project template.</span></span>
    2. <span data-ttu-id="094a2-171">**모델:** 이 폴더에는 응용 프로그램 데이터를 나타내는 클래스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-171">**Models:** This folder will contain the classes that represent your application data.</span></span>
    3. <span data-ttu-id="094a2-172">**컨트롤러** 및 **뷰**: 이러한 폴더는 **ASP.NET MVC** 및 **ASP.NET Web API** 구성 요소에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-172">**Controllers** and **Views**: These folders are required for the **ASP.NET MVC** and **ASP.NET Web API** components.</span></span> <span data-ttu-id="094a2-173">다음 연습에서 MVC 및 Web API 기술을 살펴볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-173">You will explore the MVC and Web API technologies in the next exercises.</span></span>
    4. <span data-ttu-id="094a2-174">**Default.aspx 및** **.Aspx 파일에 대 한 정보** **는 응용**프로그램과 관련 된 페이지를 빌드하기 위한 시작 점으로 사용할 수 있는 미리 정의 된 웹 폼 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-174">The **Default.aspx**, **Contact.aspx** and **About.aspx** files are pre-defined Web Form pages that you can use as starting points to build the pages specific to your application.</span></span> <span data-ttu-id="094a2-175">이러한 파일의 프로그래밍 논리는 사용 되는 언어에 따라 &quot;.aspx&quot; 또는 &quot;aspx.cs&quot; 확장명을 포함 하는 &quot;코드 숨김이&quot; 파일 이라고 하는 별도의 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-175">The programming logic of those files resides in a separate file referred to as the &quot;code-behind&quot; file, which has an &quot;.aspx.vb&quot; or &quot;.aspx.cs&quot; extension (depending on the language used).</span></span> <span data-ttu-id="094a2-176">코드 숨겨진 논리는 서버에서 실행 되 고 페이지에 대 한 HTML 출력을 동적으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-176">The code-behind logic runs on the server and dynamically produces the HTML output for your page.</span></span>
    5. <span data-ttu-id="094a2-177">**Site.master** 및 **site.master 페이지는** 응용 프로그램의 모든 페이지에 대 한 모양과 느낌 및 표준 동작을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-177">The **Site.Master** and **Site.Mobile.Master** pages define the look and feel and the standard behavior of all the pages in the application.</span></span>
5. <span data-ttu-id="094a2-178">**Default.aspx 파일을** 두 번 클릭 하 여 페이지의 내용을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-178">Double-click the **Default.aspx** file to explore the content of the page.</span></span>

    ![Default.aspx 페이지 살펴보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    <span data-ttu-id="094a2-180">*Default.aspx 페이지 살펴보기*</span><span class="sxs-lookup"><span data-stu-id="094a2-180">*Exploring the Default.aspx page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="094a2-181">파일 맨 위에 있는 **page** 지시어는 Web Forms 페이지의 특성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-181">The **Page** directive at the top of the file defines the attributes of the Web Forms page.</span></span> <span data-ttu-id="094a2-182">예를 들어 **MasterPageFile** 특성은 마스터 페이지에 대 한 경로를 지정 합니다 *.* 이 경우에는 site.master 페이지와 **Inherits** 특성이 상속할 페이지의 코드 숨김이 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-182">For example, the **MasterPageFile** attribute specifies the path to the master page -in this case, the *Site.Master* page- and the **Inherits** attribute defines the code-behind class for the page to inherit.</span></span> <span data-ttu-id="094a2-183">이 클래스는 **CodeBehind** 특성에 의해 결정 되는 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-183">This class is located in the file determined by the **CodeBehind** attribute.</span></span>
    > 
    > <span data-ttu-id="094a2-184">**Asp: Content** 컨트롤은 페이지의 실제 콘텐츠 (텍스트, 태그 및 컨트롤)를 저장 하 고 마스터 페이지의 **asp: ContentPlaceHolder** 컨트롤에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-184">The **asp:Content** control holds the actual content of the page (text, markup and controls) and is mapped to a **asp:ContentPlaceHolder** control on the master page.</span></span> <span data-ttu-id="094a2-185">이 경우 페이지 콘텐츠는 *site.master* 페이지에 정의 된 *MainContent* 컨트롤 내에서 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-185">In this case, the page content will be rendered inside the *MainContent* control defined in the *Site.Master* page.</span></span>
6. <span data-ttu-id="094a2-186">**앱\_시작** 폴더를 확장 하 고 **WebApiConfig.cs** 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-186">Expand the **App\_Start** folder and notice the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="094a2-187">ASP.NET 템플릿 하나를 사용 하 여 프로젝트를 구성 하는 경우 Web API를 포함 했기 때문에 Visual Studio에서는 생성 된 솔루션에 해당 파일을 포함 했습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-187">Visual Studio included that file in the generated solution because you included Web API when configuring your project with the One ASP.NET template.</span></span>
7. <span data-ttu-id="094a2-188">**WebApiConfig.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-188">Open the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="094a2-189">*Webapiconfig* 클래스에서 web api에 연결 된 구성을 찾을 수 있으며,이는 HTTP 경로를 **웹 api 컨트롤러**에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-189">In the *WebApiConfig* class you will find the configuration associated with Web API, which maps HTTP routes to **Web API controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. <span data-ttu-id="094a2-190">**RouteConfig.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-190">Open the **RouteConfig.cs** file.</span></span> <span data-ttu-id="094a2-191">*RegisterRoutes* 메서드 내에서 mvc와 관련 된 구성을 찾을 수 있으며,이는 HTTP 경로를 **mvc 컨트롤러**에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-191">Inside the *RegisterRoutes* method you will find the configuration associated with MVC, which maps HTTP routes to **MVC controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="094a2-192">작업 2-솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="094a2-192">Task 2 – Running the Solution</span></span>

<span data-ttu-id="094a2-193">이 작업에서는 생성 된 솔루션을 실행 하 고 앱 및 URL 재작성 및 기본 제공 인증과 같은 일부 기능을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-193">In this task you will run the generated solution, explore the app and some of its features, like URL rewriting and built-in authentication.</span></span>

1. <span data-ttu-id="094a2-194">솔루션을 실행 하려면 **F5** 키를 누르거나 도구 모음에 있는 **시작** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-194">To run the solution, press **F5** or click the **Start** button located on the toolbar.</span></span> <span data-ttu-id="094a2-195">응용 프로그램 홈 페이지가 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-195">The application home page should open in the browser.</span></span>

    ![솔루션 실행](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. <span data-ttu-id="094a2-197">Web Forms 페이지가 호출 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-197">Verify that the Web Forms pages are being invoked.</span></span> <span data-ttu-id="094a2-198">이렇게 하려면 주소 표시줄의 URL에 **/contact.aspx** 를 추가 하 고 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-198">To do this, append **/contact.aspx** to the URL in the address bar and press **Enter**.</span></span>

    ![친숙한 URL](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    <span data-ttu-id="094a2-200">*친숙 한 Url*</span><span class="sxs-lookup"><span data-stu-id="094a2-200">*Friendly URLs*</span></span>

    > [!NOTE]
    > <span data-ttu-id="094a2-201">여기에서 볼 수 있듯이 URL은 **/contact**로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-201">As you can see, the URL changes to **/contact**.</span></span> <span data-ttu-id="094a2-202">**ASP.NET 4**부터 url 라우팅 기능이 Web Forms에 추가 되었으므로 *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* 대신 *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* 와 같은 url을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-202">Starting from **ASP.NET 4**, URL routing capabilities were added to Web Forms, so you can write URLs like *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* instead of *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*.</span></span> <span data-ttu-id="094a2-203">자세한 내용은 [URL 라우팅](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="094a2-203">For more information refer to [URL Routing](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).</span></span>
3. <span data-ttu-id="094a2-204">이제 응용 프로그램에 통합 된 인증 흐름이 탐색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-204">You will now explore the authentication flow integrated into the application.</span></span> <span data-ttu-id="094a2-205">이렇게 하려면 페이지의 오른쪽 위 모퉁이에 있는 **등록** 을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-205">To do this, click **Register** in the upper-right corner of the page.</span></span>

    ![새 사용자 등록](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    <span data-ttu-id="094a2-207">*새 사용자 등록*</span><span class="sxs-lookup"><span data-stu-id="094a2-207">*Registering a new user*</span></span>
4. <span data-ttu-id="094a2-208">**등록** 페이지에서 **사용자 이름** 및 **암호**를 입력 한 다음 **등록**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-208">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    ![페이지 등록](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    <span data-ttu-id="094a2-210">*페이지 등록*</span><span class="sxs-lookup"><span data-stu-id="094a2-210">*Register page*</span></span>
5. <span data-ttu-id="094a2-211">응용 프로그램이 새 계정을 등록 하 고 사용자가 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-211">The application registers the new account, and the user is authenticated.</span></span>

    ![사용자 인증 됨](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    <span data-ttu-id="094a2-213">*사용자 인증 됨*</span><span class="sxs-lookup"><span data-stu-id="094a2-213">*User authenticated*</span></span>
6. <span data-ttu-id="094a2-214">Visual Studio로 돌아가서 **SHIFT + f5** 키를 눌러 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-214">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a><span data-ttu-id="094a2-215">연습 2: 스 캐 폴딩을 사용 하 여 MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-215">Exercise 2: Creating an MVC Controller Using Scaffolding</span></span>

<span data-ttu-id="094a2-216">이 연습에서는 Visual Studio에서 제공 하는 ASP.NET 스 캐 폴딩 프레임 워크를 활용 하 여 코드를 한 줄도 작성 하지 않고도 CRUD 작업을 수행 하는 작업 및 Razor 뷰로 ASP.NET MVC 5 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-216">In this exercise you will take advantage of the ASP.NET Scaffolding framework provided by Visual Studio to create an ASP.NET MVC 5 controller with actions and Razor views to perform CRUD operations, without writing a single line of code.</span></span> <span data-ttu-id="094a2-217">스 캐 폴딩 프로세스에서는 Entity Framework Code First를 사용 하 여 SQL database에 데이터 컨텍스트와 데이터베이스 스키마를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-217">The scaffolding process will use Entity Framework Code First to generate the data context and the database schema in the SQL database.</span></span>

<span data-ttu-id="094a2-218">**Entity Framework Code First 정보**</span><span class="sxs-lookup"><span data-stu-id="094a2-218">**About Entity Framework Code First**</span></span>

<span data-ttu-id="094a2-219">EF (Entity Framework)는 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있도록 하는 ORM (개체 관계형 매퍼)입니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-219">Entity Framework (EF) is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span>

<span data-ttu-id="094a2-220">Entity Framework Code First 모델링 워크플로를 사용 하면 사용자 고유의 도메인 클래스를 사용 하 여 쿼리, 변경 내용 추적 및 업데이트 기능을 수행할 때 EF에서 사용 하는 모델을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-220">The Entity Framework Code First modeling workflow allows you to use your own domain classes to represent the model that EF relies on when performing querying, change-tracking and updating functions.</span></span> <span data-ttu-id="094a2-221">Code First 개발 워크플로를 사용 하 여 데이터베이스를 만들거나 스키마를 지정 하 여 응용 프로그램을 시작할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-221">Using the Code First development workflow, you do not need to begin your application by creating a database or specifying a schema.</span></span> <span data-ttu-id="094a2-222">대신 응용 프로그램에 가장 적합 한 도메인 모델 개체를 정의 하는 표준 .NET 클래스를 작성할 수 있으며, Entity Framework는 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-222">Instead, you can write standard .NET classes that define the most appropriate domain model objects for your application, and Entity Framework will create the database for you.</span></span>

> [!NOTE]
> <span data-ttu-id="094a2-223">Entity Framework에 대 한 자세한 내용은 [여기](../../../entity-framework.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="094a2-223">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a><span data-ttu-id="094a2-224">작업 1-새 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-224">Task 1 – Creating a New Model</span></span>

<span data-ttu-id="094a2-225">이제 **사용자** 클래스를 정의 합니다 .이는 스 캐 폴딩 프로세스에서 MVC 컨트롤러 및 뷰를 만드는 데 사용 하는 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-225">You will now define a **Person** class, which will be the model used by the scaffolding process to create the MVC controller and the views.</span></span> <span data-ttu-id="094a2-226">먼저 **Person** 모델 클래스를 만들고, 컨트롤러의 CRUD 작업은 스 캐 폴딩 기능을 사용 하 여 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-226">You will start by creating a **Person** model class, and the CRUD operations in the controller will be automatically created using scaffolding features.</span></span>

1. <span data-ttu-id="094a2-227">**웹에 대해 Visual Studio Express 2013** 을 열고 **Source/Ex2-mvcscaffolding 캐 폴딩/Begin** 폴더에 있는 **MyHybridSite** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-227">Open **Visual Studio Express 2013 for Web** and the **MyHybridSite.sln** solution located in the **Source/Ex2-MvcScaffolding/Begin** folder.</span></span> <span data-ttu-id="094a2-228">또는 이전 연습에서 얻은 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-228">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="094a2-229">**솔루션 탐색기**에서 **MyHybridSite** 프로젝트의 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 클래스 ...** .</span><span class="sxs-lookup"><span data-stu-id="094a2-229">In **Solution Explorer**, right-click the **Models** folder of the **MyHybridSite** project and select **Add | Class...**.</span></span>

    ![Person 모델 클래스 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    <span data-ttu-id="094a2-231">*Person 모델 클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="094a2-231">*Adding the Person model class*</span></span>
3. <span data-ttu-id="094a2-232">**새 항목 추가** 대화 상자에서 파일 이름을 *Person.cs* 로 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-232">In the **Add New Item** dialog box, name the file *Person.cs* and click **Add**.</span></span>

    ![Person 모델 클래스 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    <span data-ttu-id="094a2-234">*Person 모델 클래스 만들기*</span><span class="sxs-lookup"><span data-stu-id="094a2-234">*Creating the Person model class*</span></span>
4. <span data-ttu-id="094a2-235">**Person.cs** 파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-235">Replace the content of the **Person.cs** file with the following code.</span></span> <span data-ttu-id="094a2-236">**Ctrl + S** 를 눌러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-236">Press **CTRL + S** to save the changes.</span></span>

    <span data-ttu-id="094a2-237">(코드 조각- *BringingTogetherOneAspNet-Ex2-PersonClass*)</span><span class="sxs-lookup"><span data-stu-id="094a2-237">(Code Snippet - *BringingTogetherOneAspNet - Ex2 - PersonClass*)</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. <span data-ttu-id="094a2-238">**솔루션 탐색기**에서 **MyHybridSite** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **빌드**를 선택 하거나 **ctrl + SHIFT + B** 를 눌러 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-238">In **Solution Explorer**, right-click the **MyHybridSite** project and select **Build**, or press **CTRL + SHIFT + B** to build the project.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a><span data-ttu-id="094a2-239">작업 2-MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-239">Task 2 – Creating an MVC Controller</span></span>

<span data-ttu-id="094a2-240">이제 **person** 모델을 만들었으므로 ASP.NET MVC 스 캐 폴딩을 Entity Framework와 함께 사용 하 여 **사용자**를 위한 CRUD 컨트롤러 작업 및 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-240">Now that the **Person** model is created, you will use ASP.NET MVC scaffolding with Entity Framework to create the CRUD controller actions and views for **Person**.</span></span>

1. <span data-ttu-id="094a2-241">**솔루션 탐색기**에서 **MyHybridSite** 프로젝트의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 스 캐 폴드 항목**....</span><span class="sxs-lookup"><span data-stu-id="094a2-241">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![새 스 캐 폴드 컨트롤러 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    <span data-ttu-id="094a2-243">*새 스 캐 폴드 컨트롤러 만들기*</span><span class="sxs-lookup"><span data-stu-id="094a2-243">*Creating a new Scaffolded Controller*</span></span>
2. <span data-ttu-id="094a2-244">**스 캐 폴드 추가** 대화 상자에서 **Entity Framework를 사용 하 여 MVC 5 컨트롤러 (뷰 포함)를** 선택 하 고 추가를 클릭 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="094a2-244">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework** and then click **Add.**</span></span>

    ![뷰 및 Entity Framework를 사용 하 여 MVC 5 컨트롤러 선택](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    <span data-ttu-id="094a2-246">*뷰 및 Entity Framework를 사용 하 여 MVC 5 컨트롤러 선택*</span><span class="sxs-lookup"><span data-stu-id="094a2-246">*Selecting MVC 5 Controller with views and Entity Framework*</span></span>
3. <span data-ttu-id="094a2-247">*MvcPersonController* 을 **컨트롤러 이름**으로 설정 하 고, **비동기 컨트롤러 작업 사용** 옵션을 선택 하 고, **모델 클래스로** **Person (MyHybridSite)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-247">Set *MvcPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** as the **Model class**.</span></span>

    ![스 캐 폴딩을 사용 하 여 MVC 컨트롤러 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    <span data-ttu-id="094a2-249">*스 캐 폴딩을 사용 하 여 MVC 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="094a2-249">*Adding an MVC controller with scaffolding*</span></span>
4. <span data-ttu-id="094a2-250">**데이터 컨텍스트 클래스**에서 **새 데이터 컨텍스트**...를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-250">Under **Data context class**, click **New data context...**.</span></span>

    ![새 데이터 컨텍스트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    <span data-ttu-id="094a2-252">*새 데이터 컨텍스트 만들기*</span><span class="sxs-lookup"><span data-stu-id="094a2-252">*Creating a new data context*</span></span>
5. <span data-ttu-id="094a2-253">**새 데이터 컨텍스트** 대화 상자에서 새 데이터 컨텍스트의 이름을 *PersonContext* 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-253">In the **New Data Context** dialog box, name the new data context *PersonContext* and click **Add**.</span></span>

    ![새 PersonContext 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    <span data-ttu-id="094a2-255">*새 PersonContext 형식 만들기*</span><span class="sxs-lookup"><span data-stu-id="094a2-255">*Creating the new PersonContext type*</span></span>
6. <span data-ttu-id="094a2-256">**추가** 를 클릭 하 여 스 캐 폴딩이 있는 **사용자** 에 대 한 새 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-256">Click **Add** to create the new controller for **Person** with scaffolding.</span></span> <span data-ttu-id="094a2-257">그런 다음 Visual Studio는 컨트롤러 작업, Person 데이터 컨텍스트 및 Razor 뷰를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-257">Visual Studio will then generate the controller actions, the Person data context and the Razor views.</span></span>

    ![스 캐 폴딩을 사용 하 여 MVC 컨트롤러를 만든 후](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    <span data-ttu-id="094a2-259">*스 캐 폴딩을 사용 하 여 MVC 컨트롤러를 만든 후*</span><span class="sxs-lookup"><span data-stu-id="094a2-259">*After creating the MVC controller with scaffolding*</span></span>
7. <span data-ttu-id="094a2-260">**Controllers** 폴더에서 **MvcPersonController.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-260">Open the **MvcPersonController.cs** file in the **Controllers** folder.</span></span> <span data-ttu-id="094a2-261">CRUD 작업 메서드가 자동으로 생성 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-261">Notice that the CRUD action methods have been generated automatically.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > <span data-ttu-id="094a2-262">이전 단계에서 스 캐 폴딩 옵션의 비동기 **컨트롤러 작업 사용** 확인란을 선택 하면 Visual Studio는 Person 데이터 컨텍스트에 대 한 액세스를 포함 하는 모든 작업에 대해 비동기 작업 메서드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-262">By selecting the **Use async controller actions** check box from the scaffolding options in the previous steps, Visual Studio generates asynchronous action methods for all actions that involve access to the Person data context.</span></span> <span data-ttu-id="094a2-263">요청이 처리 되는 동안 웹 서버에서 작업을 수행 하지 못하도록 차단 하지 않도록 장기 실행 CPU 바운드 요청에 대해 비동기 작업 메서드를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-263">It is recommended that you use asynchronous action methods for long-running, non-CPU bound requests to avoid blocking the Web server from performing work while the request is being processed.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="094a2-264">작업 3 – 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="094a2-264">Task 3 – Running the Solution</span></span>

<span data-ttu-id="094a2-265">이 작업에서는 솔루션을 다시 실행 하 여 **사용자** 의 뷰가 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-265">In this task, you will run the solution again to verify that the views for **Person** are working as expected.</span></span> <span data-ttu-id="094a2-266">새 사용자를 추가 하 여 데이터베이스에 성공적으로 저장 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-266">You will add a new person to verify that it is successfully saved to the database.</span></span>

1. <span data-ttu-id="094a2-267">**F5** 키를 눌러 솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-267">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="094a2-268">**/MvcPerson**로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-268">Navigate to **/MvcPerson**.</span></span> <span data-ttu-id="094a2-269">사용자 목록이 표시 되는 스 캐 폴드 뷰가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-269">The scaffolded view that shows the list of people should appear.</span></span>
3. <span data-ttu-id="094a2-270">새 사용자를 추가 하려면 **새로 만들기** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-270">Click **Create New** to add a new person.</span></span>

    ![스 캐 폴드 MVC 뷰로 이동](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    <span data-ttu-id="094a2-272">*스 캐 폴드 MVC 뷰로 이동*</span><span class="sxs-lookup"><span data-stu-id="094a2-272">*Navigating to the scaffolded MVC views*</span></span>
4. <span data-ttu-id="094a2-273">**만들기** 보기에서 사용자의 **이름과** **나** 이를 입력 하 고 **만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-273">In the **Create** view, provide a **Name** and an **Age** for the person, and click **Create**.</span></span>

    ![새 사용자 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    <span data-ttu-id="094a2-275">*새 사용자 추가*</span><span class="sxs-lookup"><span data-stu-id="094a2-275">*Adding a new person*</span></span>
5. <span data-ttu-id="094a2-276">새 사용자가 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-276">The new person is added to the list.</span></span> <span data-ttu-id="094a2-277">요소 목록에서 **세부** 정보를 클릭 하 여 사용자의 세부 정보 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-277">In the element list, click **Details** to display the person's details view.</span></span> <span data-ttu-id="094a2-278">그런 다음 **자세히** 보기에서 **목록으로** 돌아가기를 클릭 하 여 목록 보기로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-278">Then, in the **Details** view, click **Back to List** to go back to the list view.</span></span>

    ![사용자의 세부 정보 보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    <span data-ttu-id="094a2-280">*사용자의 세부 정보 보기*</span><span class="sxs-lookup"><span data-stu-id="094a2-280">*Person's details view*</span></span>
6. <span data-ttu-id="094a2-281">사용자를 삭제 하려면 **삭제** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-281">Click the **Delete** link to delete the person.</span></span> <span data-ttu-id="094a2-282">**삭제** 보기에서 **삭제** 를 클릭 하 여 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-282">In the **Delete** view, click **Delete** to confirm the operation.</span></span>

    ![사람 삭제](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    <span data-ttu-id="094a2-284">*사람 삭제*</span><span class="sxs-lookup"><span data-stu-id="094a2-284">*Deleting a person*</span></span>
7. <span data-ttu-id="094a2-285">Visual Studio로 돌아가서 **SHIFT + f5** 키를 눌러 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a><span data-ttu-id="094a2-286">연습 3: 스 캐 폴딩을 사용 하 여 Web API 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-286">Exercise 3: Creating a Web API Controller Using Scaffolding</span></span>

<span data-ttu-id="094a2-287">Web API 프레임 워크는 ASP.NET 스택의 일부 이며 일반적으로 RESTful API를 통해 JSON 또는 XML 형식의 데이터를 보내고 받는 HTTP 서비스를 보다 쉽게 구현할 수 있도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-287">The Web API framework is part of the ASP.NET Stack and designed to make implementing HTTP services easier, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span>

<span data-ttu-id="094a2-288">이 연습에서는 ASP.NET 스 캐 폴딩을 다시 사용 하 여 Web API 컨트롤러를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-288">In this exercise, you will use ASP.NET Scaffolding again to generate a Web API controller.</span></span> <span data-ttu-id="094a2-289">이전 연습에서 동일한 **person** 및 **PersonContext** 클래스를 사용 하 여 JSON 형식의 동일한 사람 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-289">You will use the same **Person** and **PersonContext** classes from the previous exercise to provide the same person data in JSON format.</span></span> <span data-ttu-id="094a2-290">동일한 ASP.NET 응용 프로그램 내에서 여러 가지 방법으로 동일한 리소스를 노출 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-290">You will see how you can expose the same resources in different ways within the same ASP.NET application.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a><span data-ttu-id="094a2-291">작업 1-Web API 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="094a2-291">Task 1 – Creating a Web API Controller</span></span>

<span data-ttu-id="094a2-292">이 작업에서는 JSON과 같은 컴퓨터를 사용할 수 있는 형식으로 개인 데이터를 노출 하는 새 **WEB API 컨트롤러** 를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-292">In this task you will create a new **Web API Controller** that will expose the person data in a machine-consumable format like JSON.</span></span>

1. <span data-ttu-id="094a2-293">아직 열지 않은 경우 **웹에 대해 Visual Studio Express 2013** 을 열고 **Source/Ex3-WebAPI/Begin** 폴더에 있는 **MyHybridSite** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-293">If not already opened, open **Visual Studio Express 2013 for Web** and open the **MyHybridSite.sln** solution located in the **Source/Ex3-WebAPI/Begin** folder.</span></span> <span data-ttu-id="094a2-294">또는 이전 연습에서 얻은 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-294">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>

    > [!NOTE]
    > <span data-ttu-id="094a2-295">연습 3에서 시작 솔루션으로 시작 하는 경우 **ctrl + SHIFT + B** 를 눌러 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-295">If you start with the Begin solution from Exercise 3, press **CTRL + SHIFT + B** to build the solution.</span></span>
2. <span data-ttu-id="094a2-296">**솔루션 탐색기**에서 **MyHybridSite** 프로젝트의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 스 캐 폴드 항목**....</span><span class="sxs-lookup"><span data-stu-id="094a2-296">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![새 스 캐 폴드 컨트롤러 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    <span data-ttu-id="094a2-298">*새 스 캐 폴드 컨트롤러 만들기*</span><span class="sxs-lookup"><span data-stu-id="094a2-298">*Creating a new scaffolded Controller*</span></span>
3. <span data-ttu-id="094a2-299">**스 캐 폴드 추가** 대화 상자의 왼쪽 창에서 **web api** 를 선택한 다음 가운데 창에서 **Entity Framework를 사용 하 여 동작을 포함 하는 web api 2 컨트롤러** 를 선택 하 고 추가를 클릭 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="094a2-299">In the **Add Scaffold** dialog box, select **Web API** in the left pane, then **Web API 2 Controller with actions, using Entity Framework** in the middle pane and then click **Add.**</span></span>

    <span data-ttu-id="094a2-300">![작업 및 Entity Framework 웹 API 2 컨트롤러 선택](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "작업 및 Entity Framework 웹 API 2 컨트롤러 선택")</span><span class="sxs-lookup"><span data-stu-id="094a2-300">![Selecting Web API 2 Controller with actions and Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Selecting Web API 2 Controller with actions and Entity Framework")</span></span>

    <span data-ttu-id="094a2-301">*작업 및 Entity Framework 웹 API 2 컨트롤러 선택*</span><span class="sxs-lookup"><span data-stu-id="094a2-301">*Selecting Web API 2 Controller with actions and Entity Framework*</span></span>
4. <span data-ttu-id="094a2-302">*ApiPersonController* 을 **컨트롤러 이름**으로 설정 하 고, **비동기 컨트롤러 작업 사용** 옵션을 선택 하 고, **모델** 및 **데이터 컨텍스트** 클래스로 각각 **Person (MyHybridSite)** 및 **PersonContext (MyHybridSite)** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-302">Set *ApiPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** and **PersonContext (MyHybridSite.Models)** as the **Model** and **Data context** classes respectively.</span></span> <span data-ttu-id="094a2-303">그런 다음, **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-303">Then click **Add**.</span></span>

    <span data-ttu-id="094a2-304">![스 캐 폴딩을 사용 하 여 Web API 컨트롤러 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "스 캐 폴딩을 사용 하 여 Web API 컨트롤러 추가")</span><span class="sxs-lookup"><span data-stu-id="094a2-304">![Adding a Web API Controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Adding a Web API controller with scaffolding")</span></span>

    <span data-ttu-id="094a2-305">*스 캐 폴딩을 사용 하 여 Web API 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="094a2-305">*Adding a Web API controller with scaffolding*</span></span>
5. <span data-ttu-id="094a2-306">그러면 Visual Studio에서 데이터를 사용할 수 있도록 네 가지 CRUD 작업을 사용 하 여 **ApiPersonController** 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-306">Visual Studio will then generate the **ApiPersonController** class with the four CRUD actions to work with your data.</span></span>

    <span data-ttu-id="094a2-307">![스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 만든 후](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 만든 후")</span><span class="sxs-lookup"><span data-stu-id="094a2-307">![After creating the Web API controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "After creating the Web API controller with scaffolding")</span></span>

    <span data-ttu-id="094a2-308">*스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 만든 후*</span><span class="sxs-lookup"><span data-stu-id="094a2-308">*After creating the Web API controller with scaffolding*</span></span>
6. <span data-ttu-id="094a2-309">**ApiPersonController.cs** 파일을 열고 *getpeople* 작업 메서드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-309">Open the **ApiPersonController.cs** file and inspect the *GetPeople* action method.</span></span> <span data-ttu-id="094a2-310">이 메서드는 사용자 데이터를 가져오기 위해 **PersonContext** 형식의 db 필드를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-310">This method queries the db field of **PersonContext** type in order to get the people data.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. <span data-ttu-id="094a2-311">이제 메서드 정의 위의 주석을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-311">Now notice the comment above the method definition.</span></span> <span data-ttu-id="094a2-312">다음 작업에서 사용할이 작업을 노출 하는 URI를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-312">It provides the URI that exposes this action which you will use in the next task.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="094a2-313">기본적으로 Web API는 */api* 경로에 대 한 쿼리를 catch 하 여 MVC 컨트롤러와의 충돌을 방지 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-313">By default, Web API is configured to catch the queries to the */api* path to avoid collisions with MVC controllers.</span></span> <span data-ttu-id="094a2-314">이 설정을 변경 해야 하는 경우 [ASP.NET Web API에서 라우팅](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="094a2-314">If you need to change this setting, refer to [Routing in ASP.NET Web API](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="094a2-315">작업 2-솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="094a2-315">Task 2 – Running the Solution</span></span>

<span data-ttu-id="094a2-316">이 작업에서는 Internet Explorer **F12 개발자 도구** 를 사용 하 여 Web API 컨트롤러에서 전체 응답을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-316">In this task you will use the Internet Explorer **F12 developer tools** to inspect the full response from the Web API controller.</span></span> <span data-ttu-id="094a2-317">응용 프로그램 데이터에 대 한 자세한 정보를 얻기 위해 네트워크 트래픽을 캡처하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-317">You will see how you can capture network traffic to get more insight into your application data.</span></span>

> [!NOTE]
> <span data-ttu-id="094a2-318">Visual Studio 도구 모음에 있는 **시작** 단추에 **Internet Explorer** 가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-318">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer 옵션](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> <span data-ttu-id="094a2-320">**F12 개발자 도구** 에는이 실습 실습에서 다루지 않는 다양 한 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-320">The **F12 developer tools** have a wide set of functionality that is not covered in this hands-on-lab.</span></span> <span data-ttu-id="094a2-321">자세히 알아보려면 [F12 개발자 도구 사용](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="094a2-321">If you want to learn more about it, refer to [Using the F12 developer tools](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).</span></span>

1. <span data-ttu-id="094a2-322">**F5** 키를 눌러 솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-322">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="094a2-323">이 작업을 올바르게 수행 하려면 응용 프로그램에 데이터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-323">In order to follow this task correctly, your application needs to have data.</span></span> <span data-ttu-id="094a2-324">데이터베이스가 비어 있는 경우 실습 2의 작업 3으로 돌아가서 MVC 뷰를 사용 하 여 새 사용자를 만드는 방법에 대 한 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-324">If your database is empty, you can go back to Task 3 in Exercise 2 and follow the steps on how to create a new person using the MVC views.</span></span>
2. <span data-ttu-id="094a2-325">브라우저에서 **F12** 키를 눌러 **개발자 도구** 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-325">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="094a2-326">**Ctrl** + **4** 를 누르거나 **네트워크** 아이콘을 클릭 한 다음 녹색 화살표 단추를 클릭 하 여 네트워크 트래픽 캡처를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-326">Press **CTRL** + **4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="094a2-327">![Web API 네트워크 캡처 시작](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Web API 네트워크 캡처 시작")</span><span class="sxs-lookup"><span data-stu-id="094a2-327">![Initiating Web API network capture](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="094a2-328">*Web API 네트워크 캡처 시작*</span><span class="sxs-lookup"><span data-stu-id="094a2-328">*Initiating Web API network capture*</span></span>
3. <span data-ttu-id="094a2-329">브라우저의 주소 표시줄에서 URL에 **api/ApiPerson** 을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-329">Append **api/ApiPerson** to the URL in the browser's address bar.</span></span> <span data-ttu-id="094a2-330">이제 **ApiPersonController**응답의 세부 정보를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-330">You will now inspect the details of the response from the **ApiPersonController**.</span></span>

    <span data-ttu-id="094a2-331">![Web API를 통해 개인 데이터 검색](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Web API를 통해 개인 데이터 검색")</span><span class="sxs-lookup"><span data-stu-id="094a2-331">![Retrieving person data through Web API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Retrieving person data through Web API")</span></span>

    <span data-ttu-id="094a2-332">*Web API를 통해 개인 데이터 검색*</span><span class="sxs-lookup"><span data-stu-id="094a2-332">*Retrieving person data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="094a2-333">다운로드가 완료 되 면 다운로드 한 파일을 사용 하 여 작업을 수행 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-333">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="094a2-334">개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있으려면 대화 상자를 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-334">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
4. <span data-ttu-id="094a2-335">이제 응답의 본문을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-335">Now you will inspect the body of the response.</span></span> <span data-ttu-id="094a2-336">이렇게 하려면 **세부 정보** 탭을 클릭 한 다음 **응답 본문**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-336">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="094a2-337">다운로드 한 데이터가 **Person** 클래스에 해당 하는 속성 **Id**, **이름** 및 **기간** 을 가진 개체 목록 인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-337">You can check that the downloaded data is a list of objects with the properties **Id**, **Name** and **Age** that correspond to the **Person** class.</span></span>

    <span data-ttu-id="094a2-338">![Web API 응답 본문 보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Web API 응답 본문 보기")</span><span class="sxs-lookup"><span data-stu-id="094a2-338">![Viewing Web API Response Body](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Viewing Web API Response Body")</span></span>

    <span data-ttu-id="094a2-339">*Web API 응답 본문 보기*</span><span class="sxs-lookup"><span data-stu-id="094a2-339">*Viewing Web API Response Body*</span></span>

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a><span data-ttu-id="094a2-340">작업 3 – Web API 도움말 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="094a2-340">Task 3 – Adding Web API Help Pages</span></span>

<span data-ttu-id="094a2-341">Web API를 만들 때 다른 개발자가 API를 호출 하는 방법을 알 수 있도록 도움말 페이지를 만드는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-341">When you create a Web API, it is useful to create a help page so that other developers will know how to call your API.</span></span> <span data-ttu-id="094a2-342">설명서 페이지를 수동으로 만들고 업데이트할 수 있지만 유지 관리 작업을 수행 하지 않도록 하기 위해 자동으로 생성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-342">You could create and update the documentation pages manually, but it is better to auto-generate them to avoid having to do maintenance work.</span></span> <span data-ttu-id="094a2-343">이 작업에서는 Nuget 패키지를 사용 하 여 웹 API 도움말 페이지를 솔루션에 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-343">In this task you will use a Nuget package to automatically generate Web API help pages to the solution.</span></span>

1. <span data-ttu-id="094a2-344">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-344">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="094a2-345">**패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-345">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > <span data-ttu-id="094a2-346">**WebApi** 패키지는 필요한 어셈블리를 설치 하 고 **영역/도움말 페이지** 폴더 아래에 도움말 페이지에 대 한 MVC 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-346">The **Microsoft.AspNet.WebApi.HelpPage** package installs the necessary assemblies and adds MVC Views for the help pages under the **Areas/HelpPage** folder.</span></span>

    <span data-ttu-id="094a2-347">![HelpPage 영역](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 영역")</span><span class="sxs-lookup"><span data-stu-id="094a2-347">![HelpPage Area](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage Area")</span></span>

    <span data-ttu-id="094a2-348">*HelpPage 영역*</span><span class="sxs-lookup"><span data-stu-id="094a2-348">*HelpPage Area*</span></span>
3. <span data-ttu-id="094a2-349">기본적으로 도움말 페이지에는 설명서에 대 한 자리 표시자 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-349">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="094a2-350">XML 문서 주석을 사용 하 여 설명서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-350">You can use XML documentation comments to create the documentation.</span></span> <span data-ttu-id="094a2-351">이 기능을 사용 하도록 설정 하려면 **영역/도움말 페이지/앱\_시작** 폴더에 있는 **HelpPageConfig.cs** 파일을 열고 다음 줄의 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-351">To enable this feature, open the **HelpPageConfig.cs** file located in the **Areas/HelpPage/App\_Start** folder and uncomment the following line:</span></span>

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. <span data-ttu-id="094a2-352">**솔루션 탐색기**에서 **MyHybridSite**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 선택한 다음 **빌드** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-352">In **Solution Explorer**, right-click the project **MyHybridSite**, select **Properties** and click the **Build** tab.</span></span>

    <span data-ttu-id="094a2-353">![빌드 탭](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "빌드 섹션")</span><span class="sxs-lookup"><span data-stu-id="094a2-353">![Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Build section")</span></span>

    <span data-ttu-id="094a2-354">*빌드 탭*</span><span class="sxs-lookup"><span data-stu-id="094a2-354">*Build tab*</span></span>
5. <span data-ttu-id="094a2-355">**출력**에서 **XML 문서 파일**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-355">Under **Output**, select **XML documentation file**.</span></span> <span data-ttu-id="094a2-356">편집 상자에 **App\_Data/XmlDocument**를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-356">In the edit box, type **App\_Data/XmlDocument.xml**.</span></span>

    <span data-ttu-id="094a2-357">![빌드 탭의 출력 섹션](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "빌드 탭의 출력 섹션")</span><span class="sxs-lookup"><span data-stu-id="094a2-357">![Output section in Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Output section in build tab")</span></span>

    <span data-ttu-id="094a2-358">*빌드 탭의 출력 섹션*</span><span class="sxs-lookup"><span data-stu-id="094a2-358">*Output section in Build tab*</span></span>
6. <span data-ttu-id="094a2-359">**Ctrl** + **S** 키를 눌러 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-359">Press **CTRL** + **S** to save the changes.</span></span>
7. <span data-ttu-id="094a2-360">**Controllers** 폴더에서 **ApiPersonController.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-360">Open the **ApiPersonController.cs** file from the **Controllers** folder.</span></span>
8. <span data-ttu-id="094a2-361">*Getpeople* 메서드 시그니처와 *//GET api/apiperson* 설명 사이에 새 줄을 입력 하 고 세 개의 슬래시를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-361">Enter a new line between the *GetPeople* method signature and the *// GET api/ApiPerson* comment, and then type three forward slashes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="094a2-362">Visual Studio는 메서드 설명서를 정의 하는 XML 요소를 자동으로 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-362">Visual Studio automatically inserts the XML elements which define the method documentation.</span></span>
9. <span data-ttu-id="094a2-363">*Getpeople* 메서드에 대 한 요약 텍스트 및 반환 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-363">Add a summary text and the return value for the *GetPeople* method.</span></span> <span data-ttu-id="094a2-364">다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-364">It should look like the following.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. <span data-ttu-id="094a2-365">**F5** 키를 눌러 솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-365">Press **F5** to run the solution.</span></span>
11. <span data-ttu-id="094a2-366">주소 표시줄의 URL에 **/help** 를 추가 하 여 도움말 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-366">Append **/help** to the URL in the address bar to browse to the help page.</span></span>

    <span data-ttu-id="094a2-367">![ASP.NET Web API 도움말 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API 도움말 페이지")</span><span class="sxs-lookup"><span data-stu-id="094a2-367">![ASP.NET Web API Help Page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API Help Page")</span></span>

    <span data-ttu-id="094a2-368">*ASP.NET Web API 도움말 페이지*</span><span class="sxs-lookup"><span data-stu-id="094a2-368">*ASP.NET Web API Help Page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="094a2-369">페이지의 기본 콘텐츠는 컨트롤러 별로 그룹화 된 Api의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-369">The main content of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="094a2-370">Table 항목은 **Iapiexplorer** 인터페이스를 사용 하 여 동적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-370">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="094a2-371">API 컨트롤러를 추가 하거나 업데이트 하는 경우 다음에 응용 프로그램을 빌드할 때 테이블이 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-371">If you add or update an API controller, the table will be automatically updated the next time you build the application.</span></span>
    > 
    > <span data-ttu-id="094a2-372">**API** 열에는 HTTP 메서드 및 상대 URI가 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-372">The **API** column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="094a2-373">**설명** 열에는 메서드의 설명서에서 추출 된 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-373">The **Description** column contains information that has been extracted from the method's documentation.</span></span>
12. <span data-ttu-id="094a2-374">메서드 정의 위에 추가한 설명이 설명 열에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-374">Note that the description you added above the method definition is displayed in the description column.</span></span>

    <span data-ttu-id="094a2-375">![API 메서드 설명](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API 메서드 설명")</span><span class="sxs-lookup"><span data-stu-id="094a2-375">![API method description](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API method description")</span></span>

    <span data-ttu-id="094a2-376">*API 메서드 설명*</span><span class="sxs-lookup"><span data-stu-id="094a2-376">*API method description*</span></span>
13. <span data-ttu-id="094a2-377">API 메서드 중 하나를 클릭 하 여 샘플 응답 본문을 포함 하 여 더 자세한 정보가 포함 된 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-377">Click one of the API methods to navigate to a page with more detailed information, including sample response bodies.</span></span>

    <span data-ttu-id="094a2-378">![세부 정보 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "세부 정보 페이지")</span><span class="sxs-lookup"><span data-stu-id="094a2-378">![Detail Information page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Detail Information page")</span></span>

    <span data-ttu-id="094a2-379">*세부 정보 페이지*</span><span class="sxs-lookup"><span data-stu-id="094a2-379">*Detailed information page*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="094a2-380">요약</span><span class="sxs-lookup"><span data-stu-id="094a2-380">Summary</span></span>

<span data-ttu-id="094a2-381">이 실습 실습을 완료 하면 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-381">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="094a2-382">Visual Studio 2013에서 하나의 ASP.NET 환경을 사용 하 여 새 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="094a2-382">Create a new Web application using the One ASP.NET Experience in Visual Studio 2013</span></span>
- <span data-ttu-id="094a2-383">여러 ASP.NET 기술을 하나의 단일 프로젝트로 통합</span><span class="sxs-lookup"><span data-stu-id="094a2-383">Integrate multiple ASP.NET technologies into one single project</span></span>
- <span data-ttu-id="094a2-384">ASP.NET 스 캐 폴딩을 사용 하 여 모델 클래스에서 MVC 컨트롤러 및 뷰 생성</span><span class="sxs-lookup"><span data-stu-id="094a2-384">Generate MVC controllers and views from your model classes using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="094a2-385">비동기 프로그래밍 및 데이터 액세스와 같은 기능을 사용 하는 웹 API 컨트롤러를 생성 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="094a2-385">Generate Web API controllers, which use features such as Async Programming and data access through Entity Framework</span></span>
- <span data-ttu-id="094a2-386">컨트롤러에 대 한 Web API 도움말 페이지를 자동으로 생성</span><span class="sxs-lookup"><span data-stu-id="094a2-386">Automatically generate Web API Help Pages for your controllers</span></span>
