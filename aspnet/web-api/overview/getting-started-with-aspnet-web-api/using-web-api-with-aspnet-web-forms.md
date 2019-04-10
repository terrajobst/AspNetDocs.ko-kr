---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: 웹 API를 사용 하 여 ASP.NET Web forms-ASP.NET 4.x
author: MikeWasson
description: Asp.net Web API ASP.NET Forms 응용 프로그램에 추가할 단계별로 코드를 사용 하 여 자습서 4.x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422579"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="eed55-103">ASP.NET Web Forms에 Web API 사용</span><span class="sxs-lookup"><span data-stu-id="eed55-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="eed55-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="eed55-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="eed55-105">이 자습서에서는 ASP.NET에서 기존의 ASP.NET Web Forms 응용 프로그램에 Web API를 추가 하는 단계를 통해 4.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="eed55-106">개요</span><span class="sxs-lookup"><span data-stu-id="eed55-106">Overview</span></span>

<span data-ttu-id="eed55-107">ASP.NET Web API는 ASP.NET MVC를 사용 하 여 패키지를 이지만 쉽게 기존의 ASP.NET Web Forms 응용 프로그램에 Web API를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="eed55-108">Web Forms 응용 프로그램에서 웹 API를 사용 하려면 두 가지 주요 단계:</span><span class="sxs-lookup"><span data-stu-id="eed55-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="eed55-109">파생 되는 Web API 컨트롤러를 추가 합니다 **ApiController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="eed55-110">경로 테이블을 추가 합니다 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="eed55-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="eed55-111">Web Forms 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="eed55-111">Create a Web Forms Project</span></span>

<span data-ttu-id="eed55-112">Visual Studio를 시작 하 고 선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="eed55-113">또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="eed55-114">에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="eed55-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="eed55-115">아래 **Visual C#** 를 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="eed55-116">프로젝트 템플릿 목록에서 선택 **ASP.NET Web Forms 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="eed55-117">프로젝트에 대 한 이름을 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="eed55-118">모델 및 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="eed55-118">Create the Model and Controller</span></span>

<span data-ttu-id="eed55-119">이 자습서와 동일한 모델 및 컨트롤러 클래스를 사용 합니다 [Getting Started](tutorial-your-first-web-api.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="eed55-120">먼저 모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-120">First, add a model class.</span></span> <span data-ttu-id="eed55-121">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **클래스 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="eed55-122">제품에 클래스 이름을 지정 하 고 다음 구현을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="eed55-123">그런 다음에 프로젝트에는 Web API 컨트롤러를 추가 *컨트롤러* 는 웹 API에 대 한 HTTP 요청을 처리 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="eed55-124">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="eed55-125">선택 **새 항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="eed55-126">아래 **설치 된 템플릿**를 확장 하 고 **Visual C#** 선택한 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="eed55-127">그런 다음 템플릿의 목록에서 선택 **Web API 컨트롤러 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="eed55-128">"ProductsController" 컨트롤러 이름을 지정 하 고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="eed55-129">합니다 **새 항목 추가** ProductsController.cs 라는 파일을 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="eed55-130">마법사를 포함 하는 메서드를 삭제 하 고 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="eed55-131">이 컨트롤러의 코드에 대 한 자세한 내용은 참조는 [Getting Started](tutorial-your-first-web-api.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="eed55-132">라우팅 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-132">Add Routing Information</span></span>

<span data-ttu-id="eed55-133">다음으로, 추가 URI 경로 이므로 폼의 해당 Uri &quot;/a pi/제품/&quot; 컨트롤러로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="eed55-134">**솔루션 탐색기**, 코드 숨김 파일 Global.asax.cs Global.asax를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="eed55-135">다음을 추가 합니다 **를 사용 하 여** 문입니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="eed55-136">다음 코드를 추가 합니다 **응용 프로그램\_시작** 메서드:</span><span class="sxs-lookup"><span data-stu-id="eed55-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="eed55-137">라우팅 테이블에 대 한 자세한 내용은 참조 하십시오 [ASP.NET Web API에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="eed55-138">클라이언트 쪽 AJAX를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="eed55-139">이것이 전부 웹 클라이언트가 액세스할 수 있는 API를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="eed55-140">이제 jQuery를 사용 하 여 API를 호출 하는 HTML 페이지를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="eed55-141">마스터 페이지에 있는지 확인 (예를 들어 *Site.Master*) 포함 된 `ContentPlaceHolder` 사용 하 여 `ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="eed55-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="eed55-142">Default.aspx 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-142">Open the file Default.aspx.</span></span> <span data-ttu-id="eed55-143">표시 된 것 처럼 주 콘텐츠 섹션에 있는 상용구 텍스트를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="eed55-144">다음으로, jQuery 원본 파일에 대 한 참조를 추가 합니다 `HeaderContent` 섹션:</span><span class="sxs-lookup"><span data-stu-id="eed55-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="eed55-145">참고: 파일을 끌어서 놓아 스크립트 참조를 쉽게 추가할 수 있습니다 **솔루션 탐색기** 코드 편집기 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="eed55-146">JQuery 스크립트 태그 아래 다음 스크립트 블록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="eed55-147">이 스크립트는 AJAX 요청에 문서가 로드 되 면 &quot;api/제품&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="eed55-148">요청에는 JSON 형식으로 제품 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="eed55-149">스크립트를 HTML 테이블에는 제품 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="eed55-150">응용 프로그램을 실행 하면 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed55-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
