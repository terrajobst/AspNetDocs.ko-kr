---
uid: whitepapers/request-validation
title: 요청 유효성 검사-스크립트 공격 방지 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 기본적으로 응용 프로그램에서 인코딩되지 않은 HTML 콘텐츠 submitt ...를 처리 하지 못하도록 ASP.NET의 요청 유효성 검사 기능에 대해 설명 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520583"
---
# <a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="2ae59-103">요청 유효성 검사 - 스크립트 공격 방지</span><span class="sxs-lookup"><span data-stu-id="2ae59-103">Request Validation - Preventing Script Attacks</span></span>

> <span data-ttu-id="2ae59-104">이 문서에서는 기본적으로 응용 프로그램에서 서버에 전송 된 인코딩되지 않은 HTML 콘텐츠를 처리 하지 못하도록 하는 ASP.NET의 요청 유효성 검사 기능에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="2ae59-105">HTML 데이터를 안전 하 게 처리 하도록 응용 프로그램을 디자인 하는 경우이 요청 유효성 검사 기능을 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="2ae59-106">ASP.NET 1.1 및 ASP.NET 2.0에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>

<span data-ttu-id="2ae59-107">버전 1.1부터 ASP.NET 기능 중 하나인 요청 유효성 검사는 서버에서 인코딩되지 않은 HTML을 포함한 콘텐츠를 허용하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="2ae59-108">이 기능은 클라이언트 스크립트 코드 또는 HTML을 무의식적으로 서버에 제출하고 저장한 다음 다른 사용자에게 제공할 수 있는 스크립트 삽입 공격을 방지하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="2ae59-109">모든 입력 데이터의 유효성을 검사하고 적절한 경우 HTML로 인코딩하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="2ae59-110">예를 들어 사용자의 전자 메일 주소를 요청 하 고 해당 전자 메일 주소를 데이터베이스에 저장 하는 웹 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="2ae59-111">사용자가 유효한 전자 메일 주소 대신 &lt;스크립트&gt;경고 ("hello from SCRIPT")&lt;/스크립트&gt;를 입력 하는 경우 해당 데이터가 표시 되 면 콘텐츠가 제대로 인코딩되지 않은 경우이 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="2ae59-112">ASP.NET의 요청 유효성 검사 기능으로 인해이 문제가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="2ae59-113">이 기능이 유용한 이유</span><span class="sxs-lookup"><span data-stu-id="2ae59-113">Why this feature is useful</span></span>

<span data-ttu-id="2ae59-114">많은 사이트에서 간단한 스크립트 삽입 공격에 대해 공개 된 것을 인식 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="2ae59-115">이러한 공격의 목적이 HTML을 표시 하 여 사이트를 사용 하거나 잠재적으로 클라이언트 스크립트를 실행 하 여 사용자를 해커 사이트로 리디렉션하는 것이 든, 스크립트 삽입 공격은 웹 개발자가 경쟁 해야 하는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="2ae59-116">스크립트 삽입 공격은 ASP.NET, ASP 또는 기타 웹 개발 기술을 사용 하는지에 관계 없이 모든 웹 개발자에 게 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="2ae59-117">ASP.NET 요청 유효성 검사 기능은 개발자가 해당 콘텐츠를 허용 하도록 결정 하지 않는 한 서버에서 인코딩되지 않은 HTML 콘텐츠를 처리할 수 없도록 하 여 이러한 공격을 사전에 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="2ae59-118">예상치 못한 항목: 오류 페이지</span><span class="sxs-lookup"><span data-stu-id="2ae59-118">What to expect: Error Page</span></span>

<span data-ttu-id="2ae59-119">아래 스크린샷은 몇 가지 샘플 ASP.NET 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="2ae59-120">이 코드를 실행 하면 텍스트 상자에 일부 텍스트를 입력할 수 있는 간단한 페이지가 표시 되며 단추를 클릭 하 고 레이블 컨트롤에 텍스트를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="2ae59-121">그러나 입력 및 제출할 `<script>alert("hello!")</script>`와 같은 JavaScript는 예외를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="2ae59-122">오류 메시지는 ' 잠재적으로 위험한 요청. 양식 값이 검색 되었습니다. ' 라는 메시지를 나타내고, 설명에 정확히 발생 한 작업과 동작을 변경 하는 방법에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="2ae59-123">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-123">For example:</span></span>

<span data-ttu-id="2ae59-124">요청 유효성 검사에서 잠재적으로 위험한 클라이언트 입력 값을 감지 하 여 요청 처리가 중단 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="2ae59-125">이 값은 사이트 간 스크립팅 공격과 같은 응용 프로그램의 보안을 손상 시키려는 시도를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="2ae59-126">페이지 지시문 또는 구성 섹션에서 `validateRequest=false`을 설정 하 여 요청 유효성 검사를 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="2ae59-127">그러나이 경우 응용 프로그램에서 모든 입력을 명시적으로 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="2ae59-128">페이지에서 요청 유효성 검사를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="2ae59-128">Disabling request validation on a page</span></span>

<span data-ttu-id="2ae59-129">페이지에서 요청 유효성 검사를 사용 하지 않도록 설정 하려면 Page 지시어의 `validateRequest` 특성을 `false`으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="2ae59-130">요청 유효성 검사를 사용 하지 않도록 설정 하면 콘텐츠를 페이지에 제출할 수 있습니다. 콘텐츠를 제대로 인코드 또는 처리 하는지 확인 하는 것은 페이지 개발자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="2ae59-131">응용 프로그램에 대 한 요청 유효성 검사 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="2ae59-131">Disabling request validation for your application</span></span>

<span data-ttu-id="2ae59-132">응용 프로그램에 대 한 요청 유효성 검사를 사용 하지 않도록 설정 하려면 응용 프로그램에 대 한 web.config 파일을 수정 하거나 만들고 `<pages />` 섹션의 validateRequest 특성을 `false`으로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="2ae59-133">서버에 있는 모든 응용 프로그램에 대 한 요청 유효성 검사를 사용 하지 않도록 설정 하려면 Machine.config 파일을 수정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="2ae59-134">요청 유효성 검사를 사용 하지 않도록 설정 하면 응용 프로그램에 콘텐츠를 제출할 수 있습니다. 응용 프로그램 개발자는 콘텐츠를 제대로 인코드 또는 처리 하는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="2ae59-135">아래 코드를 수정 하 여 요청 유효성 검사를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="2ae59-136">이제 다음 JavaScript가 텍스트 상자에 입력 되 면 결과가 `<script>alert("hello!")</script>` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="2ae59-137">이 문제가 발생 하지 않도록 하려면 요청 유효성 검사가 꺼져 있으면 콘텐츠를 HTML로 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="2ae59-138">콘텐츠를 HTML 인코딩하는 방법</span><span class="sxs-lookup"><span data-stu-id="2ae59-138">How to HTML encode content</span></span>

<span data-ttu-id="2ae59-139">요청 유효성 검사를 사용 하지 않도록 설정한 경우 나중에 사용 하기 위해 저장 되는 콘텐츠를 HTML로 인코딩하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="2ae59-140">HTML 인코딩은 '&lt;' 또는 '&gt;' (다른 여러 기호와 함께)를 해당 하는 HTML 인코딩된 표현으로 자동으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="2ae59-141">예를 들어 '&lt;'는 '&amp;l t; '로 바뀌고 '&gt;'는 '&amp;gt; '로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="2ae59-142">브라우저는 이러한 특수 코드를 사용 하 여 브라우저에서 '&lt;' 또는 '&gt;'를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="2ae59-143">`Server.HtmlEncode(string)` API를 사용 하 여 서버에서 콘텐츠를 쉽게 HTML로 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="2ae59-144">콘텐츠를 쉽게 HTML 디코딩할 수 있습니다. 즉, `Server.HtmlDecode(string)` 메서드를 사용 하 여 표준 HTML로 되돌릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ae59-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="2ae59-145">결과:</span><span class="sxs-lookup"><span data-stu-id="2ae59-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)
