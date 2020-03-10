---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API에서 예외 처리-ASP.NET 4.x
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504701"
---
# <a name="exception-handling-in-aspnet-web-api"></a><span data-ttu-id="cafb2-102">ASP.NET Web API의 예외 처리</span><span class="sxs-lookup"><span data-stu-id="cafb2-102">Exception Handling in ASP.NET Web API</span></span>

<span data-ttu-id="cafb2-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cafb2-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="cafb2-104">이 문서에서는 ASP.NET Web API의 오류 및 예외 처리에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-104">This article describes error and exception handling in ASP.NET Web API.</span></span>

- [<span data-ttu-id="cafb2-105">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="cafb2-105">HttpResponseException</span></span>](#httpresponserexception)
- [<span data-ttu-id="cafb2-106">예외 필터</span><span class="sxs-lookup"><span data-stu-id="cafb2-106">Exception Filters</span></span>](#exception_filters)
- [<span data-ttu-id="cafb2-107">예외 필터 등록</span><span class="sxs-lookup"><span data-stu-id="cafb2-107">Registering Exception Filters</span></span>](#registering_exception_filters)
- [<span data-ttu-id="cafb2-108">HttpError</span><span class="sxs-lookup"><span data-stu-id="cafb2-108">HttpError</span></span>](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a><span data-ttu-id="cafb2-109">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="cafb2-109">HttpResponseException</span></span>

<span data-ttu-id="cafb2-110">Web API 컨트롤러에서 catch 되지 않은 예외를 throw 하는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="cafb2-110">What happens if a Web API controller throws an uncaught exception?</span></span> <span data-ttu-id="cafb2-111">기본적으로 대부분의 예외는 상태 코드 500, 내부 서버 오류와 함께 HTTP 응답으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-111">By default, most exceptions are translated into an HTTP response with status code 500, Internal Server Error.</span></span>

<span data-ttu-id="cafb2-112">**HttpResponseException** 형식은 특수 한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-112">The **HttpResponseException** type is a special case.</span></span> <span data-ttu-id="cafb2-113">이 예외는 예외 생성자에서 지정 하는 모든 HTTP 상태 코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-113">This exception returns any HTTP status code that you specify in the exception constructor.</span></span> <span data-ttu-id="cafb2-114">예를 들어, 다음 메서드는 *id* 매개 변수가 잘못 된 경우 찾을 수 없는 404을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-114">For example, the following method returns 404, Not Found, if the *id* parameter is not valid.</span></span>

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

<span data-ttu-id="cafb2-115">응답에 대 한 더 많은 제어를 위해 전체 응답 메시지를 생성 하 고 HttpResponseException에 포함할 수도 있습니다 **.**</span><span class="sxs-lookup"><span data-stu-id="cafb2-115">For more control over the response, you can also construct the entire response message and include it with the **HttpResponseException:**</span></span> 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a><span data-ttu-id="cafb2-116">예외 필터</span><span class="sxs-lookup"><span data-stu-id="cafb2-116">Exception Filters</span></span>

<span data-ttu-id="cafb2-117">*예외 필터*를 작성 하 여 Web API에서 예외를 처리 하는 방법을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-117">You can customize how Web API handles exceptions by writing an *exception filter*.</span></span> <span data-ttu-id="cafb2-118">예외 필터는 컨트롤러 메서드가 **HttpResponseException** 예외가 *아닌* 처리 되지 않은 예외를 throw 할 때 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-118">An exception filter is executed when a controller method throws any unhandled exception that is *not* an **HttpResponseException** exception.</span></span> <span data-ttu-id="cafb2-119">**HttpResponseException** 형식은 HTTP 응답을 반환 하기 위해 특별히 디자인 되었기 때문에 특별 한 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-119">The **HttpResponseException** type is a special case, because it is designed specifically for returning an HTTP response.</span></span>

<span data-ttu-id="cafb2-120">예외 필터는 **system.web. filters. IExceptionFilter** 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-120">Exception filters implement the **System.Web.Http.Filters.IExceptionFilter** interface.</span></span> <span data-ttu-id="cafb2-121">예외 필터를 작성 하는 가장 간단한 방법은 **system.object** 에서 파생 하 고 **onexception** 메서드를 재정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-121">The simplest way to write an exception filter is to derive from the **System.Web.Http.Filters.ExceptionFilterAttribute** class and override the **OnException** method.</span></span>

> [!NOTE]
> <span data-ttu-id="cafb2-122">ASP.NET Web API의 예외 필터는 ASP.NET MVC의 필터와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-122">Exception filters in ASP.NET Web API are similar to those in ASP.NET MVC.</span></span> <span data-ttu-id="cafb2-123">그러나 별도의 네임 스페이스에 선언 되 고 함수는 개별적으로 함수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-123">However, they are declared in a separate namespace and function separately.</span></span> <span data-ttu-id="cafb2-124">특히 MVC에서 사용 되는 **Handleerrorattribute** 클래스는 Web API 컨트롤러에서 throw 된 예외를 처리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-124">In particular, the **HandleErrorAttribute** class used in MVC does not handle exceptions thrown by Web API controllers.</span></span>

<span data-ttu-id="cafb2-125">다음은 **NotImplementedException** 예외를 HTTP 상태 코드 501 (구현 되지 않음)로 변환 하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-125">Here is a filter that converts **NotImplementedException** exceptions into HTTP status code 501, Not Implemented:</span></span>

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

<span data-ttu-id="cafb2-126">**Httpactionexecutedcontext** 개체의 **response** 속성은 클라이언트에 전송 되는 HTTP 응답 메시지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-126">The **Response** property of the **HttpActionExecutedContext** object contains the HTTP response message that will be sent to the client.</span></span>

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a><span data-ttu-id="cafb2-127">예외 필터 등록</span><span class="sxs-lookup"><span data-stu-id="cafb2-127">Registering Exception Filters</span></span>

<span data-ttu-id="cafb2-128">다음과 같은 여러 가지 방법으로 Web API 예외 필터를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-128">There are several ways to register a Web API exception filter:</span></span>

- <span data-ttu-id="cafb2-129">작업 기준</span><span class="sxs-lookup"><span data-stu-id="cafb2-129">By action</span></span>
- <span data-ttu-id="cafb2-130">컨트롤러 기준</span><span class="sxs-lookup"><span data-stu-id="cafb2-130">By controller</span></span>
- <span data-ttu-id="cafb2-131">전역적으로</span><span class="sxs-lookup"><span data-stu-id="cafb2-131">Globally</span></span>

<span data-ttu-id="cafb2-132">특정 작업에 필터를 적용하려면 필터를 작업에 특성으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-132">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span>

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

<span data-ttu-id="cafb2-133">컨트롤러의 모든 작업에 필터를 적용 하려면 필터를 컨트롤러 클래스에 특성으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-133">To apply the filter to all of the actions on a controller, add the filter as an attribute to the controller class:</span></span>

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

<span data-ttu-id="cafb2-134">모든 Web API 컨트롤러에 필터를 전역적으로 적용 하려면 필터 인스턴스를 **Globalconfiguration. Filters** 컬렉션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-134">To apply the filter globally to all Web API controllers, add an instance of the filter to the **GlobalConfiguration.Configuration.Filters** collection.</span></span> <span data-ttu-id="cafb2-135">이 컬렉션의 예외 필터는 모든 Web API 컨트롤러 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-135">Exception filters in this collection apply to any Web API controller action.</span></span>

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

<span data-ttu-id="cafb2-136">"ASP.NET MVC 4 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여 프로젝트를 만드는 경우 응용 프로그램\_시작 폴더에 있는 `WebApiConfig` 클래스 안에 웹 API 구성 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-136">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, which is located in the App\_Start folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a><span data-ttu-id="cafb2-137">HttpError</span><span class="sxs-lookup"><span data-stu-id="cafb2-137">HttpError</span></span>

<span data-ttu-id="cafb2-138">**HttpError** 개체는 응답 본문에 오류 정보를 반환 하는 일관 된 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-138">The **HttpError** object provides a consistent way to return error information in the response body.</span></span> <span data-ttu-id="cafb2-139">다음 예제에서는 응답 본문에서 **HttpError** 를 사용 하 여 HTTP 상태 코드 404 (찾을 수 없음)를 반환 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-139">The following example shows how to return HTTP status code 404 (Not Found) with an **HttpError** in the response body.</span></span>

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

<span data-ttu-id="cafb2-140">**Createerrorresponse** 는 **시스템 .net. Http. HttpRequestMessageExtensions** 클래스에 정의 된 확장 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-140">**CreateErrorResponse** is an extension method defined in the **System.Net.Http.HttpRequestMessageExtensions** class.</span></span> <span data-ttu-id="cafb2-141">내부적으로 **Createerrorresponse** 는 **HttpError** 인스턴스를 만든 다음 **HttpError**을 포함 하는 **HttpResponseMessage** 를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-141">Internally, **CreateErrorResponse** creates an **HttpError** instance and then creates an **HttpResponseMessage** that contains the **HttpError**.</span></span>

<span data-ttu-id="cafb2-142">이 예제에서 메서드가 성공 하면 HTTP 응답에서 제품을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-142">In this example, if the method is successful, it returns the product in the HTTP response.</span></span> <span data-ttu-id="cafb2-143">그러나 요청 된 제품을 찾을 수 없는 경우 HTTP 응답은 요청 본문에 **HttpError** 를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-143">But if the requested product is not found, the HTTP response contains an **HttpError** in the request body.</span></span> <span data-ttu-id="cafb2-144">응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-144">The response might look like the following:</span></span>

[!code-console[Main](exception-handling/samples/sample9.cmd)]

<span data-ttu-id="cafb2-145">이 예에서는 **HttpError** 이 JSON으로 직렬화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-145">Notice that the **HttpError** was serialized to JSON in this example.</span></span> <span data-ttu-id="cafb2-146">**HttpError** 를 사용 하는 경우의 한 가지 이점은 강력한 형식의 다른 모델과 동일한 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md) 및 serialization 프로세스를 거치는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-146">One advantage of using **HttpError** is that it goes through the same [content-negotiation](../formats-and-model-binding/content-negotiation.md) and serialization process as any other strongly-typed model.</span></span>

### <a name="httperror-and-model-validation"></a><span data-ttu-id="cafb2-147">HttpError 및 모델 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="cafb2-147">HttpError and Model Validation</span></span>

<span data-ttu-id="cafb2-148">모델 유효성 검사의 경우 응답에 유효성 검사 오류를 포함 하기 위해 모델 상태를 **Createerrorresponse**에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-148">For model validation, you can pass the model state to **CreateErrorResponse**, to include the validation errors in the response:</span></span>

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

<span data-ttu-id="cafb2-149">이 예에서는 다음과 같은 응답을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-149">This example might return the following response:</span></span>

[!code-console[Main](exception-handling/samples/sample11.cmd)]

<span data-ttu-id="cafb2-150">모델 유효성 검사에 대 한 자세한 내용은 [ASP.NET Web API의 모델 유효성 검사](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="cafb2-150">For more information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

### <a name="using-httperror-with-httpresponseexception"></a><span data-ttu-id="cafb2-151">HttpResponseException와 함께 HttpError 사용</span><span class="sxs-lookup"><span data-stu-id="cafb2-151">Using HttpError with HttpResponseException</span></span>

<span data-ttu-id="cafb2-152">이전 예제는 컨트롤러 작업에서 **HttpResponseMessage** 메시지를 반환 하지만 **HttpResponseException** 를 사용 하 여 **HttpError**를 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-152">The previous examples return an **HttpResponseMessage** message from the controller action, but you can also use **HttpResponseException** to return an **HttpError**.</span></span> <span data-ttu-id="cafb2-153">이렇게 하면 일반적인 성공 사례에서 강력한 형식의 모델을 반환할 수 있고 오류가 발생 한 경우에는 여전히 **HttpError** 를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cafb2-153">This lets you return a strongly-typed model in the normal success case, while still returning **HttpError** if there is an error:</span></span>

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
