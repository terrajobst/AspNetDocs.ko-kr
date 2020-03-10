---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 페이지 모델 | Microsoft Docs
author: microsoft
description: ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 기반 코드 모델 중에서 선택할 것입니다. 코드 숨김이 Src 특성을 사용 하 여 구현 될 수 있습니다.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440711"
---
# <a name="the-aspnet-20-page-model"></a><span data-ttu-id="9444f-104">ASP.NET 2.0 페이지 모델</span><span class="sxs-lookup"><span data-stu-id="9444f-104">The ASP.NET 2.0 Page Model</span></span>

<span data-ttu-id="9444f-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="9444f-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9444f-106">ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 기반 코드 모델 중에서 선택할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="9444f-107">코드 숨김은 Src 특성을 사용 하거나 @Page 지시문의 CodeBehind 특성을 사용 하 여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="9444f-108">ASP.NET 2.0에서 개발자는 인라인 코드와 코드 숨김으로 선택할 수 있지만 코드 숨김이 크게 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

<span data-ttu-id="9444f-109">ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 기반 코드 모델 중에서 선택할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="9444f-110">코드 숨김은 Src 특성을 사용 하거나 @Page 지시문의 CodeBehind 특성을 사용 하 여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="9444f-111">ASP.NET 2.0에서 개발자는 인라인 코드와 코드 숨김으로 선택할 수 있지만 코드 숨김이 크게 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="9444f-112">코드 숨김이 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="9444f-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="9444f-113">ASP.NET 2.0에서 코드 숨겨진 모델의 변경 내용을 완전히 이해 하려면 모델을 ASP.NET 1.x에 있던 것과 같이 신속 하 게 검토 하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="9444f-114">ASP.NET 1.x의 코드 숨김이 모델</span><span class="sxs-lookup"><span data-stu-id="9444f-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="9444f-115">ASP.NET 1.x에서 코드에 포함 된 모델은 ASPX 파일 (Webform) 및 프로그래밍 코드를 포함 하는 코드를 포함 하는 파일로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="9444f-116">두 파일은 ASPX 파일의 @Page 지시어를 사용 하 여 연결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="9444f-117">ASPX 페이지의 각 컨트롤에는 인스턴스 변수로 코드 숨김이 파일에 해당 하는 선언이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="9444f-118">코드 숨김으로는 이벤트 바인딩과 Visual Studio 디자이너에 필요한 생성 된 코드에 대 한 코드도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="9444f-119">이 모델은 상당히 잘 작동 하지만, ASPX 페이지의 모든 ASP.NET 요소에 코드를 입력 하는 데 해당 코드가 필요 하므로 코드와 콘텐츠가 실제로 분리 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="9444f-120">예를 들어, 디자이너에서 Visual Studio IDE 외부의 ASPX 파일에 새 서버 컨트롤을 추가한 경우 코드 숨기기 파일의 해당 컨트롤에 대 한 선언이 없기 때문에 응용 프로그램이 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="9444f-121">ASP.NET 2.0의 코드 숨김이 모델</span><span class="sxs-lookup"><span data-stu-id="9444f-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="9444f-122">ASP.NET 2.0은이 모델에 대해 크게 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="9444f-123">ASP.NET 2.0에서 코드 숨김이 ASP.NET 2.0에 제공 된 새로운 *partial 클래스* 를 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="9444f-124">ASP.NET 2.0의 코드 숨김이 클래스는 partial 클래스로 정의 됩니다. 즉, 클래스 정의의 일부만 포함 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-124">The code-behind class in ASP.NET 2.0 is defined as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="9444f-125">클래스 정의의 나머지 부분은 런타임에 ASPX 페이지를 사용 하 여 ASP.NET 2.0에 의해 동적으로 생성 되거나 웹 사이트를 미리 컴파일하는 경우에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="9444f-126">@ Page 지시문을 사용 하 여 코드 숨김이 파일 및 ASPX 페이지 간의 링크를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="9444f-127">그러나 CodeBehind 또는 Src 특성 대신 ASP.NET 2.0은 이제 CodeFile 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="9444f-128">Inherits 특성은 페이지의 클래스 이름을 지정 하는 데도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="9444f-129">일반적인 @ Page 지시문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="9444f-130">ASP.NET 2.0 코드 숨김으로 표시 되는 일반적인 클래스 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="9444f-131">C#및 Visual Basic는 현재 부분 클래스를 지 원하는 관리 되는 유일한 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="9444f-132">따라서 j #을 사용 하는 개발자는 ASP.NET 2.0에서 코드 숨김이 모델을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>

<span data-ttu-id="9444f-133">개발자가 만든 코드만 포함 하는 코드 파일을 포함 하는 코드 파일을 새 모델에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="9444f-134">또한 코드 숨김이 파일에 인스턴스 변수 선언이 없기 때문에 코드와 콘텐츠의 진정한 분리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="9444f-135">ASPX 페이지의 partial 클래스는 이벤트 바인딩이 발생 하는 위치 이기 때문에 Visual Basic 개발자는 코드 숨김으로 Handles 키워드를 사용 하 여 이벤트를 바인딩하는 방법으로 약간의 성능 향상을 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="9444f-136">C#에 해당 하는 키워드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-136">C# has no equivalent keyword.</span></span>

## <a name="new--page-directive-attributes"></a><span data-ttu-id="9444f-137">새 @ Page 지시문 특성</span><span class="sxs-lookup"><span data-stu-id="9444f-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="9444f-138">ASP.NET 2.0는 @ Page 지시문에 많은 새 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="9444f-139">ASP.NET 2.0의 새로운 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="9444f-140">Async</span><span class="sxs-lookup"><span data-stu-id="9444f-140">Async</span></span>

<span data-ttu-id="9444f-141">Async 특성을 사용 하면 비동기적으로 실행 되도록 페이지를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="9444f-142">이 모듈의 뒷부분에서 비동기 페이지를 잘 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="9444f-143">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="9444f-143">AsyncTimeout</span></span>

<span data-ttu-id="9444f-144">비동기 페이지에 대 한 제한 시간을 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="9444f-145">기본값은 45 초입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="9444f-146">CodeFile</span><span class="sxs-lookup"><span data-stu-id="9444f-146">CodeFile</span></span>

<span data-ttu-id="9444f-147">CodeFile 특성은 Visual Studio 2002/2003의 CodeBehind 특성에 대 한 대체입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="9444f-148">CodeFileBaseClass</span><span class="sxs-lookup"><span data-stu-id="9444f-148">CodeFileBaseClass</span></span>

<span data-ttu-id="9444f-149">CodeFileBaseClass 특성은 여러 페이지가 단일 기본 클래스에서 파생 되 게 하려는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="9444f-150">이 특성이 없는 ASP.NET의 partial 클래스 구현으로 인해 안전망 컴파일 엔진은 페이지의 컨트롤을 기반으로 새 멤버를 자동으로 만들기 때문에 ASPX 페이지에 선언 된 컨트롤을 참조 하는 데 공유 공통 필드를 사용 하는 기본 클래스가 제대로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="9444f-151">따라서 ASP.NET에서 둘 이상의 페이지에 대 한 공통 기본 클래스를 원하는 경우 CodeFileBaseClass 특성에 기본 클래스를 지정 하 고 해당 기본 클래스에서 각 pages 클래스를 파생 하도록 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="9444f-152">이 특성을 사용 하는 경우에도 CodeFile 특성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="9444f-153">CompilationMode</span><span class="sxs-lookup"><span data-stu-id="9444f-153">CompilationMode</span></span>

<span data-ttu-id="9444f-154">이 특성을 사용 하면 ASPX 페이지의 CompilationMode 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="9444f-155">CompilationMode 속성은 **항상**, **Auto**및 **Never**값을 포함 하는 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="9444f-156">기본값은 **항상**입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-156">The default is **Always**.</span></span> <span data-ttu-id="9444f-157">**자동** 설정은 ASP.NET가 페이지를 동적으로 컴파일하는 것을 방지 합니다 (가능한 경우).</span><span class="sxs-lookup"><span data-stu-id="9444f-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="9444f-158">동적 컴파일의 페이지를 제외 하면 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="9444f-159">그러나 제외 된 페이지에 컴파일해야 하는 코드가 포함 되어 있으면 페이지를 검색할 때 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="9444f-160">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="9444f-160">EnableEventValidation</span></span>

<span data-ttu-id="9444f-161">이 특성은 다시 게시 및 콜백 이벤트의 유효성을 검사할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="9444f-162">이 기능을 사용 하는 경우 다시 게시 또는 콜백 이벤트에 대 한 인수를 검사 하 여 원래 렌더링 한 서버 컨트롤에서 해당 인수를 생성 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="9444f-163">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="9444f-163">EnableTheming</span></span>

<span data-ttu-id="9444f-164">이 특성은 페이지에서 ASP.NET 테마를 사용할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="9444f-165">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-165">The default is **false**.</span></span> <span data-ttu-id="9444f-166">ASP.NET 테마는 [모듈 10](profiles-themes-and-web-parts.md)에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="9444f-167">LinePragmas</span><span class="sxs-lookup"><span data-stu-id="9444f-167">LinePragmas</span></span>

<span data-ttu-id="9444f-168">이 특성은 컴파일하는 동안 줄 pragma를 추가할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="9444f-169">줄 pragma는 디버거에서 특정 코드 섹션을 표시 하는 데 사용 되는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="9444f-170">MaintainScrollPositionOnPostback</span><span class="sxs-lookup"><span data-stu-id="9444f-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="9444f-171">이 특성은 포스트백 사이에서 스크롤 위치를 유지 하기 위해 JavaScript가 페이지에 삽입 되는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="9444f-172">이 특성은 기본적으로 **false** 입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="9444f-173">이 특성을 **true로 설정**하면 ASP.NET는 &lt;스크립트&gt; 추가 하 여 다음과 같은 다시 게시를 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="9444f-174">이 스크립트 블록의 src는 Webresource.axd입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="9444f-175">이 리소스는 실제 경로가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-175">This resource is not a physical path.</span></span> <span data-ttu-id="9444f-176">이 스크립트를 요청 하면 ASP.NET는 스크립트를 동적으로 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="9444f-177">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="9444f-177">MasterPageFile</span></span>

<span data-ttu-id="9444f-178">이 특성은 현재 페이지의 마스터 페이지 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="9444f-179">경로는 상대적이거나 절대적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-179">The path can be relative or absolute.</span></span> <span data-ttu-id="9444f-180">마스터 페이지는 [모듈 4](master-pages.md)에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="9444f-181">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="9444f-181">StyleSheetTheme</span></span>

<span data-ttu-id="9444f-182">이 특성을 사용 하면 ASP.NET 2.0 테마에서 정의한 사용자 인터페이스 모양 속성을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="9444f-183">테마는 [모듈 10](profiles-themes-and-web-parts.md)에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="9444f-184">테마</span><span class="sxs-lookup"><span data-stu-id="9444f-184">Theme</span></span>

<span data-ttu-id="9444f-185">페이지의 테마를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-185">Specifies the theme for the page.</span></span> <span data-ttu-id="9444f-186">StyleSheetTheme 특성에 값이 지정 되지 않은 경우 테마 특성은 페이지의 컨트롤에 적용 된 모든 스타일을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="9444f-187">제목</span><span class="sxs-lookup"><span data-stu-id="9444f-187">Title</span></span>

<span data-ttu-id="9444f-188">페이지의 제목을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-188">Sets the title for the page.</span></span> <span data-ttu-id="9444f-189">여기에 지정 된 값은 렌더링 된 페이지의 &lt;title&gt; 요소에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="9444f-190">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="9444f-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="9444f-191">ViewStateEncryptionMode 열거의 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="9444f-192">사용 가능한 값은 **항상**, **자동**, **안 함**입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="9444f-193">기본값은 **Auto**입니다. 이 특성이 **Auto**값으로 설정 된 경우 viewstate는 암호화 됩니다. **RegisterRequiresViewStateEncryption** 메서드를 호출 하 여 컨트롤에서 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="9444f-194">@ Page 지시문을 통해 Public 속성 값 설정</span><span class="sxs-lookup"><span data-stu-id="9444f-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="9444f-195">ASP.NET 2.0의 @ Page 지시문의 또 다른 새로운 기능은 기본 클래스의 공용 속성에 대 한 초기 값을 설정 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="9444f-196">예를 들어, 기본 클래스에 **SomeText** 이라는 public 속성이 있고 페이지가 로드 될 때 **Hello** 로 초기화 되는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="9444f-197">이렇게 하려면 다음과 같이 @ Page 지시문의 값을 설정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="9444f-198">@ Page 지시문의 **SomeText** 특성은 기본 클래스에 있는 SomeText 속성의 초기 값을 *Hello!* 로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="9444f-199">다음 비디오는 @ Page 지시어를 사용 하 여 기본 클래스에서 공용 속성의 초기 값을 설정 하는 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>

![](the-asp-net-2-0-page-model/_static/image1.png)

[<span data-ttu-id="9444f-200">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="9444f-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="9444f-201">Page 클래스의 새 Public 속성</span><span class="sxs-lookup"><span data-stu-id="9444f-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="9444f-202">ASP.NET 2.0의 새로운 공용 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="9444f-203">AppRelativeTemplateSourceDirectory</span><span class="sxs-lookup"><span data-stu-id="9444f-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="9444f-204">페이지 또는 컨트롤에 대 한 응용 프로그램 상대 경로를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="9444f-205">예를 들어 http://app/folder/page.aspx에 있는 페이지의 경우 속성은 ~/folder/.를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="9444f-206">AppRelativeVirtualPath</span><span class="sxs-lookup"><span data-stu-id="9444f-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="9444f-207">페이지 또는 컨트롤에 대 한 상대 가상 디렉터리 경로를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="9444f-208">예를 들어 http://app/folder/page.aspx에 있는 페이지에 대 한 속성은</span><span class="sxs-lookup"><span data-stu-id="9444f-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="9444f-209">AsyncTimeout</span><span class="sxs-lookup"><span data-stu-id="9444f-209">AsyncTimeout</span></span>

<span data-ttu-id="9444f-210">비동기 페이지 처리에 사용 되는 제한 시간을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="9444f-211">비동기 페이지는이 모듈의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="9444f-212">ClientQueryString</span><span class="sxs-lookup"><span data-stu-id="9444f-212">ClientQueryString</span></span>

<span data-ttu-id="9444f-213">요청 된 URL의 쿼리 문자열 부분을 반환 하는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="9444f-214">이 값은 URL로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-214">This value is URL encoded.</span></span> <span data-ttu-id="9444f-215">HttpServerUtility 클래스의 UrlDecode 메서드를 사용 하 여이를 디코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="9444f-216">ClientScript</span><span class="sxs-lookup"><span data-stu-id="9444f-216">ClientScript</span></span>

<span data-ttu-id="9444f-217">이 속성은 클라이언트 쪽 스크립트의 안전망 내보내기를 관리 하는 데 사용할 수 있는 ClientScriptManager 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="9444f-218">ClientScriptManager 클래스는이 모듈의 뒷부분에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="9444f-219">EnableEventValidation</span><span class="sxs-lookup"><span data-stu-id="9444f-219">EnableEventValidation</span></span>

<span data-ttu-id="9444f-220">이 속성은 다시 게시 및 콜백 이벤트에 대해 이벤트 유효성 검사를 사용할지 여부를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="9444f-221">이 기능을 사용 하도록 설정 하면 다시 게시 또는 콜백 이벤트에 대 한 인수를 확인 하 여 원래 렌더링 한 서버 컨트롤에서 해당 인수를 생성 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="9444f-222">EnableTheming</span><span class="sxs-lookup"><span data-stu-id="9444f-222">EnableTheming</span></span>

<span data-ttu-id="9444f-223">이 속성은 ASP.NET 2.0 테마가 페이지에 적용 되는지 여부를 지정 하는 부울을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="9444f-224">Form</span><span class="sxs-lookup"><span data-stu-id="9444f-224">Form</span></span>

<span data-ttu-id="9444f-225">이 속성은 ASPX 페이지의 HTML 폼을 HtmlForm 개체로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="9444f-226">헤더</span><span class="sxs-lookup"><span data-stu-id="9444f-226">Header</span></span>

<span data-ttu-id="9444f-227">이 속성은 페이지 헤더를 포함 하는 HtmlHead 개체에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="9444f-228">반환 된 HtmlHead 개체를 사용 하 여 스타일 시트, 메타 태그 등을 가져오거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="9444f-229">IdSeparator</span><span class="sxs-lookup"><span data-stu-id="9444f-229">IdSeparator</span></span>

<span data-ttu-id="9444f-230">이 읽기 전용 속성은 ASP.NET가 페이지에서 컨트롤의 고유 ID를 빌드할 때 컨트롤 식별자를 구분 하는 데 사용 되는 문자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="9444f-231">코드에서 직접 사용하기에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="9444f-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="9444f-232">IsAsync</span></span>

<span data-ttu-id="9444f-233">이 속성은 비동기 페이지를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="9444f-234">비동기 페이지는이 모듈의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="9444f-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="9444f-235">IsCallback</span></span>

<span data-ttu-id="9444f-236">이 읽기 전용 속성은 페이지가 콜백 된 경우 **true** 를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="9444f-237">호출 백업은이 모듈의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="9444f-238">IsCrossPagePostBack</span><span class="sxs-lookup"><span data-stu-id="9444f-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="9444f-239">페이지가 페이지 간 포스트백의 일부인 경우이 읽기 전용 속성은 **true** 를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="9444f-240">페이지 간 포스트백은이 모듈의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="9444f-241">Items</span><span class="sxs-lookup"><span data-stu-id="9444f-241">Items</span></span>

<span data-ttu-id="9444f-242">페이지 컨텍스트에 저장 된 모든 개체를 포함 하는 IDictionary 인스턴스에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="9444f-243">이 IDictionary 개체에 항목을 추가할 수 있으며 컨텍스트의 수명 동안 해당 항목을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="9444f-244">MaintainScrollPositionOnPostBack</span><span class="sxs-lookup"><span data-stu-id="9444f-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="9444f-245">이 속성은 포스트백이 발생 한 후 브라우저에서 페이지 스크롤 위치를 유지 하는 JavaScript를 ASP.NET에서 제거할지 여부를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="9444f-246">이 속성에 대 한 자세한 내용은이 모듈의 앞부분에서 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="9444f-247">마스터</span><span class="sxs-lookup"><span data-stu-id="9444f-247">Master</span></span>

<span data-ttu-id="9444f-248">이 읽기 전용 속성은 마스터 페이지가 적용 된 페이지에 대 한 MasterPage 인스턴스에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="9444f-249">MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="9444f-249">MasterPageFile</span></span>

<span data-ttu-id="9444f-250">페이지의 마스터 페이지 파일 이름을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="9444f-251">이 속성은 PreInit 메서드에만 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="9444f-252">MaxPageStateFieldLength</span><span class="sxs-lookup"><span data-stu-id="9444f-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="9444f-253">이 속성은 페이지 상태에 대 한 최대 길이 (바이트)를 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="9444f-254">속성이 양수로 설정 된 경우 페이지 뷰 상태는 지정 된 바이트 수를 초과 하지 않도록 여러 개의 숨겨진 필드로 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="9444f-255">속성이 음수 이면 뷰 상태가 청크로 분할 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="9444f-256">PageAdapter</span><span class="sxs-lookup"><span data-stu-id="9444f-256">PageAdapter</span></span>

<span data-ttu-id="9444f-257">요청 하는 브라우저의 페이지를 수정 하는 PageAdapter 개체에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="9444f-258">PreviousPage</span><span class="sxs-lookup"><span data-stu-id="9444f-258">PreviousPage</span></span>

<span data-ttu-id="9444f-259">서버. 전송 또는 페이지 간 포스트백의 경우 이전 페이지에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="9444f-260">SkinID</span><span class="sxs-lookup"><span data-stu-id="9444f-260">SkinID</span></span>

<span data-ttu-id="9444f-261">페이지에 적용할 ASP.NET 2.0 스킨을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="9444f-262">StyleSheetTheme</span><span class="sxs-lookup"><span data-stu-id="9444f-262">StyleSheetTheme</span></span>

<span data-ttu-id="9444f-263">이 속성은 페이지에 적용 되는 스타일 시트를 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="9444f-264">TemplateControl</span><span class="sxs-lookup"><span data-stu-id="9444f-264">TemplateControl</span></span>

<span data-ttu-id="9444f-265">페이지의 포함 하는 컨트롤에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="9444f-266">테마</span><span class="sxs-lookup"><span data-stu-id="9444f-266">Theme</span></span>

<span data-ttu-id="9444f-267">페이지에 적용 되는 ASP.NET 2.0 테마의 이름을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="9444f-268">PreInit 메서드 이전에이 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="9444f-269">제목</span><span class="sxs-lookup"><span data-stu-id="9444f-269">Title</span></span>

<span data-ttu-id="9444f-270">이 속성은 페이지 머리글에서 가져온 페이지의 제목을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="9444f-271">ViewStateEncryptionMode</span><span class="sxs-lookup"><span data-stu-id="9444f-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="9444f-272">페이지의 ViewStateEncryptionMode를 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="9444f-273">이 모듈의 앞부분에서이 속성에 대 한 자세한 설명을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="9444f-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="9444f-274">Page 클래스의 새 Protected 속성</span><span class="sxs-lookup"><span data-stu-id="9444f-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="9444f-275">ASP.NET 2.0에서 페이지 클래스의 새 보호 된 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="9444f-276">어댑터</span><span class="sxs-lookup"><span data-stu-id="9444f-276">Adapter</span></span>

<span data-ttu-id="9444f-277">요청한 장치에서 페이지를 렌더링 하는 ControlAdapter에 대 한 참조를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="9444f-278">AsyncMode</span><span class="sxs-lookup"><span data-stu-id="9444f-278">AsyncMode</span></span>

<span data-ttu-id="9444f-279">이 속성은 페이지가 비동기식으로 처리 되는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="9444f-280">런타임에 사용 하기 위한 것 이며 코드에서 직접 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="9444f-281">ClientIDSeparator</span><span class="sxs-lookup"><span data-stu-id="9444f-281">ClientIDSeparator</span></span>

<span data-ttu-id="9444f-282">이 속성은 컨트롤에 대 한 고유한 클라이언트 Id를 만들 때 구분 기호로 사용 되는 문자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="9444f-283">런타임에 사용 하기 위한 것 이며 코드에서 직접 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="9444f-284">PageStatePersister</span><span class="sxs-lookup"><span data-stu-id="9444f-284">PageStatePersister</span></span>

<span data-ttu-id="9444f-285">이 속성은 페이지에 대 한 PageStatePersister 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="9444f-286">이 속성은 ASP.NET 컨트롤 개발자가 주로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="9444f-287">UniqueFilePathSuffix</span><span class="sxs-lookup"><span data-stu-id="9444f-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="9444f-288">이 속성은 브라우저 캐싱에 사용할 파일 경로에 추가 되는 고유 접미사를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-288">This property returns a unique suffix that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="9444f-289">기본값은 \_\_ufps =이 고 6 자리 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="9444f-290">Page 클래스에 대 한 새 공용 메서드</span><span class="sxs-lookup"><span data-stu-id="9444f-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="9444f-291">다음 공용 메서드는 ASP.NET 2.0의 Page 클래스에 새로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="9444f-292">AddOnPreRenderCompleteAsync</span><span class="sxs-lookup"><span data-stu-id="9444f-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="9444f-293">이 메서드는 비동기 페이지 실행에 대 한 이벤트 처리기 대리자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="9444f-294">비동기 페이지는이 모듈의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="9444f-295">ApplyStyleSheetSkin</span><span class="sxs-lookup"><span data-stu-id="9444f-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="9444f-296">페이지 스타일 시트의 속성을 페이지에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="9444f-297">ExecuteRegisteredAsyncTasks</span><span class="sxs-lookup"><span data-stu-id="9444f-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="9444f-298">이 메서드는 비동기 작업을 생물 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="9444f-299">GetValidators</span><span class="sxs-lookup"><span data-stu-id="9444f-299">GetValidators</span></span>

<span data-ttu-id="9444f-300">지정 된 유효성 검사 그룹에 대 한 유효성 검사기 컬렉션 또는 지정 된 항목이 없는 경우 기본 유효성 검사 그룹을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="9444f-301">RegisterAsyncTask</span><span class="sxs-lookup"><span data-stu-id="9444f-301">RegisterAsyncTask</span></span>

<span data-ttu-id="9444f-302">이 메서드는 새 비동기 작업을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-302">This method registers a new async task.</span></span> <span data-ttu-id="9444f-303">비동기 페이지는이 모듈의 뒷부분에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="9444f-304">RegisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="9444f-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="9444f-305">이 메서드는 pages 컨트롤 상태를 유지 해야 ASP.NET에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="9444f-306">RegisterRequiresViewStateEncryption</span><span class="sxs-lookup"><span data-stu-id="9444f-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="9444f-307">이 메서드는 페이지 viewstate에 암호화가 필요 ASP.NET에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="9444f-308">ResolveClientUrl</span><span class="sxs-lookup"><span data-stu-id="9444f-308">ResolveClientUrl</span></span>

<span data-ttu-id="9444f-309">이미지에 대 한 클라이언트 요청 등에 사용할 수 있는 상대 URL을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="9444f-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="9444f-310">SetFocus</span></span>

<span data-ttu-id="9444f-311">이 메서드는 페이지가 처음 로드 될 때 지정 된 컨트롤에 포커스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="9444f-312">UnregisterRequiresControlState</span><span class="sxs-lookup"><span data-stu-id="9444f-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="9444f-313">이 메서드는 컨트롤 상태 지 속성을 더 이상 요구 하지 않으므로 전달 된 컨트롤의 등록을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="9444f-314">페이지 수명 주기에 대 한 변경</span><span class="sxs-lookup"><span data-stu-id="9444f-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="9444f-315">ASP.NET 2.0의 페이지 수명 주기는 크게 변경 되지 않았지만 알아야 할 몇 가지 새로운 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-315">The page lifecycle in ASP.NET 2.0 hasn't changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="9444f-316">ASP.NET 2.0 페이지 수명 주기는 아래에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="9444f-317">PreInit (ASP.NET 2.0의 새로운 새)</span><span class="sxs-lookup"><span data-stu-id="9444f-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="9444f-318">PreInit 이벤트는 개발자가 액세스할 수 있는 수명 주기의 가장 이른 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="9444f-319">이 이벤트를 추가 하면 프로그래밍 방식으로 ASP.NET 2.0 테마, 마스터 페이지, ASP.NET 2.0 프로필에 대 한 액세스 속성 등을 변경할 수 있습니다. 다시 게시 상태인 경우에는 Viewstate가 현재 수명 주기의이 시점에서 컨트롤에 아직 적용 되지 않았음을 인식 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="9444f-320">따라서 개발자가이 단계에서 컨트롤의 속성을 변경 하는 경우 나중에 페이지 수명 주기에서 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="9444f-321">Init</span><span class="sxs-lookup"><span data-stu-id="9444f-321">Init</span></span>

<span data-ttu-id="9444f-322">Init 이벤트는 ASP.NET 1.x에서 변경 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="9444f-323">이 위치에서 페이지의 컨트롤 속성을 읽거나 초기화 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="9444f-324">이 단계에서는 마스터 페이지, 테마 등이 페이지에 이미 적용 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="9444f-325">InitComplete (2.0의 새로운 새)</span><span class="sxs-lookup"><span data-stu-id="9444f-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="9444f-326">InitComplete 이벤트는 페이지 초기화 단계가 끝날 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="9444f-327">수명 주기의이 시점에서 페이지의 컨트롤에 액세스할 수 있지만 상태는 아직 채워지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="9444f-328">프리 로드 (2.0의 새로운 새)</span><span class="sxs-lookup"><span data-stu-id="9444f-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="9444f-329">이 이벤트는 모든 포스트백 데이터가 적용 된 후 페이지\_로드 직전에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="9444f-330">로드</span><span class="sxs-lookup"><span data-stu-id="9444f-330">Load</span></span>

<span data-ttu-id="9444f-331">ASP.NET 1. x에서 로드 이벤트가 변경 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="9444f-332">LoadComplete (2.0의 새로운 새)</span><span class="sxs-lookup"><span data-stu-id="9444f-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="9444f-333">LoadComplete 이벤트는 페이지 로드 단계의 마지막 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="9444f-334">이 단계에서는 모든 포스트백 및 viewstate 데이터가 페이지에 적용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="9444f-335">PreRender</span><span class="sxs-lookup"><span data-stu-id="9444f-335">PreRender</span></span>

<span data-ttu-id="9444f-336">페이지에 동적으로 추가 되는 컨트롤에 대해 viewstate를 적절히 유지 하려면 PreRender 이벤트를 추가할 수 있는 마지막 기회입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="9444f-337">PreRenderComplete (2.0의 새로운 새)</span><span class="sxs-lookup"><span data-stu-id="9444f-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="9444f-338">PreRenderComplete 단계에서 모든 컨트롤이 페이지에 추가 되 고 페이지가 렌더링 될 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="9444f-339">PreRenderComplete 이벤트는 페이지 viewstate가 저장 되기 전에 발생 한 마지막 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="9444f-340">SaveStateComplete (2.0의 새로운 새)</span><span class="sxs-lookup"><span data-stu-id="9444f-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="9444f-341">SaveStateComplete 이벤트는 모든 페이지 viewstate와 컨트롤 상태가 저장 된 직후에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="9444f-342">이 이벤트는 페이지가 실제로 브라우저에 렌더링 되기 전의 마지막 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="9444f-343">렌더링</span><span class="sxs-lookup"><span data-stu-id="9444f-343">Render</span></span>

<span data-ttu-id="9444f-344">ASP.NET 1.x 이후 렌더링 메서드가 변경 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="9444f-345">HtmlTextWriter이 초기화 되 고 페이지가 브라우저에 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="9444f-346">ASP.NET 2.0에서 페이지 간 다시 게시</span><span class="sxs-lookup"><span data-stu-id="9444f-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="9444f-347">ASP.NET 1.x에서는 동일한 페이지에 게시 하는 데 포스트백이 필요 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="9444f-348">페이지 간 포스트백은 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="9444f-349">ASP.NET 2.0는 IButtonControl 인터페이스를 통해 다른 페이지로 다시 게시 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="9444f-350">새 IButtonControl 인터페이스를 구현 하는 모든 컨트롤 (Button, LinkButton 및 ImageButton과 타사 사용자 지정 컨트롤)은 PostBackUrl 특성을 사용 하 여이 새로운 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="9444f-351">다음 코드에서는 두 번째 페이지에 다시 게시 되는 단추 컨트롤을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="9444f-352">페이지가 다시 게시 되 면 다시 게시를 시작 하는 페이지는 두 번째 페이지의 PreviousPage 속성을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="9444f-353">이 기능은 ASP.NET 2.0에서 컨트롤이 다른 페이지에 다시 게시 될 때 해당 페이지에 렌더링 하는 새로운 WebForm\_DoPostBackWithOptions 클라이언트 쪽 함수를 통해 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="9444f-354">이 JavaScript 함수는 클라이언트에 스크립트를 내보내는 새 Webresource.axd 처리기에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="9444f-355">다음 비디오는 페이지 간 포스트백의 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-355">The video below is a walkthrough of a cross-page postback.</span></span>

![](the-asp-net-2-0-page-model/_static/image2.png)

[<span data-ttu-id="9444f-356">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="9444f-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="9444f-357">페이지 간 다시 게시에 대 한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="9444f-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="9444f-358">뷰</span><span class="sxs-lookup"><span data-stu-id="9444f-358">Viewstate</span></span>

<span data-ttu-id="9444f-359">페이지 간 다시 게시 시나리오에서 첫 페이지의 viewstate에 발생 하는 상황을 이미 확인 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="9444f-360">IPostBackDataHandler를 구현 하지 않는 모든 컨트롤은 viewstate를 통해 상태를 유지 하므로 페이지 간 다시 게시의 두 번째 페이지에서 해당 컨트롤의 속성에 액세스할 수 있도록 페이지의 viewstate에 대 한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="9444f-361">ASP.NET 2.0는 \_\_PREVIOUSPAGE 이라는 두 번째 페이지에서 새 숨겨진 필드를 사용 하 여이 시나리오를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="9444f-362">\_\_PREVIOUSPAGE 양식 필드는 첫 번째 페이지의 viewstate를 포함 하 여 두 번째 페이지에 있는 모든 컨트롤의 속성에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="9444f-363">우회 FindControl</span><span class="sxs-lookup"><span data-stu-id="9444f-363">Circumventing FindControl</span></span>

<span data-ttu-id="9444f-364">페이지 간 포스트백의 비디오 연습에서는 FindControl 메서드를 사용 하 여 첫 번째 페이지의 TextBox 컨트롤에 대 한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="9444f-365">해당 메서드는 이러한 용도로도 잘 작동 하지만 FindControl는 비용이 많이 들고 추가 코드를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="9444f-366">다행히 ASP.NET 2.0은이 목적을 위해 여러 시나리오에서 작동 하는 FindControl에 대 한 대안을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="9444f-367">PreviousPageType 지시문을 사용 하면 TypeName 또는 VirtualPath 특성을 사용 하 여 이전 페이지에 대 한 강력한 형식의 참조를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="9444f-368">TypeName 특성을 사용 하면 이전 페이지의 형식을 지정할 수 있는 반면 VirtualPath 특성을 사용 하면 가상 경로를 사용 하 여 이전 페이지를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="9444f-369">PreviousPageType 지시문을 설정한 후에는 공용 속성을 사용 하 여 액세스를 허용 하려는 컨트롤 등을 노출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="9444f-370">랩 1 페이지 간 다시 게시</span><span class="sxs-lookup"><span data-stu-id="9444f-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="9444f-371">이 랩에서는 ASP.NET 2.0의 새로운 페이지 간 다시 게시 기능을 사용 하는 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="9444f-372">Visual Studio 2005를 열고 새 ASP.NET 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="9444f-373">Webform 라는 새 새를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="9444f-374">디자인 뷰에서 default.aspx를 열고 단추 컨트롤과 TextBox 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="9444f-375">단추 컨트롤에 **Submitbutton 단추** 를 지정 하 고 TextBox 컨트롤에서 **UserName**id를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="9444f-376">단추의 PostBackUrl 속성을로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="9444f-377">소스 뷰에서 default.aspx를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="9444f-378">아래와 같이 @ PreviousPageType 지시어를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="9444f-379">페이지\_페이지에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="9444f-380">빌드 메뉴에서 빌드를 클릭 하 여 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="9444f-381">Default.aspx의 코드 숨김으로 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="9444f-382">페이지를 .aspx에서 로드\_페이지를 다음으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="9444f-383">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-383">Build the project.</span></span>
11. <span data-ttu-id="9444f-384">프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-384">Run the project.</span></span>
12. <span data-ttu-id="9444f-385">텍스트 상자에 사용자 이름을 입력 하 고 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="9444f-386">결과는 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="9444f-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="9444f-387">ASP.NET 2.0의 비동기 페이지</span><span class="sxs-lookup"><span data-stu-id="9444f-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="9444f-388">ASP.NET의 많은 경합 문제는 외부 호출 (예: 웹 서비스 또는 데이터베이스 호출)의 대기 시간, 파일 IO 대기 시간 등으로 인해 발생 합니다. ASP.NET 응용 프로그램에 대해 요청을 수행 하는 경우 ASP.NET는 해당 작업자 스레드 중 하나를 사용 하 여 해당 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="9444f-389">요청이 완료 되 고 응답이 전송 될 때까지 해당 요청은 해당 스레드를 소유 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="9444f-390">ASP.NET 2.0는 페이지를 비동기적으로 실행 하는 기능을 추가 하 여 이러한 유형의 문제에 대 한 대기 시간 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="9444f-391">즉, 작업자 스레드가 요청을 시작한 다음 다른 스레드에 추가 실행을 전달 하 여 사용 가능한 스레드 풀로 신속 하 게 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="9444f-392">파일 IO, 데이터베이스 호출 등이 완료 되 면 요청을 완료 하기 위해 스레드 풀에서 새 스레드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="9444f-393">페이지를 비동기적으로 실행 하는 첫 번째 단계는 다음과 같이 페이지 지시문의 **Async** 특성을 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="9444f-394">이 특성은 ASP.NET에 게 페이지에 대 한 IHttpAsyncHandler을 구현 하도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="9444f-395">다음 단계는 미리 렌더링 전의 페이지 수명 주기에 있는 지점에서 AddOnPreRenderCompleteAsync 메서드를 호출 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="9444f-396">이 메서드는 일반적으로 페이지\_로드에서 호출 됩니다. AddOnPreRenderCompleteAsync 메서드는 두 개의 매개 변수를 사용 합니다. BeginEventHandler 및 EndEventHandler</span><span class="sxs-lookup"><span data-stu-id="9444f-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="9444f-397">BeginEventHandler는 EndEventHandler에 매개 변수로 전달 되는 IAsyncResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="9444f-398">아래 비디오는 비동기 페이지 요청을 연습 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-398">The video below is a walkthrough of an asynchronous page request.</span></span>

![](the-asp-net-2-0-page-model/_static/image3.png)

[<span data-ttu-id="9444f-399">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="9444f-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> <span data-ttu-id="9444f-400">비동기 페이지는 EndEventHandler가 완료 될 때까지 브라우저로 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="9444f-401">하지만 일부 개발자는 비동기 요청을 비동기 콜백과 유사한 것으로 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="9444f-402">이는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-402">It's important to realize that they are not.</span></span> <span data-ttu-id="9444f-403">비동기 요청의 혜택은 새 요청을 처리 하기 위해 첫 번째 작업자 스레드를 스레드 풀로 반환 하 여 IO 바인딩된 것으로 인해 경합이 감소 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>

## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="9444f-404">ASP.NET 2.0의 스크립트 콜백</span><span class="sxs-lookup"><span data-stu-id="9444f-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="9444f-405">웹 개발자는 항상 콜백과 관련 된 깜박임을 방지 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="9444f-406">ASP.NET 1.x에서 SmartNavigation은 깜박임을 방지 하는 가장 일반적인 방법 이지만 SmartNavigation은 클라이언트에서 구현 하는 복잡성으로 인해 일부 개발자에 게 문제가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="9444f-407">ASP.NET 2.0는 스크립트 콜백에서이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="9444f-408">스크립트 콜백은 XMLHttp를 활용 하 여 JavaScript를 통해 웹 서버에 대 한 요청을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="9444f-409">XMLHttp 요청은 브라우저의 DOM을 통해 조작할 수 있는 XML 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="9444f-410">새 Webresource.axd 처리기가 사용자에 게 XMLHttp 코드를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="9444f-411">ASP.NET 2.0에서 스크립트 콜백을 구성 하기 위해 필요한 몇 가지 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="9444f-412">1 단계: ICallbackEventHandler 인터페이스 구현</span><span class="sxs-lookup"><span data-stu-id="9444f-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="9444f-413">ASP.NET가 스크립트 콜백에 참여 하는 것으로 페이지를 인식할 수 있도록 하려면 ICallbackEventHandler 인터페이스를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="9444f-414">다음과 같이 코드를 만든 파일에서이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="9444f-415">다음과 같이 @ Implements 지시문을 사용 하 여이 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="9444f-416">일반적으로 인라인 ASP.NET 코드를 사용할 때 @ Implements 지시문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="9444f-417">2 단계: GetCallbackEventReference 호출</span><span class="sxs-lookup"><span data-stu-id="9444f-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="9444f-418">앞에서 설명한 것 처럼 XMLHttp 호출은 Webresource.axd 처리기에 캡슐화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="9444f-419">페이지가 렌더링 되 면 ASP.NET는 Webresource.axd에서 제공 하는 클라이언트 스크립트인 WebForm\_DoCallback에 대 한 호출을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="9444f-420">WebForm\_DoCallback 함수는 콜백에 대 한 \_\_doPostBack 함수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="9444f-421">\_\_doPostBack은 페이지에 폼을 프로그래밍 방식으로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="9444f-422">콜백 시나리오에서는 포스트백을 방지 하는 것이 좋습니다. 따라서 \_\_doPostBack이 충분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="9444f-423">\_\_doPostBack은 클라이언트 스크립트 콜백 시나리오에서 페이지에 계속 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="9444f-424">그러나 콜백에는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-424">However, it's not used for the callback.</span></span>

<span data-ttu-id="9444f-425">WebForm\_DoCallback에 대 한 인수는 서버측 함수 GetCallbackEventReference를 통해 제공 됩니다 .이 함수는 일반적으로 페이지\_로드에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="9444f-426">GetCallbackEventReference에 대 한 일반적인 호출은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="9444f-427">이 경우 cm은 ClientScriptManager의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="9444f-428">ClientScriptManager 클래스는이 모듈의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-428">The ClientScriptManager class will be covered later in this module.</span></span>

<span data-ttu-id="9444f-429">GetCallbackEventReference에는 여러 개의 오버 로드 된 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="9444f-430">이 경우 인수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="9444f-431">GetCallbackEventReference가 호출 되는 컨트롤에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="9444f-432">이 경우 페이지 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="9444f-433">클라이언트 쪽 코드에서 서버측 이벤트로 전달 되는 문자열 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="9444f-434">이 경우에는 ddlCompany 라는 드롭다운 값을 전달 하는 Im입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="9444f-435">서버 쪽 콜백 이벤트에서 반환 값 (문자열로)을 수락할 클라이언트 쪽 함수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="9444f-436">이 함수는 서버 쪽 콜백이 성공한 경우에만 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="9444f-437">따라서 견고성을 위해 일반적으로 오류가 발생 한 경우 실행할 클라이언트 쪽 함수의 이름을 지정 하는 추가 문자열 인수를 사용 하는 GetCallbackEventReference의 오버 로드 된 버전을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="9444f-438">서버에 대 한 콜백 전에 시작 된 클라이언트 쪽 함수를 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="9444f-439">이 경우에는 이러한 스크립트가 없으므로 인수가 null입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="9444f-440">콜백을 비동기적으로 수행할지 여부를 지정 하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="9444f-441">클라이언트에서 WebForm\_DoCallback에 대 한 호출은 이러한 인수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="9444f-442">따라서이 페이지가 클라이언트에서 렌더링 되 면 해당 코드는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="9444f-443">클라이언트에서 함수 시그니처는 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="9444f-444">클라이언트 쪽 함수는 5 개의 문자열과 부울을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="9444f-445">추가 문자열 (위 예제의 경우 null)에는 서버 쪽 콜백에서 발생 한 모든 오류를 처리 하는 클라이언트 쪽 함수가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="9444f-446">3 단계: 클라이언트 쪽 컨트롤 이벤트 후크</span><span class="sxs-lookup"><span data-stu-id="9444f-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="9444f-447">위의 GetCallbackEventReference 반환 값이 문자열 변수에 할당 된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="9444f-448">해당 문자열은 콜백을 시작 하는 컨트롤에 대 한 클라이언트 쪽 이벤트를 연결 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="9444f-449">이 예제에서 콜백은 페이지의 드롭다운에서 시작 되므로 *OnChange* 이벤트를 후크 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="9444f-450">클라이언트 쪽 이벤트를 후크 하려면 다음과 같이 클라이언트 쪽 태그에 처리기를 추가 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="9444f-451">*CbRef* 는 GetCallbackEventReference에 대 한 호출의 반환 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="9444f-452">위에 표시 된 WebForm\_DoCallback에 대 한 호출을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="9444f-453">4 단계: 클라이언트 쪽 스크립트 등록</span><span class="sxs-lookup"><span data-stu-id="9444f-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="9444f-454">GetCallbackEventReference에 대 한 호출은 서버 쪽 콜백이 성공할 때 **Showcompanyname** 이라는 클라이언트 쪽 스크립트가 실행 되도록 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="9444f-455">ClientScriptManager 인스턴스를 사용 하 여 페이지에 해당 스크립트를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="9444f-456">ClientScriptManager 클래스는이 모듈의 뒷부분에서 설명 합니다. 이렇게 하려면 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-456">(The ClientScriptManager class will be discussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="9444f-457">5 단계: ICallbackEventHandler 인터페이스의 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="9444f-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="9444f-458">ICallbackEventHandler에는 코드에서 구현 해야 하는 두 개의 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="9444f-459">**RaiseCallbackEvent** 및 **GetCallbackEvent**입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="9444f-460">**RaiseCallbackEvent** 는 문자열을 인수로 사용 하 고 아무 것도 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="9444f-461">WebForm\_DoCallback에 대 한 클라이언트 쪽 호출에서 문자열 인수가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="9444f-462">이 경우 해당 값은 ddlCompany 라는 드롭다운에서 *value* 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="9444f-463">서버 쪽 코드는 RaiseCallbackEvent 메서드에 배치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="9444f-464">예를 들어 콜백에서 외부 리소스에 대해 WebRequest를 만드는 경우 해당 코드를 RaiseCallbackEvent에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="9444f-465">**GetCallbackEvent** 는 클라이언트에 대 한 콜백 반환을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="9444f-466">인수를 사용 하지 않고 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="9444f-467">반환 되는 문자열은 클라이언트 쪽 함수 (이 경우 *Showcompanyname*)에 인수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="9444f-468">위의 단계를 완료 하면 ASP.NET 2.0에서 스크립트 콜백을 수행할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>

![](the-asp-net-2-0-page-model/_static/image4.png)

[<span data-ttu-id="9444f-469">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="9444f-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)

<span data-ttu-id="9444f-470">ASP.NET의 스크립트 콜백은 XMLHttp 호출을 지 원하는 모든 브라우저에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="9444f-471">현재 사용 중인 모든 최신 브라우저를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="9444f-472">Internet Explorer는 XMLHttp ActiveX 개체를 사용 하는 반면, 다른 최신 브라우저 (예정 된 IE 7 포함)는 내장 XMLHttp 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="9444f-473">브라우저에서 콜백을 지원 하는지 프로그래밍 방식으로 확인 하려면. **.Browser 콜백** 속성을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="9444f-474">요청 하는 클라이언트가 스크립트 콜백을 지 원하는 경우이 속성은 **true** 를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="9444f-475">ASP.NET 2.0에서 클라이언트 스크립트 작업</span><span class="sxs-lookup"><span data-stu-id="9444f-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="9444f-476">ASP.NET 2.0의 클라이언트 스크립트는 ClientScriptManager 클래스를 사용 하 여 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="9444f-477">ClientScriptManager 클래스는 형식 및 이름을 사용 하 여 클라이언트 스크립트를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="9444f-478">이렇게 하면 동일한 스크립트가 페이지에 두 번 이상 삽입 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="9444f-479">페이지에 스크립트가 성공적으로 등록 된 후에는 동일한 스크립트를 등록 하려고 하면 스크립트가 두 번 등록 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="9444f-480">중복 스크립트가 추가 되지 않고 예외가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="9444f-481">불필요 한 계산을 방지 하기 위해 두 번 이상 등록 하지 않도록 스크립트를 이미 등록 했는지 여부를 확인 하는 데 사용할 수 있는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>

<span data-ttu-id="9444f-482">ClientScriptManager의 메서드는 모든 현재 ASP.NET 개발자에 게 친숙 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="9444f-483">RegisterClientScriptBlock</span><span class="sxs-lookup"><span data-stu-id="9444f-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="9444f-484">이 메서드는 렌더링 된 페이지의 맨 위에 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="9444f-485">이는 클라이언트에서 명시적으로 호출 되는 함수를 추가 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="9444f-486">이 메서드의 오버 로드 된 두 가지 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="9444f-487">네 가지 인수 중 세 개는 공통 된 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="9444f-488">아래에 이 계정과 키의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-488">They are:</span></span>

`type (string)`

<span data-ttu-id="9444f-489">***형식*** 인수는 스크립트의 형식을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="9444f-490">일반적으로 페이지의 형식 (이 경우)을 사용 하는 것이 좋습니다. 형식에 대 한 GetType ()).</span><span class="sxs-lookup"><span data-stu-id="9444f-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="9444f-491">***키*** 인수는 스크립트의 사용자 정의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="9444f-492">이는 각 스크립트에 대해 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-492">This should be unique for each script.</span></span> <span data-ttu-id="9444f-493">이미 추가 된 스크립트와 동일한 키와 유형을 사용 하 여 스크립트를 추가 하려고 하면 해당 스크립트는 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="9444f-494">***스크립트*** 인수는 추가할 실제 스크립트를 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="9444f-495">StringBuilder를 사용 하 여 스크립트를 만든 다음 StringBuilder에서 ToString () 메서드를 사용 하 여 ***스크립트*** 인수를 할당 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="9444f-496">3 개의 인수만 사용 하는 오버 로드 된 RegisterClientScriptBlock를 사용 하는 경우 스크립트에 스크립트 요소 (&lt;스크립트&gt; 및 &lt;/스크립트&gt;)를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="9444f-497">네 번째 인수를 사용 하는 RegisterClientScriptBlock의 오버 로드를 사용 하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="9444f-498">네 번째 인수는 ASP.NET가 스크립트 요소를 추가 해야 하는지 여부를 지정 하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="9444f-499">이 인수가 **true**이면 스크립트에 스크립트 요소를 명시적으로 포함 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="9444f-500">IsClientScriptBlockRegistered 된 메서드를 사용 하 여 스크립트가 이미 등록 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="9444f-501">이렇게 하면 이미 등록 된 스크립트를 다시 등록 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="9444f-502">RegisterClientScriptInclude (2.0의 새로운 새)</span><span class="sxs-lookup"><span data-stu-id="9444f-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="9444f-503">RegisterClientScriptInclude 태그는 외부 스크립트 파일에 연결 되는 스크립트 블록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="9444f-504">두 개의 오버 로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-504">It has two overloads.</span></span> <span data-ttu-id="9444f-505">하나는 키와 URL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-505">One takes a key and a URL.</span></span> <span data-ttu-id="9444f-506">두 번째는 형식을 지정 하는 세 번째 인수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="9444f-507">예를 들어 다음 코드는 응용 프로그램의 scripts 폴더 루트에 있는 jsfunctions에 연결 되는 스크립트 블록을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="9444f-508">이 코드는 렌더링 된 페이지에 다음 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="9444f-509">스크립트 블록은 페이지 아래쪽에 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-509">The script block is rendered at the bottom of the page.</span></span>

<span data-ttu-id="9444f-510">IsClientScriptIncludeRegistered 메서드를 사용 하 여 스크립트가 이미 등록 되었는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="9444f-511">이렇게 하면 스크립트를 다시 등록 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="9444f-512">RegisterStartupScript</span><span class="sxs-lookup"><span data-stu-id="9444f-512">RegisterStartupScript</span></span>

<span data-ttu-id="9444f-513">RegisterStartupScript 메서드는 RegisterClientScriptBlock 메서드와 동일한 인수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="9444f-514">RegisterStartupScript에 등록 된 스크립트는 페이지가 로드 된 후 OnLoad 클라이언트 쪽 이벤트 이전에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="9444f-515">1\.x에서 RegisterStartupScript로 등록 된 스크립트는 닫는 &lt;양식&gt; 태그 바로 앞에 배치 되었으며, RegisterClientScriptBlock에 등록 된 스크립트는 열기 &lt;양식&gt; 태그 바로 뒤에 배치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="9444f-516">ASP.NET 2.0에서 두 가지 모두 닫는 &lt;양식&gt; 태그 바로 앞에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="9444f-517">RegisterStartupScript를 사용 하 여 함수를 등록 하는 경우 해당 함수는 클라이언트 쪽 코드에서 명시적으로 호출할 때까지 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>

<span data-ttu-id="9444f-518">IsStartupScriptRegistered 메서드를 사용 하 여 스크립트가 이미 등록 되어 있는지 확인 하 고 스크립트를 다시 등록 하려고 시도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="9444f-519">기타 ClientScriptManager 메서드</span><span class="sxs-lookup"><span data-stu-id="9444f-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="9444f-520">ClientScriptManager 클래스의 다른 유용한 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>

|  <span data-ttu-id="9444f-521"><strong>GetCallbackEventReference</strong></span><span class="sxs-lookup"><span data-stu-id="9444f-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="9444f-522">이 모듈의 앞부분에서 콜백 스크립트를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="9444f-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="9444f-523"><strong>GetPostBackClientHyperlink</strong></span><span class="sxs-lookup"><span data-stu-id="9444f-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="9444f-524">클라이언트 쪽 이벤트에서 포스트백 하는 데 사용할 수 있는 JavaScript 참조 (javascript:&lt;호출&gt;)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="9444f-525"><strong>System.web.ui.clientscriptmanager.getpostbackeventreference</strong></span><span class="sxs-lookup"><span data-stu-id="9444f-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="9444f-526">클라이언트에서 다시 게시를 시작 하는 데 사용할 수 있는 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="9444f-527"><strong>GetWebResourceUrl</strong></span><span class="sxs-lookup"><span data-stu-id="9444f-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="9444f-528">어셈블리에 포함 된 리소스에 대 한 URL을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="9444f-529"><strong>RegisterClientScriptResource</strong>와 함께 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="9444f-530"><strong>RegisterClientScriptResource</strong></span><span class="sxs-lookup"><span data-stu-id="9444f-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="9444f-531">페이지에 웹 리소스를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="9444f-532">이러한 리소스는 어셈블리에 포함 되 고 새 Webresource.axd 처리기에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="9444f-533"><strong>RegisterHiddenField</strong></span><span class="sxs-lookup"><span data-stu-id="9444f-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="9444f-534">페이지에 숨겨진 폼 필드를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="9444f-535"><strong>RegisterOnSubmitStatement</strong></span><span class="sxs-lookup"><span data-stu-id="9444f-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="9444f-536">HTML 폼이 제출 될 때 실행 되는 클라이언트 쪽 코드를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9444f-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |
