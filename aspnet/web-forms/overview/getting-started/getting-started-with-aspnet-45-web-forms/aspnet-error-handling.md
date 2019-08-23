---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET 오류 처리 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: f420be369801208fa875d9a60e6e154afbe84aa7
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995315"
---
# <a name="aspnet-error-handling"></a><span data-ttu-id="45d7d-103">ASP.NET 오류 처리</span><span class="sxs-lookup"><span data-stu-id="45d7d-103">ASP.NET Error Handling</span></span>

<span data-ttu-id="45d7d-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="45d7d-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="45d7d-105">[정문 장난감 샘플 프로젝트 (C#) 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="45d7d-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="45d7d-106">이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="45d7d-107">[소스 코드를 포함 C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트는이 자습서 계열과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="45d7d-108">이 자습서에서는 오류 처리 및 오류 로깅을 포함 하도록 정문 장난감 샘플 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-108">In this tutorial, you will modify the Wingtip Toys sample application to include error handling and error logging.</span></span> <span data-ttu-id="45d7d-109">오류를 처리 하면 응용 프로그램에서 오류를 정상적으로 처리 하 고 오류 메시지를 적절 하 게 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-109">Error handling will allow the application to gracefully handle errors and display error messages accordingly.</span></span> <span data-ttu-id="45d7d-110">오류 로깅을 사용 하면 발생 한 오류를 찾아 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-110">Error logging will allow you to find and fix errors that have occurred.</span></span> <span data-ttu-id="45d7d-111">이 자습서는 이전 자습서 "URL 라우팅"을 기반으로 하며, 정문 장난감 자습서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-111">This tutorial builds on the previous tutorial "URL Routing" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="45d7d-112">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="45d7d-112">What you'll learn:</span></span>

- <span data-ttu-id="45d7d-113">응용 프로그램의 구성에 전역 오류 처리를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-113">How to add global error handling to the application's configuration.</span></span>
- <span data-ttu-id="45d7d-114">응용 프로그램, 페이지 및 코드 수준에서 오류 처리를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-114">How to add error handling at the application, page, and code levels.</span></span>
- <span data-ttu-id="45d7d-115">나중에 검토할 수 있도록 오류를 기록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-115">How to log errors for later review.</span></span>
- <span data-ttu-id="45d7d-116">보안을 손상 시 키 지 않는 오류 메시지를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-116">How to display error messages that do not compromise security.</span></span>
- <span data-ttu-id="45d7d-117">오류 로깅 모듈 및 처리기 (ELMAH) 오류 로깅을 구현 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-117">How to implement Error Logging Modules and Handlers (ELMAH) error logging.</span></span>

## <a name="overview"></a><span data-ttu-id="45d7d-118">개요</span><span class="sxs-lookup"><span data-stu-id="45d7d-118">Overview</span></span>

<span data-ttu-id="45d7d-119">ASP.NET 응용 프로그램은 실행 중에 발생 하는 오류를 일관 된 방식으로 처리할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-119">ASP.NET applications must be able to handle errors that occur during execution in a consistent manner.</span></span> <span data-ttu-id="45d7d-120">ASP.NET은 일관 된 방식으로 응용 프로그램에 오류를 알리는 방법을 제공 하는 CLR (공용 언어 런타임)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-120">ASP.NET uses the common language runtime (CLR), which provides a way of notifying applications of errors in a uniform way.</span></span> <span data-ttu-id="45d7d-121">오류가 발생 하면 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-121">When an error occurs, an exception is thrown.</span></span> <span data-ttu-id="45d7d-122">예외는 응용 프로그램에서 발생 하는 오류, 조건 또는 예기치 않은 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-122">An exception is any error, condition, or unexpected behavior that an application encounters.</span></span>

<span data-ttu-id="45d7d-123">.NET Framework에서 예외는 `System.Exception`에서 상속받은 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-123">In the .NET Framework, an exception is an object that inherits from the `System.Exception` class.</span></span> <span data-ttu-id="45d7d-124">예외는 문제가 발생한 코드 영역에서 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-124">An exception is thrown from an area of code where a problem has occurred.</span></span> <span data-ttu-id="45d7d-125">예외는 응용 프로그램에서 예외를 처리 하는 코드를 제공 하는 위치로 호출 스택을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-125">The exception is passed up the call stack to a place where the application provides code to handle the exception.</span></span> <span data-ttu-id="45d7d-126">응용 프로그램에서 예외를 처리 하지 않는 경우 브라우저는 오류 세부 정보를 표시 하도록 강제 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-126">If the application does not handle the exception, the browser is forced to display the error details.</span></span>

<span data-ttu-id="45d7d-127">코드 내에서 `Try` 블록의 / `Catch` 코드수준에서`Finally` 오류를 처리 하는 것이 가장 좋습니다. /</span><span class="sxs-lookup"><span data-stu-id="45d7d-127">As a best practice, handle errors in at the code level in `Try`/`Catch`/`Finally` blocks within your code.</span></span> <span data-ttu-id="45d7d-128">사용자가 발생 하는 상황에서 문제를 해결할 수 있도록 이러한 블록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-128">Try to place these blocks so that the user can correct problems in the context in which they occur.</span></span> <span data-ttu-id="45d7d-129">오류 처리 블록이 오류가 발생 한 위치에서 너무 멀리 떨어져 있는 경우 문제를 해결 하는 데 필요한 정보를 사용자에 게 제공 하는 것이 더 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-129">If the error handling blocks are too far away from where the error occurred, it becomes more difficult to provide users with the information they need to fix the problem.</span></span>

### <a name="exception-class"></a><span data-ttu-id="45d7d-130">Exception 클래스</span><span class="sxs-lookup"><span data-stu-id="45d7d-130">Exception Class</span></span>

<span data-ttu-id="45d7d-131">예외 클래스는 예외가 상속 되는 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-131">The Exception class is the base class from which exceptions inherit.</span></span> <span data-ttu-id="45d7d-132">대부분의 예외 개체는 `SystemException` 클래스 `IndexOutOfRangeException` , 클래스 또는 `ArgumentNullException` 클래스와 같은 예외 클래스의 일부 파생 클래스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-132">Most exception objects are instances of some derived class of the Exception class, such as the `SystemException` class, the `IndexOutOfRangeException` class, or the `ArgumentNullException` class.</span></span> <span data-ttu-id="45d7d-133">Exception 클래스에는 발생 한 오류에 대 `StackTrace` 한 특정 정보를 제공 하는 `Message` 속성, 속성, 속성 등의 속성이 있습니다 `InnerException` .</span><span class="sxs-lookup"><span data-stu-id="45d7d-133">The Exception class has properties, such as the `StackTrace` property, the `InnerException` property, and the `Message` property, that provide specific information about the error that has occurred.</span></span>

### <a name="exception-inheritance-hierarchy"></a><span data-ttu-id="45d7d-134">예외 상속 계층 구조</span><span class="sxs-lookup"><span data-stu-id="45d7d-134">Exception Inheritance Hierarchy</span></span>

<span data-ttu-id="45d7d-135">런타임에는 예외가 발생할 때 런타임이 throw 하는 `SystemException` 클래스에서 파생 되는 기본 예외 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-135">The runtime has a base set of exceptions deriving from the `SystemException` class that the runtime throws when an exception is encountered.</span></span> <span data-ttu-id="45d7d-136">`IndexOutOfRangeException` 클래스`ArgumentNullException` 및 클래스와 같은 예외 클래스에서 상속 되는 대부분의 클래스는 추가 멤버를 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-136">Most of the classes that inherit from the Exception class, such as the `IndexOutOfRangeException` class and the `ArgumentNullException` class, do not implement additional members.</span></span> <span data-ttu-id="45d7d-137">따라서 예외에 대 한 가장 중요 한 정보는 예외 계층 구조, 예외 이름 및 예외에 포함 된 정보에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-137">Therefore, the most important information for an exception can be found in the hierarchy of exceptions, the exception name, and the information contained in the exception.</span></span>

### <a name="exception-handling-hierarchy"></a><span data-ttu-id="45d7d-138">예외 처리 계층 구조</span><span class="sxs-lookup"><span data-stu-id="45d7d-138">Exception Handling Hierarchy</span></span>

<span data-ttu-id="45d7d-139">ASP.NET Web Forms 응용 프로그램에서는 특정 처리 계층 구조를 기반으로 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-139">In an ASP.NET Web Forms application, exceptions can be handled based on a specific handling hierarchy.</span></span> <span data-ttu-id="45d7d-140">다음 수준에서 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-140">An exception can be handled at the following levels:</span></span>

- <span data-ttu-id="45d7d-141">응용 프로그램 수준</span><span class="sxs-lookup"><span data-stu-id="45d7d-141">Application level</span></span>
- <span data-ttu-id="45d7d-142">페이지 수준</span><span class="sxs-lookup"><span data-stu-id="45d7d-142">Page level</span></span>
- <span data-ttu-id="45d7d-143">코드 수준</span><span class="sxs-lookup"><span data-stu-id="45d7d-143">Code level</span></span>

<span data-ttu-id="45d7d-144">응용 프로그램에서 예외를 처리 하는 경우 예외 클래스에서 상속 된 예외에 대 한 추가 정보를 검색 하 여 사용자에 게 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-144">When an application handles exceptions, additional information about the exception that is inherited from the Exception class can often be retrieved and displayed to the user.</span></span> <span data-ttu-id="45d7d-145">응용 프로그램, 페이지 및 코드 수준 외에도 HTTP 모듈 수준에서 및 IIS 사용자 지정 처리기를 사용 하 여 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-145">In addition to application, page, and code level, you can also handle exceptions at the HTTP module level and by using an IIS custom handler.</span></span>

### <a name="application-level-error-handling"></a><span data-ttu-id="45d7d-146">응용 프로그램 수준 오류 처리</span><span class="sxs-lookup"><span data-stu-id="45d7d-146">Application Level Error Handling</span></span>

<span data-ttu-id="45d7d-147">응용 프로그램의 구성을 수정 하거나 응용 프로그램의 `Application_Error` *global.asax* 파일에 처리기를 추가 하 여 응용 프로그램 수준에서 기본 오류를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-147">You can handle default errors at the application level either by modifying your application's configuration or by adding an `Application_Error` handler in the *Global.asax* file of your application.</span></span>

<span data-ttu-id="45d7d-148">Web.config 파일에 섹션을 `customErrors` 추가 하 여 기본 오류 및 HTTP 오류를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-148">You can handle default errors and HTTP errors by adding a `customErrors` section to the *Web.config* file.</span></span> <span data-ttu-id="45d7d-149">섹션 `customErrors` 에서는 오류가 발생할 때 사용자가 리디렉션되는 기본 페이지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-149">The `customErrors` section allows you to specify a default page that users will be redirected to when an error occurs.</span></span> <span data-ttu-id="45d7d-150">또한 특정 상태 코드 오류에 대 한 개별 페이지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-150">It also allows you to specify individual pages for specific status code errors.</span></span>

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

<span data-ttu-id="45d7d-151">그러나 구성을 사용 하 여 사용자를 다른 페이지로 리디렉션하는 경우 발생 한 오류에 대 한 세부 정보가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-151">Unfortunately, when you use the configuration to redirect the user to a different page, you do not have the details of the error that occurred.</span></span>

<span data-ttu-id="45d7d-152">그러나 `Application_Error` *global.asax* 파일의 처리기에 코드를 추가 하 여 응용 프로그램의 어디에서 나 발생 하는 오류를 트래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-152">However, you can trap errors that occur anywhere in your application by adding code to the `Application_Error` handler in the *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a><span data-ttu-id="45d7d-153">페이지 수준 오류 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="45d7d-153">Page Level Error Event Handling</span></span>

<span data-ttu-id="45d7d-154">페이지 수준 처리기는 오류가 발생 한 페이지로 사용자를 반환 하지만 컨트롤의 인스턴스가 유지 되지 않으므로 페이지에 더 이상 아무 것도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-154">A page-level handler returns the user to the page where the error occurred, but because instances of controls are not maintained, there will no longer be anything on the page.</span></span> <span data-ttu-id="45d7d-155">응용 프로그램의 사용자에 게 오류 정보를 제공 하려면 특히 오류 세부 정보를 페이지에 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-155">To provide the error details to the user of the application, you must specifically write the error details to the page.</span></span>

<span data-ttu-id="45d7d-156">일반적으로 페이지 수준 오류 처리기를 사용 하 여 처리 되지 않은 오류를 기록 하거나 사용자가 유용한 정보를 표시할 수 있는 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-156">You would typically use a page-level error handler to log unhandled errors or to take the user to a page that can display helpful information.</span></span>

<span data-ttu-id="45d7d-157">이 코드 예제에서는 ASP.NET 웹 페이지의 오류 이벤트에 대 한 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-157">This code example shows a handler for the Error event in an ASP.NET Web page.</span></span> <span data-ttu-id="45d7d-158">이 처리기는 페이지의 블록 내 `try` / `catch` 에서 아직 처리 되지 않은 모든 예외를 catch 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-158">This handler catches all exceptions that are not already handled within `try`/`catch` blocks in the page.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

<span data-ttu-id="45d7d-159">오류를 처리 한 후에는 서버 개체 ( `ClearError` `HttpServerUtility` 클래스)의 메서드를 호출 하 여 해당 오류를 지워야 합니다. 그렇지 않으면 이전에 발생 한 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-159">After you handle an error, you must clear it by calling the `ClearError` method of the Server object (`HttpServerUtility` class), otherwise you will see an error that has previously occurred.</span></span>

### <a name="code-level-error-handling"></a><span data-ttu-id="45d7d-160">코드 수준 오류 처리</span><span class="sxs-lookup"><span data-stu-id="45d7d-160">Code Level Error Handling</span></span>

<span data-ttu-id="45d7d-161">Try-catch 문은 다른 예외에 대 한 처리기를 지정 하는 하나 이상의 catch 절 뒤에 try 블록으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-161">The try-catch statement consists of a try block followed by one or more catch clauses, which specify handlers for different exceptions.</span></span> <span data-ttu-id="45d7d-162">예외가 throw 되 면 CLR (공용 언어 런타임)에서이 예외를 처리 하는 catch 문을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-162">When an exception is thrown, the common language runtime (CLR) looks for the catch statement that handles this exception.</span></span> <span data-ttu-id="45d7d-163">현재 실행 중인 메서드에 catch 블록이 없는 경우 CLR에서는 현재 메서드를 호출한 메서드 등을 확인 하 여 호출 스택을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-163">If the currently executing method does not contain a catch block, the CLR looks at the method that called the current method, and so on, up the call stack.</span></span> <span data-ttu-id="45d7d-164">Catch 블록을 찾을 수 없는 경우 CLR은 처리 되지 않은 예외 메시지를 사용자에 게 표시 하 고 프로그램의 실행을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-164">If no catch block is found, then the CLR displays an unhandled exception message to the user and stops execution of the program.</span></span>

<span data-ttu-id="45d7d-165">다음 코드 예제에서는를 사용 `try` 하 여 / `catch` / `finally` 오류를 처리 하는 일반적인 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-165">The following code example shows a common way of using `try`/`catch`/`finally` to handle errors.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

<span data-ttu-id="45d7d-166">위의 코드에서 try 블록은 가능한 예외에 대해 보호 해야 하는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-166">In the above code, the try block contains the code that needs to be guarded against a possible exception.</span></span> <span data-ttu-id="45d7d-167">블록은 예외가 throw 되거나 블록이 성공적으로 완료 될 때까지 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-167">The block is executed until either an exception is thrown or the block is completed successfully.</span></span> <span data-ttu-id="45d7d-168">`FileNotFoundException` 예외가 발생`IOException` 하거나 예외가 발생 하면 실행이 다른 페이지로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-168">If either a `FileNotFoundException` exception or an `IOException` exception occurs, the execution is transferred to a different page.</span></span> <span data-ttu-id="45d7d-169">그런 다음 오류가 발생 했는지 여부에 관계 없이 finally 블록에 포함 된 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-169">Then, the code contained in the finally block is executed, whether an error occurred or not.</span></span>

## <a name="adding-error-logging-support"></a><span data-ttu-id="45d7d-170">오류 로깅 지원 추가</span><span class="sxs-lookup"><span data-stu-id="45d7d-170">Adding Error Logging Support</span></span>

<span data-ttu-id="45d7d-171">정문 장난감 샘플 응용 프로그램에 오류 처리를 추가 하기 전에 `ExceptionUtility` *논리* 폴더에 클래스를 추가 하 여 오류 로깅 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-171">Before adding error handling to the Wingtip Toys sample application, you will add error logging support by adding an `ExceptionUtility` class to the *Logic* folder.</span></span> <span data-ttu-id="45d7d-172">이렇게 하면 응용 프로그램에서 오류를 처리할 때마다 오류 로그 파일에 오류 정보가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-172">By doing this, each time the application handles an error, the error details will be added to the error log file.</span></span>

1. <span data-ttu-id="45d7d-173">*논리* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새 항목** **추가**  - &gt; 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-173">Right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="45d7d-174">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-174">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="45d7d-175">왼쪽의 **시각적 C#**   -코드템플릿 그룹을 선택 합니다. &gt;</span><span class="sxs-lookup"><span data-stu-id="45d7d-175">Select the **Visual C#** -&gt; **Code** templates group on the left.</span></span> <span data-ttu-id="45d7d-176">그런 다음 가운데 목록에서 **클래스**를 선택 하 고 이름을 **ExceptionUtility.cs**로 지정한 다음</span><span class="sxs-lookup"><span data-stu-id="45d7d-176">Then, select **Class**from the middle list and name it **ExceptionUtility.cs**.</span></span>
3. <span data-ttu-id="45d7d-177">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-177">Choose **Add**.</span></span> <span data-ttu-id="45d7d-178">새 클래스 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-178">The new class file is displayed.</span></span>
4. <span data-ttu-id="45d7d-179">기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-179">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

<span data-ttu-id="45d7d-180">예외가 발생 하면 메서드를 `LogException` 호출 하 여 예외를 예외 로그 파일에 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-180">When an exception occurs, the exception can be written to an exception log file by calling the `LogException` method.</span></span> <span data-ttu-id="45d7d-181">이 메서드는 예외 개체와 예외의 소스에 대 한 세부 정보를 포함 하는 문자열의 두 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-181">This method takes two parameters, the exception object and a string containing details about the source of the exception.</span></span> <span data-ttu-id="45d7d-182">예외 로그는 *응용 프로그램\_데이터* 폴더의 *오류 로그 .txt* 파일에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-182">The exception log is written to the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>

### <a name="adding-an-error-page"></a><span data-ttu-id="45d7d-183">오류 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="45d7d-183">Adding an Error Page</span></span>

<span data-ttu-id="45d7d-184">정문 장난감 샘플 응용 프로그램에서 한 페이지는 오류를 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-184">In the Wingtip Toys sample application, one page will be used to display errors.</span></span> <span data-ttu-id="45d7d-185">오류 페이지는 사이트 사용자에 게 보안 오류 메시지를 표시 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-185">The error page is designed to show a secure error message to users of the site.</span></span> <span data-ttu-id="45d7d-186">그러나 사용자가 코드가 있는 컴퓨터에서 로컬로 제공 되는 HTTP 요청을 작성 하는 개발자 인 경우 오류 페이지에 추가 오류 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-186">However, if the user is a developer making an HTTP request that is being served locally on the machine where the code lives, additional error details will be displayed on the error page.</span></span>

1. <span data-ttu-id="45d7d-187">**솔루션 탐색기** 에서 프로젝트 이름 (**정문 장난감**)을 마우스 오른쪽 단추로 클릭 하 고 **새 항목** **추가**  - &gt; 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-187">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="45d7d-188">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-188">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="45d7d-189">왼쪽의 **시각적 C#**   -웹템플릿 그룹을 선택 합니다. &gt;</span><span class="sxs-lookup"><span data-stu-id="45d7d-189">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="45d7d-190">중간 목록에서 **마스터 페이지로 웹 폼**을 선택 하 고 이름을 **errorpage .aspx**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-190">From the middle list, select **Web Form with Master Page**,and name it **ErrorPage.aspx**.</span></span>
3. <span data-ttu-id="45d7d-191">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-191">Click **Add**.</span></span>
4. <span data-ttu-id="45d7d-192">마스터 페이지로 *site.master* 파일을 선택 하 고 **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-192">Select the *Site.Master* file as the master page, and then choose **OK**.</span></span>
5. <span data-ttu-id="45d7d-193">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-193">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. <span data-ttu-id="45d7d-194">다음과 같이 표시 되도록 코드 숨김으로 (*ErrorPage.aspx.cs*)의 기존 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-194">Replace the existing code of the code-behind (*ErrorPage.aspx.cs*) so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

<span data-ttu-id="45d7d-195">오류 페이지가 표시 `Page_Load` 되 면 이벤트 처리기가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-195">When the error page is displayed, the `Page_Load` event handler is executed.</span></span> <span data-ttu-id="45d7d-196">`Page_Load` 처리기에서 오류가 처음 처리 된 위치가 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-196">In the `Page_Load` handler, the location of where the error was first handled is determined.</span></span> <span data-ttu-id="45d7d-197">그런 다음 서버 개체의 메서드를 `GetLastError` 호출 하 여 마지막으로 발생 한 오류를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-197">Then, the last error that occurred is determined by call the `GetLastError` method of the Server object.</span></span> <span data-ttu-id="45d7d-198">예외가 더 이상 존재 하지 않는 경우 일반 예외가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-198">If the exception no longer exists, a generic exception is created.</span></span> <span data-ttu-id="45d7d-199">그런 다음 HTTP 요청을 로컬로 만든 경우 모든 오류 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-199">Then, if the HTTP request was made locally, all error details are shown.</span></span> <span data-ttu-id="45d7d-200">이 경우 웹 응용 프로그램을 실행 하는 로컬 컴퓨터에만 이러한 오류 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-200">In this case, only the local machine running the web application will see these error details.</span></span> <span data-ttu-id="45d7d-201">오류 정보가 표시 된 후 오류가 로그 파일에 추가 되 고 서버에서 오류가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-201">After the error information has been displayed, the error is added to the log file and the error is cleared from the server.</span></span>

### <a name="displaying-unhandled-error-messages-for-the-application"></a><span data-ttu-id="45d7d-202">응용 프로그램에 대해 처리 되지 않은 오류 메시지 표시</span><span class="sxs-lookup"><span data-stu-id="45d7d-202">Displaying Unhandled Error Messages for the Application</span></span>

<span data-ttu-id="45d7d-203">Web.config 파일에 `customErrors` 섹션을 추가 하면 응용 프로그램 전체에서 발생 하는 단순한 오류를 신속 하 게 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-203">By adding a `customErrors` section to the *Web.config* file, you can quickly handle simple errors that occur throughout the application.</span></span> <span data-ttu-id="45d7d-204">404-파일을 찾을 수 없는 경우와 같이 상태 코드 값을 기반으로 오류를 처리 하는 방법을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-204">You can also specify how to handle errors based on their status code value, such as 404 - File not found.</span></span>

#### <a name="update-the-configuration"></a><span data-ttu-id="45d7d-205">구성 업데이트</span><span class="sxs-lookup"><span data-stu-id="45d7d-205">Update the Configuration</span></span>

<span data-ttu-id="45d7d-206">Web.config 파일에 섹션을 `customErrors` 추가 하 여 구성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-206">Update the configuration by adding a `customErrors` section to the *Web.config* file.</span></span>

1. <span data-ttu-id="45d7d-207">**솔루션 탐색기**에서 정문 장난감 샘플 응용 프로그램의 루트에 있는 *web.config* 파일을 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-207">In **Solution Explorer**, find and open the *Web.config* file at the root of the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="45d7d-208">다음과 같이 `<system.web>` 노드 내의 web.config 파일에 섹션을추가합니다.`customErrors`</span><span class="sxs-lookup"><span data-stu-id="45d7d-208">Add the `customErrors` section to the *Web.config* file within the `<system.web>` node as follows:</span></span>   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. <span data-ttu-id="45d7d-209">Web.config 파일 을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-209">Save the *Web.config* file.</span></span>

<span data-ttu-id="45d7d-210">섹션 `customErrors` 은 "설정"으로 설정 된 모드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-210">The `customErrors` section specifies the mode, which is set to "On".</span></span> <span data-ttu-id="45d7d-211">또한 오류가 발생할 때 `defaultRedirect`탐색할 페이지를 응용 프로그램에 알리는를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-211">It also specifies the `defaultRedirect`, which tells the application which page to navigate to when an error occurs.</span></span> <span data-ttu-id="45d7d-212">또한 페이지를 찾을 수 없을 때 404 오류를 처리 하는 방법을 지정 하는 특정 오류 요소를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-212">In addition, you have added a specific error element that specifies how to handle a 404 error when a page is not found.</span></span> <span data-ttu-id="45d7d-213">이 자습서의 뒷부분에서는 응용 프로그램 수준에서 오류에 대 한 세부 정보를 캡처하는 추가 오류 처리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-213">Later in this tutorial, you will add additional error handling that will capture the details of an error at the application level.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="45d7d-214">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="45d7d-214">Running the Application</span></span>

<span data-ttu-id="45d7d-215">이제 응용 프로그램을 실행 하 여 업데이트 된 경로를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-215">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="45d7d-216">**F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-216">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="45d7d-217">브라우저가 열리고 default.aspx 페이지가 표시 됩니다 .</span><span class="sxs-lookup"><span data-stu-id="45d7d-217">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="45d7d-218">브라우저에 다음 URL을 입력 합니다. 포트 번호를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-218">Enter the following URL into the browser (be sure to use **your** port number):</span></span>  
    `https://localhost:44300/NoPage.aspx`
3. <span data-ttu-id="45d7d-219">브라우저에 표시 된 *Errorpage .aspx* 를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-219">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 오류 처리-페이지를 찾을 수 없음 오류](aspnet-error-handling/_static/image1.png)

<span data-ttu-id="45d7d-221">없는 *nopage .aspx* 페이지를 요청 하면 추가 세부 정보를 사용할 수 있는 경우 오류 페이지에 간단한 오류 메시지와 자세한 오류 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-221">When you request the *NoPage.aspx* page, which does not exist, the error page will show the simple error message and the detailed error information if additional details are available.</span></span> <span data-ttu-id="45d7d-222">그러나 사용자가 원격 위치에서 존재 하지 않는 페이지를 요청 하는 경우 오류 페이지는 오류 메시지만 빨간색으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-222">However, if the user requested a non-existent page from a remote location, the error page would only show the error message in red.</span></span>

### <a name="including-an-exception-for-testing-purposes"></a><span data-ttu-id="45d7d-223">테스트 목적으로 예외 포함</span><span class="sxs-lookup"><span data-stu-id="45d7d-223">Including an Exception for Testing Purposes</span></span>

<span data-ttu-id="45d7d-224">오류가 발생 했을 때 응용 프로그램이 어떻게 작동 하는지 확인 하려면 의도적으로 ASP.NET에서 오류 조건을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-224">To verify how your application will function when an error occurs, you can deliberately create error conditions in ASP.NET.</span></span> <span data-ttu-id="45d7d-225">정문 장난감 샘플 응용 프로그램에서 기본 페이지가 로드 되 면 테스트 예외를 throw 하 여 발생 하는 상황을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-225">In the Wingtip Toys sample application, you will throw a test exception when the default page loads to see what happens.</span></span>

1. <span data-ttu-id="45d7d-226">Visual Studio에서 default.aspx 페이지의 코드 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-226">Open the code-behind of the *Default.aspx* page in Visual Studio.</span></span>   
   <span data-ttu-id="45d7d-227">*Default.aspx.cs* 코드 숨겨진 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-227">The *Default.aspx.cs* code-behind page will be displayed.</span></span>
2. <span data-ttu-id="45d7d-228">`Page_Load` 처리기에서 처리기가 다음과 같이 표시 되도록 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-228">In the `Page_Load` handler, add code so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="45d7d-229">다양 한 형식의 예외를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-229">It is possible to create various different types of exceptions.</span></span> <span data-ttu-id="45d7d-230">위의 코드에서 default.aspx 페이지가 로드 `InvalidOperationException` 될 때를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-230">In the above code, you are creating an `InvalidOperationException` when the *Default.aspx* page is loaded.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="45d7d-231">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="45d7d-231">Running the Application</span></span>

<span data-ttu-id="45d7d-232">응용 프로그램을 실행 하 여 응용 프로그램에서 예외를 처리 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-232">You can run the application to see how the application handles the exception.</span></span>

1. <span data-ttu-id="45d7d-233">**Ctrl + F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-233">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="45d7d-234">응용 프로그램에서 InvalidOperationException를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-234">The application throws the InvalidOperationException.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="45d7d-235">Visual Studio에서 오류의 원인을 확인 하기 위해 코드를 중단 하지 않고 페이지를 표시 하려면 **ctrl +** f 5를 눌러야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-235">You must press **CTRL+F5** to display the page without breaking into the code to view the source of the error in Visual Studio.</span></span>
2. <span data-ttu-id="45d7d-236">브라우저에 표시 된 *Errorpage .aspx* 를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-236">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 오류 처리-오류 페이지](aspnet-error-handling/_static/image2.png)

<span data-ttu-id="45d7d-238">오류 세부 정보에서 볼 수 있듯이, web.config 파일의 `customError` 섹션에서 예외를 트래핑 했습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-238">As you can see in the error details, the exception was trapped by the `customError` section in the *Web.config* file.</span></span>

### <a name="adding-application-level-error-handling"></a><span data-ttu-id="45d7d-239">응용 프로그램 수준 오류 처리 추가</span><span class="sxs-lookup"><span data-stu-id="45d7d-239">Adding Application-Level Error Handling</span></span>

<span data-ttu-id="45d7d-240">예외에 대 한 정보를 거의 `customErrors` 얻지 못하는 *web.config* 파일의 섹션을 사용 하 여 예외를 트래핑 하는 대신 응용 프로그램 수준에서 오류를 포착 하 고 오류 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-240">Rather than trap the exception using the `customErrors` section in the *Web.config* file, where you gain little information about the exception, you can trap the error at the application level and retrieve error details.</span></span>

1. <span data-ttu-id="45d7d-241">**솔루션 탐색기**에서 *Global.asax.cs* 파일을 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-241">In **Solution Explorer**, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="45d7d-242">**\_응용 프로그램 오류** 처리기를 추가 하 여 다음과 같이 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-242">Add an **Application\_Error** handler so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

<span data-ttu-id="45d7d-243">응용 프로그램에서 오류가 발생 하 `Application_Error` 는 경우 처리기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-243">When an error occurs in the application, the `Application_Error` handler is called.</span></span> <span data-ttu-id="45d7d-244">이 처리기에서 마지막 예외를 검색 하 고 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-244">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="45d7d-245">예외가 처리 되지 않은 경우 예외에 내부 예외 세부 정보 (즉, `InnerException` 가 null이 아님)가 포함 된 경우 응용 프로그램은 예외 정보가 표시 되는 오류 페이지로 실행을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-245">If the exception was unhandled and the exception contains inner-exception details (that is, `InnerException` is not null), the application transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="45d7d-246">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="45d7d-246">Running the Application</span></span>

<span data-ttu-id="45d7d-247">응용 프로그램을 실행 하 여 응용 프로그램 수준에서 예외를 처리 하 여 제공 된 추가 오류 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-247">You can run the application to see the additional error details provided by handling the exception at the application level.</span></span>

1. <span data-ttu-id="45d7d-248">**Ctrl + F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-248">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="45d7d-249">응용 프로그램은을 `InvalidOperationException` throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-249">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="45d7d-250">브라우저에 표시 된 *Errorpage .aspx* 를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-250">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 오류 처리-응용 프로그램 수준 오류](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a><span data-ttu-id="45d7d-252">페이지 수준 오류 처리 추가</span><span class="sxs-lookup"><span data-stu-id="45d7d-252">Adding Page-Level Error Handling</span></span>

<span data-ttu-id="45d7d-253">페이지의 `ErrorPage` `@Page` 지시문에 특성을 추가 하거나 페이지의 코드 숨김으로 `Page_Error` 이벤트 처리기를 추가 하 여 페이지에 페이지 수준 오류 처리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-253">You can add page-level error handling to a page either by using adding an `ErrorPage` attribute to the `@Page` directive of the page, or by adding a `Page_Error` event handler to the code-behind of a page.</span></span> <span data-ttu-id="45d7d-254">이 섹션에서는 *errorpage .aspx* 페이지로 실행 `Page_Error` 을 전송 하는 이벤트 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-254">In this section, you will add a `Page_Error` event handler that will transfer execution to the *ErrorPage.aspx* page.</span></span>

1. <span data-ttu-id="45d7d-255">**솔루션 탐색기**에서 *Default.aspx.cs* 파일을 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-255">In **Solution Explorer**, find and open the *Default.aspx.cs* file.</span></span>
2. <span data-ttu-id="45d7d-256">코드 숨김이 `Page_Error` 다음과 같이 표시 되도록 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-256">Add a `Page_Error` handler so that the code-behind appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

<span data-ttu-id="45d7d-257">페이지에서 오류가 발생 하면 `Page_Error` 이벤트 처리기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-257">When an error occurs on the page, the `Page_Error` event handler is called.</span></span> <span data-ttu-id="45d7d-258">이 처리기에서 마지막 예외를 검색 하 고 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-258">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="45d7d-259">이 발생 하는 경우 `Page_Error` 이벤트 처리기는 예외 정보가 표시 되는 오류 페이지로 실행을 전송 합니다. `InvalidOperationException`</span><span class="sxs-lookup"><span data-stu-id="45d7d-259">If an `InvalidOperationException` occurs, the `Page_Error` event handler transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="45d7d-260">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="45d7d-260">Running the Application</span></span>

<span data-ttu-id="45d7d-261">이제 응용 프로그램을 실행 하 여 업데이트 된 경로를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-261">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="45d7d-262">**Ctrl + F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-262">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="45d7d-263">응용 프로그램은을 `InvalidOperationException` throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-263">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="45d7d-264">브라우저에 표시 된 *Errorpage .aspx* 를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-264">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 오류 처리-페이지 수준 오류](aspnet-error-handling/_static/image4.png)
3. <span data-ttu-id="45d7d-266">브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-266">Close your browser window.</span></span>

### <a name="removing-the-exception-used-for-testing"></a><span data-ttu-id="45d7d-267">테스트에 사용 되는 예외 제거</span><span class="sxs-lookup"><span data-stu-id="45d7d-267">Removing the Exception Used for Testing</span></span>

<span data-ttu-id="45d7d-268">이 자습서의 앞부분에서 추가한 예외를 발생 시 키 지 않고 정문 장난감 샘플 응용 프로그램이 작동 하도록 허용 하려면 예외를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-268">To allow the Wingtip Toys sample application to function without throwing the exception you added earlier in this tutorial, remove the exception.</span></span>

1. <span data-ttu-id="45d7d-269">Default.aspx 페이지의 코드 숨김이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-269">Open the code-behind of the *Default.aspx* page.</span></span>
2. <span data-ttu-id="45d7d-270">`Page_Load` 처리기에서 처리기가 다음과 같이 표시 되도록 예외를 throw 하는 코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-270">In the `Page_Load` handler, remove the code that throws the exception so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a><span data-ttu-id="45d7d-271">코드 수준 오류 로깅 추가</span><span class="sxs-lookup"><span data-stu-id="45d7d-271">Adding Code-Level Error Logging</span></span>

<span data-ttu-id="45d7d-272">이 자습서의 앞부분에서 설명한 것 처럼 try/catch 문을 추가 하 여 코드 섹션을 실행 하 고 발생 한 첫 번째 오류를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-272">As mentioned earlier in this tutorial, you can add try/catch statements to attempt to run a section of code and handle the first error that occurs.</span></span> <span data-ttu-id="45d7d-273">이 예에서는 오류 로그 파일에 오류 정보를 기록 하 여 나중에 오류를 검토할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-273">In this example, you will only write the error details to the error log file so that the error can be reviewed later.</span></span>

1. <span data-ttu-id="45d7d-274">**솔루션 탐색기**의 *논리* 폴더에서 *PayPalFunctions.cs* 파일을 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-274">In **Solution Explorer**, in the *Logic* folder, find and open the *PayPalFunctions.cs* file.</span></span>
2. <span data-ttu-id="45d7d-275">다음과 같이 `HttpCall` 코드를 표시 하도록 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-275">Update the `HttpCall` method so that the code appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

<span data-ttu-id="45d7d-276">위의 코드는 `ExceptionUtility` 클래스에 `LogException` 포함 된 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-276">The above code calls the `LogException` method that is contained in the `ExceptionUtility` class.</span></span> <span data-ttu-id="45d7d-277">이 자습서의 앞부분에 나오는 *논리* 폴더에 *ExceptionUtility.cs* 클래스 파일을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-277">You added the *ExceptionUtility.cs* class file to the *Logic* folder earlier in this tutorial.</span></span> <span data-ttu-id="45d7d-278">`LogException` 메서드는 두 개의 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-278">The `LogException` method takes two parameters.</span></span> <span data-ttu-id="45d7d-279">첫 번째 매개 변수는 exception 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-279">The first parameter is the exception object.</span></span> <span data-ttu-id="45d7d-280">두 번째 매개 변수는 오류의 원인을 인식 하는 데 사용 되는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-280">The second parameter is a string used to recognize the source of the error.</span></span>

### <a name="inspecting-the-error-logging-information"></a><span data-ttu-id="45d7d-281">오류 로깅 정보 검사</span><span class="sxs-lookup"><span data-stu-id="45d7d-281">Inspecting the Error Logging Information</span></span>

<span data-ttu-id="45d7d-282">앞에서 설명한 것 처럼 오류 로그를 사용 하 여 먼저 해결할 응용 프로그램의 오류를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-282">As mentioned previously, you can use the error log to determine which errors in your application should be fixed first.</span></span> <span data-ttu-id="45d7d-283">물론 오류 로그에 포착 되어 기록 된 오류만 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-283">Of course, only errors that have been trapped and written to the error log will be recorded.</span></span>

1. <span data-ttu-id="45d7d-284">**솔루션 탐색기**에서 *응용 프로그램\_데이터* 폴더의 *오류 로그 .txt* 파일을 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-284">In **Solution Explorer**, find and open the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>   
 <span data-ttu-id="45d7d-285">"**모든 파일 표시**" 옵션을 선택 하거나 **솔루션 탐색기** 맨 위에 있는 "**새로 고침**" 옵션을 선택 하 여 *오류 로그 .txt* 파일을 확인 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-285">You may need to select the "**Show All Files**" option or the "**Refresh**" option from the top of **Solution Explorer** to see the *ErrorLog.txt* file.</span></span>
2. <span data-ttu-id="45d7d-286">Visual Studio에 표시 된 오류 로그를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-286">Review the error log displayed in Visual Studio:</span></span> 

    ![ASP.NET 오류 처리-오류 로그 .txt](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a><span data-ttu-id="45d7d-288">안전 오류 메시지</span><span class="sxs-lookup"><span data-stu-id="45d7d-288">Safe Error Messages</span></span>

<span data-ttu-id="45d7d-289">응용 프로그램에서 오류 메시지를 표시 하는 경우 악의적인 사용자가 응용 프로그램을 공격 하는 데 도움이 될 수 있다는 정보를 제공 하지 않는 것이 **중요** 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-289">It is **important to note** that when your application displays error messages, it should not give away information that a malicious user might find helpful in attacking your application.</span></span> <span data-ttu-id="45d7d-290">예를 들어 응용 프로그램이 데이터베이스에 쓰려고 할 수 없는 경우 사용 중인 사용자 이름을 포함 하는 오류 메시지를 표시 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-290">For example, if your application unsuccessfully tries to write in to a database, it should not display an error message that includes the user name it is using.</span></span> <span data-ttu-id="45d7d-291">따라서 빨간색의 일반 오류 메시지가 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-291">For this reason, a generic error message in red is displayed to the user.</span></span> <span data-ttu-id="45d7d-292">모든 추가 오류 세부 정보는 로컬 컴퓨터의 개발자 에게만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-292">All additional error details are only displayed to the developer on the local machine.</span></span>

## <a name="using-elmah"></a><span data-ttu-id="45d7d-293">ELMAH 사용</span><span class="sxs-lookup"><span data-stu-id="45d7d-293">Using ELMAH</span></span>

<span data-ttu-id="45d7d-294">ELMAH (오류 로깅 모듈 및 처리기)는 NuGet 패키지로 ASP.NET 응용 프로그램에 연결 하는 오류 로깅 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-294">ELMAH (Error Logging Modules and Handlers) is an error logging facility that you plug into your ASP.NET application as a NuGet package.</span></span> <span data-ttu-id="45d7d-295">ELMAH는 다음과 같은 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-295">ELMAH provides the following capabilities:</span></span>

- <span data-ttu-id="45d7d-296">처리 되지 않은 예외에 대 한 로깅입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-296">Logging of unhandled exceptions.</span></span>
- <span data-ttu-id="45d7d-297">기록 처리 되지 않은 예외에 대 한 전체 로그를 볼 수 있는 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-297">A web page to view the entire log of recoded unhandled exceptions.</span></span>
- <span data-ttu-id="45d7d-298">기록 된 각 예외의 전체 세부 정보를 볼 수 있는 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-298">A web page to view the full details of each logged exception.</span></span>
- <span data-ttu-id="45d7d-299">발생할 때 각 오류에 대 한 전자 메일 알림</span><span class="sxs-lookup"><span data-stu-id="45d7d-299">An email notification of each error at the time it occurs.</span></span>
- <span data-ttu-id="45d7d-300">로그에서 지난 15 개 오류의 RSS 피드입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-300">An RSS feed of the last 15 errors from the log.</span></span>

<span data-ttu-id="45d7d-301">ELMAH를 사용 하려면 먼저 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-301">Before you can work with the ELMAH, you must install it.</span></span> <span data-ttu-id="45d7d-302">이는 *NuGet* 패키지 설치 관리자를 사용 하 여 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-302">This is easy using the *NuGet* package installer.</span></span> <span data-ttu-id="45d7d-303">이 자습서 시리즈의 앞부분에서 설명한 것 처럼 NuGet은 visual Studio에서 오픈 소스 라이브러리와 도구를 쉽게 설치 하 고 업데이트할 수 있도록 하는 Visual Studio 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-303">As mentioned earlier in this tutorial series, NuGet is a Visual Studio extension that makes it easy to install and update open source libraries and tools in Visual Studio.</span></span>

1. <span data-ttu-id="45d7d-304">Visual Studio의 **도구** 메뉴에서 **nuget 패키지 관리자** > **솔루션용 nuget 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-304">Within Visual Studio, from the **Tools** menu, select **NuGet Package Manager** > **Manage NuGet Packages for Solution**.</span></span> 

    ![ASP.NET 오류 처리-솔루션에 대 한 NuGet 패키지 관리](aspnet-error-handling/_static/image6.png)
2. <span data-ttu-id="45d7d-306">**NuGet 패키지 관리** 대화 상자는 Visual Studio 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-306">The **Manage NuGet Packages** dialog box is displayed within Visual Studio.</span></span>
3. <span data-ttu-id="45d7d-307">**NuGet 패키지 관리** 대화 상자에서 왼쪽의 **온라인** 을 확장 한 다음 **nuget.org**를 선택 합니다. 그런 다음 온라인에서 사용 가능한 패키지 목록에서 **ELMAH** 패키지를 찾아 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-307">In the **Manage NuGet Packages** dialog box, expand **Online** on the left, and then select **nuget.org**. Then, find and install the **ELMAH** package from the list of available packages online.</span></span> 

    ![ASP.NET 오류 처리-ELMA NuGet 패키지](aspnet-error-handling/_static/image7.png)
4. <span data-ttu-id="45d7d-309">패키지를 다운로드 하려면 인터넷에 연결 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-309">You will need to have an internet connection to download the package.</span></span>
5. <span data-ttu-id="45d7d-310">**프로젝트 선택** 대화 상자에서 **WingtipToys** 선택이 선택 되어 있는지 확인 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-310">In the **Select Projects** dialog box, make sure the **WingtipToys** selection is selected, and then click **OK**.</span></span> 

    ![ASP.NET 오류 처리-프로젝트 선택 대화 상자](aspnet-error-handling/_static/image8.png)
6. <span data-ttu-id="45d7d-312">필요한 경우 **NuGet 패키지 관리** 대화 상자에서 **닫기** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-312">Click **Close** in the **Manage NuGet Packages** dialog box if needed.</span></span>
7. <span data-ttu-id="45d7d-313">Visual Studio에서 열려 있는 모든 파일을 다시 로드 하도록 요청 하는 경우 "**모두 예**"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-313">If Visual Studio requests that you reload any open files, select "**Yes to All**".</span></span>
8. <span data-ttu-id="45d7d-314">ELMAH 패키지는 프로젝트의 루트에 있는 web.config 파일에 자신에 대 한 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-314">The ELMAH package adds entries for itself in the *Web.config* file at the root of your project.</span></span> <span data-ttu-id="45d7d-315">Visual Studio에서 수정 된 *web.config* 파일을 다시 로드할지 여부를 묻는 메시지를 표시 하려면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-315">If Visual Studio asks you if you want to reload the modified *Web.config* file, click **Yes**.</span></span>

<span data-ttu-id="45d7d-316">이제 ELMAH는 발생 하는 처리 되지 않은 오류를 저장할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-316">ELMAH is now ready to store any unhandled errors that occur.</span></span>

### <a name="viewing-the-elmah-log"></a><span data-ttu-id="45d7d-317">ELMAH 로그 보기</span><span class="sxs-lookup"><span data-stu-id="45d7d-317">Viewing the ELMAH Log</span></span>

<span data-ttu-id="45d7d-318">ELMAH 로그는 쉽게 볼 수 있지만 먼저 ELMAH 로그에 기록 되는 처리 되지 않은 예외를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-318">Viewing the ELMAH log is easy, but first you will create an unhandled exception that will be recorded in the ELMAH log.</span></span>

1. <span data-ttu-id="45d7d-319">**Ctrl + F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-319">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="45d7d-320">ELMAH 로그에 처리 되지 않은 예외를 쓰려면 브라우저에서 포트 번호를 사용 하 여 다음 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-320">To write an unhandled exception to the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    <span data-ttu-id="45d7d-321">`https://localhost:44300/NoPage.aspx`오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-321">`https://localhost:44300/NoPage.aspx` The error page will be displayed.</span></span>
3. <span data-ttu-id="45d7d-322">ELMAH 로그를 표시 하려면 브라우저에서 포트 번호를 사용 하 여 다음 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-322">To display the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 오류 처리-ELMAH 오류 로그](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="45d7d-324">요약</span><span class="sxs-lookup"><span data-stu-id="45d7d-324">Summary</span></span>

<span data-ttu-id="45d7d-325">이 자습서에서는 응용 프로그램 수준, 페이지 수준 및 코드 수준에서 오류를 처리 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-325">In this tutorial, you have learned about handling errors at the application level, the page level, and the code level.</span></span> <span data-ttu-id="45d7d-326">또한 이후 검토를 위해 처리 된 오류와 처리 되지 않은 오류를 기록 하는 방법도 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-326">You have also learned how to log handled and unhandled errors for later review.</span></span> <span data-ttu-id="45d7d-327">NuGet을 사용 하 여 응용 프로그램에 예외 로깅 및 알림을 제공 하는 ELMAH 유틸리티를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-327">You added the ELMAH utility to provide exception logging and notification to your application using NuGet.</span></span> <span data-ttu-id="45d7d-328">또한 안전 오류 메시지의 중요성에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-328">Additionally, you have learned about the importance of safe error messages.</span></span>

## <a name="tutorial-series-conclusion"></a><span data-ttu-id="45d7d-329">자습서 시리즈 결론</span><span class="sxs-lookup"><span data-stu-id="45d7d-329">Tutorial Series Conclusion</span></span>

<span data-ttu-id="45d7d-330">다음에 따라 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-330">Thanks for following along.</span></span> <span data-ttu-id="45d7d-331">이러한 일련의 자습서를 ASP.NET Web Forms에 더 친숙 하 게 하는 데 도움이 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-331">I hope this set of tutorials helped you become more familiar with ASP.NET Web Forms.</span></span> <span data-ttu-id="45d7d-332">ASP.NET 4.5 및 Visual Studio 2013에서 사용할 수 있는 Web Forms 기능에 대 한 자세한 내용은 [ASP.NET 및 Web Tools Visual Studio 2013 릴리스 정보](../../../../visual-studio/overview/2013/release-notes.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="45d7d-332">If you need more information about Web Forms features available in ASP.NET 4.5 and Visual Studio 2013, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span> <span data-ttu-id="45d7d-333">또한 **다음 단계** 섹션에 언급 된 자습서를 살펴보고 [무료 Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 사용해 defintely.</span><span class="sxs-lookup"><span data-stu-id="45d7d-333">Also, be sure to take a look at the tutorial mentioned in the **Next Steps** section and defintely try out the [free Azure trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

![감사 합니다. Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a><span data-ttu-id="45d7d-335">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45d7d-335">Next Steps</span></span>

<span data-ttu-id="45d7d-336">Microsoft Azure에 웹 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 [멤버 자격, OAuth 및 SQL Database Azure 웹 사이트에 보안 ASP.NET Web Forms 앱 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="45d7d-336">Learn more about deploying your web application to Microsoft Azure, see [Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to an Azure Web Site](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/).</span></span>

## <a name="free-trial"></a><span data-ttu-id="45d7d-337">무료 평가판</span><span class="sxs-lookup"><span data-stu-id="45d7d-337">Free Trial</span></span>

[<span data-ttu-id="45d7d-338">Microsoft Azure-무료 평가판</span><span class="sxs-lookup"><span data-stu-id="45d7d-338">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)  
 <span data-ttu-id="45d7d-339">웹 사이트를 Microsoft Azure에 게시 하면 시간, 유지 관리 및 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-339">Publishing your website to Microsoft Azure will save you time, maintenance and expense.</span></span> <span data-ttu-id="45d7d-340">Azure에 웹 앱을 배포 하는 빠른 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-340">It's a quick process to deploying your web app to Azure.</span></span> <span data-ttu-id="45d7d-341">웹 앱을 유지 관리 하 고 모니터링 해야 하는 경우 Azure에서는 다양 한 도구와 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-341">When you need to maintain and monitor your web app, Azure offers a variety of tools and services.</span></span> <span data-ttu-id="45d7d-342">Azure에서 데이터, 트래픽, id, 백업, 메시징, 미디어 및 성능을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-342">Manage data, traffic, identity, backups, messaging, media and performance in Azure.</span></span> <span data-ttu-id="45d7d-343">그리고이 모든 것이 매우 비용 효과적인 방법으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-343">And, all of this is provided in a very cost effective approach.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="45d7d-344">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="45d7d-344">Additional Resources</span></span>

<span data-ttu-id="45d7d-345">[ASP.NET Health Monitoring을 사용 하 여 오류 세부 정보 로깅](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span><span class="sxs-lookup"><span data-stu-id="45d7d-345">[Logging Error Details with ASP.NET Health Monitoring](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span></span>  
[<span data-ttu-id="45d7d-346">ELMAH</span><span class="sxs-lookup"><span data-stu-id="45d7d-346">ELMAH</span></span>](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a><span data-ttu-id="45d7d-347">감사의 글</span><span class="sxs-lookup"><span data-stu-id="45d7d-347">Acknowledgements</span></span>

<span data-ttu-id="45d7d-348">이 자습서 시리즈의 내용에 대해 상당한 기여를 수행한 다음 사용자에 게 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="45d7d-348">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="45d7d-349">Alberto poblacion, MVP &amp; MCT, 스페인</span><span class="sxs-lookup"><span data-stu-id="45d7d-349">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="45d7d-350">[Alex Thissen, 네덜란드](http://blog.alexthissen.nl/) (twitter: [@alexthissen](http://twitter.com/alexthissen))</span><span class="sxs-lookup"><span data-stu-id="45d7d-350">[Alex Thissen, Netherlands](http://blog.alexthissen.nl/) (twitter: [@alexthissen](http://twitter.com/alexthissen))</span></span>
- [<span data-ttu-id="45d7d-351">Andre Tournier, USA</span><span class="sxs-lookup"><span data-stu-id="45d7d-351">Andre Tournier, USA</span></span>](http://andret503.wordpress.com/)
- <span data-ttu-id="45d7d-352">Apurva Joshi, Microsoft</span><span class="sxs-lookup"><span data-stu-id="45d7d-352">Apurva Joshi, Microsoft</span></span>
- [<span data-ttu-id="45d7d-353">Bojan 월 Vrhovnik, 슬로베니아</span><span class="sxs-lookup"><span data-stu-id="45d7d-353">Bojan Vrhovnik, Slovenia</span></span>](http://twitter.com/bvrhovnik)
- <span data-ttu-id="45d7d-354">[Bruno Sonnino, 브라질](http://msmvps.com/blogs/bsonnino) (twitter: [@bsonnino](http://twitter.com/bsonnino))</span><span class="sxs-lookup"><span data-stu-id="45d7d-354">[Bruno Sonnino, Brazil](http://msmvps.com/blogs/bsonnino) (twitter: [@bsonnino](http://twitter.com/bsonnino))</span></span>
- [<span data-ttu-id="45d7d-355">Carlos dos Santos, 브라질</span><span class="sxs-lookup"><span data-stu-id="45d7d-355">Carlos dos Santos, Brazil</span></span>](http://www.carloscds.net/)
- <span data-ttu-id="45d7d-356">[Dave Campbell, 미국](http://www.wynapse.com/) (twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))</span><span class="sxs-lookup"><span data-stu-id="45d7d-356">[Dave Campbell, USA](http://www.wynapse.com/) (twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))</span></span>
- <span data-ttu-id="45d7d-357">[Jon Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="45d7d-357">[Jon Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- <span data-ttu-id="45d7d-358">[Michael 정자, 미국](http://www.930solutions.com/) (twitter: [@mrsharps](http://twitter.com/mrsharps))</span><span class="sxs-lookup"><span data-stu-id="45d7d-358">[Michael Sharps, USA](http://www.930solutions.com/) (twitter: [@mrsharps](http://twitter.com/mrsharps))</span></span>
- <span data-ttu-id="45d7d-359">Mike Pope</span><span class="sxs-lookup"><span data-stu-id="45d7d-359">Mike Pope</span></span>
- <span data-ttu-id="45d7d-360">[Mitchel 판매자, 미국](http://www.mitchelsellers.com/) (twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))</span><span class="sxs-lookup"><span data-stu-id="45d7d-360">[Mitchel Sellers, USA](http://www.mitchelsellers.com/) (twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))</span></span>
- [<span data-ttu-id="45d7d-361">Paul Cociuba, Microsoft</span><span class="sxs-lookup"><span data-stu-id="45d7d-361">Paul Cociuba, Microsoft</span></span>](http://linqto.me/Links/pcociuba)
- [<span data-ttu-id="45d7d-362">파울로 Ggado, 포르투갈</span><span class="sxs-lookup"><span data-stu-id="45d7d-362">Paulo Morgado, Portugal</span></span>](http://paulomorgado.net/)
- [<span data-ttu-id="45d7d-363">Pranav Rastogi, Microsoft</span><span class="sxs-lookup"><span data-stu-id="45d7d-363">Pranav Rastogi, Microsoft</span></span>](https://blogs.msdn.com/b/pranav_rastogi)
- [<span data-ttu-id="45d7d-364">Tim Am마나트 n, Microsoft</span><span class="sxs-lookup"><span data-stu-id="45d7d-364">Tim Ammann, Microsoft</span></span>](https://blogs.iis.net/timamm/default.aspx)
- [<span data-ttu-id="45d7d-365">Tom Dykstra, Microsoft</span><span class="sxs-lookup"><span data-stu-id="45d7d-365">Tom Dykstra, Microsoft</span></span>](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a><span data-ttu-id="45d7d-366">커뮤니티 기여</span><span class="sxs-lookup"><span data-stu-id="45d7d-366">Community Contributions</span></span>

- <span data-ttu-id="45d7d-367">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span><span class="sxs-lookup"><span data-stu-id="45d7d-367">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span></span>  
  <span data-ttu-id="45d7d-368">MSDN의 Visual Studio 2012 관련 코드 샘플: [정문 장난감 탐색](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span><span class="sxs-lookup"><span data-stu-id="45d7d-368">Visual Studio 2012 related code sample on MSDN: [Navigation Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span></span>
- <span data-ttu-id="45d7d-369">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span><span class="sxs-lookup"><span data-stu-id="45d7d-369">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span></span>  
  <span data-ttu-id="45d7d-370">MSDN의 Visual Studio 2012 관련 코드 샘플: [ASP.NET 4.5 Web Forms 자습서 시리즈 Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span><span class="sxs-lookup"><span data-stu-id="45d7d-370">Visual Studio 2012 related code sample on MSDN: [ASP.NET 4.5 Web Forms Tutorial Series in Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span></span>
- <span data-ttu-id="45d7d-371">Andrielle Azevedo-Microsoft의 twitter: @driazevedo(기술 대상 사용자 참여자)</span><span class="sxs-lookup"><span data-stu-id="45d7d-371">Andrielle Azevedo - Microsoft Technical Audience Contributor (twitter: @driazevedo)</span></span>  
  <span data-ttu-id="45d7d-372">Visual Studio 2012 translation: [Iniciando com ASP.NET Web Forms 4.5-Parte 1-Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span><span class="sxs-lookup"><span data-stu-id="45d7d-372">Visual Studio 2012 translation: [Iniciando com ASP.NET Web Forms 4.5 - Parte 1 - Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="45d7d-373">이전</span><span class="sxs-lookup"><span data-stu-id="45d7d-373">Previous</span></span>](url-routing.md)
