---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: '실습: ASP.NET Web API 및 node.js-ASP.NET 4.x를 사용 하 여 SPA (단일 페이지 응용 프로그램) 빌드'
author: rick-anderson
description: '단계별 코드: ASP.NET 4.x의 ASP.NET Web API 및 node.js를 사용 하 여 SPA (단일 페이지 응용 프로그램)를 빌드합니다.'
ms.author: riande
ms.date: 09/30/2015
ms.custom: seoapril2019
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 86833a890da759e489dd11dc9afb128a9b7a75e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448763"
---
# <a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a><span data-ttu-id="89a4a-103">실습: ASP.NET Web API 및 node.js를 사용 하 여 단일 페이지 응용 프로그램 (SPA) 빌드</span><span class="sxs-lookup"><span data-stu-id="89a4a-103">Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js</span></span>

<span data-ttu-id="89a4a-104">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="89a4a-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="89a4a-105">웹 캠프 교육 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="89a4a-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="89a4a-106">이 랩에서는 ASP.NET 4.x의 ASP.NET Web API 및 node.js를 사용 하 여 SPA (단일 페이지 응용 프로그램)를 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-106">This hands on lab shows you how to build a Single Page Application (SPA) with ASP.NET Web API and Angular.js for ASP.NET 4.x.</span></span>

<span data-ttu-id="89a4a-107">이 실습에서는 이러한 기술을 활용 하 여 SPA 개념을 기반으로 하는 기타 정보 웹 사이트인 Geek of 퀴즈를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-107">In this hand-on lab, you will take advantage of those technologies to implement Geek Quiz, a trivia website based on the SPA concept.</span></span> <span data-ttu-id="89a4a-108">먼저 ASP.NET Web API를 사용 하 여 서비스 계층을 구현 하 여 퀴즈 질문을 검색 하는 데 필요한 끝점을 노출 하 고 답변을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-108">You will first implement the service layer with ASP.NET Web API to expose the required endpoints to retrieve the quiz questions and store the answers.</span></span> <span data-ttu-id="89a4a-109">그런 다음 AngularJS 및 CSS3 변환 효과를 사용 하 여 풍부 하 고 응답성이 뛰어난 UI를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-109">Then, you will build a rich and responsive UI using AngularJS and CSS3 transformation effects.</span></span>

<span data-ttu-id="89a4a-110">기존 웹 응용 프로그램에서 클라이언트 (브라우저)는 페이지를 요청 하 여 서버와 통신을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-110">In traditional web applications, the client (browser) initiates the communication with the server by requesting a page.</span></span> <span data-ttu-id="89a4a-111">그러면 서버에서 요청을 처리 하 고 페이지의 HTML을 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-111">The server then processes the request and sends the HTML of the page to the client.</span></span> <span data-ttu-id="89a4a-112">이후 페이지와의 상호 작용에서 (예: 사용자가 링크로 이동 하거나 데이터를 사용 하 여 양식을 전송 – 새 요청이 서버에 전송 되 고 흐름이 다시 시작 됩니다. 서버는 요청을 처리 하 고 새 작업 요청에 대 한 응답으로 새 페이지를 브라우저로 보냅니다. 클라이언트에서 ed</span><span class="sxs-lookup"><span data-stu-id="89a4a-112">In subsequent interactions with the page –e.g. the user navigates to a link or submits a form with data– a new request is sent to the server, and the flow starts again: the server processes the request and sends a new page to the browser in response to the new action requested by the client.</span></span>
> 
> <span data-ttu-id="89a4a-113">SPAs (단일 페이지 응용 프로그램)에서는 초기 요청이 발생 한 후 전체 페이지가 브라우저에 로드 되지만 이후 상호 작용은 Ajax 요청을 통해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-113">In Single-Page Applications (SPAs) the entire page is loaded in the browser after the initial request, but subsequent interactions take place through Ajax requests.</span></span> <span data-ttu-id="89a4a-114">즉, 브라우저에서 변경 된 페이지 부분만 업데이트 해야 합니다. 전체 페이지를 다시 로드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-114">This means that the browser has to update only the portion of the page that has changed; there is no need to reload the entire page.</span></span> <span data-ttu-id="89a4a-115">SPA 접근 방식을 사용 하면 응용 프로그램에서 사용자 작업에 응답 하는 데 걸리는 시간이 줄어들고,이로 인해 보다 유체 있는 환경이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-115">The SPA approach reduces the time taken by the application to respond to user actions, resulting in a more fluid experience.</span></span>
> 
> <span data-ttu-id="89a4a-116">SPA의 아키텍처는 기존 웹 응용 프로그램에 존재 하지 않는 특정 문제를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-116">The architecture of a SPA involves certain challenges that are not present in traditional web applications.</span></span> <span data-ttu-id="89a4a-117">그러나 ASP.NET Web API, AngularJS와 같은 JavaScript 프레임 워크, CSS3에서 제공 하는 새로운 스타일 기능 등의 새로운 기술을 통해 매우 쉽게 디자인 하 고 SPAs를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-117">However, emerging technologies like ASP.NET Web API, JavaScript frameworks like AngularJS and new styling features provided by CSS3 make it really easy to design and build SPAs.</span></span>
> 
> 
> <span data-ttu-id="89a4a-118">모든 샘플 코드와 코드 조각은 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-118">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>

## <a name="overview"></a><span data-ttu-id="89a4a-119">개요</span><span class="sxs-lookup"><span data-stu-id="89a4a-119">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="89a4a-120">목표</span><span class="sxs-lookup"><span data-stu-id="89a4a-120">Objectives</span></span>

<span data-ttu-id="89a4a-121">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-121">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="89a4a-122">JSON 데이터를 보내고 받을 ASP.NET Web API 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-122">Create an ASP.NET Web API service to send and receive JSON data</span></span>
- <span data-ttu-id="89a4a-123">AngularJS를 사용 하 여 반응 형 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-123">Create a responsive UI using AngularJS</span></span>
- <span data-ttu-id="89a4a-124">CSS3 변환을 사용 하 여 UI 환경 향상</span><span class="sxs-lookup"><span data-stu-id="89a4a-124">Enhance the UI experience with CSS3 transformations</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="89a4a-125">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="89a4a-125">Prerequisites</span></span>

<span data-ttu-id="89a4a-126">이 실습 실습을 완료 하려면 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-126">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="89a4a-127">[웹 이상의 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="89a4a-127">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="89a4a-128">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="89a4a-128">Setup</span></span>

<span data-ttu-id="89a4a-129">이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="89a4a-130">Windows 탐색기를 열고 랩의 **원본** 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-130">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="89a4a-131">**Setup.exe** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행** 을 선택 하 여 환경을 구성 하는 설치 프로세스를 시작 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-131">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="89a4a-132">사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="89a4a-133">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 확인 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="89a4a-134">코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="89a4a-134">Using the Code Snippets</span></span>

<span data-ttu-id="89a4a-135">랩 문서 전체에서 코드 블록을 삽입 하 라는 지침이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="89a4a-136">사용자 편의를 위해이 코드의 대부분은 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio Code 코드 조각으로 제공 되며,이를 수동으로 추가 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="89a4a-137">각 연습에는 각 연습을 서로 독립적으로 수행할 수 있는 연습 **시작** 폴더에 있는 시작 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="89a4a-138">연습 중에 추가 된 코드 조각은 이러한 시작 솔루션에서 누락 되었으며, 연습을 완료할 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="89a4a-139">연습에 대 한 소스 코드 내에서 해당 연습의 단계를 완료 하 여 생성 된 코드를 포함 하는 Visual Studio 솔루션을 포함 하는 **끝** 폴더를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="89a4a-140">이 실습 랩을 통해 작업할 때 추가 도움이 필요한 경우 이러한 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="89a4a-141">실습</span><span class="sxs-lookup"><span data-stu-id="89a4a-141">Exercises</span></span>

<span data-ttu-id="89a4a-142">이 실습 랩에는 다음 연습이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="89a4a-143">Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-143">Creating a Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="89a4a-144">SPA 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-144">Creating a SPA Interface</span></span>](#Exercise2)

<span data-ttu-id="89a4a-145">이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="89a4a-145">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="89a4a-146">Visual Studio를 처음 시작 하는 경우 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-146">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="89a4a-147">미리 정의 된 각 컬렉션은 특정 개발 스타일에 맞게 디자인 되 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-147">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="89a4a-148">이 실습의 절차에서는 **일반 개발 설정** 컬렉션을 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-148">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="89a4a-149">개발 환경에 대해 다른 설정 컬렉션을 선택 하는 경우 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-149">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a><span data-ttu-id="89a4a-150">연습 1: Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-150">Exercise 1: Creating a Web API</span></span>

<span data-ttu-id="89a4a-151">SPA의 주요 부분 중 하나는 서비스 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-151">One of the key parts of a SPA is the service layer.</span></span> <span data-ttu-id="89a4a-152">UI에서 보낸 Ajax 호출을 처리 하 고 해당 호출에 대 한 응답으로 데이터를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-152">It is responsible for processing the Ajax calls sent by the UI and returning data in response to that call.</span></span> <span data-ttu-id="89a4a-153">검색 된 데이터는 클라이언트에서 구문 분석 되 고 사용 하기 위해 컴퓨터에서 읽을 수 있는 형식으로 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-153">The data retrieved should be presented in a machine-readable format in order to be parsed and consumed by the client.</span></span>

<span data-ttu-id="89a4a-154">Web API 프레임 워크는 ASP.NET 스택의 일부 이며 일반적으로 RESTful API를 통해 JSON 또는 XML 형식의 데이터를 보내고 받는 HTTP 서비스를 쉽게 구현할 수 있도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-154">The Web API framework is part of the ASP.NET Stack and is designed to make it easy to implement HTTP services, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span> <span data-ttu-id="89a4a-155">이 연습에서는 Geek of 퀴즈 응용 프로그램을 호스트 하는 웹 사이트를 만든 다음, ASP.NET Web API를 사용 하 여 퀴즈 데이터를 노출 하 고 유지 하기 위해 백 엔드 서비스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-155">In this exercise you will create the Web site to host the Geek Quiz application and then implement the back-end service to expose and persist the quiz data using ASP.NET Web API.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a><span data-ttu-id="89a4a-156">작업 1-Geek of 퀴즈를 위한 초기 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-156">Task 1 – Creating the Initial Project for Geek Quiz</span></span>

<span data-ttu-id="89a4a-157">이 작업에서는 Visual Studio와 함께 제공 되는 **One ASP.NET** 프로젝트 형식에 따라 ASP.NET Web API를 지 원하는 새 ASP.NET MVC 프로젝트 만들기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-157">In this task you will start creating a new ASP.NET MVC project with support for ASP.NET Web API based on the **One ASP.NET** project type that comes with Visual Studio.</span></span> <span data-ttu-id="89a4a-158">**한 ASP.NET** 는 모든 ASP.NET 기술을 통합 하 고 원하는 대로 혼합 하 고 일치 시킬 수 있는 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-158">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="89a4a-159">그런 다음 Entity Framework의 모델 클래스와 데이터베이스 이니셜라이저를 추가 하 여 퀴즈 질문을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-159">You will then add the Entity Framework's model classes and the database initializer to insert the quiz questions.</span></span>

1. <span data-ttu-id="89a4a-160">**웹에 대해 Visual Studio Express 2013** 을 열고 파일을 선택 합니다. **| 새 프로젝트** ... 새 솔루션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-160">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    <span data-ttu-id="89a4a-161">![새 프로젝트 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "새 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="89a4a-161">![Creating a New Project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "Creating a New Project")</span></span>

    <span data-ttu-id="89a4a-162">*새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="89a4a-162">*Creating a New Project*</span></span>
2. <span data-ttu-id="89a4a-163">**새 프로젝트** 대화 상자의 시각적 개체  **C# 에서 ASP.NET 웹 응용 프로그램을 선택 합니다. 웹** 탭. **.NET Framework 4.5** 을 선택 했는지 확인 하 고 이름을 *GeekQuiz*로 지정 하 고 **위치** 를 선택한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-163">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab. Make sure **.NET Framework 4.5** is selected, name it *GeekQuiz*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="89a4a-164">![새 ASP.NET 웹 응용 프로그램 프로젝트 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "새 ASP.NET 웹 응용 프로그램 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="89a4a-164">![Creating a new ASP.NET Web Application project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "Creating a new ASP.NET Web Application project")</span></span>

    <span data-ttu-id="89a4a-165">*새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="89a4a-165">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="89a4a-166">**새 ASP.NET 프로젝트** 대화 상자에서 **MVC** 템플릿을 선택 하 고 **Web API** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-166">In the **New ASP.NET Project** dialog box, select the **MVC** template and select the **Web API** option.</span></span> <span data-ttu-id="89a4a-167">또한 **인증** 옵션이 **개별 사용자 계정**으로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-167">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="89a4a-168">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-168">Click **OK** to continue.</span></span>

    ![Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    <span data-ttu-id="89a4a-170">*Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="89a4a-170">*Creating a new project with the MVC template, including Web API components*</span></span>
4. <span data-ttu-id="89a4a-171">**솔루션 탐색기**에서 **GeekQuiz** 프로젝트의 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 기존 항목**...</span><span class="sxs-lookup"><span data-stu-id="89a4a-171">In **Solution Explorer**, right-click the **Models** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="89a4a-172">![기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "기존 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="89a4a-172">![Adding an existing item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "Adding an existing item")</span></span>

    <span data-ttu-id="89a4a-173">*기존 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="89a4a-173">*Adding an existing item*</span></span>
5. <span data-ttu-id="89a4a-174">**기존 항목 추가** 대화 상자에서 **원본/자산/모델** 폴더로 이동 하 여 모든 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-174">In the **Add Existing Item** dialog box, navigate to the **Source/Assets/Models** folder and select all the files.</span></span> <span data-ttu-id="89a4a-175">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-175">Click **Add**.</span></span>

    <span data-ttu-id="89a4a-176">![모델 자산 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "모델 자산 추가")</span><span class="sxs-lookup"><span data-stu-id="89a4a-176">![Adding the model assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "Adding the model assets")</span></span>

    <span data-ttu-id="89a4a-177">*모델 자산 추가*</span><span class="sxs-lookup"><span data-stu-id="89a4a-177">*Adding the model assets*</span></span>

    > [!NOTE]
    > <span data-ttu-id="89a4a-178">이러한 파일을 추가 하면 Geek of 퀴즈 응용 프로그램에 대 한 데이터 모델, Entity Framework 데이터베이스 컨텍스트 및 데이터베이스 이니셜라이저가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-178">By adding these files, you are adding the data model, the Entity Framework's database context and the database initializer for the Geek Quiz application.</span></span>
    > 
    > <span data-ttu-id="89a4a-179">**EF (Entity Framework** )는 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있도록 하는 ORM (개체 관계형 매퍼)입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-179">**Entity Framework (EF)** is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span> <span data-ttu-id="89a4a-180">Entity Framework에 대 한 자세한 내용은 [여기](../../../entity-framework.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="89a4a-180">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>
    > 
    > <span data-ttu-id="89a4a-181">다음은 방금 추가한 클래스에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-181">The following is a description of the classes you just added:</span></span>
    > 
    > - <span data-ttu-id="89a4a-182">**Triviaoption:** 퀴즈 질문에 연결 된 단일 옵션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-182">**TriviaOption:** represents a single option associated with a quiz question</span></span>
    > - <span data-ttu-id="89a4a-183">**Triviaquestion:** 퀴즈 질문을 나타내고 **options** 속성을 통해 관련 옵션을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-183">**TriviaQuestion:** represents a quiz question and exposes the associated options through the **Options** property</span></span>
    > - <span data-ttu-id="89a4a-184">**Triviaanswer:** 퀴즈 질문에 대 한 응답으로 사용자가 선택한 옵션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-184">**TriviaAnswer:** represents the option selected by the user in response to a quiz question</span></span>
    > - <span data-ttu-id="89a4a-185">**TriviaContext:** geek of 퀴즈 응용 프로그램의 Entity Framework 데이터베이스 컨텍스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-185">**TriviaContext:** represents the Entity Framework's database context of the Geek Quiz application.</span></span> <span data-ttu-id="89a4a-186">이 클래스는 **Dcontext** 에서 파생 되며 위에서 설명한 엔터티의 컬렉션을 나타내는 **dbset** 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-186">This class derives from **DContext** and exposes **DbSet** properties that represent collections of the entities described above.</span></span>
    > - <span data-ttu-id="89a4a-187">**TriviaDatabaseInitializer:** **Createdatabaseifnotexists**에서 상속 되는 **TriviaContext** 클래스에 대 한 Entity Framework 이니셜라이저의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-187">**TriviaDatabaseInitializer:** the implementation of the Entity Framework initializer for the **TriviaContext** class which inherits from **CreateDatabaseIfNotExists**.</span></span> <span data-ttu-id="89a4a-188">이 클래스의 기본 동작은 **시드** 메서드에 지정 된 엔터티를 삽입 하는 데이터베이스가 없는 경우에만 데이터베이스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-188">The default behavior of this class is to create the database only if it does not exist, inserting the entities specified in the **Seed** method.</span></span>
6. <span data-ttu-id="89a4a-189">**Global.asax.cs** 파일을 열고 다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-189">Open the **Global.asax.cs** file and add the following using statement.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. <span data-ttu-id="89a4a-190">**응용 프로그램\_Start** 메서드의 시작 부분에 다음 코드를 추가 하 여 **TriviaDatabaseInitializer** 를 데이터베이스 이니셜라이저로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-190">Add the following code at the beginning of the **Application\_Start** method to set the **TriviaDatabaseInitializer** as the database initializer.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. <span data-ttu-id="89a4a-191">인증 된 사용자에 대 한 액세스를 제한 하도록 **홈** 컨트롤러를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-191">Modify the **Home** controller to restrict access to authenticated users.</span></span> <span data-ttu-id="89a4a-192">이렇게 하려면 **Controllers** 폴더에서 **HomeController.cs** 파일을 열고 **권한 부여** 특성을 **HomeController** 클래스 정의에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-192">To do this, open the **HomeController.cs** file inside the **Controllers** folder and add the **Authorize** attribute to the **HomeController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > <span data-ttu-id="89a4a-193">**권한 부여** 필터는 사용자가 인증 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-193">The **Authorize** filter checks to see if the user is authenticated.</span></span> <span data-ttu-id="89a4a-194">사용자가 인증 되지 않은 경우 작업을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-194">If the user is not authenticated, it returns HTTP status code 401 (Unauthorized) without invoking the action.</span></span> <span data-ttu-id="89a4a-195">전역, 컨트롤러 수준 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-195">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>
9. <span data-ttu-id="89a4a-196">이제 웹 페이지와 브랜딩의 레이아웃을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-196">You will now customize the layout of the web pages and the branding.</span></span> <span data-ttu-id="89a4a-197">이렇게 하려면 뷰 내에서 **\_Layout** 파일을 엽니다. *ASP.NET 응용 프로그램* 을 *geek of 퀴즈*로 바꿔서 **&lt;title&gt;** 요소의 콘텐츠를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-197">To do this, open the **\_Layout.cshtml** file inside the **Views | Shared** folder and update the content of the **&lt;title&gt;** element by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. <span data-ttu-id="89a4a-198">동일한 파일에서 *정보* 및 *연락처* 링크를 제거 하 고 *홈* 링크의 이름을 *Play*로 바꿔서 탐색 모음을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-198">In the same file, update the navigation bar by removing the *About* and *Contact* links and renaming the *Home* link to *Play*.</span></span> <span data-ttu-id="89a4a-199">또한 *응용 프로그램 이름* 링크의 이름을 *geek of 퀴즈*로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-199">Additionally, rename the *Application name* link to *Geek Quiz*.</span></span> <span data-ttu-id="89a4a-200">탐색 모음의 HTML은 다음 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-200">The HTML for the navigation bar should look like the following code.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. <span data-ttu-id="89a4a-201">*My ASP.NET Application* 을 *geek of 퀴즈*로 바꿔서 레이아웃 페이지의 바닥글을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-201">Update the footer of the layout page by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span> <span data-ttu-id="89a4a-202">이렇게 하려면 **&lt;바닥글&gt;** 요소의 내용을 다음 강조 표시 된 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-202">To do this, replace the content of the **&lt;footer&gt;** element with the following highlighted code.</span></span>

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a><span data-ttu-id="89a4a-203">작업 2 – TriviaController 웹 API 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-203">Task 2 – Creating the TriviaController Web API</span></span>

<span data-ttu-id="89a4a-204">이전 작업에서는 Geek of 퀴즈 웹 응용 프로그램의 초기 구조를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-204">In the previous task, you created the initial structure of the Geek Quiz web application.</span></span> <span data-ttu-id="89a4a-205">이제 퀴즈 데이터 모델과 상호 작용 하 고 다음과 같은 작업을 제공 하는 간단한 웹 API 서비스를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-205">You will now build a simple Web API service that interacts with the quiz data model and exposes the following actions:</span></span>

- <span data-ttu-id="89a4a-206">**GET/api/trivia**: 인증 된 사용자가 대답할 수 있도록 퀴즈 목록에서 다음 질문을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-206">**GET /api/trivia**: Retrieves the next question from the quiz list to be answered by the authenticated user.</span></span>
- <span data-ttu-id="89a4a-207">**POST/api/trivia**: 인증 된 사용자가 지정한 퀴즈 대답을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-207">**POST /api/trivia**: Stores the quiz answer specified by the authenticated user.</span></span>

<span data-ttu-id="89a4a-208">Visual Studio에서 제공 하는 ASP.NET 스 캐 폴딩 도구를 사용 하 여 Web API controller 클래스에 대 한 기준선을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-208">You will use the ASP.NET Scaffolding tools provided by Visual Studio to create the baseline for the Web API controller class.</span></span>

1. <span data-ttu-id="89a4a-209">**앱\_시작** 폴더에서 **WebApiConfig.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-209">Open the **WebApiConfig.cs** file inside the **App\_Start** folder.</span></span> <span data-ttu-id="89a4a-210">이 파일은 웹 api 서비스의 구성을 정의 합니다. 예를 들어, 웹 API 컨트롤러 작업에 경로를 매핑하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-210">This file defines the configuration of the Web API service, like how routes are mapped to Web API controller actions.</span></span>
2. <span data-ttu-id="89a4a-211">파일의 시작 부분에 다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-211">Add the following using statement at the beginning of the file.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. <span data-ttu-id="89a4a-212">**Register** 메서드에 다음 강조 표시 된 코드를 추가 하 여 Web API 동작 메서드에서 검색 된 JSON 데이터에 대 한 포맷터를 전역적으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-212">Add the following highlighted code to the **Register** method to globally configure the formatter for the JSON data retrieved by the Web API action methods.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="89a4a-213">**CamelCasePropertyNamesContractResolver** 는 속성 이름을 JavaScript의 속성 이름에 대 한 일반 규칙으로 자동으로 속성 이름을 *카멜식* case로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-213">The **CamelCasePropertyNamesContractResolver** automatically converts property names to *camel* case, which is the general convention for property names in JavaScript.</span></span>
4. <span data-ttu-id="89a4a-214">**솔루션 탐색기**에서 **GeekQuiz** 프로젝트의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 스 캐 폴드 항목**....</span><span class="sxs-lookup"><span data-stu-id="89a4a-214">In **Solution Explorer**, right-click the **Controllers** folder of the **GeekQuiz** project and select **Add | New Scaffolded Item...**.</span></span>

    <span data-ttu-id="89a4a-215">![새 스 캐 폴드 항목 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "새 스 캐 폴드 항목 만들기")</span><span class="sxs-lookup"><span data-stu-id="89a4a-215">![Creating a new scaffolded item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "Creating a new scaffolded item")</span></span>

    <span data-ttu-id="89a4a-216">*새 스 캐 폴드 항목 만들기*</span><span class="sxs-lookup"><span data-stu-id="89a4a-216">*Creating a new scaffolded item*</span></span>
5. <span data-ttu-id="89a4a-217">**스 캐 폴드 추가** 대화 상자에서 왼쪽 창에 **공통** 노드가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-217">In the **Add Scaffold** dialog box, make sure that the **Common** node is selected in the left pane.</span></span> <span data-ttu-id="89a4a-218">그런 다음 가운데 창에서 **WEB API 2 컨트롤러-비어** 있는 템플릿을 선택 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-218">Then, select the **Web API 2 Controller - Empty** template in the center pane and click **Add**.</span></span>

    <span data-ttu-id="89a4a-219">![Web API 2 컨트롤러 빈 템플릿 선택](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Web API 2 컨트롤러 빈 템플릿 선택")</span><span class="sxs-lookup"><span data-stu-id="89a4a-219">![Selecting the Web API 2 Controller Empty template](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Selecting the Web API 2 Controller Empty template")</span></span>

    <span data-ttu-id="89a4a-220">*Web API 2 컨트롤러 빈 템플릿 선택*</span><span class="sxs-lookup"><span data-stu-id="89a4a-220">*Selecting the Web API 2 Controller Empty template*</span></span>

    > [!NOTE]
    > <span data-ttu-id="89a4a-221">**ASP.NET 스 캐 폴딩** 은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-221">**ASP.NET Scaffolding** is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="89a4a-222">Visual Studio 2013 MVC 및 Web API 프로젝트용으로 미리 설치 된 코드 생성기를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-222">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="89a4a-223">표준 데이터 작업을 개발 하는 데 필요한 시간을 줄이기 위해 데이터 모델과 상호 작용 하는 코드를 신속 하 게 추가 하려는 경우 프로젝트에서 스 캐 폴딩을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-223">You should use scaffolding in your project when you want to quickly add code that interacts with data models in order to reduce the amount of time required to develop standard data operations.</span></span>
    > 
    > <span data-ttu-id="89a4a-224">또한 스 캐 폴딩 프로세스에서는 모든 필수 종속성이 프로젝트에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-224">The scaffolding process also ensures that all the required dependencies are installed in the project.</span></span> <span data-ttu-id="89a4a-225">예를 들어 빈 ASP.NET 프로젝트로 시작한 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가 하는 경우 필요한 Web API NuGet 패키지와 참조가 프로젝트에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-225">For example, if you start with an empty ASP.NET project and then use scaffolding to add a Web API controller, the required Web API NuGet packages and references are added to your project automatically.</span></span>
6. <span data-ttu-id="89a4a-226">**컨트롤러 추가** 대화 상자에서 **컨트롤러 이름** 텍스트 상자에 *triviacontroller* 를 입력 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-226">In the **Add Controller** dialog box, type *TriviaController* in the **Controller name** text box and click **Add**.</span></span>

    <span data-ttu-id="89a4a-227">![기타 정보 컨트롤러 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "기타 정보 컨트롤러 추가")</span><span class="sxs-lookup"><span data-stu-id="89a4a-227">![Adding the Trivia Controller](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Adding the Trivia Controller")</span></span>

    <span data-ttu-id="89a4a-228">*기타 정보 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="89a4a-228">*Adding the Trivia Controller*</span></span>
7. <span data-ttu-id="89a4a-229">그런 다음 **TriviaController.cs** 파일을 **GeekQuiz** 프로젝트의 **Controllers** 폴더에 추가 하 고 빈 **triviacontroller** 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-229">The **TriviaController.cs** file is then added to the **Controllers** folder of the **GeekQuiz** project, containing an empty **TriviaController** class.</span></span> <span data-ttu-id="89a4a-230">파일의 시작 부분에 다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-230">Add the following using statements at the beginning of the file.</span></span>

    <span data-ttu-id="89a4a-231">(코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerUsings*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-231">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerUsings*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. <span data-ttu-id="89a4a-232">**Triviacontroller** 클래스의 시작 부분에 다음 코드를 추가 하 여 컨트롤러에서 **TriviaContext** 인스턴스를 정의, 초기화 및 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-232">Add the following code at the beginning of the **TriviaController** class to define, initialize and dispose the **TriviaContext** instance in the controller.</span></span>

    <span data-ttu-id="89a4a-233">(코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerContext*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-233">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerContext*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="89a4a-234">**Triviacontroller** 의 **Dispose** 메서드는 **TriviaContext** 인스턴스의 **dispose** 메서드를 호출 하 여 **TriviaContext** 인스턴스가 삭제 되거나 가비지 수집 될 때 컨텍스트 개체에서 사용 하는 모든 리소스가 해제 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-234">The **Dispose** method of **TriviaController** invokes the **Dispose** method of the **TriviaContext** instance, which ensures that all the resources used by the context object are released when the **TriviaContext** instance is disposed or garbage-collected.</span></span> <span data-ttu-id="89a4a-235">여기에는 Entity Framework에서 연 모든 데이터베이스 연결을 닫는 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-235">This includes closing all database connections opened by Entity Framework.</span></span>
9. <span data-ttu-id="89a4a-236">**Triviacontroller** 클래스의 끝에 다음 도우미 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-236">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="89a4a-237">이 메서드는 지정 된 사용자가 응답할 수 있도록 데이터베이스에서 다음 퀴즈 질문을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-237">This method retrieves the following quiz question from the database to be answered by the specified user.</span></span>

    <span data-ttu-id="89a4a-238">(코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerNextQuestion*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-238">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerNextQuestion*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. <span data-ttu-id="89a4a-239">**Triviacontroller** 클래스에 다음 **Get** 작업 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-239">Add the following **Get** action method to the **TriviaController** class.</span></span> <span data-ttu-id="89a4a-240">이 작업 메서드는 이전 단계에서 정의 된 **NextQuestionAsync** 도우미 메서드를 호출 하 여 인증 된 사용자에 대 한 다음 질문을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-240">This action method calls the **NextQuestionAsync** helper method defined in the previous step to retrieve the next question for the authenticated user.</span></span>

    <span data-ttu-id="89a4a-241">(코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerGetAction*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-241">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerGetAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. <span data-ttu-id="89a4a-242">**Triviacontroller** 클래스의 끝에 다음 도우미 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-242">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="89a4a-243">이 메서드는 지정 된 대답을 데이터베이스에 저장 하 고 답변이 올바른지 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-243">This method stores the specified answer in the database and returns a Boolean value indicating whether or not the answer is correct.</span></span>

    <span data-ttu-id="89a4a-244">(코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerStoreAsync*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-244">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerStoreAsync*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. <span data-ttu-id="89a4a-245">**Triviacontroller** 클래스에 다음 **Post** 작업 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-245">Add the following **Post** action method to the **TriviaController** class.</span></span> <span data-ttu-id="89a4a-246">이 작업 메서드는 인증 된 사용자에 게 응답을 연결 하 고 **StoreAsync** helper 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-246">This action method associates the answer to the authenticated user and calls the **StoreAsync** helper method.</span></span> <span data-ttu-id="89a4a-247">그런 다음 도우미 메서드에서 반환 된 부울 값을 사용 하 여 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-247">Then, it sends a response with the Boolean value returned by the helper method.</span></span>

    <span data-ttu-id="89a4a-248">(코드 조각- *AspNetWebApiSpa-Ex1-TriviaControllerPostAction*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-248">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerPostAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. <span data-ttu-id="89a4a-249">**Triviacontroller** 클래스 정의에 **권한 부여** 특성을 추가 하 여 인증 된 사용자에 대 한 액세스를 제한 하도록 Web API 컨트롤러를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-249">Modify the Web API controller to restrict access to authenticated users by adding the **Authorize** attribute to the **TriviaController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="89a4a-250">작업 3 – 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="89a4a-250">Task 3 – Running the Solution</span></span>

<span data-ttu-id="89a4a-251">이 작업에서는 이전 작업에서 빌드한 Web API 서비스가 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-251">In this task you will verify that the Web API service you built in the previous task is working as expected.</span></span> <span data-ttu-id="89a4a-252">Internet Explorer **F12 개발자 도구** 를 사용 하 여 네트워크 트래픽을 캡처하고 웹 API 서비스에서 전체 응답을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-252">You will use the Internet Explorer **F12 Developer Tools** to capture the network traffic and inspect the full response from the Web API service.</span></span>

> [!NOTE]
> <span data-ttu-id="89a4a-253">Visual Studio 도구 모음에 있는 **시작** 단추에 **Internet Explorer** 가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-253">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer 옵션](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)

1. <span data-ttu-id="89a4a-255">**F5** 키를 눌러 솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-255">Press **F5** to run the solution.</span></span> <span data-ttu-id="89a4a-256">**로그인** 페이지가 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-256">The **Log in** page should appear in the browser.</span></span>

    > [!NOTE]
    > <span data-ttu-id="89a4a-257">응용 프로그램이 시작 되 면 기본 MVC 경로가 트리거되고, 기본적으로 **HomeController** 클래스의 **인덱스** 작업에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-257">When the application starts, the default MVC route is triggered, which by default is mapped to the **Index** action of the **HomeController** class.</span></span> <span data-ttu-id="89a4a-258">**HomeController** 는 인증 된 사용자로 제한 되므로 (연습 1의 **권한 부여** 특성을 사용 하 여 해당 클래스를 데코레이팅하는 경우) 사용자가 아직 인증 되지 않았으므로 응용 프로그램은 원래 요청을 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-258">Since **HomeController** is restricted to authenticated users (remember that you decorated that class with the **Authorize** attribute in Exercise 1) and there is no user authenticated yet, the application redirects the original request to the log in page.</span></span>

    <span data-ttu-id="89a4a-259">![솔루션 실행](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "솔루션 실행")</span><span class="sxs-lookup"><span data-stu-id="89a4a-259">![Running the solution](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "Running the solution")</span></span>

    <span data-ttu-id="89a4a-260">*솔루션 실행*</span><span class="sxs-lookup"><span data-stu-id="89a4a-260">*Running the solution*</span></span>
2. <span data-ttu-id="89a4a-261">**등록** 을 클릭 하 여 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-261">Click **Register** to create a new user.</span></span>

    <span data-ttu-id="89a4a-262">![새 사용자 등록](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "새 사용자 등록")</span><span class="sxs-lookup"><span data-stu-id="89a4a-262">![Registering a new user](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "Registering a new user")</span></span>

    <span data-ttu-id="89a4a-263">*새 사용자 등록*</span><span class="sxs-lookup"><span data-stu-id="89a4a-263">*Registering a new user*</span></span>
3. <span data-ttu-id="89a4a-264">**등록** 페이지에서 **사용자 이름** 및 **암호**를 입력 한 다음 **등록**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-264">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="89a4a-265">![페이지 등록](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "페이지 등록")</span><span class="sxs-lookup"><span data-stu-id="89a4a-265">![Register page](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "Register page")</span></span>

    <span data-ttu-id="89a4a-266">*페이지 등록*</span><span class="sxs-lookup"><span data-stu-id="89a4a-266">*Register page*</span></span>
4. <span data-ttu-id="89a4a-267">응용 프로그램이 새 계정을 등록 하 고 사용자가 인증 되 고 홈 페이지로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-267">The application registers the new account and the user is authenticated and redirected back to the home page.</span></span>

    <span data-ttu-id="89a4a-268">![사용자가 인증 됨](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "사용자 인증 됨")</span><span class="sxs-lookup"><span data-stu-id="89a4a-268">![User is authenticated](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "User authenticated")</span></span>

    <span data-ttu-id="89a4a-269">*사용자가 인증 됨*</span><span class="sxs-lookup"><span data-stu-id="89a4a-269">*User is authenticated*</span></span>
5. <span data-ttu-id="89a4a-270">브라우저에서 **F12** 키를 눌러 **개발자 도구** 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-270">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="89a4a-271">**Ctrl + 4** 를 누르거나 **네트워크** 아이콘을 클릭 한 다음 녹색 화살표 단추를 클릭 하 여 네트워크 트래픽 캡처를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-271">Press **CTRL + 4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="89a4a-272">![Web API 네트워크 캡처 시작](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Web API 네트워크 캡처 시작")</span><span class="sxs-lookup"><span data-stu-id="89a4a-272">![Initiating Web API network capture](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="89a4a-273">*Web API 네트워크 캡처 시작*</span><span class="sxs-lookup"><span data-stu-id="89a4a-273">*Initiating Web API network capture*</span></span>
6. <span data-ttu-id="89a4a-274">브라우저의 주소 표시줄에서 URL에 **api/기타 정보** 를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-274">Append **api/trivia** to the URL in the browser's address bar.</span></span> <span data-ttu-id="89a4a-275">이제 **Triviacontroller**의 **Get** 작업 메서드에서 응답의 세부 정보를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-275">You will now inspect the details of the response from the **Get** action method in **TriviaController**.</span></span>

    <span data-ttu-id="89a4a-276">![Web API를 통해 다음 질문 데이터 검색](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Web API를 통해 다음 질문 데이터 검색")</span><span class="sxs-lookup"><span data-stu-id="89a4a-276">![Retrieving the next question data through Web API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Retrieving the next question data through Web API")</span></span>

    <span data-ttu-id="89a4a-277">*Web API를 통해 다음 질문 데이터 검색*</span><span class="sxs-lookup"><span data-stu-id="89a4a-277">*Retrieving the next question data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="89a4a-278">다운로드가 완료 되 면 다운로드 한 파일을 사용 하 여 작업을 수행 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-278">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="89a4a-279">개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있으려면 대화 상자를 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-279">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
7. <span data-ttu-id="89a4a-280">이제 응답의 본문을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-280">Now you will inspect the body of the response.</span></span> <span data-ttu-id="89a4a-281">이렇게 하려면 **세부 정보** 탭을 클릭 한 다음 **응답 본문**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-281">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="89a4a-282">다운로드 한 데이터가 속성 **옵션** ( **Triviaoption** 개체 목록), **Id** 및 **triviaoption** 클래스에 **해당 하는** 개체 인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-282">You can check that the downloaded data is an object with the properties **options** (which is a list of **TriviaOption** objects), **id** and **title** that correspond to the **TriviaQuestion** class.</span></span>

    <span data-ttu-id="89a4a-283">![Web API 응답 본문 보기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Web API 응답 본문 보기")</span><span class="sxs-lookup"><span data-stu-id="89a4a-283">![Viewing the Web API Response Body](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Viewing the Web API Response Body")</span></span>

    <span data-ttu-id="89a4a-284">*Web API 응답 본문 보기*</span><span class="sxs-lookup"><span data-stu-id="89a4a-284">*Viewing Web API Response Body*</span></span>
8. <span data-ttu-id="89a4a-285">Visual Studio로 돌아가서 **SHIFT + f5** 키를 눌러 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a><span data-ttu-id="89a4a-286">연습 2: SPA 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-286">Exercise 2: Creating the SPA Interface</span></span>

<span data-ttu-id="89a4a-287">이 연습에서는 먼저 **AngularJS**를 사용 하 여 단일 페이지 응용 프로그램 상호 작용에 초점을 맞춘 geek of 퀴즈의 웹 프런트 엔드 부분을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-287">In this exercise you will first build the web front-end portion of Geek Quiz, focusing on the Single-Page Application interaction using **AngularJS**.</span></span> <span data-ttu-id="89a4a-288">그런 다음 CSS3를 사용 하 여 사용자 환경을 개선 하 여 다양 한 애니메이션을 수행 하 고 한 질문에서 다음 질문으로 전환할 때 컨텍스트 전환의 시각적 효과를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-288">You will then enhance the user experience with CSS3 to perform rich animations and provide a visual effect of context switching when transitioning from one question to the next.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a><span data-ttu-id="89a4a-289">작업 1-AngularJS를 사용 하 여 SPA 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-289">Task 1 – Creating the SPA Interface Using AngularJS</span></span>

<span data-ttu-id="89a4a-290">이 태스크에서는 **AngularJS** 를 사용 하 여 geek of 퀴즈 응용 프로그램의 클라이언트측을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-290">In this task you will use **AngularJS** to implement the client side of the Geek Quiz application.</span></span> <span data-ttu-id="89a4a-291">**AngularJS** 는 MVC ( *모델-뷰-컨트롤러* ) 기능을 사용 하 여 브라우저 기반 응용 프로그램을 보강 하 여 개발과 테스트를 모두 용이 하 게 하는 오픈 소스 JavaScript 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-291">**AngularJS** is an open-source JavaScript framework that augments browser-based applications with *Model-View-Controller* (MVC) capability, facilitating both development and testing.</span></span>

<span data-ttu-id="89a4a-292">Visual Studio의 패키지 관리자 콘솔에서 AngularJS를 설치 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-292">You will start by installing AngularJS from Visual Studio's Package Manager Console.</span></span> <span data-ttu-id="89a4a-293">그런 다음 Geek of 퀴즈 앱의 동작과 AngularJS 템플릿 엔진을 사용 하 여 퀴즈 질문 및 답변을 렌더링 하는 뷰를 제공 하는 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-293">Then, you will create the controller to provide the behavior of the Geek Quiz app and the view to render the quiz questions and answers using the AngularJS template engine.</span></span>

> [!NOTE]
> <span data-ttu-id="89a4a-294">AngularJS에 대 한 자세한 내용은 [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="89a4a-294">For more information about AngularJS, refer to [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/).</span></span>

1. <span data-ttu-id="89a4a-295">**웹에 대해 Visual Studio Express 2013** 을 열고 **Source/Ex2-GeekQuiz Aspainterface/Begin** 폴더에 있는 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-295">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source/Ex2-CreatingASPAInterface/Begin** folder.</span></span> <span data-ttu-id="89a4a-296">또는 이전 연습에서 얻은 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-296">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="89a4a-297">**도구** > **NuGet 패키지 관리자**에서 **패키지 관리자 콘솔** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-297">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="89a4a-298">다음 명령을 입력 하 여 **AngularJS** NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-298">Type the following command to install the **AngularJS.Core** NuGet package.</span></span>

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. <span data-ttu-id="89a4a-299">**솔루션 탐색기**에서 **GeekQuiz** 프로젝트의 **Scripts** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 폴더**.</span><span class="sxs-lookup"><span data-stu-id="89a4a-299">In **Solution Explorer**, right-click the **Scripts** folder of the **GeekQuiz** project and select **Add | New Folder**.</span></span> <span data-ttu-id="89a4a-300">폴더 이름을 **앱** 으로 입력 하 고 **enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-300">Name the folder **app** and press **Enter**.</span></span>
4. <span data-ttu-id="89a4a-301">방금 만든 **앱** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. JavaScript 파일**.</span><span class="sxs-lookup"><span data-stu-id="89a4a-301">Right-click the **app** folder you just created and select **Add | JavaScript File**.</span></span>

    ![새 JavaScript 파일 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    <span data-ttu-id="89a4a-303">*새 JavaScript 파일 만들기*</span><span class="sxs-lookup"><span data-stu-id="89a4a-303">*Creating a new JavaScript file*</span></span>
5. <span data-ttu-id="89a4a-304">**항목 이름 지정** 대화 상자에서 **항목 이름** 입력란에 *퀴즈-컨트롤러* 를 입력 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-304">In the **Specify Name for Item** dialog box, type *quiz-controller* in the **Item name** text box and click **OK**.</span></span>

    ![새 JavaScript 파일 이름 지정](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    <span data-ttu-id="89a4a-306">*새 JavaScript 파일 이름 지정*</span><span class="sxs-lookup"><span data-stu-id="89a4a-306">*Naming the new JavaScript file*</span></span>
6. <span data-ttu-id="89a4a-307">**Quiz-controller** 파일에서 AngularJS **QuizCtrl** controller를 선언 하 고 초기화 하는 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-307">In the **quiz-controller.js** file, add the following code to declare and initialize the AngularJS **QuizCtrl** controller.</span></span>

    <span data-ttu-id="89a4a-308">(코드 조각- *AspNetWebApiSpa-Ex2-AngularQuizController*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-308">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizController*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > <span data-ttu-id="89a4a-309">**QuizCtrl** controller의 constructor 함수는 **$scope**라는 injectable 매개 변수를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-309">The constructor function of the **QuizCtrl** controller expects an injectable parameter named **$scope**.</span></span> <span data-ttu-id="89a4a-310">**$Scope** 개체에 속성을 연결 하 여 생성자 함수에서 범위의 초기 상태를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-310">The initial state of the scope should be set up in the constructor function by attaching properties to the **$scope** object.</span></span> <span data-ttu-id="89a4a-311">속성은 **뷰 모델**을 포함 하며, 컨트롤러가 등록 될 때 템플릿에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-311">The properties contain the **view model**, and will be accessible to the template when the controller is registered.</span></span>
    > 
    > <span data-ttu-id="89a4a-312">**QuizCtrl** 컨트롤러는 **QuizApp**라는 모듈 내에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-312">The **QuizCtrl** controller is defined inside a module named **QuizApp**.</span></span> <span data-ttu-id="89a4a-313">모듈은 응용 프로그램을 별도의 구성 요소로 나눌 수 있는 작업 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-313">Modules are units of work that let you break your application into separate components.</span></span> <span data-ttu-id="89a4a-314">모듈을 사용 하는 경우의 주요 이점은 코드를 보다 쉽게 이해 하 고 단위 테스트, 재사용 및 유지 관리를 용이 하 게 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-314">The main advantages of using modules is that the code is easier to understand and facilitates unit testing, reusability and maintainability.</span></span>
7. <span data-ttu-id="89a4a-315">이제 뷰에서 트리거된 이벤트에 반응 하기 위해 범위에 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-315">You will now add behavior to the scope in order to react to events triggered from the view.</span></span> <span data-ttu-id="89a4a-316">**QuizCtrl** 컨트롤러의 끝에 다음 코드를 추가 하 여 **$Scope** 개체에 **nextquestion** 함수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-316">Add the following code at the end of the **QuizCtrl** controller to define the **nextQuestion** function in the **$scope** object.</span></span>

    <span data-ttu-id="89a4a-317">(코드 조각- *AspNetWebApiSpa-Ex2-AngularQuizControllerNextQuestion*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-317">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerNextQuestion*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > <span data-ttu-id="89a4a-318">이 함수는 이전 연습에서 만든 **기타 정보** 웹 API에서 다음 질문을 검색 하 고 질문 데이터를 **$scope** 개체에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-318">This function retrieves the next question from the **Trivia** Web API created in the previous exercise and attaches the question data to the **$scope** object.</span></span>
8. <span data-ttu-id="89a4a-319">**QuizCtrl** 컨트롤러의 끝에 다음 코드를 삽입 하 여 **$Scope** 개체에서 **sendanswer** 함수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-319">Insert the following code at the end of the **QuizCtrl** controller to define the **sendAnswer** function in the **$scope** object.</span></span>

    <span data-ttu-id="89a4a-320">(코드 조각- *AspNetWebApiSpa-Ex2-AngularQuizControllerSendAnswer*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-320">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerSendAnswer*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > <span data-ttu-id="89a4a-321">이 함수는 사용자가 선택한 답변을 **기타 정보** Web API에 보내고 결과를 저장 합니다. 예를 들어 답변이 올바르면이 고, 그렇지 않으면 **$scope** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-321">This function sends the answer selected by the user to the **Trivia** Web API and stores the result –i.e. if the answer is correct or not– in the **$scope** object.</span></span>
    > 
    > <span data-ttu-id="89a4a-322">위의 **Nextquestion** 및 **Sendanswer** 함수는 AngularJS **$http** 개체를 사용 하 여 브라우저에서 XMLHTTPREQUEST JavaScript 개체를 통해 Web API와의 통신을 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-322">The **nextQuestion** and **sendAnswer** functions from above use the AngularJS **$http** object to abstract the communication with the Web API via the XMLHttpRequest JavaScript object from the browser.</span></span> <span data-ttu-id="89a4a-323">AngularJS는 RESTful Api를 통해 리소스에 대해 CRUD 작업을 수행 하기 위해 더 높은 수준의 추상화를 제공 하는 다른 서비스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-323">AngularJS supports another service that brings a higher level of abstraction to perform CRUD operations against a resource through RESTful APIs.</span></span> <span data-ttu-id="89a4a-324">AngularJS **$resource** 개체는 **$http** 개체와 상호 작용할 필요 없이 높은 수준의 동작을 제공 하는 동작 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-324">The AngularJS **$resource** object has action methods which provide high-level behaviors without the need to interact with the **$http** object.</span></span> <span data-ttu-id="89a4a-325">CRUD 모델이 필요한 시나리오에서 **$resource** 개체를 사용 하는 것이 좋습니다 (전경 정보, [$resource 설명서](https://docs.angularjs.org/api/ngResource/service/$resource)참조).</span><span class="sxs-lookup"><span data-stu-id="89a4a-325">Consider using the **$resource** object in scenarios that requires the CRUD model (fore information, see the [$resource documentation](https://docs.angularjs.org/api/ngResource/service/$resource)).</span></span>
9. <span data-ttu-id="89a4a-326">다음 단계는 퀴즈에 대 한 뷰를 정의 하는 AngularJS 템플릿을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-326">The next step is to create the AngularJS template that defines the view for the quiz.</span></span> <span data-ttu-id="89a4a-327">이렇게 하려면 뷰 내에서 파일의 인덱스를 엽니다 **.**  **Home** 폴더를 입력 하 고 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-327">To do this, open the **Index.cshtml** file inside the **Views | Home** folder and replace the content with the following code.</span></span>

    <span data-ttu-id="89a4a-328">(코드 조각- *AspNetWebApiSpa-Ex2-GeekQuizView*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-328">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizView*)</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="89a4a-329">AngularJS 템플릿은 모델 및 컨트롤러의 정보를 사용 하 여 사용자가 브라우저에서 볼 수 있는 동적 뷰로 정적 태그를 변환 하는 선언적 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-329">The AngularJS template is a declarative specification that uses information from the model and the controller to transform static markup into the dynamic view that the user sees in the browser.</span></span> <span data-ttu-id="89a4a-330">다음은 템플릿에서 사용할 수 있는 AngularJS 요소 및 요소 특성의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-330">The following are examples of AngularJS elements and element attributes that can be used in a template:</span></span>
    > 
    > - <span data-ttu-id="89a4a-331">**앱** 지시문을 통해 응용 프로그램의 루트 요소를 나타내는 DOM 요소를 AngularJS에 지시할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-331">The **ng-app** directive tells AngularJS the DOM element that represents the root element of the application.</span></span>
    > - <span data-ttu-id="89a4a-332">**컨트롤러** 지시문은 지시문이 선언 된 지점에서 DOM에 컨트롤러를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-332">The **ng-controller** directive attaches a controller to the DOM at the point where the directive is declared.</span></span>
    > - <span data-ttu-id="89a4a-333">중괄호 표기법 **{{}}** 은 컨트롤러에 정의 된 범위 속성에 대 한 바인딩을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-333">The curly brace notation **{{ }}** denotes bindings to the scope properties defined in the controller.</span></span>
    > - <span data-ttu-id="89a4a-334">사용자 **클릭** 에 대 한 응답으로 범위에 정의 된 함수를 호출 하는 데는 클릭 광고 지시문이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-334">The **ng-click** directive is used to invoke the functions defined in the scope in response to user clicks.</span></span>
10. <span data-ttu-id="89a4a-335">**Content** 폴더 내에서 **사이트 .css** 파일을 열고 파일 끝에 다음 강조 표시 된 스타일을 추가 하 여 퀴즈 보기에 대 한 모양과 느낌을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-335">Open the **Site.css** file inside the **Content** folder and add the following highlighted styles at the end of the file to provide a look and feel for the quiz view.</span></span>

    <span data-ttu-id="89a4a-336">(코드 조각- *AspNetWebApiSpa-Ex2-GeekQuizStyles*)</span><span class="sxs-lookup"><span data-stu-id="89a4a-336">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizStyles*)</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="89a4a-337">작업 2-솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="89a4a-337">Task 2 – Running the Solution</span></span>

<span data-ttu-id="89a4a-338">이 작업에서는 AngularJS를 사용 하 여 빌드한 새 사용자 인터페이스를 사용 하 여 솔루션을 실행 하 여 일부 퀴즈 질문에 답변 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-338">In this task you will execute the solution using the new user interface you built with AngularJS to answer some of the quiz questions.</span></span>

1. <span data-ttu-id="89a4a-339">**F5** 키를 눌러 솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-339">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="89a4a-340">새 사용자 계정을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-340">Register a new user account.</span></span> <span data-ttu-id="89a4a-341">이렇게 하려면 연습 1, 작업 3에 설명 된 등록 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="89a4a-341">To do this, follow the registration steps described in Exercise 1, Task 3.</span></span>

    > [!NOTE]
    > <span data-ttu-id="89a4a-342">이전 연습에서 만든 솔루션을 사용 하는 경우 이전에 만든 사용자 계정으로 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-342">If you are using the solution from the previous exercise, you can log in with the user account you created before.</span></span>
3. <span data-ttu-id="89a4a-343">퀴즈의 첫 번째 질문을 보여 주는 **홈** 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-343">The **Home** page should appear, showing the first question of the quiz.</span></span> <span data-ttu-id="89a4a-344">옵션 중 하나를 클릭 하 여 질문에 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-344">Answer the question by clicking one of the options.</span></span> <span data-ttu-id="89a4a-345">이렇게 하면 이전에 정의 된 **Sendanswer** 함수를 트리거하여 선택한 옵션을 **기타 정보** Web API로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-345">This will trigger the **sendAnswer** function defined earlier, which sends the selected option to the **Trivia** Web API.</span></span>

    <span data-ttu-id="89a4a-346">![질문에 답변](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "질문에 답변")</span><span class="sxs-lookup"><span data-stu-id="89a4a-346">![Answering a question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "Answering a question")</span></span>

    <span data-ttu-id="89a4a-347">*질문에 답변*</span><span class="sxs-lookup"><span data-stu-id="89a4a-347">*Answering a question*</span></span>
4. <span data-ttu-id="89a4a-348">단추 중 하나를 클릭 하면 대답이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-348">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="89a4a-349">다음 **질문** 을 클릭 하 여 다음 질문을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-349">Click **Next Question** to show the following question.</span></span> <span data-ttu-id="89a4a-350">이렇게 하면 컨트롤러에 정의 된 **Nextquestion** 함수가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-350">This will trigger the **nextQuestion** function defined in the controller.</span></span>

    <span data-ttu-id="89a4a-351">![다음 질문 요청](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "다음 질문 요청")</span><span class="sxs-lookup"><span data-stu-id="89a4a-351">![Requesting the next question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "Requesting the next question")</span></span>

    <span data-ttu-id="89a4a-352">*다음 질문 요청*</span><span class="sxs-lookup"><span data-stu-id="89a4a-352">*Requesting the next question*</span></span>
5. <span data-ttu-id="89a4a-353">다음 질문이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-353">The next question should appear.</span></span> <span data-ttu-id="89a4a-354">질문에 대 한 대답을 원하는 횟수 만큼 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-354">Continue answering questions as many times as you want.</span></span> <span data-ttu-id="89a4a-355">모든 질문을 완료 한 후에는 첫 번째 질문으로 돌아가야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-355">After completing all the questions you should return to the first question.</span></span>

    <span data-ttu-id="89a4a-356">![다른 질문](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "다른 질문")</span><span class="sxs-lookup"><span data-stu-id="89a4a-356">![Another question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "Another question")</span></span>

    <span data-ttu-id="89a4a-357">*다음 질문*</span><span class="sxs-lookup"><span data-stu-id="89a4a-357">*Next question*</span></span>
6. <span data-ttu-id="89a4a-358">Visual Studio로 돌아가서 **SHIFT + f5** 키를 눌러 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-358">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a><span data-ttu-id="89a4a-359">작업 3 – CSS3를 사용 하 여 대칭 이동 애니메이션 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-359">Task 3 – Creating a Flip Animation Using CSS3</span></span>

<span data-ttu-id="89a4a-360">이 작업에서는 CSS3 속성을 사용 하 여 질문에 응답 하 고 다음 질문을 검색할 때 대칭 이동 효과를 추가 하 여 다양 한 애니메이션을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-360">In this task you will use CSS3 properties to perform rich animations by adding a flip effect when a question is answered and when the next question is retrieved.</span></span>

1. <span data-ttu-id="89a4a-361">**솔루션 탐색기**에서 **GeekQuiz** 프로젝트의 **Content** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 기존 항목**...</span><span class="sxs-lookup"><span data-stu-id="89a4a-361">In **Solution Explorer**, right-click the **Content** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="89a4a-362">![Content 폴더에 기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Content 폴더에 기존 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="89a4a-362">![Adding an existing item to the Content folder](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Adding an existing item to the Content folder")</span></span>

    <span data-ttu-id="89a4a-363">*Content 폴더에 기존 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="89a4a-363">*Adding an existing item to the Content folder*</span></span>
2. <span data-ttu-id="89a4a-364">**기존 항목 추가** 대화 상자에서 **원본/자산** 폴더로 이동한 다음 **대칭 이동 .css**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-364">In the **Add Existing Item** dialog box, navigate to the **Source/Assets** folder and select **Flip.css**.</span></span> <span data-ttu-id="89a4a-365">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-365">Click **Add**.</span></span>

    <span data-ttu-id="89a4a-366">![자산에서 대칭 .css 파일 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "자산에서 대칭 .css 파일 추가")</span><span class="sxs-lookup"><span data-stu-id="89a4a-366">![Adding the Flip.css file from Assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "Adding the Flip.css file from Assets")</span></span>

    <span data-ttu-id="89a4a-367">*자산에서 대칭 .css 파일 추가*</span><span class="sxs-lookup"><span data-stu-id="89a4a-367">*Adding the Flip.css file from Assets*</span></span>
3. <span data-ttu-id="89a4a-368">방금 추가한 **대칭 이동 .css** 파일을 열고 콘텐츠를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-368">Open the **Flip.css** file you just added and inspect its content.</span></span>
4. <span data-ttu-id="89a4a-369">**대칭 이동 변환** 주석을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-369">Locate the **flip transformation** comment.</span></span> <span data-ttu-id="89a4a-370">주석 아래 스타일에서는 CSS **큐브 뷰** 및 **rotateY** 변환을 사용 하 여 &quot;카드 대칭&quot; 효과를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-370">The styles below that comment use the CSS **perspective** and **rotateY** transformations to generate a &quot;card flip&quot; effect.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. <span data-ttu-id="89a4a-371">**대칭 이동 중 창 숨기기 창을** 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-371">Locate the **hide back of pane during flip** comment.</span></span> <span data-ttu-id="89a4a-372">주석 아래 스타일은 **배경 표면 표시** CSS 속성을 *hidden*으로 설정 하 여 표면에서 반대쪽을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-372">The style below that comment hides the back-side of the faces when they are facing away from the viewer by setting the **backface-visibility** CSS property to *hidden*.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. <span data-ttu-id="89a4a-373">**앱\_시작** 폴더에서 **BundleConfig.cs** 파일을 열고 **&quot;~/content/css&quot;** 스타일 번들에서 **대칭 이동 .css** 파일에 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-373">Open the **BundleConfig.cs** file inside the **App\_Start** folder and add the reference to the **Flip.css** file in the **&quot;~/Content/css&quot;** style bundle</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. <span data-ttu-id="89a4a-374">**F5** 키를 눌러 솔루션을 실행 하 고 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-374">Press **F5** to run the solution and log in with your credentials.</span></span>
8. <span data-ttu-id="89a4a-375">옵션 중 하나를 클릭 하 여 질문에 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-375">Answer a question by clicking one of the options.</span></span> <span data-ttu-id="89a4a-376">뷰 간에 전환할 때의 대칭 이동 효과를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-376">Notice the flip effect when transitioning between views.</span></span>

    <span data-ttu-id="89a4a-377">![전환 효과를 사용 하 여 질문에 답변](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "전환 효과를 사용 하 여 질문에 답변")</span><span class="sxs-lookup"><span data-stu-id="89a4a-377">![Answering a question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "Answering a question with the flip effect")</span></span>

    <span data-ttu-id="89a4a-378">*전환 효과를 사용 하 여 질문에 답변*</span><span class="sxs-lookup"><span data-stu-id="89a4a-378">*Answering a question with the flip effect*</span></span>
9. <span data-ttu-id="89a4a-379">다음 **질문** 을 클릭 하 여 다음 질문을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-379">Click **Next Question** to retrieve the following question.</span></span> <span data-ttu-id="89a4a-380">대칭 이동 효과가 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-380">The flip effect should appear again.</span></span>

    <span data-ttu-id="89a4a-381">![플립 효과를 사용 하 여 다음 질문 검색](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "플립 효과를 사용 하 여 다음 질문 검색")</span><span class="sxs-lookup"><span data-stu-id="89a4a-381">![Retrieving the following question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "Retrieving the following question with the flip effect")</span></span>

    <span data-ttu-id="89a4a-382">*플립 효과를 사용 하 여 다음 질문 검색*</span><span class="sxs-lookup"><span data-stu-id="89a4a-382">*Retrieving the following question with the flip effect*</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="89a4a-383">요약</span><span class="sxs-lookup"><span data-stu-id="89a4a-383">Summary</span></span>

<span data-ttu-id="89a4a-384">이 실습 실습을 완료 하면 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-384">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="89a4a-385">ASP.NET 스 캐 폴딩을 사용 하 여 ASP.NET Web API 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="89a4a-385">Create an ASP.NET Web API controller using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="89a4a-386">Web API Get 작업을 구현 하 여 다음 퀴즈 질문 검색</span><span class="sxs-lookup"><span data-stu-id="89a4a-386">Implement a Web API Get action to retrieve the next quiz question</span></span>
- <span data-ttu-id="89a4a-387">퀴즈 답변을 저장 하는 웹 API 게시 작업을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="89a4a-387">Implement a Web API Post action to store the quiz answers</span></span>
- <span data-ttu-id="89a4a-388">Visual Studio 패키지 관리자 콘솔에서 AngularJS 설치</span><span class="sxs-lookup"><span data-stu-id="89a4a-388">Install AngularJS from the Visual Studio Package Manager Console</span></span>
- <span data-ttu-id="89a4a-389">AngularJS 템플릿 및 컨트롤러 구현</span><span class="sxs-lookup"><span data-stu-id="89a4a-389">Implement AngularJS templates and controllers</span></span>
- <span data-ttu-id="89a4a-390">CSS3 전환을 사용 하 여 애니메이션 효과 수행</span><span class="sxs-lookup"><span data-stu-id="89a4a-390">Use CSS3 transitions to perform animation effects</span></span>
