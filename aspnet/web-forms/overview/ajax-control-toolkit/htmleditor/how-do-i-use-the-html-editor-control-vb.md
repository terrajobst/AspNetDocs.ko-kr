---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: HTML 편집기 컨트롤을 사용 어떻게 할까요?? (VB) | Microsoft Docs
author: microsoft
description: HTMLEditor은 도구 모음에서 단추를 통해 HTML 콘텐츠를 쉽게 만들고 편집할 수 있도록 하는 ASP.NET AJAX 컨트롤입니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 20f8a2f8148bc658370ba1a939ebf1b62d376bc0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446285"
---
# <a name="how-do-i-use-the-html-editor-control-vb"></a><span data-ttu-id="561ea-104">HTML 편집기 컨트롤을 사용 어떻게 할까요??</span><span class="sxs-lookup"><span data-stu-id="561ea-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="561ea-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="561ea-105">(VB)</span></span>

<span data-ttu-id="561ea-106">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="561ea-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="561ea-107">HTMLEditor은 도구 모음에서 단추를 통해 HTML 콘텐츠를 쉽게 만들고 편집할 수 있도록 하는 ASP.NET AJAX 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>

<span data-ttu-id="561ea-108">이 자습서의 목표는 AJAX 컨트롤 도구 키트에 포함 된 HTML 편집기 컨트롤의 개요를 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="561ea-109">HTML 편집기에는 글꼴 크기 변경, 글꼴 선택, 배경색 변경, 전경색 수정, 링크 추가, 이미지 추가, 텍스트 맞춤 변경, 잘라내기, 복사 및 붙여넣기 작업 수행에 대 한 옵션이 포함 되어 있습니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="561ea-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>

<span data-ttu-id="561ea-110">[HTML 편집기 ![](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="561ea-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="561ea-111">**그림 01**: HTML 편집기 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="561ea-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image2.png))</span></span>

<span data-ttu-id="561ea-112">HTML 편집기를 사용 하면 디자인 모드를 사용 하 여 콘텐츠를 입력 하거나 HTML을 직접 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="561ea-113">HTML 콘텐츠를 미리 볼 수 있는 옵션도 제공 됩니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="561ea-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>

<span data-ttu-id="561ea-114">[![디자인, HTML 및 미리 보기 단추](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="561ea-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="561ea-115">**그림 02**: 디자인, HTML 및 미리 보기 단추 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="561ea-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image4.png))</span></span>

<span data-ttu-id="561ea-116">이 자습서에서는 html 편집기를 표시 하는 방법, HTML 편집기에 표시 되는 도구 모음 단추를 사용자 지정 하는 방법 및 사이트 간 스크립팅 공격을 방지 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="561ea-117">HTML 편집기 표시</span><span class="sxs-lookup"><span data-stu-id="561ea-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="561ea-118">ASP.NET 페이지에서 HTML 편집기를 사용 하려면 먼저 페이지에 ScriptManager 컨트롤을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="561ea-119">ScriptManager 컨트롤은 Visual Studio/Visual Web Developer Express 도구 상자의 AJAX 확장 탭 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="561ea-120">페이지의 다른 컨트롤 앞에서 ScriptManager 컨트롤을 페이지 맨 위에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="561ea-121">예를 들어 서버 쪽 &lt;양식 열기&gt; 태그 바로 아래에이를 놓을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="561ea-122">HTML 편집기 컨트롤은 나머지 AJAX 컨트롤 도구 키트 컨트롤과 함께 도구 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="561ea-123">편집기 컨트롤의 이름을 지정 합니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="561ea-123">It is named the Editor control (see Figure 3).</span></span>

<span data-ttu-id="561ea-124">[HTML 편집기 컨트롤 ![](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="561ea-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="561ea-125">**그림 03**: HTML 편집기 컨트롤 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="561ea-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image6.png))</span></span>

<span data-ttu-id="561ea-126">HTML 편집기를 페이지로 끌어온 후에는 속성 시트에서 해당 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="561ea-127">예를 들어 일반적으로 Width 및 Height 속성을 설정 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="561ea-128">목록 1은 HTML 편집기를 포함 하는 ASP.NET 페이지의 소스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="561ea-129">**목록 1-SimpleEditor .aspx**</span><span class="sxs-lookup"><span data-stu-id="561ea-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

<span data-ttu-id="561ea-130">목록 1의 페이지에는 HTML 편집기 컨트롤, 단추 컨트롤 및 리터럴 컨트롤이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="561ea-131">단추를 클릭 하면 HTML 편집기의 내용이 리터럴 컨트롤에 표시 됩니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="561ea-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>

<span data-ttu-id="561ea-132">[HTML 편집기를 사용 하 여 폼을 전송 ![](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="561ea-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="561ea-133">**그림 04**: HTML 편집기를 사용 하 여 폼 제출 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="561ea-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image8.png))</span></span>

<span data-ttu-id="561ea-134">Html 편집기 콘텐츠 속성은 html 편집기에 입력 된 HTML 콘텐츠를 검색 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="561ea-135">이 HTML 콘텐츠에서 JavaScript를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="561ea-136">다음 섹션에서는 JavaScript 삽입 공격을 방지 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="561ea-137">HTML 편집기 도구 모음 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="561ea-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="561ea-138">편집기에 표시 되는 단추를 정확 하 게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="561ea-139">예를 들어 html 탭을 제거 하 여 사용자가 HTML 편집기를 HTML 모드로 전환 하지 못하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="561ea-140">또는 사용자가 포럼 메시지 게시에서 너무 큰 텍스트를 만들지 못하도록 글꼴 크기 드롭다운 목록을 제거할 수 있습니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="561ea-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>

<span data-ttu-id="561ea-141">[사용자 지정 된 HTML 편집기 ![](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="561ea-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="561ea-142">**그림 05**: 사용자 지정 된 HTML 편집기 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-html-editor-control-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="561ea-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image10.png))</span></span>

<span data-ttu-id="561ea-143">기본 편집기 클래스에서 새 HTML 편집기를 파생 시켜 도구 모음 단추를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="561ea-144">예를 들어 목록 2의 사용자 지정 편집기에는 굵게 및 기울임꼴의 도구 모음 단추만 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="561ea-145">다른 모든 도구 모음 단추는 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="561ea-146">또한 HTML 탭은 편집기의 맨 아래에서 제거 되었지만 디자인 및 미리 보기 탭도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="561ea-147">**목록 2-앱\_Code\CustomEditor.vb**</span><span class="sxs-lookup"><span data-stu-id="561ea-147">**Listing 2 - App\_Code\CustomEditor.vb**</span></span>

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

<span data-ttu-id="561ea-148">클래스가 자동으로 컴파일되도록 앱\_코드 폴더에 목록 2의 클래스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="561ea-149">앱\_코드 폴더가 웹 사이트에 없으면 폴더를 추가 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="561ea-150">사용자 지정 편집기를 만든 후에는 일반 HTML 편집기를 추가할 때와 같은 방법으로 ASP.NET 페이지에 추가할 수 있습니다 (목록 3 참조).</span><span class="sxs-lookup"><span data-stu-id="561ea-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="561ea-151">**목록 3-ShowCustomEditor**</span><span class="sxs-lookup"><span data-stu-id="561ea-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="561ea-152">XSS (교차 사이트 스크립팅) 공격 방지</span><span class="sxs-lookup"><span data-stu-id="561ea-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="561ea-153">사용자의 입력을 허용 하 고 웹 사이트에서 해당 입력을 다시 표시할 때마다 사이트 간 스크립팅 (XSS) 공격에 대해 웹 사이트를 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="561ea-154">이론적으로 악의적인 해커가 입력이 다시 표시 될 때 실행 되는 JavaScript 코드를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="561ea-155">JavaScript는 사용자 암호 또는 기타 중요 한 정보를 도용 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="561ea-156">일반적으로 웹 페이지에 표시 하기 전에 사용자가 검색 한 모든 입력을 HTML 인코딩으로 인코딩하여 XSS 공격을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="561ea-157">그러나 html 편집기의 출력을 HTML로 인코딩하면 &lt;스크립트&gt; 태그로 인코딩될 뿐만 아니라 모든 HTML 태그도 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="561ea-158">즉, 글꼴 유형, 글꼴 크기, 배경색 등의 모든 서식이 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="561ea-159">암호, 신용 카드 번호 및 주민 등록 번호와 같은 사용자의 중요 한 정보를 수집 하는 경우에는 HTML 편집기를 사용 하 여 사용자가 검색 한 인코딩된 콘텐츠를 표시 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="561ea-160">Html 콘텐츠를 표시 하지 않는 경우에만 html 편집기를 사용 해야 합니다. 그렇지 않으면 신뢰할 수 있는 당사자가 HTML 콘텐츠를 웹 사이트로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="561ea-161">예를 들어 블로그 응용 프로그램을 만드는 중 이라고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="561ea-162">이 경우 블로그 게시물을 작성할 때 HTML 편집기를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="561ea-163">블로그 게시물을 제출 하는 유일한 사용자 이며 악의적인 JavaScript를 전송 하지 않고 직접 신뢰 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="561ea-164">그러나 익명 사용자가 주석을 게시할 수 있도록 허용 하는 경우 HTML 편집기를 사용 하는 것은 의미가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="561ea-165">사용자가 암호와 같은 중요 한 정보를 제출 하는 상황에서는 특히 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="561ea-166">악의적인 사용자가 암호를 가로채기 위한 올바른 JavaScript를 포함 하는 주석을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="561ea-167">요약</span><span class="sxs-lookup"><span data-stu-id="561ea-167">Summary</span></span>

<span data-ttu-id="561ea-168">이 자습서에서는 AJAX 컨트롤 도구 키트에 포함 된 HTML 편집기 컨트롤에 대 한 간략 한 개요를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="561ea-169">HTML 편집기를 사용 하 여 사용자의 풍부한 콘텐츠를 수락 하 고 해당 콘텐츠를 서버에 제출 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="561ea-170">HTML 편집기에 표시 되는 도구 모음 단추를 사용자 지정 하는 방법에 대해서도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="561ea-171">마지막으로, HTML 편집기를 사용 하 여 잠재적으로 악의적인 입력을 허용할 때 교차 사이트 스크립팅 공격을 방지 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="561ea-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="561ea-172">이전</span><span class="sxs-lookup"><span data-stu-id="561ea-172">Previous</span></span>](how-do-i-use-the-html-editor-control-cs.md)
