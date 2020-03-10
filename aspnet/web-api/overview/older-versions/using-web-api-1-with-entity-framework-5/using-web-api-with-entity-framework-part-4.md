---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: '4 부: 관리 보기 추가 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447881"
---
# <a name="part-4-adding-an-admin-view"></a><span data-ttu-id="34dd1-102">4 부: 관리 보기 추가</span><span class="sxs-lookup"><span data-stu-id="34dd1-102">Part 4: Adding an Admin View</span></span>

<span data-ttu-id="34dd1-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="34dd1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="34dd1-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="34dd1-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="34dd1-105">관리 보기 추가</span><span class="sxs-lookup"><span data-stu-id="34dd1-105">Add an Admin View</span></span>

<span data-ttu-id="34dd1-106">이제 클라이언트 쪽으로 전환 하 고 관리 컨트롤러의 데이터를 사용할 수 있는 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="34dd1-107">페이지를 통해 사용자는 AJAX 요청을 컨트롤러에 전송 하 여 제품을 생성, 편집 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="34dd1-108">솔루션 탐색기에서 Controllers 폴더를 확장 하 고 이름이 HomeController.cs 인 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="34dd1-109">이 파일은 MVC 컨트롤러를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-109">This file contains an MVC controller.</span></span> <span data-ttu-id="34dd1-110">`Admin`라는 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="34dd1-111">**HttpRouteUrl** 메서드는 web API에 대 한 URI를 만들고 나중에 사용할 수 있도록이를 보기 모음에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="34dd1-112">그런 다음 `Admin` 작업 메서드 내에 텍스트 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 **뷰 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="34dd1-113">그러면 **보기 추가** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="34dd1-114">**보기 추가** 대화 상자에서 뷰 이름을 "Admin"으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="34dd1-115">**강력한 형식의 뷰 만들기**라는 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="34dd1-116">**모델 클래스**에서 "Product (제품명)"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="34dd1-117">다른 모든 옵션은 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="34dd1-118">**추가** 를 클릭 하면 Views/Home 아래에 Admin 이라는 파일이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="34dd1-119">이 파일을 열고 다음 HTML을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="34dd1-120">이 HTML은 페이지의 구조를 정의 하지만 아직 연결 된 기능은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="34dd1-121">관리 페이지에 대 한 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="34dd1-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="34dd1-122">솔루션 탐색기에서 Views 폴더를 확장 한 다음 공유 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="34dd1-123">\_Layout. cshtml 라는 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="34dd1-124">Id = "menu" 인 **ul** 요소와 관리 보기에 대 한 작업 링크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="34dd1-125">샘플 프로젝트에서는 "your your your your here" 문자열을 대체 하는 것과 같이 몇 가지 다른 외관상 변화를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="34dd1-126">응용 프로그램의 기능에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="34dd1-127">프로젝트를 다운로드 하 고 파일을 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-127">You can download the project and compare the files.</span></span>

<span data-ttu-id="34dd1-128">응용 프로그램을 실행 하 고 홈 페이지의 맨 위에 표시 되는 "관리" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="34dd1-129">관리 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="34dd1-130">지금은 페이지에서 어떤 작업도 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="34dd1-131">다음 섹션에서는 node.js를 사용 하 여 동적 UI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="34dd1-132">권한 부여 추가</span><span class="sxs-lookup"><span data-stu-id="34dd1-132">Add Authorization</span></span>

<span data-ttu-id="34dd1-133">현재이 사이트를 방문 하는 모든 사용자가 관리 페이지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="34dd1-134">관리자에 대 한 권한을 제한 하려면이를 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="34dd1-135">"관리자" 역할 및 관리자 사용자를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="34dd1-136">솔루션 탐색기에서 Filters 폴더를 확장 하 고 이름이 InitializeSimpleMembershipAttribute.cs 인 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="34dd1-137">`SimpleMembershipInitializer` 생성자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="34dd1-138">**InitializeDatabaseConnection**에 대 한 호출 후 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="34dd1-139">이는 "Administrator" 역할을 추가 하 고 역할에 대 한 사용자를 만들기 위한 신속 하 고 변경 된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="34dd1-140">솔루션 탐색기에서 Controllers 폴더를 확장 하 고 HomeController.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="34dd1-141">**권한 부여** 특성을 `Admin` 메서드에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="34dd1-142">AdminController.cs 파일을 열고 **권한 부여** 특성을 전체 `AdminController` 클래스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="34dd1-143">MVC 및 Web API는 서로 다른 네임 스페이스에 **권한 부여** 특성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="34dd1-144">MVC에서는 **AuthorizeAttribute**를 사용 하 고 web API는 **AuthorizeAttribute**를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>

<span data-ttu-id="34dd1-145">이제 관리자만이 관리 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="34dd1-146">또한 관리 컨트롤러에 HTTP 요청을 보내는 경우 요청은 인증 쿠키를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="34dd1-147">그렇지 않으면 서버에서 HTTP 401 (권한 없음) 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="34dd1-148">`http://localhost:*port*/api/admin`에 GET 요청을 전송 하 여 Fiddler에서이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd1-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="34dd1-149">[이전](using-web-api-with-entity-framework-part-3.md)
> [다음](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="34dd1-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
