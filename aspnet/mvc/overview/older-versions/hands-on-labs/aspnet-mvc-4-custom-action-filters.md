---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 사용자 지정 작업 필터 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC는 작업 메서드를 호출 하기 전이나 후에 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다. 작업 필터는 사용자 지정 특성 tha
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468179"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="eded8-104">ASP.NET MVC 4 사용자 지정 작업 필터</span><span class="sxs-lookup"><span data-stu-id="eded8-104">ASP.NET MVC 4 Custom Action Filters</span></span>

<span data-ttu-id="eded8-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="eded8-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="eded8-106">웹 캠프 교육 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="eded8-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="eded8-107">ASP.NET MVC는 작업 메서드를 호출 하기 전이나 후에 필터링 논리를 실행 하기 위한 작업 필터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-107">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="eded8-108">작업 필터는 사전 작업 및 작업 후 동작을 컨트롤러의 작업 메서드에 추가 하는 선언적 방법을 제공 하는 사용자 지정 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-108">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>

<span data-ttu-id="eded8-109">이 실습 랩에서는 MvcMusicStore 솔루션에 사용자 지정 작업 필터 특성을 만들어 컨트롤러의 요청을 catch 하 고 사이트의 활동을 데이터베이스 테이블에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-109">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="eded8-110">모든 컨트롤러 또는 작업에 대 한 삽입으로 로깅 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-110">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="eded8-111">마지막으로 방문자 목록을 표시 하는 로그 보기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-111">Finally, you will see the log view that shows the list of visitors.</span></span>

<span data-ttu-id="eded8-112">이 실습 랩에서는 **ASP.NET MVC**에 대 한 기본 지식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-112">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="eded8-113">이전에 **ASP.NET mvc** 를 사용 하지 않은 경우 **ASP.NET mvc 4 기본** 실습 실습을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-113">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="eded8-114">모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="eded8-115">이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 사용자 지정 작업 필터](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-115">The project specific to this lab is available at [ASP.NET MVC 4 Custom Action Filters](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="eded8-116">목표</span><span class="sxs-lookup"><span data-stu-id="eded8-116">Objectives</span></span>

<span data-ttu-id="eded8-117">이 실습 랩에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="eded8-118">사용자 지정 작업 필터 특성을 만들어 필터링 기능 확장</span><span class="sxs-lookup"><span data-stu-id="eded8-118">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="eded8-119">특정 수준에 주입 별 사용자 지정 필터 특성 적용</span><span class="sxs-lookup"><span data-stu-id="eded8-119">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="eded8-120">사용자 지정 작업 필터를 전역적으로 등록</span><span class="sxs-lookup"><span data-stu-id="eded8-120">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="eded8-121">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="eded8-121">Prerequisites</span></span>

<span data-ttu-id="eded8-122">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-122">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="eded8-123">[웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="eded8-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="eded8-124">설치 프로그램</span><span class="sxs-lookup"><span data-stu-id="eded8-124">Setup</span></span>

<span data-ttu-id="eded8-125">**코드 조각 설치**</span><span class="sxs-lookup"><span data-stu-id="eded8-125">**Installing Code Snippets**</span></span>

<span data-ttu-id="eded8-126">편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-126">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="eded8-127">코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-127">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="eded8-128">Visual Studio Code 코드 조각에 대해 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [C: 코드 조각&quot;사용](#AppendixC) &quot;부록을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-128">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="eded8-129">실습</span><span class="sxs-lookup"><span data-stu-id="eded8-129">Exercises</span></span>

<span data-ttu-id="eded8-130">이 실습 랩은 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-130">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="eded8-131">연습 1: 로깅 작업</span><span class="sxs-lookup"><span data-stu-id="eded8-131">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="eded8-132">연습 2: 여러 작업 필터 관리</span><span class="sxs-lookup"><span data-stu-id="eded8-132">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="eded8-133">이 랩을 완료 하는 데 소요 되는 예상 시간: **30 분**</span><span class="sxs-lookup"><span data-stu-id="eded8-133">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="eded8-134">각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-134">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="eded8-135">연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-135">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="eded8-136">연습 1: 로깅 작업</span><span class="sxs-lookup"><span data-stu-id="eded8-136">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="eded8-137">이 연습에서는 ASP.NET MVC 4 필터 공급자를 사용 하 여 사용자 지정 작업 로그 필터를 만드는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-137">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="eded8-138">이렇게 하려면 선택한 컨트롤러의 모든 활동을 기록 하는 로깅 필터를 MusicStore 사이트에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-138">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="eded8-139">이 필터는 **Actionfilterattributeclass** 를 확장 하 고 **onactionexecuting** 메서드를 재정의 하 여 각 요청을 catch 한 다음 로깅 동작을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-139">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="eded8-140">HTTP 요청, 실행 메서드, 결과 및 매개 변수에 대 한 컨텍스트 정보는 ASP.NET MVC **ActionExecutingContext** 클래스에서 제공 됩니다 **.**</span><span class="sxs-lookup"><span data-stu-id="eded8-140">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="eded8-141">ASP.NET MVC 4에는 사용자 지정 필터를 만들지 않고 사용할 수 있는 기본 필터 공급자도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-141">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="eded8-142">ASP.NET MVC 4는 다음과 같은 유형의 필터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-142">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="eded8-143">**권한 부여** 필터-인증 수행 또는 요청 속성의 유효성 검사 등의 동작 메서드 실행 여부에 대 한 보안 결정을 내립니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-143">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="eded8-144">**작업 필터-** 작업 메서드 실행을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-144">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="eded8-145">이 필터는 작업 메서드에 추가 데이터를 제공 하거나 반환 값을 검사 하거나 작업 메서드의 실행을 취소 하는 등의 추가 처리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-145">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="eded8-146">**결과** 필터-actionresult 개체의 실행을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-146">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="eded8-147">이 필터는 HTTP 응답 수정과 같은 결과의 추가 처리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-147">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="eded8-148">**예외** 필터-권한 부여 필터부터 시작 하 여 결과 실행으로 끝나는 동작 메서드에서 처리 되지 않은 예외가 throw 되는 경우에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-148">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="eded8-149">예외 필터는 로깅 또는 오류 페이지 표시 등의 작업에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-149">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="eded8-150">필터 공급자에 대 한 자세한 내용은 MSDN 링크 ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx))를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="eded8-150">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="eded8-151">MVC Music Store 응용 프로그램 로깅 기능 정보</span><span class="sxs-lookup"><span data-stu-id="eded8-151">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="eded8-152">이 Music Store 솔루션에는 사이트 로깅, **Actionlog**에 대 한 새 데이터 모델 테이블이 있습니다 .이 테이블에는 요청을 수신 하는 컨트롤러의 이름 (작업, 클라이언트 IP 및 타임 스탬프) 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-152">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="eded8-153">![데이터 모델. ActionLog 테이블입니다.](aspnet-mvc-4-custom-action-filters/_static/image1.png "데이터 모델. ActionLog 테이블입니다.")</span><span class="sxs-lookup"><span data-stu-id="eded8-153">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="eded8-154">*데이터 모델-ActionLog 테이블*</span><span class="sxs-lookup"><span data-stu-id="eded8-154">*Data model - ActionLog table*</span></span>

<span data-ttu-id="eded8-155">이 솔루션은 **MvcMusicStores/Views/ActionLog**에서 찾을 수 있는 작업 로그에 대 한 ASP.NET MVC 뷰를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-155">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="eded8-156">![작업 로그 보기](aspnet-mvc-4-custom-action-filters/_static/image2.png "작업 로그 보기")</span><span class="sxs-lookup"><span data-stu-id="eded8-156">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="eded8-157">*작업 로그 보기*</span><span class="sxs-lookup"><span data-stu-id="eded8-157">*Action Log view*</span></span>

<span data-ttu-id="eded8-158">이 지정 된 구조를 사용 하 여 모든 작업은 컨트롤러의 요청을 중단 하 고 사용자 지정 필터링을 사용 하 여 로깅을 수행 하는 데 집중 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-158">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="eded8-159">작업 1-컨트롤러의 요청을 Catch 하는 사용자 지정 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="eded8-159">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="eded8-160">이 작업에서는 로깅 논리를 포함 하는 사용자 지정 필터 특성 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-160">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="eded8-161">이 목적을 위해 ASP.NET MVC **Actionfilterattribute** 클래스를 확장 하 고 **iactionfilter**인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-161">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="eded8-162">**Actionfilterattribute** 는 모든 특성 필터에 대 한 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-162">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="eded8-163">이 클래스는 다음 메서드를 제공 하 여 컨트롤러 작업의 실행 전후에 특정 논리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-163">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="eded8-164">**Onactionexecuting**(ActionExecutingContext filtercontext): 동작 메서드가 호출 되기 직전입니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-164">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="eded8-165">**Onactionexecuted**됨 (actionexecutedcontext filtercontext): 동작 메서드가 호출 되 고 결과가 실행 되기 전에 (뷰 렌더링 전)</span><span class="sxs-lookup"><span data-stu-id="eded8-165">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="eded8-166">**Onresultexecuting**(ResultExecutingContext filtercontext): 결과가 실행 되기 직전 (뷰 렌더링 전).</span><span class="sxs-lookup"><span data-stu-id="eded8-166">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="eded8-167">**Onresultexecuted**(resultexecutedcontext filtercontext): 뷰가 렌더링 된 후 결과가 실행 된 후</span><span class="sxs-lookup"><span data-stu-id="eded8-167">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="eded8-168">이러한 메서드를 파생 클래스로 재정의 하 여 사용자 고유의 필터링 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-168">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>

1. <span data-ttu-id="eded8-169">**\Source\Ex01-LoggingActions\Begin** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-169">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

   1. <span data-ttu-id="eded8-170">계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-170">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="eded8-171">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-171">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="eded8-172">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-172">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="eded8-173">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-173">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="eded8-174">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-174">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="eded8-175">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-175">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="eded8-176">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-176">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="eded8-177">자세한 내용은 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="eded8-177">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="eded8-178">Filters 폴더에 C# 새 클래스를 추가 하 고 이름을 *CustomActionFilter.cs*로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-178">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="eded8-179">이 폴더에는 모든 사용자 지정 필터가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-179">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="eded8-180">**CustomActionFilter.cs** 및 **MvcMusicStore** 네임 **스페이스에 대** 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-180">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="eded8-181">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-Ex1-CustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="eded8-181">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="eded8-182">**Actionfilterattribute** 에서 **CustomActionFilter** 클래스를 상속한 다음 **CustomActionFilter** 클래스가 **iactionfilter** 인터페이스를 구현 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-182">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="eded8-183">**CustomActionFilter** 클래스가 **onactionexecuting** 메서드를 재정의 하 고 필터 실행을 기록 하는 데 필요한 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-183">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="eded8-184">이렇게 하려면 **CustomActionFilter** 클래스 내에서 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-184">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="eded8-185">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-Ex1-LoggingActions*)</span><span class="sxs-lookup"><span data-stu-id="eded8-185">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="eded8-186">**Onactionexecuting** 메서드는 **Entity Framework** 을 사용 하 여 새 actionlog 레지스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-186">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="eded8-187">**Filtercontext**의 컨텍스트 정보를 사용 하 여 새 엔터티 인스턴스를 만들고 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-187">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="eded8-188">**Controllercontext** 클래스에 대 한 자세한 내용은 [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-188">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="eded8-189">작업 2-저장소 컨트롤러 클래스에 코드 인터셉터 삽입</span><span class="sxs-lookup"><span data-stu-id="eded8-189">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="eded8-190">이 태스크에서는 사용자 지정 필터를 기록 하는 모든 컨트롤러 클래스 및 컨트롤러 작업에 삽입 하 여 해당 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-190">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="eded8-191">이 연습에서는 저장소 컨트롤러 클래스에 로그가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-191">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="eded8-192">**Actionlogfilterattribute** 사용자 지정 필터에서 **onactionexecuting** 메서드는 삽입 된 요소가 호출 될 때 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-192">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="eded8-193">특정 컨트롤러 메서드를 가로챌 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-193">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="eded8-194">**StoreController** 에서 **MvcMusicStore\Controllers** 를 열고 **필터** 네임 스페이스에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-194">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="eded8-195">클래스 선언 앞에 **[CustomActionFilter]** 특성을 추가 하 여 사용자 지정 필터 **CustomActionFilter** 에 **StoreController** 클래스를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-195">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > <span data-ttu-id="eded8-196">필터가 컨트롤러 클래스에 삽입 되 면 모든 작업도 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-196">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="eded8-197">작업 집합에 대해서만 필터를 적용 하려면 각 항목에 **[CustomActionFilter]** 을 삽입 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-197">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="eded8-198">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="eded8-198">Task 3 - Running the Application</span></span>

<span data-ttu-id="eded8-199">이 작업에서 로깅 필터가 작동 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-199">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="eded8-200">응용 프로그램을 시작 하 고 스토어를 방문 하 고 기록 된 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-200">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="eded8-201">**F5** 키를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-201">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="eded8-202">**/Clog** 로 이동 하 여 로그 뷰 초기 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-202">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="eded8-203">![페이지 작업 전 로그 추적기 상태](aspnet-mvc-4-custom-action-filters/_static/image3.png "페이지 작업 전 로그 추적기 상태")</span><span class="sxs-lookup"><span data-stu-id="eded8-203">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="eded8-204">*페이지 작업 전 로그 추적기 상태*</span><span class="sxs-lookup"><span data-stu-id="eded8-204">*Log tracker status before page activity*</span></span>

   > [!NOTE]
   > <span data-ttu-id="eded8-205">기본적으로 메뉴에 대 한 기존 장르를 검색할 때 생성 되는 하나의 항목이 항상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-205">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
   > 
   > <span data-ttu-id="eded8-206">간단 하 게 하기 위해 응용 프로그램이 실행 될 때마다 **Actionlog** 테이블을 정리 하므로 각 특정 작업의 확인에 대 한 로그만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-206">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
   > 
   > <span data-ttu-id="eded8-207">저장소 컨트롤러 내에서 실행 되는 모든 작업에 대 한 기록 로그를 저장 하려면 **Session\_Start** 메서드 ( **global.asax 클래스)** 에서 다음 코드를 제거 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-207">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="eded8-208">메뉴에서 **장르** 중 하나를 클릭 하 고 사용 가능한 앨범 탐색과 같은 몇 가지 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-208">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="eded8-209">**/Actionlog** 로 이동 하 여 로그가 비어 있으면 **F5** 키를 눌러 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-209">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="eded8-210">방문이 추적 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-210">Check that your visits were tracked:</span></span>

    <span data-ttu-id="eded8-211">![작업이 기록 된 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image4.png "작업이 기록 된 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="eded8-211">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="eded8-212">*작업이 기록 된 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="eded8-212">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="eded8-213">연습 2: 여러 작업 필터 관리</span><span class="sxs-lookup"><span data-stu-id="eded8-213">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="eded8-214">이 연습에서는 StoreController 클래스에 두 번째 사용자 지정 작업 필터를 추가 하 고 두 필터를 실행할 특정 순서를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-214">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="eded8-215">그런 다음 코드를 업데이트 하 여 전역으로 필터를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-215">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="eded8-216">필터 실행 순서를 정의할 때 고려할 다른 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-216">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="eded8-217">예를 들어 Order 속성 및 필터 범위는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-217">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="eded8-218">각 필터의 **범위** 를 정의할 수 있습니다. 예를 들어 **컨트롤러 범위**내에서 실행 되는 모든 작업 필터의 범위를 지정 하 고 모든 권한 부여 필터를 **전역 범위**에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-218">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="eded8-219">범위는 실행 순서를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-219">The scopes have a defined execution order.</span></span>

<span data-ttu-id="eded8-220">또한 각 작업 필터에는 필터 범위에서 실행 순서를 결정 하는 데 사용 되는 Order 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-220">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="eded8-221">사용자 지정 작업 필터 실행 순서에 대 한 자세한 내용은 MSDN 문서 ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx))를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="eded8-221">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="eded8-222">작업 1: 새 사용자 지정 작업 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="eded8-222">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="eded8-223">이 작업에서는 StoreController 클래스에 삽입할 새 사용자 지정 작업 필터를 만들어 필터 실행 순서를 관리 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-223">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="eded8-224">**\Source\Ex02-ManagingMultipleActionFilters\Begin** 폴더에 있는 **시작** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-224">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="eded8-225">그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-225">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="eded8-226">제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-226">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="eded8-227">이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-227">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="eded8-228">**NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-228">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="eded8-229">마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-229">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="eded8-230">NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-230">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="eded8-231">NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-231">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="eded8-232">이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-232">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="eded8-233">자세한 내용은 [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="eded8-233">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="eded8-234">Filters 폴더에 C# 새 클래스를 추가 하 고 이름을 *MyNewCustomActionFilter.cs* 로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-234">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="eded8-235">**MyNewCustomActionFilter.cs** 을 열고 **system.web** 및 **MvcMusicStore** 네임 스페이스에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-235">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="eded8-236">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-Ex2-MyNewCustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="eded8-236">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="eded8-237">기본 클래스 선언을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-237">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="eded8-238">(코드 조각- *ASP.NET MVC 4 사용자 지정 작업 필터-Ex2-MyNewCustomActionFilterClass*)</span><span class="sxs-lookup"><span data-stu-id="eded8-238">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="eded8-239">이 사용자 지정 작업 필터는 이전 연습에서 만든 것과 거의 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-239">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="eded8-240">주요 차이점은 로그에 등록 된 필터를 식별 하기 위해이 새 클래스의 이름을 사용 하 여&quot;특성을 업데이트 *한&quot;* 를 포함 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-240">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify which filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="eded8-241">작업 2: StoreController 클래스에 새 코드 인터셉터 삽입</span><span class="sxs-lookup"><span data-stu-id="eded8-241">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="eded8-242">이 작업에서는 StoreController 클래스에 새 사용자 지정 필터를 추가 하 고 솔루션을 실행 하 여 두 필터가 함께 작동 하는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-242">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="eded8-243">**MvcMusicStore\Controllers** 에 있는 **StoreController** 클래스를 열고 다음 코드에 표시 된 것 처럼 **StoreController** 클래스에 새 사용자 지정 필터 **MyNewCustomActionFilter** 을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-243">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="eded8-244">이제 응용 프로그램을 실행 하 여 이러한 두 사용자 지정 작업 필터가 작동 하는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-244">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="eded8-245">이렇게 하려면 **F5** 키를 누르고 응용 프로그램이 시작 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-245">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="eded8-246">**/Clog** 로 이동 하 여 로그 뷰 초기 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-246">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="eded8-247">![페이지 작업 전 로그 추적기 상태](aspnet-mvc-4-custom-action-filters/_static/image5.png "페이지 작업 전 로그 추적기 상태")</span><span class="sxs-lookup"><span data-stu-id="eded8-247">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="eded8-248">*페이지 작업 전 로그 추적기 상태*</span><span class="sxs-lookup"><span data-stu-id="eded8-248">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="eded8-249">메뉴에서 **장르** 중 하나를 클릭 하 고 사용 가능한 앨범 탐색과 같은 몇 가지 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-249">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="eded8-250">이 시간이 있는지 확인 합니다. **StorageController** 클래스에 추가한 사용자 지정 작업 필터 각각에 대해 한 번씩, 두 번 방문이 추적 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-250">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="eded8-251">![작업이 기록 된 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image6.png "작업이 기록 된 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="eded8-251">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="eded8-252">*작업이 기록 된 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="eded8-252">*Action log with activity logged*</span></span>
6. <span data-ttu-id="eded8-253">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-253">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="eded8-254">작업 3: 필터 순서 관리</span><span class="sxs-lookup"><span data-stu-id="eded8-254">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="eded8-255">이 태스크에서는 Order 속성을 사용 하 여 필터 실행 순서를 관리 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-255">In this task, you will learn how to manage the filters' execution order by using the Order property.</span></span>

1. <span data-ttu-id="eded8-256">**MvcMusicStore\Controllers** 에 있는 **StoreController** 클래스를 열고 아래와 같이 두 필터 모두에 **Order** 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-256">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="eded8-257">이제 Order 속성의 값에 따라 필터를 실행 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-257">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="eded8-258">순서 값이 가장 작은 필터 (**CustomActionFilter**)가 가장 먼저 실행 되는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-258">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="eded8-259">**F5** 키를 누르고 응용 프로그램이 시작 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-259">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="eded8-260">**/Clog** 로 이동 하 여 로그 뷰 초기 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-260">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="eded8-261">![페이지 작업 전 로그 추적기 상태](aspnet-mvc-4-custom-action-filters/_static/image7.png "페이지 작업 전 로그 추적기 상태")</span><span class="sxs-lookup"><span data-stu-id="eded8-261">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="eded8-262">*페이지 작업 전 로그 추적기 상태*</span><span class="sxs-lookup"><span data-stu-id="eded8-262">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="eded8-263">메뉴에서 **장르** 중 하나를 클릭 하 고 사용 가능한 앨범 탐색과 같은 몇 가지 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-263">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="eded8-264">이번에는 ' Order value: **CustomActionFilter** logs ' 필터를 기준으로 방문 시간이 먼저 추적 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-264">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="eded8-265">![작업이 기록 된 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image8.png "작업이 기록 된 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="eded8-265">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="eded8-266">*작업이 기록 된 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="eded8-266">*Action log with activity logged*</span></span>
6. <span data-ttu-id="eded8-267">이제 필터의 순서 값을 업데이트 하 고 로깅 순서가 변경 되는 방식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-267">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="eded8-268">**StoreController** 클래스에서 아래와 같이 필터의 순서 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-268">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="eded8-269">**F5**키를 눌러 응용 프로그램을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-269">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="eded8-270">메뉴에서 **장르** 중 하나를 클릭 하 고 사용 가능한 앨범 탐색과 같은 몇 가지 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-270">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="eded8-271">이번에는 **MyNewCustomActionFilter** 필터로 만든 로그가 먼저 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-271">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="eded8-272">![작업이 기록 된 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image9.png "작업이 기록 된 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="eded8-272">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="eded8-273">*작업이 기록 된 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="eded8-273">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="eded8-274">작업 4: 전역으로 필터 등록</span><span class="sxs-lookup"><span data-stu-id="eded8-274">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="eded8-275">이 태스크에서는 새 필터 (**MyNewCustomActionFilter**)를 전역 필터로 등록 하도록 솔루션을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-275">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="eded8-276">이 작업을 수행 하면 응용 프로그램에서 수행 되는 모든 작업에 의해 트리거되고 이전 작업의 경우와 마찬가지로 StoreController에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-276">By doing this, it will be triggered by all the actions performed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="eded8-277">**StoreController** 클래스에서 [ **MyNewCustomActionFilter]** 특성과 Order 속성을 **[CustomActionFilter]** 에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-277">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="eded8-278">다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-278">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="eded8-279">**Global.asax** 파일을 열고 **응용 프로그램\_Start** 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-279">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="eded8-280">응용 프로그램이 시작 될 때마다 **Filterconfig** 클래스 내에서 **registerglobalfilters** 메서드를 호출 하 여 전역 필터를 등록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-280">Notice that each time the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="eded8-281">![Global.asax에 전역 필터를 등록 하는 중](aspnet-mvc-4-custom-action-filters/_static/image10.png "Global.asax에 전역 필터를 등록 하는 중")</span><span class="sxs-lookup"><span data-stu-id="eded8-281">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="eded8-282">*Global.asax에 전역 필터를 등록 하는 중*</span><span class="sxs-lookup"><span data-stu-id="eded8-282">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="eded8-283">**앱\_시작** 폴더에서 **FilterConfig.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-283">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="eded8-284">System.web를 사용 하 여에 대 한 참조 추가 MvcMusicStore 사용 공간.</span><span class="sxs-lookup"><span data-stu-id="eded8-284">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="eded8-285">**Registerglobalfilters** 메서드를 업데이트 하 여 사용자 지정 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-285">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="eded8-286">이렇게 하려면 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-286">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="eded8-287">**F5**를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-287">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="eded8-288">메뉴에서 **장르** 중 하나를 클릭 하 고 사용 가능한 앨범 탐색과 같은 몇 가지 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-288">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="eded8-289">이제 **[MyNewCustomActionFilter]** 가 HomeController 및 ActionLogController에 삽입 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-289">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="eded8-290">![작업이 기록 된 작업 로그](aspnet-mvc-4-custom-action-filters/_static/image11.png "작업이 기록 된 작업 로그")</span><span class="sxs-lookup"><span data-stu-id="eded8-290">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="eded8-291">*글로벌 활동이 기록 된 작업 로그*</span><span class="sxs-lookup"><span data-stu-id="eded8-291">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="eded8-292">또한 [부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)를 수행 하는 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-292">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="eded8-293">요약</span><span class="sxs-lookup"><span data-stu-id="eded8-293">Summary</span></span>

<span data-ttu-id="eded8-294">이 실습 실습을 완료 하면 작업 필터를 확장 하 여 사용자 지정 작업을 실행 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-294">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="eded8-295">또한 페이지 컨트롤러에 필터를 삽입 하는 방법도 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-295">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="eded8-296">사용 되는 개념은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-296">The following concepts were used:</span></span>

- <span data-ttu-id="eded8-297">ASP.NET MVC ActionFilterAttribute 클래스를 사용 하 여 사용자 지정 작업 필터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="eded8-297">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="eded8-298">ASP.NET MVC 컨트롤러에 필터를 삽입 하는 방법</span><span class="sxs-lookup"><span data-stu-id="eded8-298">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="eded8-299">Order 속성을 사용 하 여 필터 순서를 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="eded8-299">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="eded8-300">전역으로 필터를 등록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="eded8-300">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="eded8-301">부록 A: 웹에 대 한 Visual Studio Express 2012 설치</span><span class="sxs-lookup"><span data-stu-id="eded8-301">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="eded8-302">**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-302">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="eded8-303">다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-303">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="eded8-304">[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-304">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="eded8-305">또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-305">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="eded8-306">**지금 설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-306">Click on **Install Now**.</span></span> <span data-ttu-id="eded8-307">**웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-307">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="eded8-308">**웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-308">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="eded8-309">![Visual Studio Express 설치](aspnet-mvc-4-custom-action-filters/_static/image12.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="eded8-309">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="eded8-310">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="eded8-310">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="eded8-311">모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-311">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="eded8-313">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="eded8-313">*Accepting the license terms*</span></span>
5. <span data-ttu-id="eded8-314">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-314">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="eded8-316">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="eded8-316">*Installation progress*</span></span>
6. <span data-ttu-id="eded8-317">설치가 완료 되 면 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-317">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="eded8-319">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="eded8-319">*Installation completed*</span></span>
7. <span data-ttu-id="eded8-320">**끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-320">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="eded8-321">웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-321">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="eded8-323">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="eded8-323">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="eded8-324">부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="eded8-324">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="eded8-325">이 부록에서는 windows azure 관리 포털에서 새 웹 사이트를 만들고 랩에 따라 가져온 응용 프로그램을 게시 하 여 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-325">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="eded8-326">작업 1-Windows Azure 포털에서 새 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="eded8-326">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="eded8-327">[Windows Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-327">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eded8-328">Windows Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 후 트래픽 증가에 따라 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-328">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="eded8-329">[여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-329">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="eded8-330">![Windows Azure Portal에 로그온 합니다.](aspnet-mvc-4-custom-action-filters/_static/image17.png "Windows Azure Portal에 로그온 합니다.")</span><span class="sxs-lookup"><span data-stu-id="eded8-330">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="eded8-331">*Windows Azure 관리 포털에 로그온 합니다.*</span><span class="sxs-lookup"><span data-stu-id="eded8-331">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="eded8-332">명령 모음에서 **새로 만들기** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-332">Click **New** on the command bar.</span></span>

    <span data-ttu-id="eded8-333">![새 웹 사이트 만들기](aspnet-mvc-4-custom-action-filters/_static/image18.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="eded8-333">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="eded8-334">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="eded8-334">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="eded8-335">**Compute** | **웹 사이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-335">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="eded8-336">그런 다음 **빠른 생성** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-336">Then select **Quick Create** option.</span></span> <span data-ttu-id="eded8-337">새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-337">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eded8-338">Microsoft Azure 웹 사이트는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-338">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="eded8-339">빠른 생성 옵션을 사용 하면 포털 외부에서 Windows Azure 웹 사이트에 완료 된 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-339">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="eded8-340">데이터베이스를 설정 하는 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-340">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="eded8-341">![빠른 생성을 사용 하 여 새 웹 사이트 만들기](aspnet-mvc-4-custom-action-filters/_static/image19.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="eded8-341">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="eded8-342">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="eded8-342">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="eded8-343">새 **웹 사이트가** 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-343">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="eded8-344">웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-344">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="eded8-345">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-345">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="eded8-346">![새 웹 사이트로 이동](aspnet-mvc-4-custom-action-filters/_static/image20.png "새 웹 사이트로 이동")</span><span class="sxs-lookup"><span data-stu-id="eded8-346">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="eded8-347">*새 웹 사이트로 이동*</span><span class="sxs-lookup"><span data-stu-id="eded8-347">*Browsing to the new web site*</span></span>

    <span data-ttu-id="eded8-348">![웹 사이트 실행 중](aspnet-mvc-4-custom-action-filters/_static/image21.png "웹 사이트 실행 중")</span><span class="sxs-lookup"><span data-stu-id="eded8-348">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="eded8-349">*웹 사이트 실행 중*</span><span class="sxs-lookup"><span data-stu-id="eded8-349">*Web site running*</span></span>
6. <span data-ttu-id="eded8-350">포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-350">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="eded8-351">![웹 사이트 관리 페이지 열기](aspnet-mvc-4-custom-action-filters/_static/image22.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="eded8-351">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="eded8-352">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="eded8-352">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="eded8-353">**대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-353">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eded8-354">*게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-354">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="eded8-355">게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-355">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="eded8-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 게시 프로필 읽기를 지원 하 여 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하기 위해 이러한 프로그램의 구성을 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="eded8-357">![웹 사이트 게시 프로필을 다운로드 하는 중](aspnet-mvc-4-custom-action-filters/_static/image23.png "웹 사이트 게시 프로필을 다운로드 하는 중")</span><span class="sxs-lookup"><span data-stu-id="eded8-357">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="eded8-358">*웹 사이트 게시 프로필을 다운로드 하는 중*</span><span class="sxs-lookup"><span data-stu-id="eded8-358">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="eded8-359">알려진 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-359">Download the publish profile file to a known location.</span></span> <span data-ttu-id="eded8-360">이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-360">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="eded8-361">![게시 프로필 파일을 저장 하는 중](aspnet-mvc-4-custom-action-filters/_static/image24.png "게시 프로필을 저장 하는 중")</span><span class="sxs-lookup"><span data-stu-id="eded8-361">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="eded8-362">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="eded8-362">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="eded8-363">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="eded8-363">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="eded8-364">응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-364">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="eded8-365">SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-365">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="eded8-366">응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-366">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="eded8-367">Microsoft Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL 데이터베이스** | **서버** | **서버의 대시보드**.</span><span class="sxs-lookup"><span data-stu-id="eded8-367">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="eded8-368">만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-368">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="eded8-369">다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-369">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="eded8-370">이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="eded8-370">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="eded8-371">![SQL Database 서버 대시보드](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="eded8-371">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="eded8-372">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="eded8-372">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="eded8-373">다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-373">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="eded8-374">이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](aspnet-mvc-4-custom-action-filters/_static/image26.png) 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-374">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![클라이언트 IP 주소를 추가 하는 중](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="eded8-376">*클라이언트 IP 주소를 추가 하는 중*</span><span class="sxs-lookup"><span data-stu-id="eded8-376">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="eded8-377">**클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-377">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 내용 확인](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="eded8-379">*변경 내용 확인*</span><span class="sxs-lookup"><span data-stu-id="eded8-379">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="eded8-380">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="eded8-380">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="eded8-381">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-381">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="eded8-382">**솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-382">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="eded8-383">![응용 프로그램 게시](aspnet-mvc-4-custom-action-filters/_static/image29.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="eded8-383">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="eded8-384">*웹 사이트 게시*</span><span class="sxs-lookup"><span data-stu-id="eded8-384">*Publishing the web site*</span></span>
2. <span data-ttu-id="eded8-385">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-385">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="eded8-386">![게시 프로필을 가져오는 중](aspnet-mvc-4-custom-action-filters/_static/image30.png "게시 프로필을 가져오는 중")</span><span class="sxs-lookup"><span data-stu-id="eded8-386">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="eded8-387">*게시 프로필을 가져오는 중*</span><span class="sxs-lookup"><span data-stu-id="eded8-387">*Importing publish profile*</span></span>
3. <span data-ttu-id="eded8-388">**연결 유효성 검사**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-388">Click **Validate Connection**.</span></span> <span data-ttu-id="eded8-389">유효성 검사가 완료 되 면 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-389">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eded8-390">유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-390">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="eded8-391">![연결 유효성 검사](aspnet-mvc-4-custom-action-filters/_static/image31.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="eded8-391">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="eded8-392">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="eded8-392">*Validating connection*</span></span>
4. <span data-ttu-id="eded8-393">**설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-393">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="eded8-394">![웹 배포 구성](aspnet-mvc-4-custom-action-filters/_static/image32.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="eded8-394">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="eded8-395">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="eded8-395">*Web deploy configuration*</span></span>
5. <span data-ttu-id="eded8-396">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-396">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="eded8-397">**서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-397">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="eded8-398">**사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-398">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="eded8-399">**암호** 에 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-399">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="eded8-400">새 데이터베이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-400">Type a new database name.</span></span>

     <span data-ttu-id="eded8-401">![대상 연결 문자열 구성](aspnet-mvc-4-custom-action-filters/_static/image33.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="eded8-401">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="eded8-402">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="eded8-402">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="eded8-403">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-403">Then click **OK**.</span></span> <span data-ttu-id="eded8-404">데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-404">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="eded8-405">![데이터베이스 만들기](aspnet-mvc-4-custom-action-filters/_static/image34.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="eded8-405">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="eded8-406">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="eded8-406">*Creating the database*</span></span>
7. <span data-ttu-id="eded8-407">Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-407">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="eded8-408">그런 후 **Next** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-408">Then click **Next**.</span></span>

    <span data-ttu-id="eded8-409">![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-custom-action-filters/_static/image35.png "SQL Database를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="eded8-409">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="eded8-410">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="eded8-410">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="eded8-411">**미리 보기** 페이지에서 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-411">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="eded8-412">![웹 응용 프로그램 게시](aspnet-mvc-4-custom-action-filters/_static/image36.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="eded8-412">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="eded8-413">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="eded8-413">*Publishing the web application*</span></span>
9. <span data-ttu-id="eded8-414">게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-414">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="eded8-415">부록 C: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="eded8-415">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="eded8-416">코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-416">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="eded8-417">랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-417">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="eded8-418">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-custom-action-filters/_static/image37.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")</span><span class="sxs-lookup"><span data-stu-id="eded8-418">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="eded8-419">*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*</span><span class="sxs-lookup"><span data-stu-id="eded8-419">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="eded8-420">***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***</span><span class="sxs-lookup"><span data-stu-id="eded8-420">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="eded8-421">코드를 삽입할 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-421">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="eded8-422">조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-422">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="eded8-423">IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-423">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="eded8-424">올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-424">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="eded8-425">Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-425">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="eded8-426">![코드 조각 이름 입력 시작](aspnet-mvc-4-custom-action-filters/_static/image38.png "코드 조각 이름 입력 시작")</span><span class="sxs-lookup"><span data-stu-id="eded8-426">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="eded8-427">*코드 조각 이름 입력 시작*</span><span class="sxs-lookup"><span data-stu-id="eded8-427">*Start typing the snippet name*</span></span>

<span data-ttu-id="eded8-428">![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-custom-action-filters/_static/image39.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="eded8-428">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="eded8-429">*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="eded8-429">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="eded8-430">![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-custom-action-filters/_static/image40.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")</span><span class="sxs-lookup"><span data-stu-id="eded8-430">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="eded8-431">*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="eded8-431">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="eded8-432">***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1).</span><span class="sxs-lookup"><span data-stu-id="eded8-432">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="eded8-433">코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-433">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="eded8-434">코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-434">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="eded8-435">목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eded8-435">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="eded8-436">![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-custom-action-filters/_static/image41.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="eded8-436">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="eded8-437">*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="eded8-437">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="eded8-438">![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-custom-action-filters/_static/image42.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="eded8-438">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="eded8-439">*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="eded8-439">*Pick the relevant snippet from the list, by clicking on it*</span></span>
