---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 작업 만들기 (VB) | Microsoft Docs
author: microsoft
description: ASP.NET MVC 컨트롤러에 새 작업을 추가 하는 방법에 대해 알아봅니다. 메서드가 동작 하기 위한 요구 사항에 대해 알아봅니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: b1b53bea899deecef203551b23c087944e3990ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470159"
---
# <a name="creating-an-action-vb"></a><span data-ttu-id="30110-104">작업 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="30110-104">Creating an Action (VB)</span></span>

<span data-ttu-id="30110-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="30110-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="30110-106">ASP.NET MVC 컨트롤러에 새 작업을 추가 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30110-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="30110-107">메서드가 동작 하기 위한 요구 사항에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30110-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="30110-108">이 자습서의 목표는 새 컨트롤러 작업을 만드는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30110-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="30110-109">작업 방법의 요구 사항에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30110-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="30110-110">메서드가 작업으로 노출 되지 않도록 하는 방법에 대해서도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30110-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="30110-111">컨트롤러에 작업 추가</span><span class="sxs-lookup"><span data-stu-id="30110-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="30110-112">컨트롤러에 새 메서드를 추가 하 여 컨트롤러에 새 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30110-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="30110-113">예를 들어 1을 나열 하는 컨트롤러에는 Index () 라는 작업과 SayHello () 라는 동작이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="30110-114">두 메서드는 모두 작업으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30110-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="30110-115">**목록 1-Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="30110-115">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

<span data-ttu-id="30110-116">작업으로 universe에 노출 되기 위해 메서드는 특정 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30110-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="30110-117">메서드는 public 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30110-117">The method must be public.</span></span>
- <span data-ttu-id="30110-118">메서드는 정적 메서드 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="30110-119">메서드는 확장 메서드 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="30110-120">메서드는 생성자, getter 또는 setter가 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="30110-121">이 메서드에는 개방형 제네릭 형식을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="30110-122">메서드가 컨트롤러 기본 클래스의 메서드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="30110-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="30110-123">메서드는 **ref** 또는 **out** 매개 변수를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="30110-124">컨트롤러 작업의 반환 형식에 대 한 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="30110-125">컨트롤러 작업은 문자열, 날짜/시간, 임의 클래스의 인스턴스 또는 void를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="30110-126">ASP.NET MVC 프레임 워크는 작업 결과가 아닌 반환 형식을 문자열로 변환 하 고 브라우저에 문자열을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="30110-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="30110-127">이러한 요구 사항을 위반 하지 않는 메서드를 컨트롤러에 추가 하면 메서드가 컨트롤러 작업으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30110-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="30110-128">여기에서 주의 하세요.</span><span class="sxs-lookup"><span data-stu-id="30110-128">Be careful here.</span></span> <span data-ttu-id="30110-129">컨트롤러 작업은 인터넷에 연결 된 모든 사용자가 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="30110-130">예를 들어 DeleteMyWebsite () 컨트롤러 작업을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="30110-131">Public 메서드가 호출 되지 않도록 방지</span><span class="sxs-lookup"><span data-stu-id="30110-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="30110-132">컨트롤러 클래스에서 공용 메서드를 만들어야 하는데 컨트롤러 작업으로 메서드를 노출 하지 않으려는 경우 &lt;NonAction&gt; 특성을 사용 하 여 메서드가 호출 되지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the &lt;NonAction&gt; attribute.</span></span> <span data-ttu-id="30110-133">예를 들어 목록 2의 컨트롤러에는 &lt;NonAction&gt; 특성으로 데코레이팅된 CompanySecrets () 라는 공용 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30110-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the &lt;NonAction&gt; attribute.</span></span>

<span data-ttu-id="30110-134">**목록 2-Controllerss\ststomom.vb**</span><span class="sxs-lookup"><span data-stu-id="30110-134">**Listing 2 - Controllers\WorkController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

<span data-ttu-id="30110-135">브라우저의 주소 표시줄에/Work/CompanySecrets를 입력 하 여 CompanySecrets () 컨트롤러 작업을 호출 하려고 하면 그림 1에 표시 된 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30110-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="30110-136">[비 작업 메서드를 호출 하 ![](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="30110-136">[![Invoking a NonAction method](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span></span>

<span data-ttu-id="30110-137">**그림 01**: nonaction 메서드 호출 ([전체 크기 이미지를 보려면 클릭](creating-an-action-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="30110-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-vb/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="30110-138">[이전](creating-a-controller-vb.md)
> [다음](aspnet-mvc-controllers-overview-cs.md)</span><span class="sxs-lookup"><span data-stu-id="30110-138">[Previous](creating-a-controller-vb.md)
[Next](aspnet-mvc-controllers-overview-cs.md)</span></span>
