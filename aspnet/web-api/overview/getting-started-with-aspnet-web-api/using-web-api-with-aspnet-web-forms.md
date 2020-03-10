---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: ASP.NET Web Forms에서 Web API 사용-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x 용 ASP.NET Forms 응용 프로그램에 Web API를 추가 하는 과정을 단계별로 안내 하는 코드를 사용 하는 자습서
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448535"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="1fbca-103">ASP.NET 웹 양식과 Web API 사용</span><span class="sxs-lookup"><span data-stu-id="1fbca-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="1fbca-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1fbca-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="1fbca-105">이 자습서에서는 ASP.NET 4.x에서 기존 ASP.NET Web Forms 응용 프로그램에 Web API를 추가 하는 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="1fbca-106">개요</span><span class="sxs-lookup"><span data-stu-id="1fbca-106">Overview</span></span>

<span data-ttu-id="1fbca-107">ASP.NET Web API는 ASP.NET MVC를 사용 하 여 패키지 되지만 기존 ASP.NET Web Forms 응용 프로그램에 Web API를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="1fbca-108">Web Forms 응용 프로그램에서 Web API를 사용 하려면 두 가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="1fbca-109">**ApiController** 클래스에서 파생 되는 Web API 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="1fbca-110">**응용 프로그램\_Start** 메서드에 경로 테이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="1fbca-111">Web Forms 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="1fbca-111">Create a Web Forms Project</span></span>

<span data-ttu-id="1fbca-112">Visual Studio를 시작 하 고 **시작** 페이지에서 **새 프로젝트** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="1fbca-113">또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="1fbca-114">**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="1fbca-115">**시각적 개체 C#** 에서 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="1fbca-116">프로젝트 템플릿 목록에서 **ASP.NET Web Forms 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="1fbca-117">프로젝트의 이름을 입력 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="1fbca-118">모델 및 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="1fbca-118">Create the Model and Controller</span></span>

<span data-ttu-id="1fbca-119">이 자습서에서는 [시작](tutorial-your-first-web-api.md) 자습서와 동일한 모델 및 컨트롤러 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="1fbca-120">먼저 모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-120">First, add a model class.</span></span> <span data-ttu-id="1fbca-121">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **클래스 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="1fbca-122">클래스 이름을 Product로, 다음 구현을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="1fbca-123">그런 다음 프로젝트에 웹 API 컨트롤러를 추가 합니다. *컨트롤러* 는 web api에 대 한 HTTP 요청을 처리 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="1fbca-124">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="1fbca-125">**새 항목 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="1fbca-126">**설치 된 템플릿**에서  **C# Visual** 을 확장 하 고 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="1fbca-127">그런 다음 템플릿 목록에서 **WEB API 컨트롤러 클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="1fbca-128">컨트롤러 이름을 "ProductsController"로 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="1fbca-129">**새 항목 추가** 마법사에서 이름이 ProductsController.cs 인 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="1fbca-130">마법사에 포함 된 메서드를 삭제 하 고 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="1fbca-131">이 컨트롤러의 코드에 대 한 자세한 내용은 [초보자](tutorial-your-first-web-api.md) 를 위한 자습서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbca-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="1fbca-132">라우팅 정보 추가</span><span class="sxs-lookup"><span data-stu-id="1fbca-132">Add Routing Information</span></span>

<span data-ttu-id="1fbca-133">다음으로,/api/products/&quot; &quot;폼의 Uri가 컨트롤러로 라우팅되도록 URI 경로를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="1fbca-134">**솔루션 탐색기**에서 global.asax를 두 번 클릭 하 여 코드 Global.asax.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="1fbca-135">다음 **using** 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="1fbca-136">그런 다음 **응용 프로그램\_Start** 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="1fbca-137">라우팅 테이블에 대 한 자세한 내용은 [ASP.NET Web API 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1fbca-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="1fbca-138">클라이언트 쪽 AJAX 추가</span><span class="sxs-lookup"><span data-stu-id="1fbca-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="1fbca-139">클라이언트에서 액세스할 수 있는 web API를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="1fbca-140">이제 jQuery를 사용 하 여 API를 호출 하는 HTML 페이지를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="1fbca-141">마스터 페이지 (예: site.master)에 `ID="HeadContent"`의 `ContentPlaceHolder` 포함 되어 있는지 *확인 합니다.*</span><span class="sxs-lookup"><span data-stu-id="1fbca-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="1fbca-142">Default.aspx 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-142">Open the file Default.aspx.</span></span> <span data-ttu-id="1fbca-143">다음과 같이 주 콘텐츠 섹션에 있는 상용구 텍스트를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="1fbca-144">다음으로 `HeaderContent` 섹션에서 jQuery 소스 파일에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="1fbca-145">참고: **솔루션 탐색기** 파일을 코드 편집기 창으로 끌어서 놓아 스크립트 참조를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="1fbca-146">JQuery 스크립트 태그 아래에 다음 스크립트 블록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="1fbca-147">문서가 로드 되 면이 스크립트는 &quot;api/products&quot;에 대 한 AJAX 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="1fbca-148">요청은 제품 목록을 JSON 형식으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="1fbca-149">스크립트는 HTML 테이블에 제품 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="1fbca-150">응용 프로그램을 실행 하는 경우 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fbca-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
