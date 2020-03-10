---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 열린 리디렉션 공격 방지 (C#) | Microsoft Docs
author: jongalloway
description: 이 자습서에서는 ASP.NET MVC 응용 프로그램에서 open 리디렉션 공격을 방지 하는 방법을 설명 합니다. 이 자습서에서는 적용 된 변경 내용을 설명 합니다.
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: cfa635d4fd14d031993c5b452325cbe334f82dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432587"
---
# <a name="preventing-open-redirection-attacks-c"></a><span data-ttu-id="6ddda-104">오픈 리디렉션 공격 방지(C#)</span><span class="sxs-lookup"><span data-stu-id="6ddda-104">Preventing Open Redirection Attacks (C#)</span></span>

<span data-ttu-id="6ddda-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="6ddda-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="6ddda-106">이 자습서에서는 ASP.NET MVC 응용 프로그램에서 open 리디렉션 공격을 방지 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-106">This tutorial explains how you can prevent open redirection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="6ddda-107">이 자습서에서는 ASP.NET MVC 3에서 AccountController에 적용 된 변경 내용에 대해 설명 하 고 기존 ASP.NET MVC 1.0 및 2 응용 프로그램에서 이러한 변경 사항을 적용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-107">This tutorial discusses the changes that have been made in the AccountController in ASP.NET MVC 3 and demonstrates how you can apply these changes in your existing ASP.NET MVC 1.0 and 2 applications.</span></span>

## <a name="what-is-an-open-redirection-attack"></a><span data-ttu-id="6ddda-108">개방형 리디렉션 공격 이란?</span><span class="sxs-lookup"><span data-stu-id="6ddda-108">What is an Open Redirection Attack?</span></span>

<span data-ttu-id="6ddda-109">Querystring 또는 양식 데이터와 같은 요청을 통해 지정 된 URL로 리디렉션하는 모든 웹 응용 프로그램은 사용자를 안전 하 고 악의적인 URL로 리디렉션하는 변조 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-109">Any web application that redirects to a URL that is specified via the request such as the querystring or form data can potentially be tampered with to redirect users to an external, malicious URL.</span></span> <span data-ttu-id="6ddda-110">이러한 변조를 개방 리디렉션 공격 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-110">This tampering is called an open redirection attack.</span></span>

<span data-ttu-id="6ddda-111">응용 프로그램 논리가 지정 된 URL로 리디렉션되는 경우 항상 리디렉션 URL이 변조 되지 않았는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-111">Whenever your application logic redirects to a specified URL, you must verify that the redirection URL hasn't been tampered with.</span></span> <span data-ttu-id="6ddda-112">ASP.NET MVC 1.0 및 ASP.NET MVC 2에 대 한 기본 AccountController에서 사용 되는 로그인은 오픈 리디렉션 공격에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-112">The login used in the default AccountController for both ASP.NET MVC 1.0 and ASP.NET MVC 2 is vulnerable to open redirection attacks.</span></span> <span data-ttu-id="6ddda-113">다행히 기존 응용 프로그램을 업데이트 하 여 ASP.NET MVC 3 Preview의 수정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-113">Fortunately, it is easy to update your existing applications to use the corrections from the ASP.NET MVC 3 Preview.</span></span>

<span data-ttu-id="6ddda-114">취약성을 이해 하려면 기본 ASP.NET MVC 2 웹 응용 프로그램 프로젝트에서 로그인 리디렉션이 작동 하는 방식을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-114">To understand the vulnerability, let's look at how the login redirection works in a default ASP.NET MVC 2 Web Application project.</span></span> <span data-ttu-id="6ddda-115">이 응용 프로그램에서 [권한 부여] 특성이 있는 컨트롤러 작업을 방문 하려고 하면 권한이 없는 사용자가/svrvview 보기로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-115">In this application, attempting to visit a controller action that has the [Authorize] attribute will redirect unauthorized users to the /Account/LogOn view.</span></span> <span data-ttu-id="6ddda-116">ReturnUrl에 대 한이 리디렉션에는 사용자가 성공적으로 로그인 한 후 원래 요청 된 URL로 반환 될 수 있도록 querystring 매개 변수가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-116">This redirect to /Account/LogOn will include a returnUrl querystring parameter so that the user can be returned to the originally requested URL after they have successfully logged in.</span></span>

<span data-ttu-id="6ddda-117">아래 스크린샷에서는 로그인 하지 않을 때/Cv/ps 뷰에 대 한 액세스 시도가 실패 하는 것을 볼 수 있습니다. ReturnUrl =% 2fAccount% 2fChangePassword% 2f.</span><span class="sxs-lookup"><span data-stu-id="6ddda-117">In the screenshot below, we can see that an attempt to access the /Account/ChangePassword view when not logged in results in a redirect to /Account/LogOn?ReturnUrl=%2fAccount%2fChangePassword%2f.</span></span>

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

<span data-ttu-id="6ddda-118">**그림 01**: 열린 리디렉션이 있는 로그인 페이지</span><span class="sxs-lookup"><span data-stu-id="6ddda-118">**Figure 01**: Login page with an open redirection</span></span>

<span data-ttu-id="6ddda-119">ReturnUrl querystring 매개 변수의 유효성이 검사 되지 않으므로 공격자는 URL 주소를 매개 변수에 삽입 하도록 수정 하 여 열린 리디렉션 공격을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-119">Since the ReturnUrl querystring parameter is not validated, an attacker can modify it to inject any URL address into the parameter to conduct an open redirection attack.</span></span> <span data-ttu-id="6ddda-120">이를 보여 주기 위해 ReturnUrl 매개 변수를 [http://bing.com](http://bing.com)로 수정 하 여 결과 로그인 URL은/Account/LogOn 입니까? ReturnUrl =<http://www.bing.com/>.</span><span class="sxs-lookup"><span data-stu-id="6ddda-120">To demonstrate this, we can modify the ReturnUrl parameter to [http://bing.com](http://bing.com), so the resulting login URL will be /Account/LogOn?ReturnUrl=<http://www.bing.com/>.</span></span> <span data-ttu-id="6ddda-121">사이트에 성공적으로 로그인 하면 [http://bing.com](http://bing.com)으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-121">Upon successfully logging in to the site, we are redirected to [http://bing.com](http://bing.com).</span></span> <span data-ttu-id="6ddda-122">이 리디렉션의 유효성은 검사 되지 않으므로 사용자를 속이는 악의적인 사이트를 가리키도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-122">Since this redirection is not validated, it could instead point to a malicious site that attempts to trick the user.</span></span>

### <a name="a-more-complex-open-redirection-attack"></a><span data-ttu-id="6ddda-123">더 복잡 한 개방형 리디렉션 공격</span><span class="sxs-lookup"><span data-stu-id="6ddda-123">A more complex Open Redirection Attack</span></span>

<span data-ttu-id="6ddda-124">공격자는 특정 웹 사이트에 로그인을 시도 하 고 있으며이로 인해 [피싱 공격](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)에 취약 하다는 것을 알고 있기 때문에 열린 리디렉션 공격은 특히 위험 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-124">Open redirection attacks are especially dangerous because an attacker knows that we're trying to log into a specific website, which makes us vulnerable to a [phishing attack](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span></span> <span data-ttu-id="6ddda-125">예를 들어 공격자는 암호 캡처를 시도 하 여 악의적인 전자 메일을 웹 사이트 사용자에 게 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-125">For example, an attacker could send malicious emails to website users in an attempt to capture their passwords.</span></span> <span data-ttu-id="6ddda-126">이 작업을 수행 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-126">Let's look at how this would work on the NerdDinner site.</span></span> <span data-ttu-id="6ddda-127">(오픈 리디렉션 공격 으로부터 보호 하도록 라이브 된 Ddddinner 사이트를 업데이트 했습니다.)</span><span class="sxs-lookup"><span data-stu-id="6ddda-127">(Note that the live NerdDinner site has been updated to protect against open redirection attacks.)</span></span>

<span data-ttu-id="6ddda-128">먼저 공격자는 위조 된 페이지로의 리디렉션을 포함 하는 회사 간 Ddinner의 로그인 페이지에 대 한 링크를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-128">First, an attacker sends us a link to the login page on NerdDinner that includes a redirect to their forged page:</span></span>

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

<span data-ttu-id="6ddda-129">반환 URL은 dinner 이라는 단어에서 "n"이 누락 된 nerddiner.com를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-129">Note that the return URL points to nerddiner.com, which is missing an "n" from the word dinner.</span></span> <span data-ttu-id="6ddda-130">이 예제에서는 공격자가 제어 하는 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-130">In this example, this is a domain that the attacker controls.</span></span> <span data-ttu-id="6ddda-131">위의 링크에 액세스할 때 합법적인 NerdDinner.com 로그인 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-131">When we access the above link, we're taken to the legitimate NerdDinner.com login page.</span></span>

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

<span data-ttu-id="6ddda-132">**그림 02**: 열린 리디렉션이 있는 동료의 내부 로그인 페이지</span><span class="sxs-lookup"><span data-stu-id="6ddda-132">**Figure 02**: NerdDinner login page with an open redirection</span></span>

<span data-ttu-id="6ddda-133">올바르게 로그인 하면 ASP.NET MVC AccountController의 LogOn 동작이 returnUrl querystring 매개 변수에 지정 된 URL로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-133">When we correctly log in, the ASP.NET MVC AccountController's LogOn action redirects us to the URL specified in the returnUrl querystring parameter.</span></span> <span data-ttu-id="6ddda-134">이 경우 공격자가 입력 한 URL 이며 [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-134">In this case, it's the URL that the attacker has entered, which is [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn).</span></span> <span data-ttu-id="6ddda-135">매우 watchful 않는 한이는 특히 공격자가 위조 된 페이지가 합법적인 로그인 페이지와 정확히 일치 하는지 확인 하는 데 주의를 기울여야 했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-135">Unless we're extremely watchful, it's very likely we won't notice this, especially because the attacker has been careful to make sure that their forged page looks exactly like the legitimate login page.</span></span> <span data-ttu-id="6ddda-136">이 로그인 페이지에는 다시 로그인을 요청 하는 오류 메시지가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-136">This login page includes an error message requesting that we login again.</span></span> <span data-ttu-id="6ddda-137">미국 괴로운 암호를 잘못 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-137">Clumsy us, we must have mistyped our password.</span></span>

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

<span data-ttu-id="6ddda-138">**그림 03**: 위조 되는 내부 로그인 화면</span><span class="sxs-lookup"><span data-stu-id="6ddda-138">**Figure 03**: Forged NerdDinner Login screen</span></span>

<span data-ttu-id="6ddda-139">사용자 이름 및 암호를 다시 입력 하면 위조 된 로그인 페이지가 정보를 저장 하 고 합법적인 NerdDinner.com 사이트로 다시 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-139">When we retype our user name and password, the forged login page saves the information and sends us back to the legitimate NerdDinner.com site.</span></span> <span data-ttu-id="6ddda-140">이 시점에서 NerdDinner.com 사이트는 이미 인증 되었으므로 위조 된 로그인 페이지가 해당 페이지로 직접 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-140">At this point, the NerdDinner.com site has already authenticated us, so the forged login page can redirect directly to that page.</span></span> <span data-ttu-id="6ddda-141">최종 결과는 공격자에 게 사용자 이름과 암호가 있으며 사용자에 게 제공 된 것을 인식 하지 못하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-141">The end result is that the attacker has our user name and password, and we are unaware that we've provided it to them.</span></span>

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a><span data-ttu-id="6ddda-142">AccountController 로그온 작업에서 취약 한 코드 확인</span><span class="sxs-lookup"><span data-stu-id="6ddda-142">Looking at the vulnerable code in the AccountController LogOn Action</span></span>

<span data-ttu-id="6ddda-143">ASP.NET MVC 2 응용 프로그램의 LogOn 동작에 대 한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-143">The code for the LogOn action in an ASP.NET MVC 2 application is shown below.</span></span> <span data-ttu-id="6ddda-144">성공적으로 로그인 되 면 컨트롤러는 returnUrl에 대 한 리디렉션을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-144">Note that upon a successful login, the controller returns a redirect to the returnUrl.</span></span> <span data-ttu-id="6ddda-145">ReturnUrl 매개 변수에 대해 유효성 검사가 수행 되지 않는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-145">You can see that no validation is being performed against the returnUrl parameter.</span></span>

<span data-ttu-id="6ddda-146">**목록 1 – ASP.NET MVC 2 로그온 작업 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="6ddda-146">**Listing 1 – ASP.NET MVC 2 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

<span data-ttu-id="6ddda-147">이제 ASP.NET MVC 3 로그온 동작에 대 한 변경 내용을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-147">Now let's look at the changes to the ASP.NET MVC 3 LogOn action.</span></span> <span data-ttu-id="6ddda-148">이 코드는 `IsLocalUrl()`이라는 returnUrl 도우미 클래스에서 새 메서드를 호출 하 여 매개 변수의 유효성을 검사 하도록 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-148">This code has been changed to validate the returnUrl parameter by calling a new method in the System.Web.Mvc.Url helper class named `IsLocalUrl()`.</span></span>

<span data-ttu-id="6ddda-149">**목록 2 – ASP.NET MVC 3 LogOn 작업 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="6ddda-149">**Listing 2 – ASP.NET MVC 3 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

<span data-ttu-id="6ddda-150">이는 system.string 도우미 클래스에서 새 메서드를 호출 하 여 반환 URL 매개 변수의 유효성을 검사 하도록 변경 되었습니다 `IsLocalUrl()`.</span><span class="sxs-lookup"><span data-stu-id="6ddda-150">This has been changed to validate the return URL parameter by calling a new method in the System.Web.Mvc.Url helper class, `IsLocalUrl()`.</span></span>

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a><span data-ttu-id="6ddda-151">ASP.NET MVC 1.0 및 MVC 2 응용 프로그램 보호</span><span class="sxs-lookup"><span data-stu-id="6ddda-151">Protecting Your ASP.NET MVC 1.0 and MVC 2 Applications</span></span>

<span data-ttu-id="6ddda-152">IsLocalUrl () 도우미 메서드를 추가 하 고 returnUrl 매개 변수의 유효성을 검사 하기 위해 LogOn 작업을 업데이트 하 여 기존 ASP.NET MVC 1.0 및 2 응용 프로그램의 ASP.NET MVC 3 변경 내용을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-152">We can take advantage of the ASP.NET MVC 3 changes in our existing ASP.NET MVC 1.0 and 2 applications by adding the IsLocalUrl() helper method and updating the LogOn action to validate the returnUrl parameter.</span></span>

<span data-ttu-id="6ddda-153">UrlHelper IsLocalUrl () 메서드는 실제로 System.web. 웹 페이지에서 메서드를 호출 하는 것입니다 .이 유효성 검사는 ASP.NET 웹 페이지 응용 프로그램 에서도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-153">The UrlHelper IsLocalUrl() method actually just calling into a method in System.Web.WebPages, as this validation is also used by ASP.NET Web Pages applications.</span></span>

<span data-ttu-id="6ddda-154">**목록 3 – ASP.NET MVC 3 UrlHelper의 IsLocalUrl () 메서드 `class`**</span><span class="sxs-lookup"><span data-stu-id="6ddda-154">**Listing 3 – The IsLocalUrl() method from the ASP.NET MVC 3 UrlHelper `class`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

<span data-ttu-id="6ddda-155">IsUrlLocalToHost 메서드는 4 목록에 표시 된 것 처럼 실제 유효성 검사 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-155">The IsUrlLocalToHost method contains the actual validation logic, as shown in Listing 4.</span></span>

<span data-ttu-id="6ddda-156">**목록 4 – IsUrlLocalToHost () 메서드를 System.web. 웹 페이지 RequestExtensions 클래스에서**</span><span class="sxs-lookup"><span data-stu-id="6ddda-156">**Listing 4 – IsUrlLocalToHost() method from the System.Web.WebPages RequestExtensions class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

<span data-ttu-id="6ddda-157">ASP.NET MVC 1.0 또는 2 응용 프로그램에서는 IsLocalUrl () 메서드를 AccountController에 추가 하지만 가능한 경우 별도의 도우미 클래스에 추가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-157">In our ASP.NET MVC 1.0 or 2 application, we'll add a IsLocalUrl() method to the AccountController, but you're encouraged to add it to a separate helper class if possible.</span></span> <span data-ttu-id="6ddda-158">ASP.NET MVC 3 버전의 IsLocalUrl ()을 두 번 변경 하 여 AccountController 내에서 작동 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-158">We will make two small changes to the ASP.NET MVC 3 version of IsLocalUrl() so that it will work inside the AccountController.</span></span> <span data-ttu-id="6ddda-159">먼저 컨트롤러의 공용 메서드를 컨트롤러 작업으로 액세스할 수 있기 때문에 공용 메서드에서 private 메서드로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-159">First, we'll change it from a public method to a private method, since public methods in controllers can be accessed as controller actions.</span></span> <span data-ttu-id="6ddda-160">둘째, 응용 프로그램 호스트에 대해 URL 호스트를 확인 하는 호출을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-160">Second, we'll modify the call that checks the URL host against the application host.</span></span> <span data-ttu-id="6ddda-161">이 호출은 UrlHelper 클래스에서 로컬 RequestContext 필드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-161">That call makes use of a local RequestContext field in the UrlHelper class.</span></span> <span data-ttu-id="6ddda-162">대신 사용 합니다. RequestContext. i n. i n. i n. . Url. 호스트.</span><span class="sxs-lookup"><span data-stu-id="6ddda-162">Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host.</span></span> <span data-ttu-id="6ddda-163">다음 코드에서는 ASP.NET MVC 1.0 및 2 응용 프로그램에서 컨트롤러 클래스와 함께 사용 하기 위해 수정 된 IsLocalUrl () 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-163">The following code shows the modified IsLocalUrl() method for use with a controller class in ASP.NET MVC 1.0 and 2 applications.</span></span>

<span data-ttu-id="6ddda-164">**목록 5 – IsLocalUrl () 메서드 (MVC 컨트롤러 클래스에서 사용 하도록 수정 됨)**</span><span class="sxs-lookup"><span data-stu-id="6ddda-164">**Listing 5 – IsLocalUrl() method, which is modified for use with an MVC Controller class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

<span data-ttu-id="6ddda-165">이제 IsLocalUrl () 메서드가 준비 되었으므로 다음 코드와 같이 LogOn 작업에서 호출 하 여 returnUrl 매개 변수의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-165">Now that the IsLocalUrl() method is in place, we can call it from our LogOn action to validate the returnUrl parameter, as shown in the following code.</span></span>

<span data-ttu-id="6ddda-166">**목록 6 – returnUrl 매개 변수의 유효성을 검사 하는 업데이트 된 로그온 방법**</span><span class="sxs-lookup"><span data-stu-id="6ddda-166">**Listing 6 – Updated LogOn method which validates the returnUrl parameter**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

<span data-ttu-id="6ddda-167">이제 외부 반환 URL을 사용 하 여 로그인을 시도 하 여 열린 리디렉션 공격을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-167">Now we can test an open redirection attack by attempting to log in using an external return URL.</span></span> <span data-ttu-id="6ddda-168">/Ss/LogOn을 사용 하겠습니다. ReturnUrl =<http://www.bing.com/>.</span><span class="sxs-lookup"><span data-stu-id="6ddda-168">Let's use /Account/LogOn?ReturnUrl=<http://www.bing.com/> again.</span></span>

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

<span data-ttu-id="6ddda-169">**그림 04**: 업데이트 된 로그온 작업 테스트</span><span class="sxs-lookup"><span data-stu-id="6ddda-169">**Figure 04**: Testing the updated LogOn Action</span></span>

<span data-ttu-id="6ddda-170">성공적으로 로그인 한 후에는 외부 URL이 아닌 Home/Index 컨트롤러 작업으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-170">After successfully logging in, we are redirected to the Home/Index Controller action rather than the external URL.</span></span>

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

<span data-ttu-id="6ddda-171">**그림 05**: 오픈 리디렉션 공격 패배</span><span class="sxs-lookup"><span data-stu-id="6ddda-171">**Figure 05**: Open Redirection attack defeated</span></span>

## <a name="summary"></a><span data-ttu-id="6ddda-172">요약</span><span class="sxs-lookup"><span data-stu-id="6ddda-172">Summary</span></span>

<span data-ttu-id="6ddda-173">리디렉션 Url이 응용 프로그램에 대 한 URL에 매개 변수로 전달 되는 경우에는 열기 리디렉션 공격이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-173">Open redirection attacks can occur when redirection URLs are passed as parameters in the URL for an application.</span></span> <span data-ttu-id="6ddda-174">ASP.NET MVC 3 템플릿에는 개방형 리디렉션 공격 으로부터 보호 하는 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-174">The ASP.NET MVC 3 template includes code to protect against open redirection attacks.</span></span> <span data-ttu-id="6ddda-175">ASP.NET MVC 1.0 및 2 응용 프로그램을 수정 하 여이 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-175">You can add this code with some modification to ASP.NET MVC 1.0 and 2 applications.</span></span> <span data-ttu-id="6ddda-176">ASP.NET 1.0 및 2 개 응용 프로그램에 로그인 할 때 개방 리디렉션 공격 으로부터 보호 하려면 IsLocalUrl () 메서드를 추가 하 고 LogOn 작업에서 returnUrl 매개 변수의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ddda-176">To protect against open redirection attacks when logging into ASP.NET 1.0 and 2 applications, add a IsLocalUrl() method and validate the returnUrl parameter in the LogOn action.</span></span>
