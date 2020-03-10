---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 기본 사항 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서는 MVC (모델 뷰 컨트롤러) 음악 저장소, ASP.NET MV를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램을 기반으로 합니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484571"
---
# <a name="aspnet-mvc-4-fundamentals"></a><span data-ttu-id="d8136-103">ASP.NET MVC 4 기본 사항</span><span class="sxs-lookup"><span data-stu-id="d8136-103">ASP.NET MVC 4 Fundamentals</span></span>

<span data-ttu-id="d8136-104">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="d8136-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="d8136-105">웹 캠프 교육 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="d8136-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="d8136-106">이 실습 랩은 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램 인 MVC (모델 뷰 컨트롤러) 음악 저장소를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-106">This Hands-On Lab is based on MVC (Model View Controller) Music Store, a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="d8136-107">랩 전체에서 이러한 기술을 함께 사용 하는 것이 더 간단 하지만,</span><span class="sxs-lookup"><span data-stu-id="d8136-107">Throughout the lab you will learn the simplicity, yet power of using these technologies together.</span></span> <span data-ttu-id="d8136-108">간단한 응용 프로그램으로 시작 하 여 완벽 하 게 작동 하는 ASP.NET MVC 4 웹 응용 프로그램을 만들 때까지 빌드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-108">You will start with a simple application and will build it until you have a fully functional ASP.NET MVC 4 Web Application.</span></span>

<span data-ttu-id="d8136-109">이 랩은 ASP.NET MVC 4와 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-109">This Lab works with ASP.NET MVC 4.</span></span>

<span data-ttu-id="d8136-110">ASP.NET MVC 3 버전의 자습서 응용 프로그램을 탐색 하려는 경우이를 [mvc-음악 저장소](https://github.com/evilDave/MVC-Music-Store)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-110">If you wish to explore the ASP.NET MVC 3 version of the tutorial application, you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="d8136-111">이 실습 랩에서는 개발자가 HTML 및 JavaScript와 같은 웹 개발 기술을 경험 하 고 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-111">This Hands-On Lab assumes that the developer has experience in Web development technologies, such as HTML and JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="d8136-112">모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-112">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="d8136-113">이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 기본 사항](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-113">The project specific to this lab is available at [ASP.NET MVC 4 Fundamentals](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span></span>

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a><span data-ttu-id="d8136-114">Music Store 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d8136-114">The Music Store application</span></span>

<span data-ttu-id="d8136-115">이 랩에서 구축할 Music Store 웹 응용 프로그램은 쇼핑, 구매 및 관리의 세 가지 주요 부분으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-115">The Music Store web application that will be built throughout this Lab comprises three main parts: shopping, checkout, and administration.</span></span> <span data-ttu-id="d8136-116">방문자는 장르별로 앨범을 탐색 하 고, 바구니에 앨범을 추가 하 고, 선택 항목을 검토 하 고, 마지막으로 체크 아웃으로 이동 하 여 주문을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-116">Visitors will be able to browse albums by genre, add albums to their cart, review their selection and finally proceed to checkout to login and complete the order.</span></span> <span data-ttu-id="d8136-117">또한 저장소 관리자는 사용 가능한 앨범 뿐만 아니라 주 속성도 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-117">Additionally, store administrators will be able to manage the available albums as well as their main properties.</span></span>

<span data-ttu-id="d8136-118">![뮤직 저장소 화면](aspnet-mvc-4-fundamentals/_static/image1.png "뮤직 저장소 화면")</span><span class="sxs-lookup"><span data-stu-id="d8136-118">![Music Store screens](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store screens")</span></span>

<span data-ttu-id="d8136-119">*뮤직 저장소 화면*</span><span class="sxs-lookup"><span data-stu-id="d8136-119">*Music Store screens*</span></span>

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a><span data-ttu-id="d8136-120">ASP.NET MVC 4 Essentials</span><span class="sxs-lookup"><span data-stu-id="d8136-120">ASP.NET MVC 4 Essentials</span></span>

<span data-ttu-id="d8136-121">Music Store 응용 프로그램은 응용 프로그램을 세 가지 주요 구성 요소로 구분 하는 아키텍처 패턴 인 **MVC (모델 뷰 컨트롤러)** 를 사용 하 여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-121">Music Store application will be built using **Model View Controller (MVC)**, an architectural pattern that separates an application into three main components:</span></span>

- <span data-ttu-id="d8136-122">**모델**: 모델 개체는 도메인 논리를 구현 하는 응용 프로그램의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-122">**Models**: Model objects are the parts of the application that implement the domain logic.</span></span> <span data-ttu-id="d8136-123">모델 개체는 또한 데이터베이스에서 모델 상태를 검색 하 고 저장 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-123">Often, model objects also retrieve and store model state in a database.</span></span>
- <span data-ttu-id="d8136-124">**보기:** 보기는 응용 프로그램 UI (사용자 인터페이스)를 표시 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-124">**Views:** Views are the components that display the application's user interface (UI).</span></span> <span data-ttu-id="d8136-125">일반적으로 이 UI는 모델 데이터에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-125">Typically, this UI is created from the model data.</span></span> <span data-ttu-id="d8136-126">예를 들어 앨범 개체의 현재 상태를 기반으로 하는 드롭다운 목록과 텍스트 상자를 표시 하는 앨범의 편집 뷰가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-126">An example would be the edit view of Albums that displays text boxes and a drop-down list based on the current state of an Album object.</span></span>
- <span data-ttu-id="d8136-127">**컨트롤러:** 컨트롤러는 사용자 상호 작용을 처리 하 고, 모델을 조작 하 고, 궁극적으로 UI를 렌더링 하는 뷰를 선택 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-127">**Controllers:** Controllers are the components that handle user interaction, manipulate the model, and ultimately select a view to render the UI.</span></span> <span data-ttu-id="d8136-128">MVC 응용 프로그램에서 뷰는 정보만 표시하고 컨트롤러는 사용자 입력에 대한 응답 및 상호 작용을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-128">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="d8136-129">MVC 패턴을 사용 하면 응용 프로그램의 다양 한 측면 (입력 논리, 비즈니스 논리 및 UI 논리)을 분리 하는 동시에 이러한 요소 간의 느슨한 결합을 제공 하는 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-129">The MVC pattern helps you to create applications that separate the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="d8136-130">이러한 분리를 통해 응용 프로그램을 빌드할 때 복잡성을 관리할 수 있습니다 .이를 통해 한 번에 하나의 구현 측면에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-130">This separation helps you manage complexity when you build an application, as it allows you to focus on one aspect of the implementation at a time.</span></span> <span data-ttu-id="d8136-131">또한 MVC 패턴을 사용 하면 응용 프로그램을 쉽게 테스트할 수 있으며, 응용 프로그램을 만들기 위해 TDD (테스트 기반 개발)를 사용 하는 것도 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-131">In addition, the MVC pattern makes it easy to test applications, also encouraging the use of test-driven development (TDD) for creating applications.</span></span>

<span data-ttu-id="d8136-132">**ASP.NET mvc** 프레임 워크는 ASP.NET Mvc 기반 웹 응용 프로그램을 만들기 위한 ASP.NET Web Forms 패턴의 대안을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-132">The **ASP.NET MVC** framework provides an alternative to the ASP.NET Web Forms pattern for creating ASP.NET MVC-based Web applications.</span></span> <span data-ttu-id="d8136-133">**ASP.NET MVC** 프레임 워크는 웹 폼 기반 응용 프로그램과 마찬가지로 마스터 페이지 및 멤버 기반 인증과 같은 기존 ASP.NET 기능과 통합 되어 핵심 .net framework의 모든 기능을 활용할 수 있는 간단 하 고 테스트 하기 용이한 프레젠테이션 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-133">The **ASP.NET MVC** framework is a lightweight, highly testable presentation framework that (as with Web-forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication so you get all the power of the core .NET framework.</span></span> <span data-ttu-id="d8136-134">이미 사용 하 고 있는 모든 라이브러리를 ASP.NET MVC 4에서 사용할 수 있기 때문에 ASP.NET Web Forms에 이미 익숙한 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-134">This is useful if you are already familiar with ASP.NET Web Forms because all the libraries that you already use are available in ASP.NET MVC 4 as well.</span></span>

<span data-ttu-id="d8136-135">또한 MVC 응용 프로그램의 세 가지 주요 구성 요소 간의 느슨한 결합은 병렬 개발을 촉진 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-135">In addition, the loose coupling between the three main components of an MVC application also promotes parallel development.</span></span> <span data-ttu-id="d8136-136">예를 들어 한 개발자가 보기에서 작업 하 고, 두 번째 개발자는 컨트롤러 논리에 대해 작업을 수행할 수 있으며, 세 번째 개발자는 모델의 비즈니스 논리에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-136">For instance, one developer can work on the view, a second developer can work on the controller logic, and a third developer can focus on the business logic in the model.</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="d8136-137">목표</span><span class="sxs-lookup"><span data-stu-id="d8136-137">Objectives</span></span>

<span data-ttu-id="d8136-138">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-138">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="d8136-139">Music Store 응용 프로그램 자습서를 기반으로 하 여 처음부터 ASP.NET MVC 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-139">Create an ASP.NET MVC application from scratch based on the Music Store Application tutorial</span></span>
- <span data-ttu-id="d8136-140">사이트의 홈 페이지에 대 한 Url을 처리 하 고 주 기능을 검색 하는 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-140">Add Controllers to handle URLs to the Home page of the site and for browsing its main functionality</span></span>
- <span data-ttu-id="d8136-141">보기를 추가 하 여 스타일과 함께 표시 되는 콘텐츠를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-141">Add a View to customize the content displayed along with its style</span></span>
- <span data-ttu-id="d8136-142">데이터 및 도메인 논리를 포함 하 고 관리 하는 모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-142">Add Model classes to contain and manage data and domain logic</span></span>
- <span data-ttu-id="d8136-143">모델 패턴 보기를 사용 하 여 컨트롤러 작업에서 보기 템플릿으로 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-143">Use View Model pattern to pass information from controller actions to the view templates</span></span>
- <span data-ttu-id="d8136-144">인터넷 응용 프로그램에 대 한 ASP.NET MVC 4 새 템플릿 살펴보기</span><span class="sxs-lookup"><span data-stu-id="d8136-144">Explore the ASP.NET MVC 4 new template for internet applications</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="d8136-145">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="d8136-145">Prerequisites</span></span>

<span data-ttu-id="d8136-146">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-146">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="d8136-147">[Visual Studio 2012 Express For Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a](#AppendixA) 참조)</span><span class="sxs-lookup"><span data-stu-id="d8136-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (read [Appendix A](#AppendixA) for instructions on how to install it)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="d8136-148">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="d8136-148">Setup</span></span>

<span data-ttu-id="d8136-149">**코드 조각 설치**</span><span class="sxs-lookup"><span data-stu-id="d8136-149">**Installing Code Snippets**</span></span>

<span data-ttu-id="d8136-150">편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-150">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="d8136-151">코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-151">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="d8136-152">Visual Studio Code 코드 조각에 대해 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [C: 코드 조각&quot;사용](#AppendixC) &quot;부록을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-152">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="d8136-153">실습</span><span class="sxs-lookup"><span data-stu-id="d8136-153">Exercises</span></span>

<span data-ttu-id="d8136-154">이 실습 랩은 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-154">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="d8136-155">연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-155">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>](#Exercise1)
2. [<span data-ttu-id="d8136-156">연습 2: 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-156">Exercise 2: Creating a Controller</span></span>](#Exercise2)
3. [<span data-ttu-id="d8136-157">연습 3: 컨트롤러에 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="d8136-157">Exercise 3: Passing parameters to a Controller</span></span>](#Exercise3)
4. [<span data-ttu-id="d8136-158">연습 4: 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-158">Exercise 4: Creating a View</span></span>](#Exercise4)
5. [<span data-ttu-id="d8136-159">연습 5: 뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-159">Exercise 5: Creating a View Model</span></span>](#Exercise5)
6. [<span data-ttu-id="d8136-160">연습 6: 뷰에서 매개 변수 사용</span><span class="sxs-lookup"><span data-stu-id="d8136-160">Exercise 6: Using parameters in View</span></span>](#Exercise6)
7. [<span data-ttu-id="d8136-161">연습 7: ASP.NET MVC 4 새 템플릿 살펴보기</span><span class="sxs-lookup"><span data-stu-id="d8136-161">Exercise 7: A lap around ASP.NET MVC 4 New Template</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="d8136-162">각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-162">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="d8136-163">연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-163">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="d8136-164">이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="d8136-164">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a><span data-ttu-id="d8136-165">연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-165">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="d8136-166">이 연습에서는 Visual Studio 2012 Express for Web 및 기본 폴더 구성에서 ASP.NET MVC 응용 프로그램을 만드는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-166">In this exercise, you will learn how to create an ASP.NET MVC application in Visual Studio 2012 Express for Web as well as its main folder organization.</span></span> <span data-ttu-id="d8136-167">또한 새 컨트롤러를 추가 하 고 응용 프로그램의 홈 페이지에 간단한 문자열을 표시 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-167">Additionally, you will learn how to add a new Controller and make it display a simple string in the application's home page.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a><span data-ttu-id="d8136-168">작업 1-ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-168">Task 1 - Creating the ASP.NET MVC Web Application Project</span></span>

1. <span data-ttu-id="d8136-169">이 작업에서는 MVC Visual Studio 템플릿을 사용 하 여 빈 ASP.NET MVC 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-169">In this task, you will create an empty ASP.NET MVC application project using the MVC Visual Studio template.</span></span> <span data-ttu-id="d8136-170">**VS Express for Web**를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-170">Start **VS Express for Web**.</span></span>
2. <span data-ttu-id="d8136-171">**파일** 메뉴에서 **새 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-171">On the **File** menu, click **New Project**.</span></span>
3. <span data-ttu-id="d8136-172">**새 프로젝트** 대화 상자에서 **시각적 개체 C#,** **웹** 템플릿 목록 아래에 있는 **ASP.NET MVC 4 웹 응용 프로그램** 프로젝트 형식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-172">In the **New Project** dialog box select the **ASP.NET MVC 4 Web Application** project type, located under **Visual C#,** **Web** template list.</span></span>
4. <span data-ttu-id="d8136-173">**이름** 을 *MvcMusicStore*로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-173">Change the **Name** to *MvcMusicStore*.</span></span>
5. <span data-ttu-id="d8136-174">이 연습의 원본 폴더에 있는 새 **시작** 폴더 (예: **[\Source\Ex01-CreatingMusicStoreProject\Begin]** ) 내에 솔루션의 위치를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-174">Set the location of the solution inside a new **Begin** folder in this Exercise's Source folder, for example **[YOUR-HOL-PATH]\Source\Ex01-CreatingMusicStoreProject\Begin**.</span></span> <span data-ttu-id="d8136-175">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-175">Click **OK**.</span></span>

    <span data-ttu-id="d8136-176">![새 프로젝트 만들기 대화 상자](aspnet-mvc-4-fundamentals/_static/image2.png "새 프로젝트 만들기 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="d8136-176">![Create New Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image2.png "Create New Project Dialog Box")</span></span>

    <span data-ttu-id="d8136-177">*새 프로젝트 만들기 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="d8136-177">*Create New Project Dialog Box*</span></span>
6. <span data-ttu-id="d8136-178">**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **기본** 템플릿을 선택 하 고 선택 된 **뷰 엔진이** **Razor**인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-178">In the **New ASP.NET MVC 4 Project** dialog box select the **Basic** template and make sure that the **View engine** selected is **Razor**.</span></span> <span data-ttu-id="d8136-179">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-179">Click **OK**.</span></span>

    <span data-ttu-id="d8136-180">![New ASP.NET MVC 4 프로젝트 대화 상자](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 프로젝트 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="d8136-180">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="d8136-181">*New ASP.NET MVC 4 프로젝트 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="d8136-181">*New ASP.NET MVC 4 Project Dialog Box*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a><span data-ttu-id="d8136-182">작업 2-솔루션 구조 탐색</span><span class="sxs-lookup"><span data-stu-id="d8136-182">Task 2 - Exploring the Solution Structure</span></span>

<span data-ttu-id="d8136-183">ASP.NET MVC 프레임 워크에는 MVC 패턴을 지 원하는 웹 응용 프로그램을 만드는 데 도움이 되는 Visual Studio 프로젝트 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-183">The ASP.NET MVC framework includes a Visual Studio project template that helps you create Web applications supporting the MVC pattern.</span></span> <span data-ttu-id="d8136-184">이 템플릿은 필수 폴더, 항목 템플릿 및 구성 파일 항목을 사용 하 여 새 ASP.NET MVC 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-184">This template creates a new ASP.NET MVC Web application with the required folders, item templates, and configuration-file entries.</span></span>

<span data-ttu-id="d8136-185">이 작업에서는 솔루션 구조를 검사 하 여 관련 된 요소 및 해당 관계를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-185">In this task, you will examine the solution structure to understand the elements that are involved and their relationships.</span></span> <span data-ttu-id="d8136-186">ASP.NET MVC 프레임 워크는 기본적으로 구성&quot; 접근 방법에 &quot;규칙을 사용 하 고 폴더 명명 규칙에 따라 몇 가지 기본 가정을 만들기 때문에 모든 ASP.NET MVC 응용 프로그램에는 다음 폴더가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-186">The following folders are included in all the ASP.NET MVC application because the ASP.NET MVC framework by default uses a &quot;convention over configuration&quot; approach, and makes some default assumptions based on folder naming conventions.</span></span>

1. <span data-ttu-id="d8136-187">프로젝트를 만든 후에는 오른쪽 솔루션 탐색기에서 생성 된 폴더 구조를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-187">Once the project is created, review the folder structure that has been created in the Solution Explorer on the right side:</span></span>

    <span data-ttu-id="d8136-188">![솔루션 탐색기 ASP.NET MVC 폴더 구조](aspnet-mvc-4-fundamentals/_static/image4.png "솔루션 탐색기 ASP.NET MVC 폴더 구조")</span><span class="sxs-lookup"><span data-stu-id="d8136-188">![ASP.NET MVC Folder structure in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image4.png "ASP.NET MVC Folder structure in Solution Explorer")</span></span>

    <span data-ttu-id="d8136-189">*솔루션 탐색기 ASP.NET MVC 폴더 구조*</span><span class="sxs-lookup"><span data-stu-id="d8136-189">*ASP.NET MVC Folder structure in Solution Explorer*</span></span>

   1. <span data-ttu-id="d8136-190">**컨트롤러**.</span><span class="sxs-lookup"><span data-stu-id="d8136-190">**Controllers**.</span></span> <span data-ttu-id="d8136-191">이 폴더에는 컨트롤러 클래스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-191">This folder will contain the controller classes.</span></span> <span data-ttu-id="d8136-192">MVC 기반 응용 프로그램에서 컨트롤러는 최종 사용자 상호 작용을 처리 하 고, 모델을 조작 하 고, 궁극적으로 UI를 렌더링 하기 위해 뷰를 선택 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-192">In an MVC based application, controllers are responsible for handling end user interaction, manipulating the model, and ultimately choosing a view to render the UI.</span></span>

       > [!NOTE]
       > <span data-ttu-id="d8136-193">MVC 프레임 워크에는 모든 컨트롤러의 이름이 &quot;Controller&quot;(예: HomeController, LoginController 또는 제품 컨트롤러)로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-193">The MVC framework requires the names of all controllers to end with &quot;Controller&quot;-for example, HomeController, LoginController, or ProductController.</span></span>
   2. <span data-ttu-id="d8136-194">**모델**.</span><span class="sxs-lookup"><span data-stu-id="d8136-194">**Models**.</span></span> <span data-ttu-id="d8136-195">이 폴더는 MVC 웹 응용 프로그램에 대 한 응용 프로그램 모델을 나타내는 클래스에 대해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-195">This folder is provided for classes that represent the application model for the MVC Web application.</span></span> <span data-ttu-id="d8136-196">일반적으로 개체를 정의 하는 코드와 데이터 저장소와 상호 작용 하는 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-196">This usually includes code that defines objects and the logic for interacting with the data store.</span></span> <span data-ttu-id="d8136-197">실제 모델 개체의 일반적 위치는 이 폴더가 아니라 별도의 클래스 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-197">Typically, the actual model objects will be in separate class libraries.</span></span> <span data-ttu-id="d8136-198">그러나 새 응용 프로그램을 만들 때 클래스를 포함 한 다음 개발 주기의 이후 시점에서 별도의 클래스 라이브러리로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-198">However, when you create a new application, you might include classes and then move them into separate class libraries at a later point in the development cycle.</span></span>
   3. <span data-ttu-id="d8136-199">**뷰입니다**.</span><span class="sxs-lookup"><span data-stu-id="d8136-199">**Views**.</span></span> <span data-ttu-id="d8136-200">이 폴더는 응용 프로그램의 사용자 인터페이스 표시를 담당 하는 구성 요소인 보기의 권장 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-200">This folder is the recommended location for views, the components responsible for displaying the application's user interface.</span></span> <span data-ttu-id="d8136-201">뷰 렌더링 뷰와 관련 된 다른 모든 파일 뿐만 아니라 .aspx, .ascx, cshtml 및 .master 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-201">Views use .aspx, .ascx, .cshtml and .master files, in addition to any other files that are related to rendering views.</span></span> <span data-ttu-id="d8136-202">Views 폴더에는 각 컨트롤러에 대 한 폴더가 포함 됩니다. 폴더 이름은 컨트롤러 이름 접두사로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-202">Views folder contains a folder for each controller; the folder is named with the controller-name prefix.</span></span> <span data-ttu-id="d8136-203">예를 들어 **HomeController**라는 컨트롤러가 있는 경우 Views 폴더에 Home 이라는 폴더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-203">For example, if you have a controller named **HomeController**, the Views folder will contain a folder named Home.</span></span> <span data-ttu-id="d8136-204">기본적으로 ASP.NET MVC 프레임 워크는 뷰를 로드할 때 Views\controllerName 폴더 (**뷰 [controllerName] [action] .aspx**) 또는 (뷰 **[ControllerName] [action]. cshtml**)에서 요청 된 뷰 이름을 사용 하 여 .aspx 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-204">By default, when the ASP.NET MVC framework loads a view, it looks for an .aspx file with the requested view name in the Views\controllerName folder (**Views[ControllerName][Action].aspx**) or (**Views[ControllerName][Action].cshtml**) for Razor Views.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d8136-205">이전에 나열 된 폴더 외에도 MVC 웹 응용 **프로그램은 global.asax 파일을** 사용 하 여 전역 URL 라우팅 기본값을 설정 하 고 **web.config** 파일을 사용 하 여 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-205">In addition to the folders listed previously, an MVC Web application uses the **Global.asax** file to set global URL routing defaults, and it uses the **Web.config** file to configure the application.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a><span data-ttu-id="d8136-206">작업 3-HomeController 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-206">Task 3 - Adding a HomeController</span></span>

<span data-ttu-id="d8136-207">MVC 프레임 워크를 사용 하지 않는 ASP.NET 응용 프로그램에서 사용자 상호 작용은 페이지를 중심으로 구성 되며 해당 페이지에서 발생 하는 이벤트를 처리 하 고 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-207">In ASP.NET applications that do not use the MVC framework, user interaction is organized around pages, and around raising and handling events from those pages.</span></span> <span data-ttu-id="d8136-208">이와 대조적으로 ASP.NET MVC 응용 프로그램과의 사용자 상호 작용은 컨트롤러와 해당 작업 메서드를 중심으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-208">In contrast, user interaction with ASP.NET MVC applications is organized around controllers and their action methods.</span></span>

<span data-ttu-id="d8136-209">반면에 ASP.NET MVC 프레임 워크는 컨트롤러 라고 하는 클래스에 Url을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-209">On the other hand, ASP.NET MVC framework maps URLs to classes that are referred to as controllers.</span></span> <span data-ttu-id="d8136-210">컨트롤러는 들어오는 요청을 처리 하 고, 사용자 입력 및 상호 작용을 처리 하 고, 적절 한 응용 프로그램 논리를 실행 하 고, 클라이언트에 다시 전송 하는 응답 (HTML 표시, 파일 다운로드, 다른 URL로 리디렉션 등)을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-210">Controllers process incoming requests, handle user input and interactions, execute appropriate application logic and determine the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span> <span data-ttu-id="d8136-211">HTML을 표시 하는 경우 컨트롤러 클래스는 일반적으로 별도의 뷰 구성 요소를 호출 하 여 요청에 대 한 HTML 태그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-211">In the case of displaying HTML, a controller class typically calls a separate view component to generate the HTML markup for the request.</span></span> <span data-ttu-id="d8136-212">MVC 응용 프로그램에서 뷰는 정보만 표시하고 컨트롤러는 사용자 입력에 대한 응답 및 상호 작용을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-212">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="d8136-213">이 작업에서는 Url을 처리 하는 컨트롤러 클래스를 Music Store 사이트의 홈 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-213">In this task, you will add a Controller class that will handle URLs to the Home page of the Music Store site.</span></span>

1. <span data-ttu-id="d8136-214">솔루션 탐색기 내의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **컨트롤러** 명령을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-214">Right-click **Controllers** folder within the Solution Explorer, select **Add** and then **Controller** command:</span></span>

    <span data-ttu-id="d8136-215">![컨트롤러 명령 추가](aspnet-mvc-4-fundamentals/_static/image5.png "컨트롤러 명령 추가")</span><span class="sxs-lookup"><span data-stu-id="d8136-215">![Add a Controller Command](aspnet-mvc-4-fundamentals/_static/image5.png "Add a Controller Command")</span></span>

    <span data-ttu-id="d8136-216">*컨트롤러 추가 명령*</span><span class="sxs-lookup"><span data-stu-id="d8136-216">*Add Controller Command*</span></span>
2. <span data-ttu-id="d8136-217">**컨트롤러 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-217">The **Add Controller** dialog appears.</span></span> <span data-ttu-id="d8136-218">컨트롤러 이름을 *HomeController* 로 하 고 **추가**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-218">Name the controller *HomeController* and press **Add**.</span></span>

    <span data-ttu-id="d8136-219">![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image6.png "컨트롤러 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="d8136-219">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image6.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="d8136-220">*컨트롤러 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="d8136-220">*Add Controller Dialog*</span></span>
3. <span data-ttu-id="d8136-221">**HomeController.cs** 파일이 **Controllers** 폴더에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-221">The file **HomeController.cs** is created in the **Controllers** folder.</span></span> <span data-ttu-id="d8136-222">**HomeController** 가 인덱스 작업에서 문자열을 반환 하도록 하려면 **index** 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-222">In order to have the **HomeController** return a string on its Index action, replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="d8136-223">(코드 조각- *ASP.NET MVC 4 기본-Ex1 HomeController Index*)</span><span class="sxs-lookup"><span data-stu-id="d8136-223">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex1 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="d8136-224">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d8136-224">Task 4 - Running the Application</span></span>

<span data-ttu-id="d8136-225">이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-225">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="d8136-226">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-226">Press **F5** to run the Application.</span></span> <span data-ttu-id="d8136-227">프로젝트가 컴파일되고 로컬 IIS 웹 서버가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-227">The project is compiled and the local IIS Web Server starts.</span></span> <span data-ttu-id="d8136-228">로컬 IIS 웹 서버에서 웹 서버의 URL을 가리키는 웹 브라우저가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-228">The local IIS Web Server will automatically open a web browser pointing to the URL of the Web server.</span></span>

    <span data-ttu-id="d8136-229">![웹 브라우저에서 실행 되는 응용 프로그램](aspnet-mvc-4-fundamentals/_static/image7.png "웹 브라우저에서 실행 되는 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="d8136-229">![Application running in a web browser](aspnet-mvc-4-fundamentals/_static/image7.png "Application running in a web browser")</span></span>

    <span data-ttu-id="d8136-230">*웹 브라우저에서 실행 되는 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="d8136-230">*Application running in a web browser*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8136-231">로컬 IIS 웹 서버는 사용 가능한 임의의 포트 번호를 사용 하 여 웹 사이트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-231">The local IIS Web Server will run the website on a random free port number.</span></span> <span data-ttu-id="d8136-232">위의 그림에서 사이트는 `http://localhost:50103/`에서 실행 되므로 포트 50103를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-232">In the figure above, the site is running at `http://localhost:50103/`, so it's using port 50103.</span></span> <span data-ttu-id="d8136-233">포트 번호는 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-233">Your port number may vary.</span></span>
2. <span data-ttu-id="d8136-234">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-234">Close the browser.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a><span data-ttu-id="d8136-235">연습 2: 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-235">Exercise 2: Creating a Controller</span></span>

<span data-ttu-id="d8136-236">이 연습에서는 Music Store 응용 프로그램의 간단한 기능을 구현 하도록 컨트롤러를 업데이트 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-236">In this exercise, you will learn how to update the controller to implement simple functionality of the Music Store application.</span></span> <span data-ttu-id="d8136-237">해당 컨트롤러는 다음의 각 특정 요청을 처리 하는 작업 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-237">That controller will define action methods to handle each of the following specific requests:</span></span>

- <span data-ttu-id="d8136-238">Music Store의 음악 장르 목록 페이지</span><span class="sxs-lookup"><span data-stu-id="d8136-238">A listing page of the music genres in the Music Store</span></span>
- <span data-ttu-id="d8136-239">특정 장르에 대 한 모든 음악 앨범을 나열 하는 찾아보기 페이지</span><span class="sxs-lookup"><span data-stu-id="d8136-239">A browse page that lists all of the music albums for a particular genre</span></span>
- <span data-ttu-id="d8136-240">특정 음악 앨범에 대 한 정보를 표시 하는 세부 정보 페이지</span><span class="sxs-lookup"><span data-stu-id="d8136-240">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="d8136-241">이 연습의 범위에서 이러한 작업은 단순히 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-241">For the scope of this exercise, those actions will simply return a string by now.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a><span data-ttu-id="d8136-242">작업 1-새 StoreController 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-242">Task 1 - Adding a New StoreController Class</span></span>

<span data-ttu-id="d8136-243">이 작업에서는 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-243">In this task, you will add a new Controller.</span></span>

1. <span data-ttu-id="d8136-244">아직 열려 있지 않으면 **2012 VS Express for Web**시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-244">If not already open, start **VS Express for Web 2012**.</span></span>
2. <span data-ttu-id="d8136-245">**파일** 메뉴에서 **프로젝트 열기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-245">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="d8136-246">프로젝트 열기 대화 상자에서 **Source\Ex02-CreatingAController\Begin**로 이동 하 고 **시작** 을 선택 하 고 **열기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-246">In the Open Project dialog, browse to **Source\Ex02-CreatingAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="d8136-247">또는 이전 연습을 완료 한 후 얻은 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-247">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="d8136-248">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-248">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="d8136-249">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-249">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="d8136-250">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-250">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="d8136-251">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-251">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d8136-252">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-252">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="d8136-253">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-253">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="d8136-254">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-254">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="d8136-255">새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-255">Add the new controller.</span></span> <span data-ttu-id="d8136-256">이렇게 하려면 솔루션 탐색기 내의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **컨트롤러** 명령을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-256">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="d8136-257">**컨트롤러 이름을** *StoreController*로 변경 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-257">Change the **Controller Name** to *StoreController*, and click **Add**.</span></span>

    <span data-ttu-id="d8136-258">![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image8.png "컨트롤러 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="d8136-258">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image8.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="d8136-259">*컨트롤러 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="d8136-259">*Add Controller Dialog*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a><span data-ttu-id="d8136-260">작업 2-StoreController의 작업 수정</span><span class="sxs-lookup"><span data-stu-id="d8136-260">Task 2 - Modifying the StoreController's Actions</span></span>

<span data-ttu-id="d8136-261">이 작업에서는 **작업**이라고 하는 컨트롤러 메서드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-261">In this task, you will modify the Controller methods that are called **actions**.</span></span> <span data-ttu-id="d8136-262">작업은 URL 요청을 처리 하 고 브라우저 또는 URL을 호출한 사용자에 게 다시 보내야 하는 콘텐츠를 결정 하는 작업을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-262">Actions are responsible for handling URL requests and determining the content that should be sent back to the browser or user that invoked the URL.</span></span>

1. <span data-ttu-id="d8136-263">**StoreController** 클래스에는 이미 **인덱스** 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-263">The **StoreController** class already has an **Index** method.</span></span> <span data-ttu-id="d8136-264">이 랩에서 나중에 사용 하 여 음악 상점의 모든 장르를 나열 하는 페이지를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-264">You will use it later in this Lab to implement the page that lists all genres of the music store.</span></span> <span data-ttu-id="d8136-265">지금은 **index** 메서드를 Store. index ()&quot;에서 &quot;Hello 문자열을 반환 하는 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-265">For now, just replace the **Index** method with the following code that returns a string &quot;Hello from Store.Index()&quot;:</span></span>

    <span data-ttu-id="d8136-266">(코드 조각- *ASP.NET MVC 4 기본-Ex2 StoreController Index*)</span><span class="sxs-lookup"><span data-stu-id="d8136-266">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. <span data-ttu-id="d8136-267">**찾아보기** 및 **세부 정보** 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-267">Add **Browse** and **Details** methods.</span></span> <span data-ttu-id="d8136-268">이렇게 하려면 **StoreController**에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-268">To do this, add the following code to the **StoreController**:</span></span>

    <span data-ttu-id="d8136-269">(코드 조각- *ASP.NET MVC 4 기본-Ex2 StoreController BrowseAndDetails*)</span><span class="sxs-lookup"><span data-stu-id="d8136-269">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController BrowseAndDetails*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="d8136-270">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d8136-270">Task 3 - Running the Application</span></span>

<span data-ttu-id="d8136-271">이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-271">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="d8136-272">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-272">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d8136-273">프로젝트가 **홈** 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-273">The project starts in the **Home** page.</span></span> <span data-ttu-id="d8136-274">URL을 변경 하 여 각 작업의 구현을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-274">Change the URL to verify each action's implementation.</span></span>

    1. <span data-ttu-id="d8136-275">**/Store**.</span><span class="sxs-lookup"><span data-stu-id="d8136-275">**/Store**.</span></span> <span data-ttu-id="d8136-276">**Store. Index ()&quot;에서&quot;Hello** 가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-276">You will see **&quot;Hello from Store.Index()&quot;**.</span></span>
    2. <span data-ttu-id="d8136-277">**/Svers를 찾습니다**.</span><span class="sxs-lookup"><span data-stu-id="d8136-277">**/Store/Browse**.</span></span> <span data-ttu-id="d8136-278">**Store. Browse ()&quot;에서&quot;Hello** 가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-278">You will see **&quot;Hello from Store.Browse()&quot;**.</span></span>
    3. <span data-ttu-id="d8136-279">**/Sv/ds/자세히**입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-279">**/Store/Details**.</span></span> <span data-ttu-id="d8136-280">**Store. Details ()&quot;에서&quot;Hello** 가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-280">You will see **&quot;Hello from Store.Details()&quot;**.</span></span>

        <span data-ttu-id="d8136-281">![검색 방법 찾아보기](aspnet-mvc-4-fundamentals/_static/image9.png "검색 방법 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="d8136-281">![Browsing StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Browsing StoreBrowse")</span></span>

        <span data-ttu-id="d8136-282">*검색/이동/찾아보기*</span><span class="sxs-lookup"><span data-stu-id="d8136-282">*Browsing /Store/Browse*</span></span>
3. <span data-ttu-id="d8136-283">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-283">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a><span data-ttu-id="d8136-284">연습 3: 컨트롤러에 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="d8136-284">Exercise 3: Passing parameters to a Controller</span></span>

<span data-ttu-id="d8136-285">지금까지 컨트롤러에서 상수 문자열을 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-285">Until now, you have been returning constant strings from the Controllers.</span></span> <span data-ttu-id="d8136-286">이 연습에서는 URL 및 querystring을 사용 하 여 매개 변수를 컨트롤러에 전달한 다음 메서드 작업이 텍스트를 사용 하 여 브라우저에 응답 하 게 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-286">In this exercise you will learn how to pass parameters to a Controller using the URL and querystring, and then making the method actions respond with text to the browser.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a><span data-ttu-id="d8136-287">작업 1-StoreController에 장르 매개 변수 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-287">Task 1 - Adding Genre Parameter to StoreController</span></span>

<span data-ttu-id="d8136-288">이 태스크에서는 **querystring** 을 사용 하 여 **StoreController**의 **Browse** 동작 메서드에 매개 변수를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-288">In this task, you will use the **querystring** to send parameters to the **Browse** action method in the **StoreController**.</span></span>

1. <span data-ttu-id="d8136-289">아직 열려 있지 않은 경우 **VS Express for Web**를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-289">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="d8136-290">**파일** 메뉴에서 **프로젝트 열기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-290">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="d8136-291">프로젝트 열기 대화 상자에서 **Source\Ex03-PassingParametersToAController\Begin**로 이동 하 고 **시작** 을 선택 하 고 **열기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-291">In the Open Project dialog, browse to **Source\Ex03-PassingParametersToAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="d8136-292">또는 이전 연습을 완료 한 후 얻은 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-292">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="d8136-293">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-293">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="d8136-294">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-294">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="d8136-295">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-295">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="d8136-296">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-296">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d8136-297">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-297">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="d8136-298">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-298">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="d8136-299">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-299">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="d8136-300">**StoreController** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-300">Open **StoreController** class.</span></span> <span data-ttu-id="d8136-301">이렇게 하려면 **솔루션 탐색기**에서 **Controllers** 폴더를 확장 하 고 **StoreController.cs**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-301">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
4. <span data-ttu-id="d8136-302">**찾아보기** 메서드를 변경 하 여 특정 장르를 요청 하는 문자열 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-302">Change the **Browse** method, adding a string parameter to request for a specific genre.</span></span> <span data-ttu-id="d8136-303">ASP.NET MVC는 호출 될 때 **장르** 라는 모든 querystring 또는 폼 post 매개 변수를이 작업 메서드에 자동으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-303">ASP.NET MVC will automatically pass any querystring or form post parameters named **genre** to this action method when invoked.</span></span> <span data-ttu-id="d8136-304">이렇게 하려면 **Browse** 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-304">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="d8136-305">(코드 조각- *ASP.NET MVC 4 기본-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="d8136-305">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="d8136-306">사용자가 **HtmlEncode** 유틸리티 메서드를 사용 하 여 사용자가/sv/dherer>와 같은 링크를 사용 하 여 Javascript를 뷰에 삽입 하지 못하도록 합니다.  **장르 =&lt;스크립트&gt;창. location = '[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;** .</span><span class="sxs-lookup"><span data-stu-id="d8136-306">You are using the **HttpUtility.HtmlEncode** utility method to prevents users from injecting Javascript into the View with a link like **/Store/Browse?Genre=&lt;script&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.</span></span>
> 
> <span data-ttu-id="d8136-307">자세한 설명은 [이 msdn 문서](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d8136-307">For further explanation, please visit [this msdn article](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="d8136-308">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d8136-308">Task 2 - Running the Application</span></span>

<span data-ttu-id="d8136-309">이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 보고 **장르** 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-309">In this task, you will try out the Application in a web browser and use the **genre** parameter.</span></span>

1. <span data-ttu-id="d8136-310">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-310">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d8136-311">프로젝트가 **홈** 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-311">The project starts in the **Home** page.</span></span> <span data-ttu-id="d8136-312">URL을/Svs\hers로 변경 *하 시겠습니까? 장르 = Disco* 작업에서 장르 매개 변수를 수신 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-312">Change the URL to */Store/Browse?Genre=Disco* to verify that the action receives the genre parameter.</span></span>

    <span data-ttu-id="d8136-313">![StoreBrowseGenre = Disco 찾아보기](aspnet-mvc-4-fundamentals/_static/image10.png "StoreBrowseGenre = Disco 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="d8136-313">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span></span>

    <span data-ttu-id="d8136-314">*검색/선택/찾아보기 장르 = Disco*</span><span class="sxs-lookup"><span data-stu-id="d8136-314">*Browsing /Store/Browse?Genre=Disco*</span></span>
3. <span data-ttu-id="d8136-315">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-315">Close the browser.</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a><span data-ttu-id="d8136-316">작업 3-URL에 포함 된 Id 매개 변수 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-316">Task 3 - Adding an Id Parameter Embedded in the URL</span></span>

<span data-ttu-id="d8136-317">이 태스크에서는 **URL** 을 사용 하 여 **StoreController**의 **Details** action 메서드에 **Id** 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-317">In this task, you will use the **URL** to pass an **Id** parameter to the **Details** action method of the **StoreController**.</span></span> <span data-ttu-id="d8136-318">ASP.NET MVC의 기본 라우팅 규칙은 작업 메서드 이름 뒤에 있는 URL의 세그먼트를 **Id**라는 매개 변수로 처리 하는 것입니다. 작업 메서드에 이름이 Id 인 매개 변수가 있는 경우 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-318">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named **Id**. If your action method has parameter named Id, then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span> <span data-ttu-id="d8136-319">URL **저장소/세부 정보/5**에서 **Id** 는 **5**로 해석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-319">In the URL **Store/Details/5**, **Id** will be interpreted as **5**.</span></span>

1. <span data-ttu-id="d8136-320">**Id**라는 **int** 매개 변수를 추가 하 여 **StoreController**의 **세부 정보** 메서드를 변경 합니다. 이렇게 하려면 **Details** 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-320">Change the **Details** method of the **StoreController**, adding an **int** parameter called **id**. To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="d8136-321">(코드 조각- *ASP.NET MVC 4 기본-Ex3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="d8136-321">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="d8136-322">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d8136-322">Task 4 - Running the Application</span></span>

<span data-ttu-id="d8136-323">이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 보고 **Id** 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-323">In this task, you will try out the Application in a web browser and use the **Id** parameter.</span></span>

1. <span data-ttu-id="d8136-324">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-324">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d8136-325">프로젝트가 **홈** 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-325">The project starts in the **Home** page.</span></span> <span data-ttu-id="d8136-326">URL을 */Store/Details/5* 로 변경 하 여 동작에서 id 매개 변수를 수신 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-326">Change the URL to */Store/Details/5* to verify that the action receives the id parameter.</span></span>

    <span data-ttu-id="d8136-327">![StoreDetails5 찾아보기](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="d8136-327">![Browsing StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Browsing StoreDetails5")</span></span>

    <span data-ttu-id="d8136-328">*/Store/Details/5 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="d8136-328">*Browsing /Store/Details/5*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a><span data-ttu-id="d8136-329">연습 4: 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-329">Exercise 4: Creating a View</span></span>

<span data-ttu-id="d8136-330">지금까지 컨트롤러 작업에서 문자열을 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-330">So far you have been returning strings from controller actions.</span></span> <span data-ttu-id="d8136-331">이는 컨트롤러의 작동 방식을 이해 하는 데 유용한 방법 이지만 실제 웹 응용 프로그램을 빌드하는 방법은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-331">Although that is a useful way of understanding how controllers work, it is not how your real Web applications are built.</span></span> <span data-ttu-id="d8136-332">뷰는 템플릿 파일을 사용 하 여 브라우저에 다시 HTML을 생성 하는 더 나은 방법을 제공 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-332">Views are components that provide a better approach for generating HTML back to the browser with the use of template files.</span></span>

<span data-ttu-id="d8136-333">이 연습에서는 사이트의 모양과 느낌을 개선 하는 스타일 시트를 사용 하 여 공용 HTML 콘텐츠에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법과 HomeController에서 HTML을 반환 하도록 하는 뷰 템플릿을 설정 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-333">In this exercise you will learn how to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel of the site and finally a View template to enable HomeController to return HTML.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a><span data-ttu-id="d8136-334">작업 1-파일 \_레이아웃 수정. cshtml</span><span class="sxs-lookup"><span data-stu-id="d8136-334">Task 1 - Modifying the file \_layout.cshtml</span></span>

<span data-ttu-id="d8136-335">File **~/Views/Shared/\_layout. cshtml** 를 사용 하면 전체 웹 사이트에서 사용할 공통 HTML 용 템플릿을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-335">The file **~/Views/Shared/\_layout.cshtml** allows you to setup a template for common HTML to use across the entire website.</span></span> <span data-ttu-id="d8136-336">이 작업에서는 홈 페이지 및 상점 영역에 대 한 링크가 포함 된 공통 머리글을 사용 하 여 레이아웃 마스터 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-336">In this task you will add a layout master page with a common header with links to the Home page and Store area.</span></span>

1. <span data-ttu-id="d8136-337">아직 열려 있지 않은 경우 **VS Express for Web**를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-337">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="d8136-338">**파일** 메뉴에서 **프로젝트 열기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-338">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="d8136-339">프로젝트 열기 대화 상자에서 **Source\ex04-creatingaview\begin**으로 이동 하 여 **begin .sln** 을 선택 하 고 **열기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-339">In the Open Project dialog, browse to **Source\Ex04-CreatingAView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="d8136-340">또는 이전 연습을 완료 한 후 얻은 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-340">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="d8136-341">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-341">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="d8136-342">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-342">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="d8136-343">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-343">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="d8136-344">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-344">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d8136-345">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-345">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="d8136-346">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-346">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="d8136-347">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-347">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="d8136-348">파일 <strong>\_레이아웃. cshtml</strong> 에는 사이트의 모든 페이지에 대 한 HTML 컨테이너 레이아웃이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-348">The file <strong>\_layout.cshtml</strong> contains the HTML container layout for all pages on the site.</span></span> <span data-ttu-id="d8136-349">HTML 응답에 대 한 <strong>&lt;html&gt;</strong> 요소 뿐만 아니라 <strong>&lt;head&gt;</strong> 및 <strong>&lt;body&gt;</strong> 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-349">It includes the <strong>&lt;html&gt;</strong> element for the HTML response, as well as the <strong>&lt;head&gt;</strong> and <strong>&lt;body&gt;</strong> elements.</span></span> <span data-ttu-id="d8136-350">HTML 본문 내의 <strong>@RenderBody()</strong> 는 보기 템플릿을 통해 동적 콘텐츠로 채울 수 있는 영역을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-350"><strong>@RenderBody()</strong> within the HTML body identify regions that view templates will be able to fill in with dynamic content.</span></span>
   <span data-ttu-id="d8136-351">(C#)</span><span class="sxs-lookup"><span data-stu-id="d8136-351">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. <span data-ttu-id="d8136-352">홈 페이지에 대 한 링크가 포함 된 공통 헤더를 추가 하 고 사이트의 모든 페이지에 저장 영역을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-352">Add a common header with links to the Home page and Store area on all pages in the site.</span></span> <span data-ttu-id="d8136-353">이 작업을 수행 하려면 &lt;body&gt; 문 아래에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-353">In order to do that, add the following code below &lt;body&gt; statement.</span></span>
   <span data-ttu-id="d8136-354">(C#)</span><span class="sxs-lookup"><span data-stu-id="d8136-354">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. <span data-ttu-id="d8136-355">각 페이지의 본문 구역을 렌더링 하려면 div를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-355">Include a div to render the body section of each page.</span></span> <span data-ttu-id="d8136-356"><strong>@RenderBody()</strong> 를 강조 표시 된 다음 코드로 바꿉니다.C#()</span><span class="sxs-lookup"><span data-stu-id="d8136-356">Replace <strong>@RenderBody()</strong> with the following highlighted code: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="d8136-357">알고 계십니까?</span><span class="sxs-lookup"><span data-stu-id="d8136-357">Did you know?</span></span> <span data-ttu-id="d8136-358">Visual Studio 2012에는 HTML, 코드 파일 등에서 자주 사용 되는 코드를 쉽게 추가할 수 있도록 하는 코드 조각이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-358">Visual Studio 2012 has snippets that make it easy to add commonly used code in HTML, code files and more!</span></span> <span data-ttu-id="d8136-359">**&lt;div&gt;** 를 입력 하 고 **tab** 키를 두 번 눌러서 전체 **div** 태그를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-359">Try it out by typing **&lt;div&gt;** and pressing **TAB** twice to insert a complete **div** tag.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a><span data-ttu-id="d8136-360">작업 2-CSS 스타일 시트 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-360">Task 2 - Adding CSS Stylesheet</span></span>

<span data-ttu-id="d8136-361">빈 프로젝트 템플릿에는 기본 폼 및 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-361">The empty project template includes a very streamlined CSS file which just includes styles used to display basic forms and validation messages.</span></span> <span data-ttu-id="d8136-362">사이트의 모양과 느낌을 향상 시키기 위해 디자이너에서 제공 하는 추가 CSS 및 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-362">You will use additional CSS and images (potentially provided by a designer) in order to enhance the look and feel of the site.</span></span>

<span data-ttu-id="d8136-363">이 태스크에서는 CSS 스타일 시트를 추가 하 여 사이트의 스타일을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-363">In this task, you will add a CSS stylesheet to define the styles of the site.</span></span>

1. <span data-ttu-id="d8136-364">CSS 파일 및 이미지는이 랩의 **Source\assets\content** 폴더에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-364">The CSS file and images are included in the **Source\Assets\Content** folder of this Lab.</span></span> <span data-ttu-id="d8136-365">응용 프로그램에 추가 하려면 아래와 같이 **Windows 탐색기** 창에서 웹에 대 한 Visual Studio Express의 **솔루션 탐색기** 로 해당 콘텐츠를 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-365">In order to add them to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Studio Express for Web, as shown below:</span></span>

    <span data-ttu-id="d8136-366">![스타일 내용 끌기](aspnet-mvc-4-fundamentals/_static/image12.png "스타일 내용 끌기")</span><span class="sxs-lookup"><span data-stu-id="d8136-366">![Dragging style contents](aspnet-mvc-4-fundamentals/_static/image12.png "Dragging style contents")</span></span>

    <span data-ttu-id="d8136-367">*스타일 내용 끌기*</span><span class="sxs-lookup"><span data-stu-id="d8136-367">*Dragging style contents*</span></span>
2. <span data-ttu-id="d8136-368">**사이트 .css** 파일 및 일부 기존 이미지를 바꾸도록 확인 하는 경고 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-368">A warning dialog will appear, asking for confirmation to replace **Site.css** file and some existing images.</span></span> <span data-ttu-id="d8136-369">**모든 항목에 적용을** 선택 하 고 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-369">Check **Apply to all items** and click **Yes**.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a><span data-ttu-id="d8136-370">작업 3-보기 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-370">Task 3 - Adding a View Template</span></span>

<span data-ttu-id="d8136-371">이 작업에서는 뷰 템플릿을 추가 하 여이 연습에서 추가 된 레이아웃 마스터 페이지 및 CSS를 사용 하는 HTML 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-371">In this task, you will add a View template to generate the HTML response that will use the layout master page and CSS added in this exercise.</span></span>

1. <span data-ttu-id="d8136-372">사이트의 홈 페이지를 검색할 때 보기 템플릿을 사용 하려면 먼저 문자열을 반환 하는 대신 **HomeController Index** 메서드를 사용 하 여 **뷰**를 반환 하도록 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-372">To use a View template when browsing the site's home page, you will first need to indicate that instead of returning a string, the **HomeController Index** method will return a **View**.</span></span> <span data-ttu-id="d8136-373">**HomeController** 클래스를 열고 **Index** 메서드를 변경 하 여 **Actionresult**를 반환 하 고 **View ()** 를 반환 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-373">Open **HomeController** class and change its **Index** method to return an **ActionResult**, and have it return **View()**.</span></span>

    <span data-ttu-id="d8136-374">(코드 조각- *ASP.NET MVC 4 기본-Ex4 HomeController Index*)</span><span class="sxs-lookup"><span data-stu-id="d8136-374">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex4 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. <span data-ttu-id="d8136-375">이제 적절 한 뷰 템플릿을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-375">Now, you need to add an appropriate View template.</span></span> <span data-ttu-id="d8136-376">이렇게 하려면 **인덱스** 동작 메서드 내부를 **마우스 오른쪽 단추로 클릭** 하 고 **뷰 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-376">To do this, **right-click** inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="d8136-377">그러면 **보기 추가** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-377">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="d8136-378">![Index 메서드 내에서 뷰 추가](aspnet-mvc-4-fundamentals/_static/image13.png "Index 메서드 내에서 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="d8136-378">![Adding a View from within the Index method](aspnet-mvc-4-fundamentals/_static/image13.png "Adding a View from within the Index method")</span></span>

    <span data-ttu-id="d8136-379">*Index 메서드 내에서 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="d8136-379">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="d8136-380">뷰 **추가** 대화 상자가 표시 되 면 뷰 템플릿 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-380">The **Add View** Dialog will appear to generate a View template file.</span></span> <span data-ttu-id="d8136-381">기본적으로이 대화 상자는 뷰 템플릿의 이름을 미리 채워이를 사용 하는 작업 메서드와 일치 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-381">By default, this dialog pre-populates the name of the View template so that it matches the action method that will use it.</span></span> <span data-ttu-id="d8136-382">HomeController 내의 **index** 동작 메서드 내에서 **뷰 추가** 상황에 맞는 메뉴를 사용 했기 때문에 **뷰 추가** 대화 상자에는 기본 뷰 이름으로 인덱스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-382">Because you used the **Add View** context menu within the **Index** action method within the HomeController, the **Add View** dialog has Index as the default view name.</span></span> <span data-ttu-id="d8136-383">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-383">Click **Add**.</span></span>

    <span data-ttu-id="d8136-384">![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image14.png "뷰 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="d8136-384">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image14.png "Add View Dialog")</span></span>

    <span data-ttu-id="d8136-385">*뷰 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="d8136-385">*Add View Dialog*</span></span>
4. <span data-ttu-id="d8136-386">Visual Studio는 **Views\Home** 폴더 안에 **Index. cshtml** 뷰 템플릿을 생성 한 다음 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-386">Visual Studio generates an **Index.cshtml** view template inside the **Views\Home** folder and then opens it.</span></span>

    <span data-ttu-id="d8136-387">![만든 홈 인덱스 보기](aspnet-mvc-4-fundamentals/_static/image15.png "만든 홈 인덱스 보기")</span><span class="sxs-lookup"><span data-stu-id="d8136-387">![Home Index view created](aspnet-mvc-4-fundamentals/_static/image15.png "Home Index view created")</span></span>

    <span data-ttu-id="d8136-388">*만든 홈 인덱스 보기*</span><span class="sxs-lookup"><span data-stu-id="d8136-388">*Home Index view created*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8136-389">인덱스의 이름 및 위치입니다 **. cshtml** 파일은 관련 되며 기본 ASP.NET MVC 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-389">name and location of the **Index.cshtml** file is relevant and follows the default ASP.NET MVC naming conventions.</span></span>
    > 
    > <span data-ttu-id="d8136-390">\Views\**홈*\* 폴더는 컨트롤러 이름 (**홈** 컨트롤러)과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-390">The folder \Views\**Home*\* matches the controller name (**Home** Controller).</span></span> <span data-ttu-id="d8136-391">뷰 템플릿 이름 (**인덱스**)은 뷰를 표시 하는 컨트롤러 작업 메서드와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-391">The View template name (**Index**), matches the controller action method which will be displaying the View.</span></span>
    > 
    > <span data-ttu-id="d8136-392">이러한 방식으로 ASP.NET MVC는이 명명 규칙을 사용 하 여 뷰를 반환할 때 뷰 템플릿의 이름이 나 위치를 명시적으로 지정 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-392">This way, ASP.NET MVC avoids having to explicitly specify the name or location of a View template when using this naming convention to return a View.</span></span>
5. <span data-ttu-id="d8136-393">생성 된 뷰 템플릿은\_레이아웃을 기반으로 **합니다. cshtml** 템플릿 이전에 정의 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-393">The generated View template is based on the **\_layout.cshtml** template earlier defined.</span></span> <span data-ttu-id="d8136-394">아래 코드에 표시 된 것 처럼 ViewBag 속성을 **home**으로 업데이트 하 고, 기본 콘텐츠를 **이 홈 페이지**로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-394">Update the ViewBag.Title property to **Home**, and change the main content to **This is the Home Page**, as shown in the code below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. <span data-ttu-id="d8136-395">솔루션 탐색기에서 **MvcMusicStore** 프로젝트를 선택 하 고 **F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-395">Select **MvcMusicStore** project in the Solution Explorer and Press **F5** to run the Application.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a><span data-ttu-id="d8136-396">작업 4: 확인</span><span class="sxs-lookup"><span data-stu-id="d8136-396">Task 4: Verification</span></span>

<span data-ttu-id="d8136-397">이전 연습에서 모든 단계를 올바르게 수행 했는지 확인 하려면 다음과 같이 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-397">In order to verify that you have correctly performed all the steps in the previous exercise, proceed as follows:</span></span>

<span data-ttu-id="d8136-398">응용 프로그램이 브라우저에서 열리면 다음 사항을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-398">With the application opened in a browser, you should note that:</span></span>

1. <span data-ttu-id="d8136-399">뷰 템플릿이 표준 명명 규칙을 준수 하기 때문에 HomeController의 인덱스 작업 메서드가 **반환 뷰 ()** 를 호출 하는 경우에도 **\Views\Home\Index.cshtml** view 템플릿을 찾아 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-399">The HomeController's Index action method found and displayed the **\Views\Home\Index.cshtml** View template, even though the code called **return View()**, because the View template followed the standard naming convention.</span></span>
2. <span data-ttu-id="d8136-400">홈 페이지에는 **\Views\Home\Index.cshtml** view 템플릿 내에 정의 된 환영 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-400">The Home Page displays the welcome message defined within the **\Views\Home\Index.cshtml** view template.</span></span>
3. <span data-ttu-id="d8136-401">홈 페이지는 **\_레이아웃** 을 사용 하 고 있으므로 시작 메시지는 표준 사이트 HTML 레이아웃에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-401">The Home Page is using the **\_layout.cshtml** template, and so the welcome message is contained within the standard site HTML layout.</span></span>

    <span data-ttu-id="d8136-402">![정의 된 LayoutPage 및 style을 사용 하는 홈 인덱스 보기](aspnet-mvc-4-fundamentals/_static/image16.png "정의 된 LayoutPage 및 style을 사용 하는 홈 인덱스 보기")</span><span class="sxs-lookup"><span data-stu-id="d8136-402">![Home Index View using the defined LayoutPage and style](aspnet-mvc-4-fundamentals/_static/image16.png "Home Index View using the defined LayoutPage and style")</span></span>

    <span data-ttu-id="d8136-403">*정의 된 LayoutPage 및 style을 사용 하는 홈 인덱스 보기*</span><span class="sxs-lookup"><span data-stu-id="d8136-403">*Home Index View using the defined LayoutPage and style*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a><span data-ttu-id="d8136-404">연습 5: 뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-404">Exercise 5: Creating a View Model</span></span>

<span data-ttu-id="d8136-405">지금 까지는 뷰가 하드 코드 된 HTML을 표시 하지만 동적 웹 응용 프로그램을 만들기 위해 뷰 템플릿이 컨트롤러에서 정보를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-405">So far, you made your Views display hardcoded HTML, but, in order to create dynamic web applications, the View template should receive information from the Controller.</span></span> <span data-ttu-id="d8136-406">이러한 목적으로 사용 되는 일반적인 방법 중 하나는 컨트롤러에서 적절 한 HTML 응답을 생성 하는 데 필요한 모든 정보를 패키지할 수 있도록 하는 **ViewModel** 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-406">One common technique to be used for that purpose is the **ViewModel** pattern, which allows a Controller to package up all the information needed to generate the appropriate HTML response.</span></span>

<span data-ttu-id="d8136-407">이 연습에서는 ViewModel 클래스를 만들고 필요한 속성을 추가 하는 방법에 대해 알아봅니다. 스토어의 장르 수와 해당 장르 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-407">In this exercise, you will learn how to create a ViewModel class and add the required properties: the number of genres in the store and a list of those genres.</span></span> <span data-ttu-id="d8136-408">또한 생성 된 ViewModel을 사용 하도록 StoreController을 업데이트 하 고, 마지막으로 페이지에 언급 된 속성을 표시 하는 새 뷰 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-408">You will also update the StoreController to use the created ViewModel, and finally, you will create a new View template that will display the mentioned properties in the page.</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a><span data-ttu-id="d8136-409">작업 1-ViewModel 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-409">Task 1 - Creating a ViewModel Class</span></span>

<span data-ttu-id="d8136-410">이 작업에서는 스토어 장르 목록 시나리오를 구현 하는 ViewModel 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-410">In this task, you will create a ViewModel class that will implement the Store genre listing scenario.</span></span>

1. <span data-ttu-id="d8136-411">아직 열려 있지 않은 경우 **VS Express for Web**를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-411">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="d8136-412">**파일** 메뉴에서 **프로젝트 열기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-412">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="d8136-413">프로젝트 열기 대화 상자에서 **Source\ex05-creatingaviewmodel\begin**으로 이동 하 여 **begin .sln** 을 선택 하 고 **열기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-413">In the Open Project dialog, browse to **Source\Ex05-CreatingAViewModel\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="d8136-414">또는 이전 연습을 완료 한 후 얻은 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-414">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="d8136-415">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-415">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="d8136-416">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-416">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="d8136-417">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-417">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="d8136-418">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-418">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d8136-419">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-419">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="d8136-420">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-420">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="d8136-421">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-421">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="d8136-422">ViewModel을 보관할 **Viewmodels** 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-422">Create a **ViewModels** folder to hold the ViewModel.</span></span> <span data-ttu-id="d8136-423">이렇게 하려면 최상위 **MvcMusicStore** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **새 폴더**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-423">To do this, right-click the top-level **MvcMusicStore** project, select **Add** and then **New Folder**.</span></span>

    <span data-ttu-id="d8136-424">![새 폴더 추가](aspnet-mvc-4-fundamentals/_static/image17.png "새 폴더 추가")</span><span class="sxs-lookup"><span data-stu-id="d8136-424">![Adding a new folder](aspnet-mvc-4-fundamentals/_static/image17.png "Adding a new folder")</span></span>

    <span data-ttu-id="d8136-425">*새 폴더 추가*</span><span class="sxs-lookup"><span data-stu-id="d8136-425">*Adding a new folder*</span></span>
4. <span data-ttu-id="d8136-426">폴더 이름을 *Viewmodels*으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-426">Name the folder *ViewModels*.</span></span>

    <span data-ttu-id="d8136-427">![솔루션 탐색기의 ViewModels 폴더](aspnet-mvc-4-fundamentals/_static/image18.png "솔루션 탐색기의 ViewModels 폴더")</span><span class="sxs-lookup"><span data-stu-id="d8136-427">![ViewModels folder in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels folder in Solution Explorer")</span></span>

    <span data-ttu-id="d8136-428">*솔루션 탐색기의 ViewModels 폴더*</span><span class="sxs-lookup"><span data-stu-id="d8136-428">*ViewModels folder in Solution Explorer*</span></span>
5. <span data-ttu-id="d8136-429">**ViewModel** 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-429">Create a **ViewModel** class.</span></span> <span data-ttu-id="d8136-430">이렇게 하려면 최근에 만든 **Viewmodels** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** , **새 항목**을 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-430">To do this, right-click on the **ViewModels** folder recently created, select **Add** and then **New Item**.</span></span> <span data-ttu-id="d8136-431">**코드**에서 **클래스** 항목을 선택 하 고 파일 이름을 *StoreIndexViewModel.cs*으로 지정한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-431">Under **Code**, choose the **Class** item and name the file *StoreIndexViewModel.cs*, then click **Add**.</span></span>

    <span data-ttu-id="d8136-432">![새 클래스 추가](aspnet-mvc-4-fundamentals/_static/image19.png "새 클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="d8136-432">![Adding a new Class](aspnet-mvc-4-fundamentals/_static/image19.png "Adding a new Class")</span></span>

    <span data-ttu-id="d8136-433">*새 클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="d8136-433">*Adding a new Class*</span></span>

    <span data-ttu-id="d8136-434">![이 클래스 만들기](aspnet-mvc-4-fundamentals/_static/image20.png "이 클래스 만들기")</span><span class="sxs-lookup"><span data-stu-id="d8136-434">![Creating StoreIndexViewModel class](aspnet-mvc-4-fundamentals/_static/image20.png "Creating StoreIndexViewModel class")</span></span>

    <span data-ttu-id="d8136-435">*이 클래스 만들기*</span><span class="sxs-lookup"><span data-stu-id="d8136-435">*Creating StoreIndexViewModel class*</span></span>

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a><span data-ttu-id="d8136-436">작업 2-ViewModel 클래스에 속성 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-436">Task 2 - Adding Properties to the ViewModel class</span></span>

<span data-ttu-id="d8136-437">예상 되는 HTML 응답을 생성 하기 위해 StoreController에서 뷰 템플릿으로 전달 되는 두 개의 매개 변수 (매장의 장르 수와 해당 장르 목록)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-437">There are two parameters to be passed from the StoreController to the View template in order to generate the expected HTML response: the number of genres in the store and a list of those genres.</span></span>

<span data-ttu-id="d8136-438">이 태스크에서는 해당 2 개의 속성을 **사용자의 사용자** 속성: **numberofgenres** (정수) 및 **장르** (문자열 목록)에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-438">In this task, you will add those 2 properties to the **StoreIndexViewModel** class: **NumberOfGenres** (an integer) and **Genres** (a list of strings).</span></span>

1. <span data-ttu-id="d8136-439">이 클래스에 **numberofgenres** 및 **장르** 속성을 **추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d8136-439">Add **NumberOfGenres** and **Genres** properties to the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="d8136-440">이렇게 하려면 클래스 정의에 다음 두 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-440">To do this, add the following 2 lines to the class definition:</span></span>

    <span data-ttu-id="d8136-441">(코드 조각- *ASP.NET MVC 4 기본-Ex5 StoreIndexViewModel 속성*)</span><span class="sxs-lookup"><span data-stu-id="d8136-441">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> <span data-ttu-id="d8136-442">**{Get; set;}** 표기법은의 자동 구현 C#속성 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-442">The **{ get; set; }** notation makes use of C#'s auto-implemented properties feature.</span></span> <span data-ttu-id="d8136-443">지원 필드를 선언 하지 않고도 속성의 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-443">It provides the benefits of a property without requiring us to declare a backing field.</span></span>

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a><span data-ttu-id="d8136-444">작업 3-StoreController Indexviewmodel을 사용 하도록 업데이트</span><span class="sxs-lookup"><span data-stu-id="d8136-444">Task 3 - Updating StoreController to use the StoreIndexViewModel</span></span>

<span data-ttu-id="d8136-445">StoreController **Indexviewmodel** 클래스는 응답을 생성 하기 위해의 **인덱스** 메서드를 뷰 템플릿으로 전달 하는 데 필요한 정보를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-445">The **StoreIndexViewModel** class encapsulates the information needed to pass from **StoreController**'s **Index** method to a View template in order to generate a response.</span></span>

<span data-ttu-id="d8136-446">이 작업에서는 **StoreController** **인덱스 viewmodel**을 사용 하도록 해당 사용자를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-446">In this task, you will update the **StoreController** to use the **StoreIndexViewModel**.</span></span>

1. <span data-ttu-id="d8136-447">**StoreController** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-447">Open **StoreController** class.</span></span>

    <span data-ttu-id="d8136-448">![StoreController 클래스 열기](aspnet-mvc-4-fundamentals/_static/image21.png "StoreController 클래스 열기")</span><span class="sxs-lookup"><span data-stu-id="d8136-448">![Opening StoreController class](aspnet-mvc-4-fundamentals/_static/image21.png "Opening StoreController class")</span></span>

    <span data-ttu-id="d8136-449">*StoreController 클래스 열기*</span><span class="sxs-lookup"><span data-stu-id="d8136-449">*Opening StoreController class*</span></span>
2. <span data-ttu-id="d8136-450">**StoreController에서** **indexviewmodel** 클래스를 사용 하려면 **StoreController** 코드의 맨 위에 다음 네임 스페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-450">In order to use the **StoreIndexViewModel** class from the **StoreController**, add the following namespace at the top of the **StoreController** code:</span></span>

    <span data-ttu-id="d8136-451">(코드 조각- *ASP.NET MVC 4 기본 사항-ViewModels을 사용 하 여 Ex5 StoreIndexViewModel*)</span><span class="sxs-lookup"><span data-stu-id="d8136-451">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel using ViewModels*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. <span data-ttu-id="d8136-452">**StoreController**의 **Index** 동작 메서드를 변경 하 여이 개체를 만들고이 **개체를 뷰** 템플릿에 전달 하 여 HTML 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-452">Change the **StoreController**'s **Index** action method so that it creates and populates a **StoreIndexViewModel** object and then passes it off to a View template to generate an HTML response with it.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8136-453">Lab &quot;ASP.NET MVC 모델 및 데이터 액세스&quot; 데이터베이스에서 스토어 장르 목록을 검색 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-453">In Lab &quot;ASP.NET MVC Models and Data Access&quot; you will write code that retrieves the list of store genres from a database.</span></span> <span data-ttu-id="d8136-454">다음 코드에서는 복사본 **인덱스 viewmodel**을 채울 더미 데이터 장르 **목록을** 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-454">In the following code, you will create a **List** of dummy data genres that will populate the **StoreIndexViewModel**.</span></span>
    > 
    > <span data-ttu-id="d8136-455">이 개체를 만들고 설정 하면 **해당 개체는** **뷰** 메서드에 인수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-455">After creating and setting up the **StoreIndexViewModel** object, it will be passed as an argument to the **View** method.</span></span> <span data-ttu-id="d8136-456">이는 뷰 템플릿에서 해당 개체를 사용 하 여 HTML 응답을 생성 한다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-456">This indicates that the View template will use that object to generate an HTML response with it.</span></span>
4. <span data-ttu-id="d8136-457">**Index** 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-457">Replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="d8136-458">(코드 조각- *ASP.NET MVC 4 기본-Ex5 StoreController Index 메서드*)</span><span class="sxs-lookup"><span data-stu-id="d8136-458">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreController Index method*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> <span data-ttu-id="d8136-459">에 C#익숙하지 않은 경우 **var** 을 사용 한다고 해 서 **viewModel** 변수가 런타임에 바인딩되어 있다고 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-459">If you're unfamiliar with C#, you may assume that using **var** means that the **viewModel** variable is late-bound.</span></span> <span data-ttu-id="d8136-460">올바르지 **않습니다. 컴파일러**는 C# 변수에 할당 된 항목을 기반으로 하는 형식 유추를 사용 하 여 **viewModel** 이 복사본 형식 인지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-460">That's not correct - the C# compiler is using type-inference based on what you assign to the variable to determine that **viewModel** is of type **StoreIndexViewModel**.</span></span> <span data-ttu-id="d8136-461">또한 로컬 **viewModel** **변수를 기능 코드 형식으로** 컴파일하면 컴파일 시간 검사 및 Visual Studio 코드 편집기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-461">Also, by compiling the local **viewModel** variable as a **StoreIndexViewModel** type you get compile-time checking and Visual Studio code-editor support.</span></span>

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a><span data-ttu-id="d8136-462">작업 4-기능을 사용 하는 뷰 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-462">Task 4 - Creating a View Template that Uses StoreIndexViewModel</span></span>

<span data-ttu-id="d8136-463">이 태스크에서는 컨트롤러에서 전달 된 복사본 인덱스 Viewmodel 개체를 사용 하 여 장르 목록을 표시 하는 보기 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-463">In this task, you will create a View template that will use a StoreIndexViewModel object passed from the Controller to display a list of genres.</span></span>

1. <span data-ttu-id="d8136-464">새 뷰 템플릿을 만들기 전에 **보기 추가 대화 상자** 에서 자동으로 파일 **인덱스 viewmodel** 클래스를 인식할 수 있도록 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-464">Before creating the new View template, let's build the project so that the **Add View Dialog** knows about the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="d8136-465">**빌드** 메뉴 항목을 선택한 다음 **MvcMusicStore 빌드**를 선택 하 여 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-465">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="d8136-466">![프로젝트 빌드](aspnet-mvc-4-fundamentals/_static/image22.png "프로젝트 빌드")</span><span class="sxs-lookup"><span data-stu-id="d8136-466">![Building the project](aspnet-mvc-4-fundamentals/_static/image22.png "Building the project")</span></span>

    <span data-ttu-id="d8136-467">*프로젝트 빌드*</span><span class="sxs-lookup"><span data-stu-id="d8136-467">*Building the project*</span></span>
2. <span data-ttu-id="d8136-468">새 뷰 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-468">Create a new View template.</span></span> <span data-ttu-id="d8136-469">이렇게 하려면 **Index** 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-469">To do that, right-click inside the **Index** method and select **Add View**.</span></span>

    <span data-ttu-id="d8136-470">![보기 추가](aspnet-mvc-4-fundamentals/_static/image23.png "보기 추가")</span><span class="sxs-lookup"><span data-stu-id="d8136-470">![Adding a View](aspnet-mvc-4-fundamentals/_static/image23.png "Adding a View")</span></span>

    <span data-ttu-id="d8136-471">*보기 추가*</span><span class="sxs-lookup"><span data-stu-id="d8136-471">*Adding a View*</span></span>
3. <span data-ttu-id="d8136-472">**뷰 추가 대화 상자** 는 **StoreController**에서 호출 되기 때문에 기본적으로 **\Views\Store\Index.cshtml** 파일에 뷰 템플릿이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-472">Because the **Add View Dialog** was invoked from the **StoreController**, it will add the View template by default in a **\Views\Store\Index.cshtml** file.</span></span> <span data-ttu-id="d8136-473">강력한 형식의 **뷰 만들기** 확인란을 선택 하 고 **모델 클래스로**이 클래스 **이름 지정** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-473">Check the **Create a strongly-typed-view** checkbox and then select **StoreIndexViewModel** as the **Model class**.</span></span> <span data-ttu-id="d8136-474">또한 선택 된 뷰 엔진이 **Razor**인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-474">Also, make sure that the View engine selected is **Razor**.</span></span> <span data-ttu-id="d8136-475">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-475">Click **Add**.</span></span>

    <span data-ttu-id="d8136-476">![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image24.png "뷰 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="d8136-476">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image24.png "Add View Dialog")</span></span>

    <span data-ttu-id="d8136-477">*뷰 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="d8136-477">*Add View Dialog*</span></span>

    <span data-ttu-id="d8136-478">**\Views\Store\Index.cshtml** View 템플릿 파일을 만들고 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-478">The **\Views\Store\Index.cshtml** View template file is created and opened.</span></span> <span data-ttu-id="d8136-479">보기 템플릿은 마지막 단계에서 **보기 추가** 대화 상자에 제공 된 정보를 기준으로 HTML **응답을 생성** 하는 데 사용할 데이터를 데이터로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-479">Based on the information provided to the **Add View** dialog in the last step, the View template will expect a **StoreIndexViewModel** instance as the data to use to generate an HTML response.</span></span> <span data-ttu-id="d8136-480">템플릿이에서 C#`ViewPage<musicstore.viewmodels.storeindexviewmodel>`를 상속 하는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-480">You will notice that the template inherits a `ViewPage<musicstore.viewmodels.storeindexviewmodel>` in C#.</span></span>

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a><span data-ttu-id="d8136-481">작업 5-보기 템플릿 업데이트</span><span class="sxs-lookup"><span data-stu-id="d8136-481">Task 5 - Updating the View Template</span></span>

<span data-ttu-id="d8136-482">이 태스크에서는 마지막 작업에서 만든 보기 템플릿을 업데이트 하 여 장르 수와 페이지 내에서의 해당 이름을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-482">In this task, you will update the View template created in the last task to retrieve the number of genres and their names within the page.</span></span>

> [!NOTE]
> <span data-ttu-id="d8136-483">@ 구문 (&quot;code 너 깃&quot;라고도 함)을 사용 하 여 뷰 템플릿 내에서 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-483">You will use @ syntax (often referred to as &quot;code nuggets&quot;) to execute code within the View template.</span></span>

1. <span data-ttu-id="d8136-484">**인덱스 cshtml** 파일의 **Store** 폴더 내에서 해당 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-484">In the **Index.cshtml** file, within the **Store** folder, replace its code with the following:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. <span data-ttu-id="d8136-485">을 (를) 사용 하 여에 있는 장르 목록에 대해 루프를 **실행 하 고** **foreach** 루프를 사용 하 여 HTML **&lt;ul&gt;** 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-485">Loop over the genre list in **StoreIndexViewModel** and create an HTML **&lt;ul&gt;** list using a **foreach** loop.</span></span>
   <span data-ttu-id="d8136-486">(C#)</span><span class="sxs-lookup"><span data-stu-id="d8136-486">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. <span data-ttu-id="d8136-487">**F5** 키를 눌러 응용 프로그램을 실행 하 고 **/Store**를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-487">Press **F5** to run the Application and browse **/Store**.</span></span> <span data-ttu-id="d8136-488">**StoreController** 에서 보기 템플릿에 전달 된 장르 목록이 표시 됩니다. **이 개체는 해당 개체** 에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-488">You will see the list of genres passed in the **StoreIndexViewModel** object from the **StoreController** to the View template.</span></span>

    <span data-ttu-id="d8136-489">![장르 목록을 표시 하는 보기](aspnet-mvc-4-fundamentals/_static/image26.png "장르 목록을 표시 하는 보기")</span><span class="sxs-lookup"><span data-stu-id="d8136-489">![View displaying a list of genres](aspnet-mvc-4-fundamentals/_static/image26.png "View displaying a list of genres")</span></span>

    <span data-ttu-id="d8136-490">*장르 목록을 표시 하는 보기*</span><span class="sxs-lookup"><span data-stu-id="d8136-490">*View displaying a list of genres*</span></span>
4. <span data-ttu-id="d8136-491">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-491">Close the browser.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a><span data-ttu-id="d8136-492">연습 6: 뷰에서 매개 변수 사용</span><span class="sxs-lookup"><span data-stu-id="d8136-492">Exercise 6: Using Parameters in View</span></span>

<span data-ttu-id="d8136-493">연습 3에서는 매개 변수를 컨트롤러에 전달 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-493">In Exercise 3 you learned how to pass parameters to the Controller.</span></span> <span data-ttu-id="d8136-494">이 연습에서는 보기 템플릿에서 해당 매개 변수를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-494">In this exercise, you will learn how to use those parameters in the View template.</span></span> <span data-ttu-id="d8136-495">이러한 목적을 위해 데이터 및 도메인 논리를 관리 하는 데 도움이 되는 모델 클래스를 먼저 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-495">For that purpose, you will be introduced first to Model classes that will help you to manage your data and domain logic.</span></span> <span data-ttu-id="d8136-496">또한 URL 경로 인코딩과 같은 항목을 걱정 하지 않고 ASP.NET MVC 응용 프로그램 내에서 페이지에 대 한 링크를 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-496">Additionally, you will learn how to create links to pages inside the ASP.NET MVC application without worrying of things like URL paths encoding.</span></span>

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a><span data-ttu-id="d8136-497">작업 1-모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-497">Task 1 - Adding Model Classes</span></span>

<span data-ttu-id="d8136-498">컨트롤러에서 뷰로 정보를 전달 하기 위해 만들어진 ViewModels과 달리 모델 클래스는 데이터 및 도메인 논리를 포함 하 고 관리 하기 위해 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-498">Unlike ViewModels, which are created just to pass information from the Controller to the View, Model classes are built to contain and manage data and domain logic.</span></span> <span data-ttu-id="d8136-499">이 작업에서는 **장르** 및 **앨범**이라는 두 가지 모델 클래스를 추가 하 여 이러한 개념을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-499">In this task you will add two model classes to represent these concepts: **Genre** and **Album**.</span></span>

1. <span data-ttu-id="d8136-500">아직 열려 있지 않은 경우 시작 **VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="d8136-500">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="d8136-501">**파일** 메뉴에서 **프로젝트 열기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-501">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="d8136-502">프로젝트 열기 대화 상자에서 **Source\Ex06-UsingParametersInView\Begin**로 이동 하 고 **시작** 을 선택 하 고 **열기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-502">In the Open Project dialog, browse to **Source\Ex06-UsingParametersInView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="d8136-503">또는 이전 연습을 완료 한 후 얻은 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-503">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="d8136-504">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-504">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="d8136-505">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-505">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="d8136-506">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-506">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="d8136-507">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-507">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d8136-508">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-508">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="d8136-509">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-509">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="d8136-510">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-510">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="d8136-511">**장르** 모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-511">Add a **Genre** Model class.</span></span> <span data-ttu-id="d8136-512">이렇게 하려면 **솔루션 탐색기**의 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **새 항목** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-512">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="d8136-513">**코드**에서 **클래스** 항목을 선택 하 고 파일 이름을 *Genre.cs*으로 지정한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-513">Under **Code**, choose the **Class** item and name the file *Genre.cs*, then click **Add**.</span></span>

    <span data-ttu-id="d8136-514">![클래스 추가](aspnet-mvc-4-fundamentals/_static/image27.png "클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="d8136-514">![Adding a class](aspnet-mvc-4-fundamentals/_static/image27.png "Adding a class")</span></span>

    <span data-ttu-id="d8136-515">*새 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="d8136-515">*Adding a new item*</span></span>

    <span data-ttu-id="d8136-516">![장르 모델 클래스 추가](aspnet-mvc-4-fundamentals/_static/image28.png "장르 모델 클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="d8136-516">![Add Genre Model Class](aspnet-mvc-4-fundamentals/_static/image28.png "Add Genre Model Class")</span></span>

    <span data-ttu-id="d8136-517">*장르 모델 클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="d8136-517">*Add Genre Model Class*</span></span>
4. <span data-ttu-id="d8136-518">장르 클래스에 **이름** 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-518">Add a **Name** property to the Genre class.</span></span> <span data-ttu-id="d8136-519">이렇게 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-519">To do this, add the following code:</span></span>

    <span data-ttu-id="d8136-520">(코드 조각- *ASP.NET MVC 4 기본-Ex6 장르*)</span><span class="sxs-lookup"><span data-stu-id="d8136-520">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. <span data-ttu-id="d8136-521">이전과 동일한 절차를 수행 하 여 **앨범** 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-521">Following the same procedure as before, add an **Album** class.</span></span> <span data-ttu-id="d8136-522">이렇게 하려면 **솔루션 탐색기**의 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **새 항목** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-522">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="d8136-523">**코드**에서 **클래스** 항목을 선택 하 고 파일 이름을 *Album.cs*으로 지정한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-523">Under **Code**, choose the **Class** item and name the file *Album.cs*, then click **Add**.</span></span>
6. <span data-ttu-id="d8136-524">앨범 클래스에 **장르** 및 **제목**이라는 두 가지 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-524">Add two properties to the Album class: **Genre** and **Title**.</span></span> <span data-ttu-id="d8136-525">이렇게 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-525">To do this, add the following code:</span></span>

    <span data-ttu-id="d8136-526">(코드 조각- *ASP.NET MVC 4 기본-Ex6 앨범*)</span><span class="sxs-lookup"><span data-stu-id="d8136-526">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a><span data-ttu-id="d8136-527">작업 2-StoreBrowseViewModel 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-527">Task 2 - Adding a StoreBrowseViewModel</span></span>

<span data-ttu-id="d8136-528">**StoreBrowseViewModel** 은이 작업에서 선택 된 장르와 일치 하는 앨범을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-528">A **StoreBrowseViewModel** will be used in this task to show the Albums that match a selected Genre.</span></span> <span data-ttu-id="d8136-529">이 작업에서는이 클래스를 만든 후 **장르** 및 해당 **앨범**목록을 처리 하는 두 개의 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-529">In this task, you will create this class and then add two properties to handle the **Genre** and its **Album**'s List.</span></span>

1. <span data-ttu-id="d8136-530">**StoreBrowseViewModel** 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-530">Add a **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="d8136-531">이렇게 하려면 **솔루션 탐색기**의 **viewmodels** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **새 항목** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-531">To do this, right-click the **ViewModels** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="d8136-532">**코드**에서 **클래스** 항목을 선택 하 고 파일 이름을 *StoreBrowseViewModel.cs*으로 지정한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-532">Under **Code**, choose the **Class** item and name the file *StoreBrowseViewModel.cs*, then click **Add**.</span></span>
2. <span data-ttu-id="d8136-533">**StoreBrowseViewModel** 클래스에서 모델에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-533">Add a reference to the Models in **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="d8136-534">이렇게 하려면 네임 스페이스를 사용 하 여 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-534">To do this, add the following using namespace:</span></span>

    <span data-ttu-id="d8136-535">(코드 조각- *ASP.NET MVC 4 기본-Ex6 UsingModel*)</span><span class="sxs-lookup"><span data-stu-id="d8136-535">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModel*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. <span data-ttu-id="d8136-536">**StoreBrowseViewModel** 클래스: **장르** 및 **앨범**에 두 개의 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-536">Add two properties to **StoreBrowseViewModel** class: **Genre** and **Albums**.</span></span> <span data-ttu-id="d8136-537">이렇게 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-537">To do this, add the following code:</span></span>

    <span data-ttu-id="d8136-538">(코드 조각- *ASP.NET MVC 4 기본-Ex6 ModelProperties*)</span><span class="sxs-lookup"><span data-stu-id="d8136-538">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 ModelProperties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> <span data-ttu-id="d8136-539">**List&lt;앨범&gt;** ?:이 정의는 **list&lt;t&gt;** 형식을 사용 합니다. 여기서 **t** 는이 **목록의** 요소가 속하는 형식 ( **이 경우에** 는 해당 항목 또는 해당 하위 항목)에 대 한 형식을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-539">What is **List&lt;Album&gt;** ?: This definition is using the **List&lt;T&gt;** type, where **T** constrains the type to which elements of this **List** belong to, in this case **Album** (or any of its descendants).</span></span>
> 
> <span data-ttu-id="d8136-540">클래스 또는 메서드를 클라이언트 코드에서 선언 하 고 인스턴스화할 때까지 하나 이상의 형식에 대 한 사양을 지연 하는 클래스 및 메서드를 디자인 하는 기능은 **제네릭**이라는 C# 언어의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-540">This ability to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code is a feature of the C# language called **Generics**.</span></span>
> 
> <span data-ttu-id="d8136-541">**List&lt;t&gt;** 는 **ArrayList** 형식에 해당 하는 제네릭 이며 **system.object** 네임 스페이스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-541">**List&lt;T&gt;** is the generic equivalent of the **ArrayList** type and is available in the **System.Collections.Generic** namespace.</span></span> <span data-ttu-id="d8136-542">**제네릭을** 사용 하는 경우의 이점 중 하나는 형식이 지정 된 경우에는 **ArrayList**를 사용 하는 것 처럼 요소를 **앨범** 으로 캐스팅 하는 것과 같은 형식 검사 작업을 처리할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-542">One of the benefits of using **generics** is that since the type is specified, you do not need to take care of type checking operations such as casting the elements into **Album** as you would do with an **ArrayList**.</span></span>

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a><span data-ttu-id="d8136-543">작업 3-StoreController에서 새 ViewModel 사용</span><span class="sxs-lookup"><span data-stu-id="d8136-543">Task 3 - Using the New ViewModel in the StoreController</span></span>

<span data-ttu-id="d8136-544">이 작업에서는 새 **StoreBrowseViewModel**를 사용 하도록 **StoreController**의 **Browse** 및 **Details** 작업 메서드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-544">In this task, you will modify the **StoreController**'s **Browse** and **Details** action methods to use the new **StoreBrowseViewModel**.</span></span>

1. <span data-ttu-id="d8136-545">**StoreController** 클래스의 모델 폴더에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-545">Add a reference to the Models folder in **StoreController** class.</span></span> <span data-ttu-id="d8136-546">이렇게 하려면 **솔루션 탐색기** 의 **컨트롤러** 폴더를 확장 하 고 **StoreController** 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-546">To do this, expand the **Controllers** folder in the **Solution Explorer** and open the **StoreController** class.</span></span> <span data-ttu-id="d8136-547">그런 후에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-547">Then add the following code:</span></span>

    <span data-ttu-id="d8136-548">(코드 조각- *ASP.NET MVC 4 기본-Ex6 UsingModelInController*)</span><span class="sxs-lookup"><span data-stu-id="d8136-548">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModelInController*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. <span data-ttu-id="d8136-549">**StoreViewBrowseController** 클래스를 사용 하도록 **Browse** action 메서드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-549">Replace the **Browse** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="d8136-550">더미 데이터를 사용 하 여 장르와 두 개의 새 앨범 개체를 만듭니다. 다음 실습 랩에서는 데이터베이스의 실제 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-550">You will create a Genre and two new Albums objects with dummy data (in the next Hands-on Lab you will consume real data from a database).</span></span> <span data-ttu-id="d8136-551">이렇게 하려면 **Browse** 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-551">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="d8136-552">(코드 조각- *ASP.NET MVC 4 기본-Ex6 BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="d8136-552">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. <span data-ttu-id="d8136-553">**StoreViewBrowseController** 클래스를 사용 하도록 **Details** 작업 메서드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-553">Replace the **Details** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="d8136-554">**뷰에**반환 될 새 **앨범** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-554">You will create a new **Album** object to be returned to the **View**.</span></span> <span data-ttu-id="d8136-555">이렇게 하려면 **Details** 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-555">To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="d8136-556">(코드 조각- *ASP.NET MVC 4 기본-Ex6 DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="d8136-556">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a><span data-ttu-id="d8136-557">작업 4-찾아보기 보기 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-557">Task 4 - Adding a Browse View Template</span></span>

<span data-ttu-id="d8136-558">이 작업에서는 특정 장르에 대해 찾은 앨범을 표시 하는 **찾아보기** 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-558">In this task, you will add a **Browse** View to show the Albums found for a specific Genre.</span></span>

1. <span data-ttu-id="d8136-559">새 뷰 템플릿을 만들기 전에 **보기 추가** 대화 상자에서 사용할 **ViewModel** 클래스에 대해 알 수 있도록 프로젝트를 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-559">Before creating the new View template, you should build the project so that the **Add View** Dialog knows about the **ViewModel** class to use.</span></span> <span data-ttu-id="d8136-560">**빌드** 메뉴 항목을 선택한 다음 **MvcMusicStore 빌드**를 선택 하 여 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-560">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>
2. <span data-ttu-id="d8136-561">**찾아보기** 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-561">Add a **Browse** View.</span></span> <span data-ttu-id="d8136-562">이렇게 하려면 **StoreController** 의 **찾아보기** 동작 메서드를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-562">To do this, right-click in the **Browse** action method of the **StoreController** and click **Add View**.</span></span>
3. <span data-ttu-id="d8136-563">**보기 추가** 대화 상자에서 보기 이름이 **찾아보기**인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-563">In the **Add View** dialog box, verify that the View Name is **Browse**.</span></span> <span data-ttu-id="d8136-564">**강력한 형식의 뷰 만들기** 확인란을 선택 하 고 **모델 클래스** 드롭다운에서 **StoreBrowseViewModel** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-564">Check the **Create a strongly-typed view** checkbox and select **StoreBrowseViewModel** from the **Model class** dropdown.</span></span> <span data-ttu-id="d8136-565">다른 필드는 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-565">Leave the other fields with their default value.</span></span> <span data-ttu-id="d8136-566">그런 다음, **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-566">Then click **Add**.</span></span>

    <span data-ttu-id="d8136-567">![찾아보기 보기 추가](aspnet-mvc-4-fundamentals/_static/image29.png "찾아보기 보기 추가")</span><span class="sxs-lookup"><span data-stu-id="d8136-567">![Adding a Browse View](aspnet-mvc-4-fundamentals/_static/image29.png "Adding a Browse View")</span></span>

    <span data-ttu-id="d8136-568">*찾아보기 보기 추가*</span><span class="sxs-lookup"><span data-stu-id="d8136-568">*Adding a Browse View*</span></span>
4. <span data-ttu-id="d8136-569">StoreBrowseViewModel를 **수정 하 여** 장르 정보를 표시 하 고 뷰 템플릿에 전달 되는 개체에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-569">Modify the **Browse.cshtml** to display the Genre's information, accessing the **StoreBrowseViewModel** object that is passed to the view template.</span></span> <span data-ttu-id="d8136-570">이렇게 하려면 콘텐츠를 다음으로 바꿉니다. (C#)</span><span class="sxs-lookup"><span data-stu-id="d8136-570">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="d8136-571">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d8136-571">Task 5 - Running the Application</span></span>

<span data-ttu-id="d8136-572">이 작업에서는 browse 메서드가 **browse** **메서드 작업** 에서 앨범을 검색 하도록 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-572">In this task, you will test that the **Browse** method retrieves Albums from the **Browse** method action.</span></span>

1. <span data-ttu-id="d8136-573">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-573">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d8136-574">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-574">The project starts in the Home page.</span></span> <span data-ttu-id="d8136-575">URL을/Svs\hers로 변경 **하 시겠습니까? 장르 = Disco** 작업에서 두 개의 앨범이 반환 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-575">Change the URL to **/Store/Browse?Genre=Disco** to verify that the action returns two Albums.</span></span>

    <span data-ttu-id="d8136-576">![저장소 검색 Disco 앨범](aspnet-mvc-4-fundamentals/_static/image30.png "저장소 검색 Disco 앨범")</span><span class="sxs-lookup"><span data-stu-id="d8136-576">![Browsing Store Disco Albums](aspnet-mvc-4-fundamentals/_static/image30.png "Browsing Store Disco Albums")</span></span>

    <span data-ttu-id="d8136-577">*저장소 검색 Disco 앨범*</span><span class="sxs-lookup"><span data-stu-id="d8136-577">*Browsing Store Disco Albums*</span></span>

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a><span data-ttu-id="d8136-578">작업 6-특정 앨범에 대 한 정보 표시</span><span class="sxs-lookup"><span data-stu-id="d8136-578">Task 6 - Displaying information About a Specific Album</span></span>

<span data-ttu-id="d8136-579">이 태스크에서는 **저장소/세부 정보** 보기를 구현 하 여 특정 앨범에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-579">In this task, you will implement the **Store/Details** view to display information about a specific album.</span></span> <span data-ttu-id="d8136-580">이 실습 랩에서는 앨범에 대해 표시 되는 모든 항목이 **보기** 템플릿에 이미 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-580">In this Hands-on Lab, everything you will display about the album is already contained in the **View** template.</span></span> <span data-ttu-id="d8136-581">따라서 **StoreDetailsViewModel** 클래스를 만드는 대신 현재 **StoreBrowseViewModel** 템플릿을 사용 하 여 앨범을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-581">So, instead of creating a **StoreDetailsViewModel** class, you will use the current **StoreBrowseViewModel** template passing the Album to it.</span></span>

1. <span data-ttu-id="d8136-582">필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-582">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="d8136-583">**StoreController**의 **details** 작업 메서드에 대 한 새 **세부 정보** 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-583">Add a new **Details** view for the **StoreController**'s **Details** action method.</span></span> <span data-ttu-id="d8136-584">이렇게 하려면 **StoreController** 클래스에서 **Details** 메서드를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-584">To do this, right-click the **Details** method in the **StoreController** class and click **Add View**.</span></span>
2. <span data-ttu-id="d8136-585">**보기 추가** 대화 상자에서 **보기 이름이** **Details**인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-585">In the **Add View** dialog, verify that the **View Name** is **Details**.</span></span> <span data-ttu-id="d8136-586">**강력한 형식의 뷰 만들기** 확인란을 선택 하 고 **모델 클래스** 드롭다운에서 **앨범** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-586">Check the **Create a strongly-typed view** checkbox and select **Album** from the **Model class** drop-down.</span></span> <span data-ttu-id="d8136-587">다른 필드는 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-587">Leave the other fields with their default value.</span></span> <span data-ttu-id="d8136-588">그런 다음, **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-588">Then click **Add**.</span></span> <span data-ttu-id="d8136-589">그러면 **\Views\Store\Details.cshtml** 파일이 생성 되 고 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-589">This will create and open a **\Views\Store\Details.cshtml** file.</span></span>

    <span data-ttu-id="d8136-590">![세부 정보 보기 추가](aspnet-mvc-4-fundamentals/_static/image31.png "세부 정보 보기 추가")</span><span class="sxs-lookup"><span data-stu-id="d8136-590">![Adding a Details View](aspnet-mvc-4-fundamentals/_static/image31.png "Adding a Details View")</span></span>

    <span data-ttu-id="d8136-591">*세부 정보 보기 추가*</span><span class="sxs-lookup"><span data-stu-id="d8136-591">*Adding a Details View*</span></span>
3. <span data-ttu-id="d8136-592">**세부** 정보를 수정 하 여 앨범 정보를 표시 하 고 보기 템플릿에 전달 된 **앨범** 개체에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-592">Modify the **Details.cshtml** file to display the Album's information, accessing the **Album** object that is passed to the view template.</span></span> <span data-ttu-id="d8136-593">이렇게 하려면 콘텐츠를 다음으로 바꿉니다. (C#)</span><span class="sxs-lookup"><span data-stu-id="d8136-593">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="d8136-594">작업 7-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d8136-594">Task 7 - Running the Application</span></span>

<span data-ttu-id="d8136-595">이 작업에서는 details **작업** 메서드에서 앨범 정보를 검색 하는 **세부** 정보 보기를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-595">In this task, you will test that the **Details** View retrieves Album's information from the **Details action** method.</span></span>

1. <span data-ttu-id="d8136-596">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-596">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d8136-597">프로젝트가 **홈** 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-597">The project starts in the **Home** page.</span></span> <span data-ttu-id="d8136-598">URL을 **/Store/Details/5** 로 변경 하 여 앨범 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-598">Change the URL to **/Store/Details/5** to verify the album's information.</span></span>

    <span data-ttu-id="d8136-599">![앨범 탐색 세부 정보](aspnet-mvc-4-fundamentals/_static/image32.png "앨범 탐색 세부 정보")</span><span class="sxs-lookup"><span data-stu-id="d8136-599">![Browsing Albums Detail](aspnet-mvc-4-fundamentals/_static/image32.png "Browsing Albums Detail")</span></span>

    <span data-ttu-id="d8136-600">*탐색 앨범의 세부 정보*</span><span class="sxs-lookup"><span data-stu-id="d8136-600">*Browsing Album's Detail*</span></span>

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a><span data-ttu-id="d8136-601">작업 8-페이지 간 링크 추가</span><span class="sxs-lookup"><span data-stu-id="d8136-601">Task 8 - Adding Links Between Pages</span></span>

<span data-ttu-id="d8136-602">이 작업에서는 스토어 보기의 링크를 추가 하 여 모든 장르 이름에 적절 한 **/Sv/svhurl** 에 대 한 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-602">In this task, you will add a link in the Store View to have a link in every Genre name to the appropriate **/Store/Browse** URL.</span></span> <span data-ttu-id="d8136-603">이러한 방식으로, 예를 들어, 장르를 클릭 하면 **disco**로 이동 하 여 **/Source= Disco** URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-603">This way, when you click on a Genre, for instance **Disco**, it will navigate to **/Store/Browse?genre=Disco** URL.</span></span>

1. <span data-ttu-id="d8136-604">필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-604">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="d8136-605">**인덱스** 페이지를 업데이트 하 여 **찾아보기** 페이지에 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-605">Update the **Index** page to add a link to the **Browse** page.</span></span> <span data-ttu-id="d8136-606">이렇게 하려면 **솔루션 탐색기** 에서 **Views** 폴더를 확장 한 다음 **저장소** 폴더를 확장 하 고, **Index. cshtml** 페이지를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-606">To do this, in the **Solution Explorer** expand the **Views** folder, then the **Store** folder and double-click the **Index.cshtml** page.</span></span>
2. <span data-ttu-id="d8136-607">선택 된 장르를 나타내는 찾아보기 보기에 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-607">Add a link to the Browse view indicating the genre selected.</span></span> <span data-ttu-id="d8136-608">이렇게 하려면 **&lt;li&gt;** 태그에서 다음 강조 표시 된 코드를 바꿉니다. (C#)</span><span class="sxs-lookup"><span data-stu-id="d8136-608">To do this, replace the following highlighted code within the **&lt;li&gt;** tags: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > <span data-ttu-id="d8136-609">또 다른 방법은 다음과 같은 코드를 사용 하 여 페이지에 직접 연결 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-609">another approach would be linking directly to the page, with a code like the following:</span></span>
   > 
   > <span data-ttu-id="d8136-610">&lt;href =&quot;/svs\hhhhher? 장르 =@genreName&quot;&gt;@genreName&lt;/a&gt;</span><span class="sxs-lookup"><span data-stu-id="d8136-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span></span>
   > 
   > <span data-ttu-id="d8136-611">이 방법이 작동 하지만 하드 코드 된 문자열에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-611">Although this approach works, it depends on a hardcoded string.</span></span> <span data-ttu-id="d8136-612">나중에 컨트롤러의 이름을 바꾸는 경우에는이 명령을 수동으로 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-612">If you later rename the Controller, you will have to change this instruction manually.</span></span> <span data-ttu-id="d8136-613">더 나은 대안은 **HTML 도우미** 메서드를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-613">A better alternative is to use an **HTML Helper** method.</span></span> <span data-ttu-id="d8136-614">ASP.NET MVC에는 이러한 작업에 사용할 수 있는 HTML 도우미 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-614">ASP.NET MVC includes an HTML Helper method which is available for such tasks.</span></span> <span data-ttu-id="d8136-615">Html.actionlink **()** 도우미 메서드를 사용 하면 **&gt;링크&lt;** html을 쉽게 빌드할 수 있으므로 url 경로가 적절 하 게 url로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-615">The **Html.ActionLink()** helper method makes it easy to build HTML **&lt;a&gt;** links, making sure URL paths are properly URL encoded.</span></span>
   > 
   > <span data-ttu-id="d8136-616">Html.actionlink에는 여러 오버 로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-616">Html.ActionLink has several overloads.</span></span> <span data-ttu-id="d8136-617">이 연습에서는 다음 3 개의 매개 변수를 사용 하는 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-617">In this exercise you will use one that takes three parameters:</span></span>
   > 
   > 1. <span data-ttu-id="d8136-618">장르 이름을 표시 하는 링크 텍스트</span><span class="sxs-lookup"><span data-stu-id="d8136-618">Link text, which will display the Genre name</span></span>
   > 2. <span data-ttu-id="d8136-619">컨트롤러 작업 이름 (**찾아보기**)</span><span class="sxs-lookup"><span data-stu-id="d8136-619">Controller action name (**Browse**)</span></span>
   > 3. <span data-ttu-id="d8136-620">이름 (**장르**) 및 값 (**장르 이름**)을 모두 지정 하는 경로 매개 변수 값</span><span class="sxs-lookup"><span data-stu-id="d8136-620">Route parameter values, specifying both the name (**Genre**) and the value (**Genre name**)</span></span>

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a><span data-ttu-id="d8136-621">작업 9-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d8136-621">Task 9 - Running the Application</span></span>

<span data-ttu-id="d8136-622">이 작업에서는 각 장르가 적절 한 **/Sv/svhurl** 에 대 한 링크와 함께 표시 되는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-622">In this task, you will test that each Genre is displayed with a link to the appropriate **/Store/Browse** URL.</span></span>

1. <span data-ttu-id="d8136-623">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-623">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d8136-624">프로젝트가 홈 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-624">The project starts in the Home page.</span></span> <span data-ttu-id="d8136-625">**/Store** 에 대 한 url을 변경 하 여 각 장르가 적절 한 **/sv/dvurl** 에 링크 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-625">Change the URL to **/Store** to verify that each Genre links to the appropriate **/Store/Browse** URL.</span></span>

    <span data-ttu-id="d8136-626">![찾아보기 페이지로 이동 하는 링크를 사용 하 여 장르 검색](aspnet-mvc-4-fundamentals/_static/image33.png "찾아보기 페이지로 이동 하는 링크를 사용 하 여 장르 검색")</span><span class="sxs-lookup"><span data-stu-id="d8136-626">![Browsing Genres with links to Browse page](aspnet-mvc-4-fundamentals/_static/image33.png "Browsing Genres with links to Browse page")</span></span>

    <span data-ttu-id="d8136-627">*찾아보기 페이지로 이동 하는 링크를 사용 하 여 장르 검색*</span><span class="sxs-lookup"><span data-stu-id="d8136-627">*Browsing Genres with links to Browse page*</span></span>

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a><span data-ttu-id="d8136-628">작업 10-동적 ViewModel 컬렉션을 사용 하 여 값 전달</span><span class="sxs-lookup"><span data-stu-id="d8136-628">Task 10 - Using Dynamic ViewModel Collection to Pass Values</span></span>

<span data-ttu-id="d8136-629">이 태스크에서는 모델을 변경 하지 않고 컨트롤러와 뷰 간에 값을 전달 하는 간단 하 고 강력한 메서드를 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-629">In this task, you will learn a simple and powerful method to pass values between the Controller and the View without making any changes in the Model.</span></span> <span data-ttu-id="d8136-630">ASP.NET MVC 4는 &quot;ViewModel&quot;컬렉션을 제공 합니다 .이 컬렉션은 동적 값에 할당 하 고 컨트롤러 및 뷰 내에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-630">ASP.NET MVC 4 provides the collection &quot;ViewModel&quot;, which can be assigned to any dynamic value and accessed inside controllers and views as well.</span></span>

<span data-ttu-id="d8136-631">이제 ViewBag 동적 컬렉션을 사용 하 여 컨트롤러에서 뷰로 &quot;**별표 표시 장르**&quot; 목록을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-631">You will now use the ViewBag dynamic collection to pass a list of &quot;**Starred genres**&quot; from the controller to the view.</span></span> <span data-ttu-id="d8136-632">저장소 인덱스 보기는 **ViewModel** 에 액세스 하 고 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-632">The Store Index view will access to **ViewModel** and display the information.</span></span>

1. <span data-ttu-id="d8136-633">필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-633">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="d8136-634">**StoreController.cs** 를 열고 **Index** 메서드를 수정 하 여 ViewModel 컬렉션에 별표 표시 장르 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-634">Open **StoreController.cs** and modify **Index** method to create a list of starred genres into ViewModel collection :</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > <span data-ttu-id="d8136-635">**Viewbag [&quot;별표 표시&quot;]** 구문을 사용 하 여 속성에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-635">You could also use the syntax **ViewBag[&quot;Starred&quot;]** to access the properties.</span></span>
2. <span data-ttu-id="d8136-636">**별표 표시&quot;별&quot;** 아이콘이이 랩의 **Source\assets\images** 폴더에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-636">The star icon **&quot;starred.png&quot;** is included in the **Source\Assets\Images** folder of this lab.</span></span> <span data-ttu-id="d8136-637">응용 프로그램에 추가 하려면 아래와 같이 **Windows 탐색기** 창에서 Visual Web Developer Express의 **솔루션 탐색기** 로 해당 콘텐츠를 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-637">In order to add it to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Web Developer Express, as shown below:</span></span>

    <span data-ttu-id="d8136-638">![솔루션에 별모양 이미지 추가](aspnet-mvc-4-fundamentals/_static/image34.png "솔루션에 별모양 이미지 추가")</span><span class="sxs-lookup"><span data-stu-id="d8136-638">![Adding star image to the solution](aspnet-mvc-4-fundamentals/_static/image34.png "Adding star image to the solution")</span></span>

    <span data-ttu-id="d8136-639">*솔루션에 별모양 이미지 추가*</span><span class="sxs-lookup"><span data-stu-id="d8136-639">*Adding star image to the solution*</span></span>
3. <span data-ttu-id="d8136-640">**저장소/인덱스** 를 열고 내용을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-640">Open the view **Store/Index.cshtml** and modify the content.</span></span> <span data-ttu-id="d8136-641">**Viewbag** 컬렉션에서 &quot;별표 표시&quot; 속성을 읽고 현재 장르 이름이 목록에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-641">You will read the &quot;starred&quot; property in the **ViewBag** collection, and ask if the current genre name is in the list.</span></span> <span data-ttu-id="d8136-642">이 경우에는 장르 링크에 바로 별 아이콘이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-642">In that case you will show a star icon right to the genre link.</span></span>
   <span data-ttu-id="d8136-643">(C#)</span><span class="sxs-lookup"><span data-stu-id="d8136-643">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a><span data-ttu-id="d8136-644">작업 11-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d8136-644">Task 11 - Running the Application</span></span>

<span data-ttu-id="d8136-645">이 작업에서는 별표 표시 장르에 별 아이콘이 표시 되는 것을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-645">In this task, you will test that the starred genres display a star icon.</span></span>

1. <span data-ttu-id="d8136-646">**F5** 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-646">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d8136-647">프로젝트가 **홈** 페이지에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-647">The project starts in the **Home** page.</span></span> <span data-ttu-id="d8136-648">URL을 **/Store** 로 변경 하 여 각 주요 장르에 준수 레이블이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-648">Change the URL to **/Store** to verify that each featured genre has the respecting label:</span></span>

    <span data-ttu-id="d8136-649">![별표 표시 요소를 사용 하 여 장르 검색](aspnet-mvc-4-fundamentals/_static/image35.png "별표 표시 요소를 사용 하 여 장르 검색")</span><span class="sxs-lookup"><span data-stu-id="d8136-649">![Browsing Genres with starred elements](aspnet-mvc-4-fundamentals/_static/image35.png "Browsing Genres with starred elements")</span></span>

    <span data-ttu-id="d8136-650">*별표 표시 요소를 사용 하 여 장르 검색*</span><span class="sxs-lookup"><span data-stu-id="d8136-650">*Browsing Genres with starred elements*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a><span data-ttu-id="d8136-651">연습 7: ASP.NET MVC 4 새 템플릿 살펴보기</span><span class="sxs-lookup"><span data-stu-id="d8136-651">Exercise 7: A lap around ASP.NET MVC 4 new template</span></span>

<span data-ttu-id="d8136-652">이 연습에서는 ASP.NET MVC 4 프로젝트 템플릿의 향상 된 기능을 살펴보고 새 템플릿의 가장 관련성이 높은 기능을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-652">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 project templates, taking a look at the most relevant features of the new template.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a><span data-ttu-id="d8136-653">작업 1: ASP.NET MVC 4 인터넷 응용 프로그램 템플릿 탐색</span><span class="sxs-lookup"><span data-stu-id="d8136-653">Task 1: Exploring the ASP.NET MVC 4 Internet Application Template</span></span>

1. <span data-ttu-id="d8136-654">아직 열려 있지 않은 경우 시작 **VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="d8136-654">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="d8136-655">파일을 선택 합니다. **| 새로 만들기 | 프로젝트** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-655">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="d8136-656">**새 프로젝트** 대화 상자에서 **시각적 개체 C#| 웹** 템플릿을 선택 하 고 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-656">In the **New Project** dialog, select the **Visual C#|Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="d8136-657">프로젝트 **이름을** *MusicStore* 로 지정 하 고 **솔루션 이름을** *시작*으로 업데이트 한 다음 위치를 선택 하거나 기본값을 그대로 유지 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-657">**Name** the project *MusicStore* and update the **solution name** to *Begin*, then select a location (or leave the default) and click **OK**.</span></span>

    <span data-ttu-id="d8136-658">![새 ASP.NET MVC 4 프로젝트 만들기](aspnet-mvc-4-fundamentals/_static/image36.png "새 ASP.NET MVC 4 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="d8136-658">![Creating a new ASP.NET MVC 4 Project](aspnet-mvc-4-fundamentals/_static/image36.png "Creating a new ASP.NET MVC 4 Project")</span></span>

    <span data-ttu-id="d8136-659">*새 ASP.NET MVC 4 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="d8136-659">*Creating a new ASP.NET MVC 4 Project*</span></span>
3. <span data-ttu-id="d8136-660">**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 프로젝트 템플릿을 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-660">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="d8136-661">보기 엔진으로 Razor 또는 ASPX를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-661">Notice you can select either Razor or ASPX as the view engine.</span></span>

    <span data-ttu-id="d8136-662">![새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기](aspnet-mvc-4-fundamentals/_static/image37.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")</span><span class="sxs-lookup"><span data-stu-id="d8136-662">![Creating a new ASP.NET MVC 4 Internet Application](aspnet-mvc-4-fundamentals/_static/image37.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="d8136-663">*새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*</span><span class="sxs-lookup"><span data-stu-id="d8136-663">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8136-664">Razor 구문는 ASP.NET MVC 3에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-664">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="d8136-665">이는 파일에 필요한 문자 및 키 입력 수를 최소화 하 여 빠르고 유체 코딩 워크플로를 사용 하도록 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-665">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="d8136-666">Razor는 기존 C#/vb (또는 기타) 언어 기술을 활용 하 고 멋진 HTML 생성 워크플로를 활성화 하는 템플릿 태그 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-666">Razor leverages existing C#/VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="d8136-667">**F5** 키를 눌러 솔루션을 실행 하 고 갱신 된 템플릿을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-667">Press **F5** to run the solution and see the renewed template.</span></span> <span data-ttu-id="d8136-668">다음 기능을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-668">You can check out the following features:</span></span>

    1. <span data-ttu-id="d8136-669">**최신 스타일 템플릿**</span><span class="sxs-lookup"><span data-stu-id="d8136-669">**Modern-style templates**</span></span>

        <span data-ttu-id="d8136-670">템플릿이 갱신 되어 최신 스타일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-670">The templates have been renewed, providing more modern-looking styles.</span></span>

        <span data-ttu-id="d8136-671">![ASP.NET MVC 4 스타일 지정 템플릿](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 스타일 지정 템플릿")</span><span class="sxs-lookup"><span data-stu-id="d8136-671">![ASP.NET MVC 4 restyled templates](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 restyled templates")</span></span>

        <span data-ttu-id="d8136-672">*ASP.NET MVC 4 스타일 지정 템플릿*</span><span class="sxs-lookup"><span data-stu-id="d8136-672">*ASP.NET MVC 4 restyled templates*</span></span>
    2. <span data-ttu-id="d8136-673">**적응 렌더링**</span><span class="sxs-lookup"><span data-stu-id="d8136-673">**Adaptive Rendering**</span></span>

        <span data-ttu-id="d8136-674">브라우저 창의 크기를 조정 하 고 페이지 레이아웃이 새 창 크기에 동적으로 적응 하는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-674">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="d8136-675">이러한 템플릿은 적응 렌더링 기술을 사용 하 여 사용자 지정 없이 데스크톱과 모바일 플랫폼 모두에서 적절히 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-675">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

        <span data-ttu-id="d8136-676">![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿](aspnet-mvc-4-fundamentals/_static/image39.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")</span><span class="sxs-lookup"><span data-stu-id="d8136-676">![ASP.NET MVC 4 project template in different browser sizes](aspnet-mvc-4-fundamentals/_static/image39.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

        <span data-ttu-id="d8136-677">*다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*</span><span class="sxs-lookup"><span data-stu-id="d8136-677">*ASP.NET MVC 4 project template in different browser sizes*</span></span>
5. <span data-ttu-id="d8136-678">디버거를 중지 하 고 Visual Studio로 돌아가려면 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-678">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="d8136-679">이제 솔루션을 탐색 하 고 프로젝트 템플릿에서 ASP.NET MVC 4에서 도입 된 새로운 기능 중 일부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-679">Now you are able to explore the solution and check out some of the new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="d8136-680">![ASP.NET (MVC4)-프로젝트 템플릿](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿")</span><span class="sxs-lookup"><span data-stu-id="d8136-680">![ASP.NET MVC4-internet-application-project-template](aspnet-mvc-4-fundamentals/_static/image40.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    <span data-ttu-id="d8136-681">*ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*</span><span class="sxs-lookup"><span data-stu-id="d8136-681">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   1. <span data-ttu-id="d8136-682">**HTML5 태그**</span><span class="sxs-lookup"><span data-stu-id="d8136-682">**HTML5 markup**</span></span>

       <span data-ttu-id="d8136-683">템플릿 뷰를 탐색 하 여 새 테마 태그를 찾습니다. 예를 들어 **Home** 폴더 내에서 열기 **About. cshtml** 보기를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-683">Browse template views to find out the new theme markup, for example open **About.cshtml** view within **Home** folder.</span></span>

       <span data-ttu-id="d8136-684">![새 템플릿, Razor 및 HTML5 태그 사용](aspnet-mvc-4-fundamentals/_static/image41.png "새 템플릿, Razor 및 HTML5 태그 사용")</span><span class="sxs-lookup"><span data-stu-id="d8136-684">![New template, using Razor and HTML5 markup](aspnet-mvc-4-fundamentals/_static/image41.png "New template, using Razor and HTML5 markup")</span></span>

       <span data-ttu-id="d8136-685">*새 템플릿, Razor 및 HTML5 태그 사용*</span><span class="sxs-lookup"><span data-stu-id="d8136-685">*New template, using Razor and HTML5 markup*</span></span>
   2. <span data-ttu-id="d8136-686">**포함 된 JavaScript 라이브러리**</span><span class="sxs-lookup"><span data-stu-id="d8136-686">**JavaScript libraries included**</span></span>

      1. <span data-ttu-id="d8136-687">**jquery**: JQUERY는 HTML 문서 트래버스, 이벤트 처리, 애니메이션 및 Ajax 상호 작용을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-687">**jQuery**: jQuery simplifies HTML document traversing, event handling, animating, and Ajax interactions.</span></span>
      2. <span data-ttu-id="d8136-688">**JQUERY UI**:이 라이브러리는 Jquery JavaScript 라이브러리를 기반으로 구축 된 낮은 수준의 상호 작용 및 애니메이션, 고급 효과 및 themeable 위젯에 대 한 추상화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-688">**jQuery UI**: This library provides abstractions for low-level interaction and animation, advanced effects and themeable widgets, built on top of the jQuery JavaScript Library.</span></span>

         > [!NOTE]
         > <span data-ttu-id="d8136-689">[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)에서 jQuery 및 jquery UI에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-689">You can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>
      3. <span data-ttu-id="d8136-690">**KnockoutJS**: ASP.NET MVC 4 기본 템플릿에는 JAVASCRIPT 및 HTML을 사용 하 여 풍부 하 고 응답성이 뛰어난 웹 응용 프로그램을 만들 수 있는 javascript MVVM 프레임 워크인 **KnockoutJS**가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-690">**KnockoutJS**: The ASP.NET MVC 4 default template now includes **KnockoutJS**, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="d8136-691">ASP.NET MVC 3의 경우와 마찬가지로 jQuery 및 jQuery UI 라이브러리도 ASP.NET MVC 4에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-691">Like in ASP.NET MVC 3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

          > [!NOTE]
          > <span data-ttu-id="d8136-692">이 링크에서 KnockOutJS library에 대 한 자세한 내용은 [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="d8136-692">You can get more information about KnockOutJS library in this link: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span></span>
      4. <span data-ttu-id="d8136-693">**Modernizr**:이 라이브러리는 HTML5 및 CSS3 기술을 사용 하는 경우 사이트가 이전 브라우저와 호환 되도록 자동으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-693">**Modernizr**: This library runs automatically, making your site compatible with older browsers when using HTML5 and CSS3 technologies.</span></span>

          > [!NOTE]
          > <span data-ttu-id="d8136-694">이 링크에서 Modernizr library에 대 한 자세한 내용은 [http://www.modernizr.com/](http://www.modernizr.com/)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="d8136-694">You can get more information about Modernizr library in this link: [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>
   3. <span data-ttu-id="d8136-695">**솔루션에 포함 된 SimpleMembership**</span><span class="sxs-lookup"><span data-stu-id="d8136-695">**SimpleMembership included in the solution**</span></span>

       <span data-ttu-id="d8136-696">SimpleMembership는 이전 ASP.NET 역할 및 멤버 자격 공급자 시스템에 대 한 대체로 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-696">SimpleMembership has been designed as a replacement for the previous ASP.NET Role and Membership provider system.</span></span> <span data-ttu-id="d8136-697">개발자가 보다 유연 하 게 웹 페이지를 보다 쉽게 보호할 수 있도록 하는 여러 가지 새로운 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-697">It has many new features that make it easier for the developer to secure web pages in a more flexible way.</span></span>

       <span data-ttu-id="d8136-698">인터넷 템플릿에서 SimpleMembership를 통합 하기 위한 몇 가지 작업을 이미 설정 했습니다. 예를 들어 AccountController는 OAuthWebSecurity (OAuth 계정 등록, 로그인, 관리 등) 및 웹 보안을 사용할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-698">The Internet template already has set up a few things to integrate SimpleMembership, for example, the AccountController is prepared to use OAuthWebSecurity (for OAuth account registration, login, management, etc.) and Web Security.</span></span>

       <span data-ttu-id="d8136-699">![솔루션에 포함 된 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "솔루션에 포함 된 SimpleMembership")</span><span class="sxs-lookup"><span data-stu-id="d8136-699">![SimpleMembership Included in the solution](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership Included in the solution")</span></span>

       <span data-ttu-id="d8136-700">*솔루션에 포함 된 SimpleMembership*</span><span class="sxs-lookup"><span data-stu-id="d8136-700">*SimpleMembership Included in the solution*</span></span>

       > [!NOTE]
       > <span data-ttu-id="d8136-701">MSDN의 [Oauthwebsecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) 에 대 한 자세한 내용을 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="d8136-701">Find more information about [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) in MSDN.</span></span>

> [!NOTE]
> <span data-ttu-id="d8136-702">또한 [부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)를 수행 하는 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-702">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="d8136-703">요약</span><span class="sxs-lookup"><span data-stu-id="d8136-703">Summary</span></span>

<span data-ttu-id="d8136-704">이 실습 실습을 완료 하면 ASP.NET MVC의 기본 사항에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-704">By completing this Hands-On Lab you have learned the fundamentals of ASP.NET MVC:</span></span>

- <span data-ttu-id="d8136-705">MVC 응용 프로그램의 핵심 요소 및 상호 작용 방법</span><span class="sxs-lookup"><span data-stu-id="d8136-705">The core elements of an MVC application and how they interact</span></span>
- <span data-ttu-id="d8136-706">ASP.NET MVC 응용 프로그램을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="d8136-706">How to create an ASP.NET MVC Application</span></span>
- <span data-ttu-id="d8136-707">URL 및 querystring을 통해 전달 되는 매개 변수를 처리 하는 컨트롤러를 추가 및 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d8136-707">How to add and configure Controllers to handle parameters passed through the URL and querystring</span></span>
- <span data-ttu-id="d8136-708">일반 HTML 콘텐츠에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법, 모양과 느낌을 개선 하는 스타일 시트 및 HTML 콘텐츠를 표시 하는 보기 템플릿</span><span class="sxs-lookup"><span data-stu-id="d8136-708">How to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel and a View template to display HTML content</span></span>
- <span data-ttu-id="d8136-709">동적 정보를 표시 하기 위해 뷰 템플릿에 속성을 전달 하는 데 ViewModel 패턴을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d8136-709">How to use the ViewModel pattern for passing properties to the View template to display dynamic information</span></span>
- <span data-ttu-id="d8136-710">뷰 템플릿에서 컨트롤러에 전달 된 매개 변수를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d8136-710">How to use parameters passed to Controllers in the View template</span></span>
- <span data-ttu-id="d8136-711">ASP.NET MVC 응용 프로그램 내 페이지에 대 한 링크를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d8136-711">How to add links to pages inside the ASP.NET MVC application</span></span>
- <span data-ttu-id="d8136-712">뷰에서 동적 속성을 추가 하 고 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d8136-712">How to add and use dynamic properties in a View</span></span>
- <span data-ttu-id="d8136-713">ASP.NET MVC 4 프로젝트 템플릿의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="d8136-713">The enhancements in the ASP.NET MVC 4 project templates</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="d8136-714">부록 A: 웹에 대 한 Visual Studio Express 2012 설치</span><span class="sxs-lookup"><span data-stu-id="d8136-714">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="d8136-715">**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-715">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="d8136-716">다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-716">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="d8136-717">[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-717">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="d8136-718">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-718">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="d8136-719">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-719">Click on **Install Now**.</span></span> <span data-ttu-id="d8136-720">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-720">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="d8136-721">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-721">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="d8136-722">![Visual Studio Express 설치](aspnet-mvc-4-fundamentals/_static/image43.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="d8136-722">![Install Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="d8136-723">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="d8136-723">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="d8136-724">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-724">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-fundamentals/_static/image44.png)

    <span data-ttu-id="d8136-726">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="d8136-726">*Accepting the license terms*</span></span>
5. <span data-ttu-id="d8136-727">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-727">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-fundamentals/_static/image45.png)

    <span data-ttu-id="d8136-729">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="d8136-729">*Installation progress*</span></span>
6. <span data-ttu-id="d8136-730">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-730">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-fundamentals/_static/image46.png)

    <span data-ttu-id="d8136-732">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="d8136-732">*Installation completed*</span></span>
7. <span data-ttu-id="d8136-733">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-733">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="d8136-734">웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-734">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](aspnet-mvc-4-fundamentals/_static/image47.png)

    <span data-ttu-id="d8136-736">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="d8136-736">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="d8136-737">부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="d8136-737">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="d8136-738">이 부록에서는 windows azure 관리 포털에서 새 웹 사이트를 만들고 랩에 따라 가져온 응용 프로그램을 게시 하 여 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-738">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="d8136-739">작업 1-Windows Azure 포털에서 새 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="d8136-739">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="d8136-740">[Windows Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-740">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8136-741">Windows Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 후 트래픽 증가에 따라 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-741">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="d8136-742">[여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-742">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="d8136-743">![Windows Azure Portal에 로그온 합니다.](aspnet-mvc-4-fundamentals/_static/image48.png "Windows Azure Portal에 로그온 합니다.")</span><span class="sxs-lookup"><span data-stu-id="d8136-743">![Log on to Windows Azure portal](aspnet-mvc-4-fundamentals/_static/image48.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="d8136-744">*Windows Azure 관리 포털에 로그온 합니다.*</span><span class="sxs-lookup"><span data-stu-id="d8136-744">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="d8136-745">명령 모음에서 **새로 만들기** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-745">Click **New** on the command bar.</span></span>

    <span data-ttu-id="d8136-746">![새 웹 사이트 만들기](aspnet-mvc-4-fundamentals/_static/image49.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="d8136-746">![Creating a new Web Site](aspnet-mvc-4-fundamentals/_static/image49.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="d8136-747">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="d8136-747">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="d8136-748">**Compute** | **웹 사이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-748">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="d8136-749">그런 다음 **빠른 생성** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-749">Then select **Quick Create** option.</span></span> <span data-ttu-id="d8136-750">새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-750">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8136-751">Microsoft Azure 웹 사이트는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-751">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="d8136-752">빠른 생성 옵션을 사용 하면 포털 외부에서 Windows Azure 웹 사이트에 완료 된 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-752">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="d8136-753">데이터베이스를 설정 하는 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-753">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="d8136-754">![빠른 생성을 사용 하 여 새 웹 사이트 만들기](aspnet-mvc-4-fundamentals/_static/image50.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="d8136-754">![Creating a new Web Site using Quick Create](aspnet-mvc-4-fundamentals/_static/image50.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="d8136-755">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="d8136-755">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="d8136-756">새 **웹 사이트가** 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-756">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="d8136-757">웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-757">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="d8136-758">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-758">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="d8136-759">![새 웹 사이트로 이동](aspnet-mvc-4-fundamentals/_static/image51.png "새 웹 사이트로 이동")</span><span class="sxs-lookup"><span data-stu-id="d8136-759">![Browsing to the new web site](aspnet-mvc-4-fundamentals/_static/image51.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="d8136-760">*새 웹 사이트로 이동*</span><span class="sxs-lookup"><span data-stu-id="d8136-760">*Browsing to the new web site*</span></span>

    <span data-ttu-id="d8136-761">![웹 사이트 실행 중](aspnet-mvc-4-fundamentals/_static/image52.png "웹 사이트 실행 중")</span><span class="sxs-lookup"><span data-stu-id="d8136-761">![Web site running](aspnet-mvc-4-fundamentals/_static/image52.png "Web site running")</span></span>

    <span data-ttu-id="d8136-762">*웹 사이트 실행 중*</span><span class="sxs-lookup"><span data-stu-id="d8136-762">*Web site running*</span></span>
6. <span data-ttu-id="d8136-763">포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-763">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="d8136-764">![웹 사이트 관리 페이지 열기](aspnet-mvc-4-fundamentals/_static/image53.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="d8136-764">![Opening the web site management pages](aspnet-mvc-4-fundamentals/_static/image53.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="d8136-765">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="d8136-765">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="d8136-766">**대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-766">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8136-767">*게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-767">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="d8136-768">게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-768">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="d8136-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 게시 프로필 읽기를 지원 하 여 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하기 위해 이러한 프로그램의 구성을 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="d8136-770">![웹 사이트 게시 프로필을 다운로드 하는 중](aspnet-mvc-4-fundamentals/_static/image54.png "웹 사이트 게시 프로필을 다운로드 하는 중")</span><span class="sxs-lookup"><span data-stu-id="d8136-770">![Downloading the web site publish profile](aspnet-mvc-4-fundamentals/_static/image54.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="d8136-771">*웹 사이트 게시 프로필을 다운로드 하는 중*</span><span class="sxs-lookup"><span data-stu-id="d8136-771">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="d8136-772">알려진 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-772">Download the publish profile file to a known location.</span></span> <span data-ttu-id="d8136-773">이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-773">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="d8136-774">![게시 프로필 파일을 저장 하는 중](aspnet-mvc-4-fundamentals/_static/image55.png "게시 프로필을 저장 하는 중")</span><span class="sxs-lookup"><span data-stu-id="d8136-774">![Saving the publish profile file](aspnet-mvc-4-fundamentals/_static/image55.png "Saving the publish profile")</span></span>

    <span data-ttu-id="d8136-775">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="d8136-775">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="d8136-776">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="d8136-776">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="d8136-777">응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-777">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="d8136-778">SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-778">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="d8136-779">응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-779">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="d8136-780">Microsoft Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL 데이터베이스** | **서버** | **서버의 대시보드**.</span><span class="sxs-lookup"><span data-stu-id="d8136-780">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="d8136-781">만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-781">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="d8136-782">다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-782">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="d8136-783">이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d8136-783">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="d8136-784">![SQL Database 서버 대시보드](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="d8136-784">![SQL Database Server Dashboard](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="d8136-785">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="d8136-785">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="d8136-786">다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-786">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="d8136-787">이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](aspnet-mvc-4-fundamentals/_static/image57.png) 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-787">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) button.</span></span>

    ![클라이언트 IP 주소를 추가 하는 중](aspnet-mvc-4-fundamentals/_static/image58.png)

    <span data-ttu-id="d8136-789">*클라이언트 IP 주소를 추가 하는 중*</span><span class="sxs-lookup"><span data-stu-id="d8136-789">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="d8136-790">**클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-790">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 내용 확인](aspnet-mvc-4-fundamentals/_static/image59.png)

    <span data-ttu-id="d8136-792">*변경 내용 확인*</span><span class="sxs-lookup"><span data-stu-id="d8136-792">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="d8136-793">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="d8136-793">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="d8136-794">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-794">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="d8136-795">**솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-795">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="d8136-796">![응용 프로그램 게시](aspnet-mvc-4-fundamentals/_static/image60.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="d8136-796">![Publishing the Application](aspnet-mvc-4-fundamentals/_static/image60.png "Publishing the Application")</span></span>

    <span data-ttu-id="d8136-797">*웹 사이트 게시*</span><span class="sxs-lookup"><span data-stu-id="d8136-797">*Publishing the web site*</span></span>
2. <span data-ttu-id="d8136-798">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-798">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="d8136-799">![게시 프로필을 가져오는 중](aspnet-mvc-4-fundamentals/_static/image61.png "게시 프로필을 가져오는 중")</span><span class="sxs-lookup"><span data-stu-id="d8136-799">![Importing the publish profile](aspnet-mvc-4-fundamentals/_static/image61.png "Importing the publish profile")</span></span>

    <span data-ttu-id="d8136-800">*게시 프로필을 가져오는 중*</span><span class="sxs-lookup"><span data-stu-id="d8136-800">*Importing publish profile*</span></span>
3. <span data-ttu-id="d8136-801">**연결 유효성 검사**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-801">Click **Validate Connection**.</span></span> <span data-ttu-id="d8136-802">유효성 검사가 완료 되 면 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-802">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8136-803">유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-803">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="d8136-804">![연결 유효성 검사](aspnet-mvc-4-fundamentals/_static/image62.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="d8136-804">![Validating connection](aspnet-mvc-4-fundamentals/_static/image62.png "Validating connection")</span></span>

    <span data-ttu-id="d8136-805">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="d8136-805">*Validating connection*</span></span>
4. <span data-ttu-id="d8136-806">**설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-806">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="d8136-807">![웹 배포 구성](aspnet-mvc-4-fundamentals/_static/image63.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="d8136-807">![Web deploy configuration](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy configuration")</span></span>

    <span data-ttu-id="d8136-808">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="d8136-808">*Web deploy configuration*</span></span>
5. <span data-ttu-id="d8136-809">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-809">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="d8136-810">**서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-810">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="d8136-811">**사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-811">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="d8136-812">**암호** 에 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-812">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="d8136-813">새 데이터베이스 이름 (예: *MVC4SampleDB*)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-813">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="d8136-814">![대상 연결 문자열 구성](aspnet-mvc-4-fundamentals/_static/image64.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="d8136-814">![Configuring destination connection string](aspnet-mvc-4-fundamentals/_static/image64.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="d8136-815">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="d8136-815">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="d8136-816">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-816">Then click **OK**.</span></span> <span data-ttu-id="d8136-817">데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-817">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="d8136-818">![데이터베이스 만들기](aspnet-mvc-4-fundamentals/_static/image65.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="d8136-818">![Creating the database](aspnet-mvc-4-fundamentals/_static/image65.png "Creating the database string")</span></span>

    <span data-ttu-id="d8136-819">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="d8136-819">*Creating the database*</span></span>
7. <span data-ttu-id="d8136-820">Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-820">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="d8136-821">그런 후 **Next** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-821">Then click **Next**.</span></span>

    <span data-ttu-id="d8136-822">![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-fundamentals/_static/image66.png "SQL Database를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="d8136-822">![Connection string pointing to SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="d8136-823">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="d8136-823">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="d8136-824">**미리 보기** 페이지에서 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-824">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="d8136-825">![웹 응용 프로그램 게시](aspnet-mvc-4-fundamentals/_static/image67.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="d8136-825">![Publishing the web application](aspnet-mvc-4-fundamentals/_static/image67.png "Publishing the web application")</span></span>

    <span data-ttu-id="d8136-826">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="d8136-826">*Publishing the web application*</span></span>
9. <span data-ttu-id="d8136-827">게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-827">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="d8136-828">![Windows Azure에 게시 된 응용 프로그램](aspnet-mvc-4-fundamentals/_static/image68.png "Windows Azure에 게시 된 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="d8136-828">![Application published to Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="d8136-829">*Windows Azure에 게시 된 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="d8136-829">*Application published to Windows Azure*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="d8136-830">부록 C: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="d8136-830">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="d8136-831">코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-831">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="d8136-832">랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-832">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="d8136-833">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-fundamentals/_static/image69.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")</span><span class="sxs-lookup"><span data-stu-id="d8136-833">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-fundamentals/_static/image69.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="d8136-834">*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*</span><span class="sxs-lookup"><span data-stu-id="d8136-834">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="d8136-835">***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***</span><span class="sxs-lookup"><span data-stu-id="d8136-835">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="d8136-836">코드를 삽입할 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-836">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="d8136-837">조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-837">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="d8136-838">IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-838">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="d8136-839">올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-839">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="d8136-840">Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-840">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="d8136-841">![코드 조각 이름 입력 시작](aspnet-mvc-4-fundamentals/_static/image70.png "코드 조각 이름 입력 시작")</span><span class="sxs-lookup"><span data-stu-id="d8136-841">![Start typing the snippet name](aspnet-mvc-4-fundamentals/_static/image70.png "Start typing the snippet name")</span></span>

<span data-ttu-id="d8136-842">*코드 조각 이름 입력 시작*</span><span class="sxs-lookup"><span data-stu-id="d8136-842">*Start typing the snippet name*</span></span>

<span data-ttu-id="d8136-843">![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-fundamentals/_static/image71.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="d8136-843">![Press Tab to select the highlighted snippet](aspnet-mvc-4-fundamentals/_static/image71.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="d8136-844">*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="d8136-844">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="d8136-845">![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-fundamentals/_static/image72.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="d8136-845">![Press Tab again and the snippet will expand](aspnet-mvc-4-fundamentals/_static/image72.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="d8136-846">*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="d8136-846">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="d8136-847">***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1).</span><span class="sxs-lookup"><span data-stu-id="d8136-847">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="d8136-848">코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-848">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="d8136-849">코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-849">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="d8136-850">목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8136-850">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="d8136-851">![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-fundamentals/_static/image73.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="d8136-851">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="d8136-852">*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="d8136-852">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="d8136-853">![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-fundamentals/_static/image74.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="d8136-853">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-fundamentals/_static/image74.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="d8136-854">*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="d8136-854">*Pick the relevant snippet from the list, by clicking on it*</span></span>
