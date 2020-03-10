---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: 빌드하는 tagbuilder 클래스를 사용 하 여 HTML 도우미 빌드 (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther는 빌드하는 tagbuilder 클래스 라는 ASP.NET MVC 프레임 워크에서 유용한 유틸리티 클래스를 소개 합니다. 빌드하는 tagbuilder 클래스를 사용 하 여 쉽게 수행할 수 있습니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b0aa9816209cc326d3dea4b8dfb1b13cf697fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485585"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a><span data-ttu-id="579a5-104">빌드하는 tagbuilder 클래스를 사용 하 여 HTML 도우미 빌드 (VB)</span><span class="sxs-lookup"><span data-stu-id="579a5-104">Using the TagBuilder Class to Build HTML Helpers (VB)</span></span>

<span data-ttu-id="579a5-105">[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="579a5-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="579a5-106">Stephen Walther는 빌드하는 tagbuilder 클래스 라는 ASP.NET MVC 프레임 워크에서 유용한 유틸리티 클래스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="579a5-107">빌드하는 tagbuilder 클래스를 사용 하 여 HTML 태그를 쉽게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-107">You can use the TagBuilder class to easily build HTML tags.</span></span>

<span data-ttu-id="579a5-108">ASP.NET MVC 프레임 워크에는 HTML 도우미를 빌드할 때 사용할 수 있는 빌드하는 tagbuilder 클래스 라는 유용한 유틸리티 클래스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="579a5-109">클래스 이름으로 빌드하는 tagbuilder 클래스를 사용 하면 HTML 태그를 쉽게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="579a5-110">이 간략 한 자습서에서는 빌드하는 tagbuilder 클래스에 대 한 개요를 제공 하 고, HTML &lt;img&gt; 태그를 렌더링 하는 간단한 HTML 도우미를 빌드할 때이 클래스를 사용 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="579a5-111">빌드하는 tagbuilder 클래스 개요</span><span class="sxs-lookup"><span data-stu-id="579a5-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="579a5-112">빌드하는 tagbuilder 클래스는 System.web 네임 스페이스에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="579a5-113">다음과 같은 5 가지 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-113">It has five methods:</span></span>

- <span data-ttu-id="579a5-114">AddCssClass () – 새 *class = ""* 특성을 태그에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-114">AddCssClass() – Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="579a5-115">GenerateId () – 태그에 id 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-115">GenerateId() – Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="579a5-116">이 메서드는 자동으로 id의 마침표를 바꿉니다 (기본적으로 마침표는 밑줄로 바뀜).</span><span class="sxs-lookup"><span data-stu-id="579a5-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="579a5-117">MergeAttribute () – 태그에 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-117">MergeAttribute() – Enables you to add attributes to a tag.</span></span> <span data-ttu-id="579a5-118">이 메서드의 오버 로드가 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="579a5-119">SetInnerText () – 태그의 내부 텍스트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-119">SetInnerText() – Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="579a5-120">내부 텍스트는 자동으로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="579a5-121">ToString () – 태그를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-121">ToString() – Enables you to render the tag.</span></span> <span data-ttu-id="579a5-122">일반 태그, 시작 태그, 끝 태그 또는 자체 닫는 태그를 만들지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>

<span data-ttu-id="579a5-123">빌드하는 tagbuilder 클래스에는 다음과 같은 네 가지 중요 한 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="579a5-124">Attributes – 태그의 모든 특성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-124">Attributes – Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="579a5-125">IdAttributeDotReplacement – GenerateId () 메서드가 마침표를 대체 하는 데 사용 하는 문자를 나타냅니다. 기본값은 밑줄입니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-125">IdAttributeDotReplacement – Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="579a5-126">InnerHTML – 태그의 내부 콘텐츠를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-126">InnerHTML – Represents the inner contents of the tag.</span></span> <span data-ttu-id="579a5-127">문자열을이 속성에 할당 하면 문자열을 HTML로 *인코딩하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="579a5-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="579a5-128">TagName – 태그의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-128">TagName – Represents the name of the tag.</span></span>

<span data-ttu-id="579a5-129">이러한 메서드와 속성은 HTML 태그를 작성 하는 데 필요한 모든 기본 메서드 및 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="579a5-130">빌드하는 tagbuilder 클래스를 반드시 사용할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="579a5-131">대신 StringBuilder 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="579a5-132">그러나 빌드하는 tagbuilder 클래스를 사용 하면 좀 더 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="579a5-133">이미지 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="579a5-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="579a5-134">빌드하는 tagbuilder 클래스의 인스턴스를 만들 때 빌드하는 tagbuilder 생성자에 빌드 하려는 태그의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="579a5-135">그런 다음 AddCssClass 및 MergeAttribute () 메서드와 같은 메서드를 호출 하 여 태그의 특성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="579a5-136">마지막으로 ToString () 메서드를 호출 하 여 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="579a5-137">예를 들어 목록 1에는 이미지 HTML 도우미가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="579a5-138">이미지 도우미는 HTML &lt;img&gt; 태그를 나타내는 빌드하는 tagbuilder를 사용 하 여 내부적으로 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="579a5-139">**목록 1 – Helpers\ImageHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="579a5-139">**Listing 1 – Helpers\ImageHelper.vb**</span></span>

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

<span data-ttu-id="579a5-140">목록 1의 모듈에는 Image () 라는 두 개의 오버 로드 된 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-140">The module in Listing 1 contains two overloaded methods named Image().</span></span> <span data-ttu-id="579a5-141">Image () 메서드를 호출 하는 경우 HTML 특성 집합을 나타내는 개체를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="579a5-142">빌드하는 tagbuilder. MergeAttribute () 메서드를 사용 하 여 src 특성과 같은 개별 특성을 빌드하는 tagbuilder에 추가 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="579a5-143">또한 빌드하는 tagbuilder. MergeAttributes () 메서드를 사용 하 여 빌드하는 tagbuilder에 특성 컬렉션을 추가 하는 방법도 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="579a5-144">MergeAttributes () 메서드는 Dictionary&lt;string, object&gt; 매개 변수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="579a5-145">RouteValueDictionary 클래스는 특성의 컬렉션을 나타내는 개체를 사전&lt;문자열, 개체&gt;로 변환 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="579a5-146">이미지 도우미를 만든 후에는 다른 표준 HTML 도우미와 마찬가지로 ASP.NET MVC 뷰에서 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="579a5-147">목록 2의 보기는 이미지 도우미를 사용 하 여 Xbox의 동일한 이미지를 두 번 표시 합니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="579a5-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="579a5-148">Image () 도우미는 HTML 특성 컬렉션을 사용 하거나 사용 하지 않고 모두 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="579a5-149">**목록 2 – Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="579a5-149">**Listing 2 – Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]

<span data-ttu-id="579a5-150">[새 프로젝트 대화 상자 ![](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="579a5-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="579a5-151">**그림 01**: 이미지 도우미 사용 ([전체 크기 이미지를 보려면 클릭](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="579a5-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span></span>

<span data-ttu-id="579a5-152">Index .aspx 뷰의 맨 위에 있는 이미지 도우미와 연결 된 네임 스페이스를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="579a5-153">도우미는 다음 지시문을 사용 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

<span data-ttu-id="579a5-154">Visual Basic 응용 프로그램에서 기본 네임 스페이스는 응용 프로그램의 이름과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="579a5-154">In a Visual Basic application, the default namespace is the same as the name of the application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="579a5-155">[이전](creating-custom-html-helpers-vb.md)
> [다음](creating-page-layouts-with-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="579a5-155">[Previous](creating-custom-html-helpers-vb.md)
[Next](creating-page-layouts-with-view-master-pages-vb.md)</span></span>
