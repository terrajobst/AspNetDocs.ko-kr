---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL 라우팅 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 66b727b69ca4f9a3d35b67f492f9a554146e09ef
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590716"
---
# <a name="url-routing"></a><span data-ttu-id="dabdf-103">URL 라우팅</span><span class="sxs-lookup"><span data-stu-id="dabdf-103">URL Routing</span></span>

<span data-ttu-id="dabdf-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="dabdf-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="dabdf-105">[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="dabdf-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="dabdf-106">이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="dabdf-107">[소스 코드를 포함 C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트는이 자습서 계열과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="dabdf-108">이 자습서에서는 URL 라우팅을 지원 하도록 정문 장난감 샘플 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-108">In this tutorial, you will modify the Wingtip Toys sample application to support URL routing.</span></span> <span data-ttu-id="dabdf-109">라우팅을 사용 하면 웹 응용 프로그램에서 친숙 하 고 쉽게 기억할 수 있는 Url을 사용 하 고 검색 엔진에서 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-109">Routing enables your web application to use URLs that are friendly, easier to remember, and better supported by search engines.</span></span> <span data-ttu-id="dabdf-110">이 자습서는 이전 자습서 "멤버 자격 및 관리"를 기반으로 하며, 정문 장난감 자습서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-110">This tutorial builds on the previous tutorial "Membership and Administration" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="dabdf-111">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="dabdf-111">What you'll learn:</span></span>

- <span data-ttu-id="dabdf-112">ASP.NET Web Forms 응용 프로그램에 대 한 경로를 등록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-112">How to register routes for an ASP.NET Web Forms application.</span></span>
- <span data-ttu-id="dabdf-113">웹 페이지에 경로를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="dabdf-113">How to add routes to a web page.</span></span>
- <span data-ttu-id="dabdf-114">경로를 지원 하기 위해 데이터베이스에서 데이터를 선택 하는 방법</span><span class="sxs-lookup"><span data-stu-id="dabdf-114">How to select data from a database to support routes.</span></span>

## <a name="aspnet-routing-overview"></a><span data-ttu-id="dabdf-115">ASP.NET 라우팅 개요</span><span class="sxs-lookup"><span data-stu-id="dabdf-115">ASP.NET Routing Overview</span></span>

<span data-ttu-id="dabdf-116">URL 라우팅을 사용 하면 실제 파일에 매핑되지 않는 요청 Url을 허용 하도록 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-116">URL routing allows you to configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="dabdf-117">요청 URL은 웹 사이트에서 페이지를 찾기 위해 사용자가 브라우저에 입력 하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-117">A request URL is simply the URL a user enters into their browser to find a page on your web site.</span></span> <span data-ttu-id="dabdf-118">라우팅을 사용 하 여 사용자에 게 의미 있는 의미 있는 Url을 정의 하 고 SEO (검색 엔진 최적화)에 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-118">You use routing to define URLs that are semantically meaningful to users and that can help with search-engine optimization (SEO).</span></span>

<span data-ttu-id="dabdf-119">기본적으로 Web Forms 템플릿에는 [ASP.NET 친화적인 url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-119">By default, the Web Forms template includes [ASP.NET Friendly URLs](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/).</span></span> <span data-ttu-id="dabdf-120">기본 라우팅 작업의 대부분은 *친숙 한 url*을 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-120">Much of the basic routing work will be implemented by using *Friendly URLs*.</span></span> <span data-ttu-id="dabdf-121">그러나이 자습서에서는 사용자 지정 된 라우팅 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-121">However, in this tutorial you will add customized routing capabilities.</span></span>

<span data-ttu-id="dabdf-122">URL 라우팅을 사용자 지정 하기 전에 다음 URL을 사용 하 여 정문 장난감 샘플 응용 프로그램을 제품에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-122">Before customizing URL routing, the Wingtip Toys sample application can link to a product using the following URL:</span></span>

`https://localhost:44300/ProductDetails.aspx?productID=2`

<span data-ttu-id="dabdf-123">URL 라우팅을 사용자 지정 하 여 URL을 더 쉽게 읽을 수 있도록 정문 장난감 샘플 응용 프로그램이 동일한 제품에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-123">By customizing URL routing, the Wingtip Toys sample application will link to the same product using an easier to read URL:</span></span>

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a><span data-ttu-id="dabdf-124">경로</span><span class="sxs-lookup"><span data-stu-id="dabdf-124">Routes</span></span>

<span data-ttu-id="dabdf-125">경로는 처리기에 매핑되는 URL 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-125">A route is a URL pattern that is mapped to a handler.</span></span> <span data-ttu-id="dabdf-126">처리기는 Web Forms 응용 프로그램의 .aspx 파일과 같은 물리적 파일이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-126">The handler can be a physical file, such as an .aspx file in a Web Forms application.</span></span> <span data-ttu-id="dabdf-127">처리기는 요청을 처리 하는 클래스 일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-127">A handler can also be a class that processes the request.</span></span> <span data-ttu-id="dabdf-128">경로를 정의 하려면 경로 클래스의 인스턴스를 만듭니다. 여기에는 URL 패턴, 처리기 및 경로 이름 (선택 사항)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-128">To define a route, you create an instance of the Route class by specifying the URL pattern, the handler, and optionally a name for the route.</span></span>

<span data-ttu-id="dabdf-129">`RouteTable` 클래스의 정적 `Routes` 속성에 `Route` 개체를 추가 하 여 응용 프로그램에 경로를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-129">You add the route to the application by adding the `Route` object to the static `Routes` property of the `RouteTable` class.</span></span> <span data-ttu-id="dabdf-130">경로 속성은 응용 프로그램에 대 한 모든 경로를 저장 하는 `RouteCollection` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-130">The Routes property is a `RouteCollection` object that stores all the routes for the application.</span></span>

### <a name="url-patterns"></a><span data-ttu-id="dabdf-131">URL 패턴</span><span class="sxs-lookup"><span data-stu-id="dabdf-131">URL Patterns</span></span>

<span data-ttu-id="dabdf-132">URL 패턴에는 리터럴 값과 변수 자리 표시자 (URL 매개 변수 라고 함)가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-132">A URL pattern can contain literal values and variable placeholders (referred to as URL parameters).</span></span> <span data-ttu-id="dabdf-133">리터럴과 자리 표시자는 슬래시 (`/`) 문자로 구분 되는 URL의 세그먼트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-133">The literals and placeholders are located in segments of the URL which are delimited by the slash (`/`) character.</span></span>

<span data-ttu-id="dabdf-134">웹 응용 프로그램에 대 한 요청을 만들면 URL은 세그먼트와 자리 표시자로 구문 분석 되 고 변수 값은 요청 처리기에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-134">When a request to your web application is made, the URL is parsed into segments and placeholders, and the variable values are provided to the request handler.</span></span> <span data-ttu-id="dabdf-135">이 프로세스는 쿼리 문자열의 데이터를 구문 분석 하 여 요청 처리기에 전달 하는 방법과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-135">This process is similar to the way the data in a query string is parsed and passed to the request handler.</span></span> <span data-ttu-id="dabdf-136">두 경우 모두 변수 정보는 URL에 포함 되 고 키-값 쌍 형식으로 처리기에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-136">In both cases, variable information is included in the URL and passed to the handler in the form of key-value pairs.</span></span> <span data-ttu-id="dabdf-137">쿼리 문자열의 경우 키와 값은 모두 URL에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-137">For query strings, both the keys and the values are in the URL.</span></span> <span data-ttu-id="dabdf-138">경로의 경우 키는 URL 패턴에 정의 된 자리 표시자 이름이 고, 값만 URL에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-138">For routes, the keys are the placeholder names defined in the URL pattern, and only the values are in the URL.</span></span>

<span data-ttu-id="dabdf-139">URL 패턴에서 자리 표시자를 중괄호 (`{` 및 `}`)로 묶어 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-139">In a URL pattern, you define placeholders by enclosing them in braces ( `{` and `}` ).</span></span> <span data-ttu-id="dabdf-140">세그먼트에 두 개 이상의 자리 표시자를 정의할 수 있지만 자리 표시자를 리터럴 값으로 구분 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-140">You can define more than one placeholder in a segment, but the placeholders must be separated by a literal value.</span></span> <span data-ttu-id="dabdf-141">예를 들어 `{language}-{country}/{action}`은 유효한 경로 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-141">For example, `{language}-{country}/{action}` is a valid route pattern.</span></span> <span data-ttu-id="dabdf-142">그러나 자리 표시자 사이에 리터럴 값 이나 구분 기호가 없기 때문에 `{language}{country}/{action}`은 올바른 패턴이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-142">However, `{language}{country}/{action}` is not a valid pattern, because there is no literal value or delimiter between the placeholders.</span></span> <span data-ttu-id="dabdf-143">따라서 라우팅은 국가 자리 표시자에 대 한 값에서 언어 자리 표시자 값을 분리할 위치를 결정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-143">Therefore, routing cannot determine where to separate the value for the language placeholder from the value for the country placeholder.</span></span>

### <a name="mapping-and-registering-routes"></a><span data-ttu-id="dabdf-144">경로 매핑 및 등록</span><span class="sxs-lookup"><span data-stu-id="dabdf-144">Mapping and Registering Routes</span></span>

<span data-ttu-id="dabdf-145">정문 장난감 샘플 응용 프로그램의 페이지에 대 한 경로를 포함 하려면 먼저 응용 프로그램이 시작 될 때 경로를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-145">Before you can include routes to pages of the Wingtip Toys sample application, you must register the routes when the application starts.</span></span> <span data-ttu-id="dabdf-146">경로를 등록 하려면 `Application_Start` 이벤트 처리기를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-146">To register the routes, you will modify the `Application_Start` event handler.</span></span>

1. <span data-ttu-id="dabdf-147">Visual Studio **솔루션 탐색기**에서 *Global.asax.cs* 파일을 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-147">In **Solution Explorer**of Visual Studio, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="dabdf-148">다음과 같이 노란색으로 강조 표시 된 코드를 *Global.asax.cs* 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-148">Add the code highlighted in yellow to the *Global.asax.cs* file as follows:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

<span data-ttu-id="dabdf-149">정문 장난감 샘플 응용 프로그램이 시작 되 면 `Application_Start` 이벤트 처리기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-149">When the Wingtip Toys sample application starts, it calls the `Application_Start` event handler.</span></span> <span data-ttu-id="dabdf-150">이 이벤트 처리기의 끝 부분에서 `RegisterCustomRoutes` 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-150">At the end of this event handler, the `RegisterCustomRoutes` method is called.</span></span> <span data-ttu-id="dabdf-151">`RegisterCustomRoutes` 메서드는 `RouteCollection` 개체의 `MapPageRoute` 메서드를 호출 하 여 각 경로를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-151">The `RegisterCustomRoutes` method adds each route by calling the `MapPageRoute` method of the `RouteCollection` object.</span></span> <span data-ttu-id="dabdf-152">경로는 경로 이름, 경로 URL 및 실제 URL을 사용 하 여 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-152">Routes are defined using a route name, a route URL and a physical URL.</span></span>

<span data-ttu-id="dabdf-153">첫 번째 매개 변수 ("`ProductsByCategoryRoute`")는 경로 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-153">The first parameter ("`ProductsByCategoryRoute`") is the route name.</span></span> <span data-ttu-id="dabdf-154">필요할 때 경로를 호출 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-154">It is used to call the route when it is needed.</span></span> <span data-ttu-id="dabdf-155">두 번째 매개 변수 ("`Category/{categoryName}`")는 코드에 따라 동적으로 사용할 수 있는 대체 URL을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-155">The second parameter ("`Category/{categoryName}`") defines the friendly replacement URL that can be dynamic based on code.</span></span> <span data-ttu-id="dabdf-156">데이터를 기반으로 생성 된 링크를 사용 하 여 데이터 컨트롤을 채울 때이 경로를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-156">You use this route when you are populating a data control with links that are generated based on data.</span></span> <span data-ttu-id="dabdf-157">경로는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-157">A route is shown as follows:</span></span>

[!code-csharp[Main](url-routing/samples/sample2.cs)]

<span data-ttu-id="dabdf-158">경로의 두 번째 매개 변수에는 중괄호 (`{ }`)로 지정 된 동적 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-158">The second parameter of the route includes a dynamic value specified by braces (`{ }`).</span></span> <span data-ttu-id="dabdf-159">이 경우 `categoryName`은 적절 한 라우팅 경로를 결정 하는 데 사용 되는 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-159">In this case, the `categoryName` is a variable that will be used to determine the proper routing path.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dabdf-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="dabdf-160">**Optional**</span></span>
> 
> <span data-ttu-id="dabdf-161">`RegisterCustomRoutes` 메서드를 별도의 클래스로 이동 하 여 코드를 보다 쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-161">You might find it easier to manage your code by moving the `RegisterCustomRoutes` method to a separate class.</span></span> <span data-ttu-id="dabdf-162">*논리* 폴더에서 별도의 `RouteActions` 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-162">In the *Logic* folder, create a separate `RouteActions` class.</span></span> <span data-ttu-id="dabdf-163">*Global.asax.cs* 파일에서 위의 `RegisterCustomRoutes` 메서드를 새 `RoutesActions` 클래스로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-163">Move the above `RegisterCustomRoutes` method from the *Global.asax.cs* file into the new `RoutesActions` class.</span></span> <span data-ttu-id="dabdf-164">*Global.asax.cs* 파일에서 `RegisterCustomRoutes` 메서드를 호출 하는 방법의 예로 `RoleActions` 클래스 및 `createAdmin` 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-164">Use the `RoleActions` class and the `createAdmin` method as an example of how to call the `RegisterCustomRoutes` method from the *Global.asax.cs* file.</span></span>

<span data-ttu-id="dabdf-165">`Application_Start` 이벤트 처리기의 시작 부분에서 `RouteConfig` 개체를 사용 하 여 `RegisterRoutes` 메서드 호출을 발견할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-165">You may also have noticed the `RegisterRoutes` method call using the `RouteConfig` object at the beginning of the `Application_Start` event handler.</span></span> <span data-ttu-id="dabdf-166">이 호출은 기본 라우팅을 구현 하기 위해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-166">This call is made to implement default routing.</span></span> <span data-ttu-id="dabdf-167">Visual Studio의 Web Forms 템플릿을 사용 하 여 응용 프로그램을 만들 때 기본 코드로 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-167">It was included as default code when you created the application using Visual Studio's Web Forms template.</span></span>

## <a name="retrieving-and-using-route-data"></a><span data-ttu-id="dabdf-168">경로 데이터 검색 및 사용</span><span class="sxs-lookup"><span data-stu-id="dabdf-168">Retrieving and Using Route Data</span></span>

<span data-ttu-id="dabdf-169">위에서 설명한 것 처럼 경로를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-169">As mentioned above, routes can be defined.</span></span> <span data-ttu-id="dabdf-170">*Global.asax.cs* 파일에서 `Application_Start` 이벤트 처리기에 추가한 코드는 정의 가능한 경로를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-170">The code that you added to the `Application_Start` event handler in the *Global.asax.cs* file loads the definable routes.</span></span>

### <a name="setting-routes"></a><span data-ttu-id="dabdf-171">경로 설정</span><span class="sxs-lookup"><span data-stu-id="dabdf-171">Setting Routes</span></span>

<span data-ttu-id="dabdf-172">경로를 추가 하려면 코드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-172">Routes require you to add additional code.</span></span> <span data-ttu-id="dabdf-173">이 자습서에서는 모델 바인딩을 사용 하 여 데이터 컨트롤의 데이터를 사용 하 여 경로를 생성할 때 사용 되는 `RouteValueDictionary` 개체를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-173">In this tutorial, you will use model binding to retrieve a `RouteValueDictionary` object that is used when generating the routes using data from a data control.</span></span> <span data-ttu-id="dabdf-174">`RouteValueDictionary` 개체에는 제품의 특정 범주에 속하는 제품 이름 목록이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-174">The `RouteValueDictionary` object will contain a list of product names that belong to a specific category of products.</span></span> <span data-ttu-id="dabdf-175">데이터 및 경로를 기반으로 하 여 각 제품에 대 한 링크가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-175">A link is created for each product based on the data and route.</span></span>

#### <a name="enable-routes-for-categories-and-products"></a><span data-ttu-id="dabdf-176">범주 및 제품에 대 한 경로 사용</span><span class="sxs-lookup"><span data-stu-id="dabdf-176">Enable Routes for Categories and Products</span></span>

<span data-ttu-id="dabdf-177">다음으로 `ProductsByCategoryRoute`를 사용 하 여 각 제품 범주 링크에 포함할 올바른 경로를 결정 하도록 응용 프로그램을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-177">Next, you'll update the application to use the `ProductsByCategoryRoute` to determine the correct route to include for each product category link.</span></span> <span data-ttu-id="dabdf-178">또한 각 제품에 대 한 라우트된 링크를 포함 하도록 *ProductList* 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-178">You'll also update the *ProductList.aspx* page to include a routed link for each product.</span></span> <span data-ttu-id="dabdf-179">이 링크는 변경 전 상태로 표시 되지만 이제 링크에서 URL 라우팅을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-179">The links will be displayed as they were before the change, however the links will now use URL routing.</span></span>

1. <span data-ttu-id="dabdf-180">**솔루션 탐색기**에서 site.master 페이지가 아직 열려 있지 않으면 엽니다 *.*</span><span class="sxs-lookup"><span data-stu-id="dabdf-180">In **Solution Explorer**, open the *Site.Master* page if it is not already open.</span></span>
2. <span data-ttu-id="dabdf-181">"`categoryList`" 이라는 **ListView** 컨트롤을 노란색으로 강조 표시 된 변경 내용으로 업데이트 하므로 태그는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-181">Update the **ListView** control named "`categoryList`" with the changes highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. <span data-ttu-id="dabdf-182">**솔루션 탐색기**에서 *ProductList* 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-182">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
4. <span data-ttu-id="dabdf-183">노란색으로 강조 표시 된 업데이트를 사용 하 여 *ProductList* 페이지의 `ItemTemplate` 요소를 업데이트 합니다. 그러면 태그가 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-183">Update the `ItemTemplate` element of the *ProductList.aspx* page with the updates highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. <span data-ttu-id="dabdf-184">*ProductList.aspx.cs* 의 코드를 열고 노란색으로 강조 표시 된 다음 네임 스페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-184">Open the code-behind of *ProductList.aspx.cs* and add the following namespace as highlighted in yellow:</span></span>  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. <span data-ttu-id="dabdf-185">코드 숨김으로 (*ProductList.aspx.cs*)의 `GetProducts` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-185">Replace the `GetProducts` method of the code-behind (*ProductList.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a><span data-ttu-id="dabdf-186">제품 정보에 대 한 코드 추가</span><span class="sxs-lookup"><span data-stu-id="dabdf-186">Add Code for Product Details</span></span>

<span data-ttu-id="dabdf-187">이제 경로 데이터를 사용 하도록 *제품 세부 정보 .aspx* 페이지에 대 한 코드를 업데이트 합니다 (*ProductDetails.aspx.cs*).</span><span class="sxs-lookup"><span data-stu-id="dabdf-187">Now, update the code-behind (*ProductDetails.aspx.cs*) for the *ProductDetails.aspx* page to use route data.</span></span> <span data-ttu-id="dabdf-188">새 `GetProduct` 메서드는 사용자에 게 더 이상 라우팅되지 않은 이전 URL을 사용 하는 링크가 있는 경우에도 쿼리 문자열 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-188">Notice that the new `GetProduct` method also accepts a query string value for the case where the user has a link bookmarked that uses the older non-friendly, non-routed URL.</span></span>

1. <span data-ttu-id="dabdf-189">코드 숨김으로 (*ProductDetails.aspx.cs*)의 `GetProduct` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-189">Replace the `GetProduct` method of the code-behind (*ProductDetails.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a><span data-ttu-id="dabdf-190">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="dabdf-190">Running the Application</span></span>

<span data-ttu-id="dabdf-191">이제 응용 프로그램을 실행 하 여 업데이트 된 경로를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-191">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="dabdf-192">**F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-192">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="dabdf-193">브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="dabdf-193">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="dabdf-194">페이지 맨 위에 있는 **제품** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-194">Click the **Products** link at the top of the page.</span></span>  
 <span data-ttu-id="dabdf-195">모든 제품은 *ProductList* 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-195">All products are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="dabdf-196">브라우저에 대 한 다음 URL (포트 번호 사용)이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-196">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/ProductList`
3. <span data-ttu-id="dabdf-197">그런 다음 페이지 위쪽의 **자동차** 범주 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-197">Next, click the **Cars** category link near the top of the page.</span></span>  
 <span data-ttu-id="dabdf-198">자동차가 *ProductList* 페이지에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-198">Only cars are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="dabdf-199">브라우저에 대 한 다음 URL (포트 번호 사용)이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-199">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Category/Cars`
4. <span data-ttu-id="dabdf-200">페이지에 나열 된 첫 번째 자동차의 이름을 포함 하는 링크를 클릭 하여 제품 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-200">Click the link containing the name of the first car listed on the page ("**Convertible Car**") to display the product details.</span></span>  
 <span data-ttu-id="dabdf-201">브라우저에 대 한 다음 URL (포트 번호 사용)이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-201">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Product/Convertible%20Car`
5. <span data-ttu-id="dabdf-202">그런 다음 경로를 사용 하지 않는 다음 URL을 브라우저에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-202">Next, enter the following non-routed URL (using your port number) into the browser:</span></span>  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 <span data-ttu-id="dabdf-203">코드는 사용자에 게 책갈피가 있는 링크를 포함 하는 경우 쿼리 문자열을 포함 하는 URL을 계속 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-203">The code still recognizes a URL that includes a query string, for the case where a user has a link bookmarked.</span></span>

## <a name="summary"></a><span data-ttu-id="dabdf-204">요약</span><span class="sxs-lookup"><span data-stu-id="dabdf-204">Summary</span></span>

<span data-ttu-id="dabdf-205">이 자습서에서는 범주 및 제품에 대 한 경로를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-205">In this tutorial, you have added routes for categories and products.</span></span> <span data-ttu-id="dabdf-206">모델 바인딩을 사용 하는 데이터 컨트롤과 경로를 통합 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-206">You have learned how routes can be integrated with data controls that use model binding.</span></span> <span data-ttu-id="dabdf-207">다음 자습서에서는 전역 오류 처리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="dabdf-207">In the next tutorial, you will implement global error handling.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dabdf-208">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="dabdf-208">Additional Resources</span></span>

[<span data-ttu-id="dabdf-209">ASP.NET 친화적인 Url</span><span class="sxs-lookup"><span data-stu-id="dabdf-209">ASP.NET Friendly URLs</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[<span data-ttu-id="dabdf-210">멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET Web Forms 앱을 배포 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="dabdf-210">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="dabdf-211">Microsoft Azure-무료 평가판</span><span class="sxs-lookup"><span data-stu-id="dabdf-211">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="dabdf-212">[이전](membership-and-administration.md)
> [다음](aspnet-error-handling.md)</span><span class="sxs-lookup"><span data-stu-id="dabdf-212">[Previous](membership-and-administration.md)
[Next](aspnet-error-handling.md)</span></span>
