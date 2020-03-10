---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
title: 컨트롤러 만들기 (VB) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서 Stephen Walther는 ASP.NET MVC 응용 프로그램에 컨트롤러를 추가 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 204b7e86-f560-4611-8adb-785b33e777b9
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
msc.type: authoredcontent
ms.openlocfilehash: 60636b79ab5fc06ca904dee90ce74f256e046d12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486833"
---
# <a name="creating-a-controller-vb"></a><span data-ttu-id="833b9-103">컨트롤러 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="833b9-103">Creating a Controller (VB)</span></span>

<span data-ttu-id="833b9-104">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="833b9-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="833b9-105">이 자습서에서 Stephen Walther는 ASP.NET MVC 응용 프로그램에 컨트롤러를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>

<span data-ttu-id="833b9-106">이 자습서의 목표는 새 ASP.NET MVC 컨트롤러를 만드는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="833b9-107">Visual Studio 컨트롤러 추가 메뉴 옵션을 사용 하 고 직접 클래스 파일을 만들어 컨트롤러를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="833b9-108">컨트롤러 추가 메뉴 옵션 사용</span><span class="sxs-lookup"><span data-stu-id="833b9-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="833b9-109">새 컨트롤러를 만드는 가장 쉬운 방법은 Visual Studio 솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가, 컨트롤러** 메뉴 옵션을 선택 하는 것입니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="833b9-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="833b9-110">이 메뉴 옵션을 선택 하면 **컨트롤러 추가** 대화 상자가 열립니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="833b9-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>

<span data-ttu-id="833b9-111">[새 프로젝트 대화 상자 ![](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="833b9-111">[![The New Project dialog box](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)</span></span>

<span data-ttu-id="833b9-112">**그림 01**: 새 컨트롤러 추가 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="833b9-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-vb/_static/image2.png))</span></span>

<span data-ttu-id="833b9-113">[새 프로젝트 대화 상자 ![](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="833b9-113">[![The New Project dialog box](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)</span></span>

<span data-ttu-id="833b9-114">**그림 02**: 컨트롤러 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="833b9-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-vb/_static/image4.png))</span></span>

<span data-ttu-id="833b9-115">컨트롤러 이름의 첫 번째 부분은 **컨트롤러 추가** 대화 상자에서 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="833b9-116">모든 컨트롤러 이름은 접미사 *컨트롤러로*끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="833b9-117">예를 들어 Product *controller* 라는 컨트롤러가 아니라 *Product*라는 컨트롤러를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>

<span data-ttu-id="833b9-118">*컨트롤러 접미사가 없는* 컨트롤러를 만드는 경우 컨트롤러를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="833b9-119">이 작업을 수행 하지 마세요 .이 작업을 수행한 후에는 많은 시간 동안 지속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>

<span data-ttu-id="833b9-120">**목록 1-Controller\entstomom.xml**</span><span class="sxs-lookup"><span data-stu-id="833b9-120">**Listing 1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample1.vb)]

<span data-ttu-id="833b9-121">항상 controllers 폴더에 컨트롤러를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="833b9-122">그렇지 않으면 ASP.NET MVC의 규칙을 위반 하 게 됩니다. 다른 개발자는 응용 프로그램을 이해 하는 데 더 많은 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="833b9-123">스 캐 폴딩 작업 메서드</span><span class="sxs-lookup"><span data-stu-id="833b9-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="833b9-124">컨트롤러를 만들 때 만들기, 업데이트 및 세부 정보 작업 메서드를 자동으로 생성 하는 옵션이 있습니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="833b9-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="833b9-125">이 옵션을 선택 하면 목록 2의 컨트롤러 클래스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-125">If you select this option then the controller class in Listing 2 is generated.</span></span>

<span data-ttu-id="833b9-126">[작업 메서드 자동 생성 ![](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="833b9-126">[![Creating action methods automatically](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)</span></span>

<span data-ttu-id="833b9-127">**그림 03**: 자동으로 작업 메서드 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="833b9-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-vb/_static/image6.png))</span></span>

<span data-ttu-id="833b9-128">**목록 2-Controllers\CustomerController.vb**</span><span class="sxs-lookup"><span data-stu-id="833b9-128">**Listing 2 - Controllers\CustomerController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample2.vb)]

<span data-ttu-id="833b9-129">이러한 생성 된 메서드는 스텁 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-129">These generated methods are stub methods.</span></span> <span data-ttu-id="833b9-130">고객에 대 한 세부 정보를 만들고, 업데이트 하 고, 표시 하는 실제 논리를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="833b9-131">그러나 스텁 메서드는 좋은 시작 지점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="833b9-132">컨트롤러 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="833b9-132">Creating a Controller Class</span></span>

<span data-ttu-id="833b9-133">ASP.NET MVC 컨트롤러는 클래스 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="833b9-134">원하는 경우 편리한 Visual Studio 컨트롤러 스 캐 폴딩을 무시 하 고 컨트롤러 클래스를 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="833b9-135">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="833b9-135">Follow these steps:</span></span>

1. <span data-ttu-id="833b9-136">Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목** 을 차례로 선택한 다음 **클래스** 템플릿을 선택 합니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="833b9-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="833b9-137">새 클래스 이름을 PersonController로 하 고 **추가** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-137">Name the new class PersonController.vb and click the **Add** button.</span></span>
3. <span data-ttu-id="833b9-138">클래스가 기본 System.object 클래스에서 상속 하도록 결과 클래스 파일을 수정 합니다 (목록 3 참조).</span><span class="sxs-lookup"><span data-stu-id="833b9-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>

<span data-ttu-id="833b9-139">[새 클래스를 만드는 ![](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="833b9-139">[![Creating a new class](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)</span></span>

<span data-ttu-id="833b9-140">**그림 04**: 새 클래스 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="833b9-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-vb/_static/image8.png))</span></span>

<span data-ttu-id="833b9-141">**목록 3-Controllers\PersonController.vb**</span><span class="sxs-lookup"><span data-stu-id="833b9-141">**Listing 3 - Controllers\PersonController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample3.vb)]

<span data-ttu-id="833b9-142">목록 3의 컨트롤러는 "Hello World!" 문자열을 반환 하는 Index () 라는 하나의 동작을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="833b9-143">응용 프로그램을 실행 하 고 다음과 같은 URL을 요청 하 여이 컨트롤러 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="833b9-144">ASP.NET 개발 서버는 임의의 포트 번호 (예: 40071)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="833b9-145">컨트롤러를 호출 하는 데 사용할 URL을 입력 하는 경우 올바른 포트 번호를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="833b9-146">화면 오른쪽 아래에 있는 Windows 알림 영역에서 ASP.NET 개발 서버 아이콘 위에 마우스를 가져가면 포트 번호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="833b9-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="833b9-147">[이전](adding-dynamic-content-to-a-cached-page-vb.md)
> [다음](creating-an-action-vb.md)</span><span class="sxs-lookup"><span data-stu-id="833b9-147">[Previous](adding-dynamic-content-to-a-cached-page-vb.md)
[Next](creating-an-action-vb.md)</span></span>
