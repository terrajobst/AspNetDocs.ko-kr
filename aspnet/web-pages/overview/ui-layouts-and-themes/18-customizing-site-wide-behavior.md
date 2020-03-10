---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: ASP.NET 웹 페이지 (Razor) 사이트에 대 한 사이트 전체 동작 사용자 지정 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 페이지가 아니라 전체 웹 사이트 또는 전체 폴더에 대 한 설정을 만드는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: f05e05f725d9209bce283ce18659ae5efe4de2ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515249"
---
# <a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a><span data-ttu-id="63749-103">ASP.NET 웹 페이지 (Razor) 사이트에 대 한 사이트 전체 동작 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="63749-103">Customizing Site-Wide Behavior for ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="63749-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="63749-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="63749-105">이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트의 페이지에 대 한 사이트 쪽 설정을 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-105">This article explains how to make site-side settings for pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="63749-106">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="63749-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="63749-107">사이트의 모든 페이지에 대해 값 (전역 값 또는 도우미 설정)을 설정 하는 데 사용할 수 있는 코드를 실행 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="63749-107">How to run code that lets you set values (global values or helper settings) for all pages in a site.</span></span>
> - <span data-ttu-id="63749-108">폴더의 모든 페이지에 대 한 값을 설정 하는 데 사용할 수 있는 코드를 실행 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="63749-108">How to run code that lets you set values for all pages in a folder.</span></span>
> - <span data-ttu-id="63749-109">페이지 로드 전후에 코드를 실행 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="63749-109">How to run code before and after a page loads.</span></span>
> - <span data-ttu-id="63749-110">오류를 중앙 오류 페이지로 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="63749-110">How to send errors to a central error page.</span></span>
> - <span data-ttu-id="63749-111">폴더의 모든 페이지에 인증을 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="63749-111">How to add authentication to all pages in a folder.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="63749-112">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="63749-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="63749-113">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="63749-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="63749-114">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="63749-114">WebMatrix 3</span></span>
> - <span data-ttu-id="63749-115">ASP.NET 웹 도우미 라이브러리 (NuGet 패키지)</span><span class="sxs-lookup"><span data-stu-id="63749-115">ASP.NET Web Helpers Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="63749-116">ASP.NET 웹 도우미 라이브러리를 사용할 수 없다는 점을 제외 하 고이 자습서는 ASP.NET 웹 페이지 3 및 Visual Studio 2013 (또는 웹 Visual Studio Express 2013) 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-116">This tutorial also works with ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web), except you cannot use the ASP.NET Web Helpers Library.</span></span>

<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a><span data-ttu-id="63749-117">ASP.NET 웹 페이지에 대 한 웹 사이트 시작 코드 추가</span><span class="sxs-lookup"><span data-stu-id="63749-117">Adding Website Startup Code for ASP.NET Web Pages</span></span>

<span data-ttu-id="63749-118">ASP.NET 웹 페이지에서 작성 하는 코드의 대부분이 개별 페이지에 해당 페이지에 필요한 모든 코드가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-118">For much of the code that you write in ASP.NET Web Pages, an individual page can contain all the code that's required for that page.</span></span> <span data-ttu-id="63749-119">예를 들어, 페이지에서 전자 메일 메시지를 보내는 경우 해당 작업에 대 한 모든 코드를 단일 페이지에 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-119">For example, if a page sends an email message, it's possible to put all the code for that operation in a single page.</span></span> <span data-ttu-id="63749-120">여기에는 전자 메일을 보내기 위한 설정 (즉, SMTP 서버)을 초기화 하 고 전자 메일 메시지를 보내는 코드가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-120">This can include the code to initialize the settings for sending email (that is, for the SMTP server) and for sending the email message.</span></span>

<span data-ttu-id="63749-121">그러나 일부 경우에는 사이트의 모든 페이지가 실행 되기 전에 일부 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-121">However, in some situations, you might want to run some code before any page on the site runs.</span></span> <span data-ttu-id="63749-122">이는 사이트의 어디에서 나 사용할 수 있는 값 ( *전역 값*이라고 함)을 설정 하는 데 유용 합니다. 예를 들어 일부 도우미는 전자 메일 설정 또는 계정 키와 같은 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-122">This is useful for setting values that can be used anywhere in the site (referred to as *global values*.) For example, some helpers require you to provide values like email settings or account keys.</span></span> <span data-ttu-id="63749-123">이러한 설정을 전역 값으로 유지 하는 것이 편리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-123">It can be handy to keep these settings in global values.</span></span>

<span data-ttu-id="63749-124">사이트의 루트에 *\_AppStart* 라는 페이지를 만들어이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-124">You can do this by creating a page named *\_AppStart.cshtml* in the root of the site.</span></span> <span data-ttu-id="63749-125">이 페이지가 있으면 사이트의 페이지가 처음 요청 될 때 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63749-125">If this page exists, it runs the first time any page in the site is requested.</span></span> <span data-ttu-id="63749-126">따라서 코드를 실행 하 여 전역 값을 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-126">Therefore, it's a good place to run code to set global values.</span></span> <span data-ttu-id="63749-127">AppStart에는 밑줄 접두사가 *\_* 있기 때문에 ASP.NET는 사용자가 직접 요청 하는 경우에도 페이지를 브라우저로 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-127">(Because *\_AppStart.cshtml* has an underscore prefix, ASP.NET won't send the page to a browser even if users request it directly.)</span></span>

<span data-ttu-id="63749-128">다음 다이어그램에서는 *\_AppStart* 페이지가 작동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63749-128">The following diagram shows how the *\_AppStart.cshtml* page works.</span></span> <span data-ttu-id="63749-129">페이지에 대 한 요청이 들어오면이 요청이 사이트의 모든 페이지에 대 한 첫 번째 요청이 면 ASP.NET는 먼저 *\_AppStart* 페이지가 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-129">When a request comes in for a page, and if this is the first request for any page in the site, ASP.NET first checks whether a *\_AppStart.cshtml* page exists.</span></span> <span data-ttu-id="63749-130">이 경우 *\_AppStart* 페이지의 모든 코드가 실행 되 고 요청한 페이지가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63749-130">If so, any code in the *\_AppStart.cshtml* page runs, and then the requested page runs.</span></span>

![[이미지]](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a><span data-ttu-id="63749-132">웹 사이트에 대 한 전역 값 설정</span><span class="sxs-lookup"><span data-stu-id="63749-132">Setting Global Values for Your Website</span></span>

1. <span data-ttu-id="63749-133">WebMatrix 웹 사이트의 루트 폴더에서 *AppStart\_* 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63749-133">In the root folder of a WebMatrix website, create a file named *\_AppStart.cshtml*.</span></span> <span data-ttu-id="63749-134">파일은 사이트의 루트에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-134">The file must be in the root of the site.</span></span>
2. <span data-ttu-id="63749-135">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-135">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    <span data-ttu-id="63749-136">이 코드는 사이트의 모든 페이지에서 자동으로 사용할 수 있는 `AppState` 사전에 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-136">This code stores a value in the `AppState` dictionary, which is automatically available to all pages in the site.</span></span> <span data-ttu-id="63749-137">*\_AppStart* 파일에는 태그가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-137">Notice that the *\_AppStart.cshtml* file does not have any markup in it.</span></span> <span data-ttu-id="63749-138">이 페이지는 코드를 실행 한 다음 원래 요청 된 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-138">The page will run the code and then redirect to the page that was originally requested.</span></span>

    > [!NOTE]
    > <span data-ttu-id="63749-139">*\_AppStart* 파일에 코드를 넣을 때는 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-139">Be careful when you put code in the *\_AppStart.cshtml* file.</span></span> <span data-ttu-id="63749-140">*\_AppStart* 파일의 코드에서 오류가 발생 하는 경우 웹 사이트가 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-140">If any errors occur in code in the *\_AppStart.cshtml* file, the website won't start.</span></span>
3. <span data-ttu-id="63749-141">루트 폴더에서 *AppName. cshtml*이라는 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63749-141">In the root folder, create a new page named *AppName.cshtml*.</span></span>
4. <span data-ttu-id="63749-142">기본 태그와 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-142">Replace the default markup and code with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    <span data-ttu-id="63749-143">이 코드는 *\_AppStart* 페이지에서 설정한 `AppState` 개체에서 값을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-143">This code extracts the value from the `AppState` object that you set in the *\_AppStart.cshtml* page.</span></span>
5. <span data-ttu-id="63749-144">브라우저에서 *AppName* 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-144">Run the *AppName.cshtml* page in a browser.</span></span> <span data-ttu-id="63749-145">(파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 이 페이지에는 전역 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63749-145">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays the global value.</span></span> 

    ![[이미지]](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a><span data-ttu-id="63749-147">도우미에 대 한 값 설정</span><span class="sxs-lookup"><span data-stu-id="63749-147">Setting Values for Helpers</span></span>

<span data-ttu-id="63749-148">*\_AppStart* 파일에 사용 하는 것은 사이트에서 사용 하 고 초기화 해야 하는 도우미에 대 한 값을 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="63749-148">A good use for the *\_AppStart.cshtml* file is to set values for helpers that you use in your site and that have to be initialized.</span></span> <span data-ttu-id="63749-149">일반적인 예는 `WebMail` 도우미에 대 한 전자 메일 설정 및 `ReCaptcha` 도우미에 대 한 개인 및 공개 키입니다.</span><span class="sxs-lookup"><span data-stu-id="63749-149">Typical examples are email settings for the `WebMail` helper and the private and public keys for the `ReCaptcha` helper.</span></span> <span data-ttu-id="63749-150">이와 같은 경우에 *\_AppStart* 에서 값을 한 번 설정할 수 있습니다. 그러면 해당 값이 사이트의 모든 페이지에 대해 이미 설정 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="63749-150">In cases like these, you can set the values once in the *\_AppStart.cshtml* and then they're already set for all the pages in your site.</span></span>

<span data-ttu-id="63749-151">이 절차에서는 `WebMail` 설정을 전역적으로 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63749-151">This procedure shows you how to set `WebMail` settings globally.</span></span> <span data-ttu-id="63749-152">`WebMail` 도우미를 사용 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 페이지 사이트에 전자 메일 추가](../getting-started/11-adding-email-to-your-web-site.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="63749-152">(For more information about using the `WebMail` helper, see [Adding Email to an ASP.NET Web Pages Site](../getting-started/11-adding-email-to-your-web-site.md).)</span></span>

1. <span data-ttu-id="63749-153">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)의 설명에 따라 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가 합니다 (아직 추가 하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="63749-153">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="63749-154">*\_AppStart* 파일이 아직 없는 경우 웹 사이트의 루트 폴더에서 *AppStart\_* 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63749-154">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
3. <span data-ttu-id="63749-155">다음 `WebMail` 설정을 *\_AppStart* 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-155">Add the following `WebMail` settings to the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    <span data-ttu-id="63749-156">코드에서 다음과 같은 전자 메일 관련 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-156">Modify the following email related settings in the code:</span></span>

   - <span data-ttu-id="63749-157">`your-SMTP-host`를 액세스할 수 있는 SMTP 서버의 이름으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-157">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
   - <span data-ttu-id="63749-158">`your-user-name-here`를 SMTP 서버 계정에 대 한 사용자 이름으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-158">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
   - <span data-ttu-id="63749-159">`your-account-password`를 SMTP 서버 계정의 암호로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-159">Set `your-account-password` to the password for your SMTP server account.</span></span>
   - <span data-ttu-id="63749-160">`your-email-address-here`를 본인의 전자 메일 주소로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-160">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="63749-161">메시지가 전송 되는 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="63749-161">This is the email address that the message is sent from.</span></span> <span data-ttu-id="63749-162">(일부 전자 메일 공급자는 다른 `From` 주소를 지정 하는 것을 허용 하지 않으며 사용자 이름을 `From` 주소로 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="63749-162">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

     <span data-ttu-id="63749-163">SMTP 설정에 대 한 자세한 내용은 [ASP.NET 웹 페이지 (razor) 사이트에서 전자 메일 보내기](https://go.microsoft.com/fwlink/?LinkID=202899) 및 [ASP.NET 웹 페이지 (Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)에서 전자 [메일 보내기와 관련 된 문제](https://go.microsoft.com/fwlink/?LinkId=253001#email) 문서에서 [전자 메일 설정 구성](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="63749-163">For more information about SMTP settings, see [Configuring Email Settings](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) in the article [Sending Email from an ASP.NET Web Pages (Razor) Site](https://go.microsoft.com/fwlink/?LinkID=202899) and [Issues with Sending Email](https://go.microsoft.com/fwlink/?LinkId=253001#email) in the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>
4. <span data-ttu-id="63749-164">*\_AppStart* 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-164">Save the *\_AppStart.cshtml* file and close it.</span></span>
5. <span data-ttu-id="63749-165">웹 사이트의 루트 폴더에서 *Testemail. cshtml*라는 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63749-165">In the root folder of a website, create new page named *TestEmail.cshtml*.</span></span>
6. <span data-ttu-id="63749-166">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-166">Replace the existing content with the following:</span></span> 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. <span data-ttu-id="63749-167">브라우저에서 *Testemail. cshtml* 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-167">Run the *TestEmail.cshtml* page in a browser.</span></span>
8. <span data-ttu-id="63749-168">필드를 입력 하 여 자신에 게 전자 메일 메시지를 보낸 다음 **보내기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-168">Fill in the fields to send yourself an email message and then click **Send**.</span></span>
9. <span data-ttu-id="63749-169">전자 메일을 확인 하 여 메시지를 받았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-169">Check your email to make sure you've gotten the message.</span></span>

<span data-ttu-id="63749-170">이 예제의 중요 한 부분은 일반적으로 변경 되지 않는 설정 (예: SMTP 서버 이름 및 전자 메일 자격 증명)이 *\_AppStart* 파일에 설정 되어 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="63749-170">The important part of this example is that the settings that you don't usually change — like the name of your SMTP server and your email credentials — are set in the *\_AppStart.cshtml* file.</span></span> <span data-ttu-id="63749-171">이렇게 하면 전자 메일을 보내는 각 페이지에서 다시 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-171">That way you don't need to set them again in each page where you send email.</span></span> <span data-ttu-id="63749-172">어떤 이유로 이러한 설정을 변경 해야 하는 경우에는 페이지에서 개별적으로 설정할 수 있습니다. 페이지에서 받는 사람 및 전자 메일 메시지 본문과 같이 일반적으로 매번 변경 되는 값만 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-172">(Although if for some reason you need to change those settings, you can set them individually in a page.) In the page, you only set the values that typically change each time, like the recipient and the body of the email message.</span></span>

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a><span data-ttu-id="63749-173">폴더의 파일 전후에 코드 실행</span><span class="sxs-lookup"><span data-stu-id="63749-173">Running Code Before and After Files in a Folder</span></span>

<span data-ttu-id="63749-174">*AppStart를\_* 사용 하 여 사이트의 페이지가 실행 되기 전에 코드를 작성 하는 것과 마찬가지로 특정 폴더의 모든 페이지가 실행 되기 전에 실행 되는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-174">Just like you can use *\_AppStart.cshtml* to write code before pages in the site run, you can write code that runs before (and after) any page in a particular folder run.</span></span> <span data-ttu-id="63749-175">폴더의 모든 페이지에 대해 동일한 레이아웃 페이지를 설정 하거나 폴더의 페이지를 실행 하기 전에 사용자가 로그인 했는지 확인 하는 등의 작업을 수행 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-175">This is useful for things like setting the same layout page for all the pages in a folder, or for checking that a user is logged in before running a page in the folder.</span></span>

<span data-ttu-id="63749-176">특정 폴더의 페이지에 대해 *\_PageStart. cshtml*이라는 파일에 코드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-176">For pages in particular folders, you can create code in a file named *\_PageStart.cshtml*.</span></span> <span data-ttu-id="63749-177">다음 다이어그램에서는 *\_PageStart. cshtml* 페이지가 작동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63749-177">The following diagram shows how the *\_PageStart.cshtml* page works.</span></span> <span data-ttu-id="63749-178">페이지에 대 한 요청이 들어오면 ASP.NET는 먼저 *\_AppStart* 페이지를 확인 하 고이를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-178">When a request comes in for a page, ASP.NET first checks for a *\_AppStart.cshtml* page and runs that.</span></span> <span data-ttu-id="63749-179">그런 다음 ASP.NET는 *\_PageStart. cshtml* 페이지가 있는지 여부를 확인 하 고, 있는 경우이를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-179">Then ASP.NET checks whether there's a *\_PageStart.cshtml* page, and if so, runs that.</span></span> <span data-ttu-id="63749-180">그런 다음 요청 된 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-180">It then runs the requested page.</span></span>

<span data-ttu-id="63749-181">*\_PageStart. cshtml* 페이지 내에서 처리 중에 `RunPage` 메서드를 포함 하 여 요청 된 페이지를 실행 하려는 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-181">Inside the *\_PageStart.cshtml* page, you can specify where during processing you want the requested page to run by including a `RunPage` method.</span></span> <span data-ttu-id="63749-182">이렇게 하면 요청 된 페이지가 실행 되기 전에 코드를 실행 한 후 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-182">This lets you run code before the requested page runs and then again after it.</span></span> <span data-ttu-id="63749-183">`RunPage`를 포함 하지 않는 경우 *\_PageStart* 의 모든 코드가 실행 되 고 요청한 페이지가 자동으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63749-183">If you don't include `RunPage`, all the code in *\_PageStart.cshtml* runs, and then the requested page runs automatically.</span></span>

![[이미지]](18-customizing-site-wide-behavior/_static/image3.jpg)

<span data-ttu-id="63749-185">ASP.NET를 사용 하면 *\_PageStart. cshtml* 파일의 계층 구조를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-185">ASP.NET lets you create a hierarchy of *\_PageStart.cshtml* files.</span></span> <span data-ttu-id="63749-186">사이트의 루트 및 모든 하위 폴더에 *\_PageStart. cshtml* 파일을 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-186">You can put a *\_PageStart.cshtml* file in the root of the site and in any subfolder.</span></span> <span data-ttu-id="63749-187">페이지가 요청 되 면 최상위 수준 (사이트 루트에 가장 가까운)의 *\_PageStart. cshtml* 파일이 실행 된 다음, 다음 하위 폴더의 *\_pagestart. cshtml* 파일 및 요청이 요청 된 페이지를 포함 하는 폴더에 도달할 때까지 하위 폴더 구조에서 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63749-187">When a page is requested, the *\_PageStart.cshtml* file at the top-most level (nearest to the site root) runs, followed by the *\_PageStart.cshtml* file in the next subfolder, and so on down the subfolder structure until the request reaches the folder that contains the requested page.</span></span> <span data-ttu-id="63749-188">해당 하는 모든 *\_PageStart. cshtml* 파일이 실행 된 후 요청 된 페이지가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63749-188">After all the applicable *\_PageStart.cshtml* files have run, the requested page runs.</span></span>

<span data-ttu-id="63749-189">예를 들어 다음과 같은 *\_PageStart. cshtml* 파일 및 *기본값 cshtml* 파일의 조합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-189">For example, you might have the following combination of *\_PageStart.cshtml* files and *Default.cshtml* file:</span></span>

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

<span data-ttu-id="63749-190">*/Myfolder/default.cshtml*를 실행 하면 다음이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63749-190">When you run */myfolder/default.cshtml*, you'll see the following:</span></span>

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a><span data-ttu-id="63749-191">폴더의 모든 페이지에 대 한 초기화 코드 실행</span><span class="sxs-lookup"><span data-stu-id="63749-191">Running Initialization Code for All Pages in a Folder</span></span>

<span data-ttu-id="63749-192">*\_PageStart. cshtml* 파일은 단일 폴더에 있는 모든 파일에 대해 동일한 레이아웃 페이지를 초기화 하는 데 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-192">A good use for *\_PageStart.cshtml* files is to initialize the same layout page for all files in a single folder.</span></span>

1. <span data-ttu-id="63749-193">루트 폴더에서 *Initpages*라는 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63749-193">In the root folder, create a new folder named *InitPages*.</span></span>
2. <span data-ttu-id="63749-194">웹 사이트의 *Initpages* 폴더에서 이름이 *\_pagestart. cshtml* 인 파일을 만들고 기본 태그와 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-194">In the *InitPages* folder of your website, create a file named *\_PageStart.cshtml* and replace the default markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. <span data-ttu-id="63749-195">웹 사이트의 루트에서 *Shared*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63749-195">In the root of the website, create a folder named *Shared*.</span></span>
4. <span data-ttu-id="63749-196">*공유* 폴더에서 *Layout1\_* 라는 파일을 만들고 기본 태그와 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-196">In the *Shared* folder, create a file named *\_Layout1.cshtml* and replace the default markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. <span data-ttu-id="63749-197">*Initpages* 폴더에서 *Content1* 라는 파일을 만들고 기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-197">In the *InitPages* folder, create a file named *Content1.cshtml* and replace the existing content with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. <span data-ttu-id="63749-198">*Initpages* 폴더에서 *Content2* 이라는 다른 파일을 만들고 기본 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-198">In the *InitPages* folder, create another file named *Content2.cshtml* and replace the default markup with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. <span data-ttu-id="63749-199">브라우저에서 *Content1* 를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-199">Run *Content1.cshtml* in a browser.</span></span> 

    ![[이미지]](18-customizing-site-wide-behavior/_static/image4.jpg)

    <span data-ttu-id="63749-201">*Content1* 페이지가 실행 되 면 *\_pagestart. cshtml* 파일은 `Layout`를 설정 하 고 `PageData["MyBackground"]`를 색으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-201">When the *Content1.cshtml* page runs, the *\_PageStart.cshtml* file sets `Layout` and also sets `PageData["MyBackground"]` to a color.</span></span> <span data-ttu-id="63749-202">*Content1*에서 레이아웃과 색이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63749-202">In *Content1.cshtml*, the layout and color are applied.</span></span>
8. <span data-ttu-id="63749-203">브라우저에 *Content2* 를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-203">Display *Content2.cshtml* in a browser.</span></span> 

    <span data-ttu-id="63749-204">두 페이지가 모두 동일한 레이아웃 페이지와 *\_PageStart. cshtml*에서 초기화 된 색을 사용 하기 때문에 레이아웃은 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-204">The layout is the same, because both pages use the same layout page and color as initialized in *\_PageStart.cshtml*.</span></span>

## <a name="using-_pagestartcshtml-to-handle-errors"></a><span data-ttu-id="63749-205">\_PageStart. cshtml를 사용 하 여 오류 처리</span><span class="sxs-lookup"><span data-stu-id="63749-205">Using \_PageStart.cshtml to Handle Errors</span></span>

<span data-ttu-id="63749-206">*\_PageStart. cshtml* 파일의 또 다른 용도는 폴더의 모든 *cshtml* 페이지에서 발생할 수 있는 프로그래밍 오류 (예외)를 처리 하는 방법을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="63749-206">Another good use for the *\_PageStart.cshtml* file is to create a way to handle programming errors (exceptions) that might occur in any *.cshtml* page in a folder.</span></span> <span data-ttu-id="63749-207">이 예제에서는이 작업을 수행 하는 한 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63749-207">This example shows you one way to do this.</span></span>

1. <span data-ttu-id="63749-208">루트 폴더에서 *Initcatch*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63749-208">In the root folder, create a folder named *InitCatch*.</span></span>
2. <span data-ttu-id="63749-209">웹 사이트의 *Initcatch* 폴더에서 이름이 *\_pagestart. cshtml* 인 파일을 만들고 기존 태그와 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-209">In the *InitCatch* folder of your website, create a file named *\_PageStart.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    <span data-ttu-id="63749-210">이 코드에서는 `try` 블록 내에서 `RunPage` 메서드를 호출 하 여 요청 된 페이지를 명시적으로 실행 해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="63749-210">In this code, you try running the requested page explicitly by calling the `RunPage` method inside a `try` block.</span></span> <span data-ttu-id="63749-211">요청 된 페이지에서 프로그래밍 오류가 발생 하면 `catch` 블록 내의 코드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63749-211">If any programming errors occur in the requested page, the code inside the `catch` block runs.</span></span> <span data-ttu-id="63749-212">이 경우 코드는 페이지로 리디렉션되고 (*오류. cshtml*) URL의 일부로 오류가 발생 한 파일의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-212">In this case, the code redirects to a page (*Error.cshtml*) and passes the name of the file that experienced the error as part of the URL.</span></span> <span data-ttu-id="63749-213">(곧 페이지를 만듭니다.)</span><span class="sxs-lookup"><span data-stu-id="63749-213">(You'll create the page shortly.)</span></span>
3. <span data-ttu-id="63749-214">웹 사이트의 *Initcatch* 폴더에서 다음과 같이 *file 이라는 파일* 을 만들고 기존 태그와 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-214">In the *InitCatch* folder of your website, create a file named *Exception.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    <span data-ttu-id="63749-215">이 예의 목적에 따라이 페이지에서 수행 하는 작업은 존재 하지 않는 데이터베이스 파일을 열려고 시도 하 여 의도적으로 오류를 생성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="63749-215">For purposes of this example, what you're doing in this page is deliberately creating an error by trying to open a database file that doesn't exist.</span></span>
4. <span data-ttu-id="63749-216">루트 폴더에서 *오류. cshtml* 라는 파일을 만들고 기존 태그와 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-216">In the root folder, create a file named *Error.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    <span data-ttu-id="63749-217">이 페이지에서 식 `@Request["source"]` URL에서 값을 가져와 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-217">In this page, the expression `@Request["source"]` gets the value out of the URL and displays it.</span></span>
5. <span data-ttu-id="63749-218">도구 모음에서 **저장**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-218">In the toolbar, click **Save**.</span></span>
6. <span data-ttu-id="63749-219">브라우저에서 *. cshtml* 를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-219">Run *Exception.cshtml* in a browser.</span></span> 

    ![[이미지]](18-customizing-site-wide-behavior/_static/image5.jpg)

    <span data-ttu-id="63749-221">오류가 발생 했기 *때문에* *\_pagestart. cshtml* 페이지는 메시지를 표시 하는 *오류. cshtml* 파일로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-221">Because an error occurs in *Exception.cshtml*, the *\_PageStart.cshtml* page redirects to the *Error.cshtml* file, which displays the message.</span></span>

    <span data-ttu-id="63749-222">예외에 대 한 자세한 내용은 [Razor 구문을 사용한 ASP.NET 웹 페이지 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=251587)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="63749-222">For more information about exceptions, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587).</span></span>

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-_pagestartcshtml-to-restrict-folder-access"></a><span data-ttu-id="63749-223">\_PageStart. cshtml를 사용 하 여 폴더 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="63749-223">Using \_PageStart.cshtml to Restrict Folder Access</span></span>

<span data-ttu-id="63749-224">*\_PageStart. cshtml* 파일을 사용 하 여 폴더의 모든 파일에 대 한 액세스를 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-224">You can also use the *\_PageStart.cshtml* file to restrict access to all the files in a folder.</span></span>

1. <span data-ttu-id="63749-225">WebMatrix에서 **템플릿에서 사이트** 옵션을 사용 하 여 새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63749-225">In WebMatrix, create a new website using the **Site From Template** option.</span></span>
2. <span data-ttu-id="63749-226">사용 가능한 템플릿에서 **스타터 사이트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-226">From the available templates, select **Starter Site**.</span></span>
3. <span data-ttu-id="63749-227">루트 폴더에서 이름이 *AuthenticatedContent*인 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63749-227">In the root folder, create a folder named *AuthenticatedContent*.</span></span>
4. <span data-ttu-id="63749-228">*AuthenticatedContent* 폴더에서 *\_이름이 pagestart. cshtml* 인 파일을 만들고 기존 태그와 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-228">In the *AuthenticatedContent* folder, create a file named *\_PageStart.cshtml* and replace the existing markup and code with the following:</span></span> 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    <span data-ttu-id="63749-229">이 코드는 폴더의 모든 파일이 캐시 되는 것을 방지 하는 것으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-229">The code starts by preventing all files in the folder from being cached.</span></span> <span data-ttu-id="63749-230">이는 사용자의 캐시 된 페이지를 다음 사용자가 사용할 수 없도록 하려는 공용 컴퓨터와 같은 시나리오에 필요 합니다. 그런 다음 코드는 사용자가 사이트에 로그인 했는지 여부를 확인 한 다음 폴더의 모든 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-230">(This is required for scenarios like public computers, where you don't want one user's cached pages to be available to the next user.) Next, the code determines whether the user has signed in to the site before they can view any of the pages in the folder.</span></span> <span data-ttu-id="63749-231">사용자가 로그인 하지 않은 경우에는 코드가 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="63749-231">If the user is not signed in, the code redirects to the login page.</span></span> <span data-ttu-id="63749-232">로그인 페이지는 `ReturnUrl`라는 쿼리 문자열 값을 포함 하는 경우 원래 요청 된 페이지로 사용자를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-232">The login page can return the user to the page that was originally requested if you include a query string value named `ReturnUrl`.</span></span>
5. <span data-ttu-id="63749-233">AuthenticatedContent 폴더에 라는 새 페이지를 만듭니다 *.*</span><span class="sxs-lookup"><span data-stu-id="63749-233">Create a new page in the *AuthenticatedContent* folder named *Page.cshtml*.</span></span>
6. <span data-ttu-id="63749-234">기본 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63749-234">Replace the default markup with the following:</span></span>  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. <span data-ttu-id="63749-235">브라우저에서 *페이지* 탐색기를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-235">Run *Page.cshtml* in a browser.</span></span> <span data-ttu-id="63749-236">이 코드는 사용자를 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-236">The code redirects you to a login page.</span></span> <span data-ttu-id="63749-237">로그인 하려면 먼저 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63749-237">You must register before logging in.</span></span> <span data-ttu-id="63749-238">등록 하 고 로그인 한 후에는 페이지로 이동 하 여 해당 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63749-238">After you've registered and logged in, you can navigate to the page and view its contents.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="63749-239">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="63749-239">Additional Resources</span></span>

[<span data-ttu-id="63749-240">Razor 구문을 사용한 ASP.NET 웹 페이지 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="63749-240">Introduction to ASP.NET Web Pages Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=251587)
