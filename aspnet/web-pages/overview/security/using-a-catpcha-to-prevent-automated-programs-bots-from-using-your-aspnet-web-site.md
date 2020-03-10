---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: CAPTCHA를 사용 하 여 봇에서 ASP.NET 웹 Razor 사용 방지 Microsoft Docs
author: microsoft
description: 이 문서에서는 ReCaptcha (보안 측정값)를 사용 하 여 자동 프로그램 (봇)이 ASP.NET 웹 페이지 (Razor)에서 작업을 수행 하지 못하도록 방지 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440195"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="9dd27-103">CAPTCHA를 사용 하 여 봇에서 ASP.NET 웹 Razor를 사용 하지 못하도록 방지) 사이트</span><span class="sxs-lookup"><span data-stu-id="9dd27-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="9dd27-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="9dd27-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9dd27-105">이 문서에서는 ReCaptcha (보안 측정값)를 사용 하 여 자동 프로그램 (봇)이 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 작업을 수행 하는 것을 방지 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="9dd27-106">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="9dd27-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="9dd27-107">CAPTCHA 테스트를 사이트에 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9dd27-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="9dd27-108">다음은이 문서에 도입 된 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="9dd27-109">`ReCaptcha` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="9dd27-110">이 문서의 정보는 ASP.NET 웹 페이지 1.0 및 웹 페이지 2에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="9dd27-111">CAPTCHAs 정보</span><span class="sxs-lookup"><span data-stu-id="9dd27-111">About CAPTCHAs</span></span>

<span data-ttu-id="9dd27-112">사용자가 사이트에 등록 하도록 하거나 이름 및 URL (예: 블로그 설명)을 입력 하는 경우에도 가짜 이름이 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="9dd27-113">이러한 기능은 일반적으로 찾을 수 있는 모든 웹 사이트에서 Url을 유지 하는 자동 프로그램 (봇)으로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="9dd27-114">(일반적으로 판매 하는 제품의 Url을 게시 하는 것이 일반적입니다.)</span><span class="sxs-lookup"><span data-stu-id="9dd27-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="9dd27-115">*CAPTCHA* 를 사용 하 여 사용자가 등록 하거나 사용자의 이름과 사이트를 입력 하는 경우 사용자의 유효성을 검사 하 여 사용자가 실제 사용자 인지 확인 하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="9dd27-116">CAPTCHA는 완전히 자동화 된 공용 Turing 테스트를 통해 컴퓨터와 사람을 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="9dd27-117">CAPTCHA는 사용자가 자동화 된 프로그램의 작업을 수행 하는 데 필요한 작업을 수행 하는 데 필요한 작업을 수행 하는 데 필요한 작업을 사용자에 게 요청 하는 *챌린지-응답* 테스트입니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="9dd27-118">가장 일반적인 유형의 CAPTCHA은 일부 왜곡 된 문자를 표시 하 고 입력 하 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="9dd27-119">왜곡은 봇에서 문자를 해독할 수 있도록 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="9dd27-120">ReCaptcha 테스트 추가</span><span class="sxs-lookup"><span data-stu-id="9dd27-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="9dd27-121">ASP.NET 페이지에서 `ReCaptcha` 도우미를 사용 하 여 ReCaptcha 서비스 ([http://recaptcha.net](http://recaptcha.net))를 기반으로 하는 CAPTCHA 테스트를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="9dd27-122">`ReCaptcha` 도우미는 페이지의 유효성을 검사 하기 전에 사용자가 올바르게 입력 해야 하는 두 개의 왜곡 된 단어로 이루어진 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="9dd27-123">ReCaptcha.Net 서비스에서 사용자 응답의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="9dd27-124">ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net))에서 웹 사이트를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="9dd27-125">등록을 완료 하면 공개 키와 개인 키를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="9dd27-126">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="9dd27-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="9dd27-127">*\_AppStart* 파일이 아직 없는 경우 웹 사이트의 루트 폴더에서 *AppStart\_* 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="9dd27-128">다음 `Recaptcha` 도우미 설정을 *\_AppStart* 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="9dd27-129">사용자 고유의 공개 키와 개인 키를 사용 하 여 `PublicKey` 및 `PrivateKey` 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="9dd27-130">*\_AppStart* 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="9dd27-131">웹 사이트의 루트 폴더에서 *Recaptcha*라는 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="9dd27-132">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="9dd27-133">브라우저에서 *Recaptcha* 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="9dd27-134">`PrivateKey` 값이 유효 하면 페이지에 ReCaptcha 컨트롤과 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="9dd27-135">*\_AppStart*에서 전역으로 키를 설정 하지 않은 경우 페이지에 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="9dd27-136">테스트에 사용할 단어를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-136">Enter the words for the test.</span></span> <span data-ttu-id="9dd27-137">ReCaptcha 테스트를 전달 하면 해당 효과에 대 한 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="9dd27-138">그렇지 않으면 오류 메시지가 표시 되 고 ReCaptcha 컨트롤이 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="9dd27-139">컴퓨터가 프록시 서버를 사용 하는 도메인에 있는 경우 *web.config 파일의* `defaultproxy` 요소를 구성 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="9dd27-140">다음 예제에서는 ReCaptcha 서비스가 작동 하도록 구성 된 `defaultproxy` 요소가 *포함 된 web.config 파일을* 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9dd27-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="9dd27-141">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9dd27-141">Additional Resources</span></span>

- [<span data-ttu-id="9dd27-142">ASP.NET 웹 페이지 사이트에 대 한 사이트 전체 동작 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="9dd27-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="9dd27-143">ReCaptcha 사이트</span><span class="sxs-lookup"><span data-stu-id="9dd27-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
