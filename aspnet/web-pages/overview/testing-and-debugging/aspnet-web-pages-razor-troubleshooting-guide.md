---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET 웹 페이지 (Razor) 문제 해결 가이드 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Razor (ASP.NET 웹 페이지)를 사용 하 여 작업할 때 발생할 수 있는 문제 및 제안 된 몇 가지 솔루션을 설명 합니다. Software 버전 ASP.NET Web Pag ...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473381"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a><span data-ttu-id="0b220-104">ASP.NET 웹 페이지(Razor) 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="0b220-104">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>

<span data-ttu-id="0b220-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0b220-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0b220-106">이 문서에서는 Razor (ASP.NET 웹 페이지)를 사용 하 여 작업할 때 발생할 수 있는 문제 및 제안 된 몇 가지 솔루션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-106">This article describes issues that you might have when working with ASP.NET Web Pages (Razor) and some suggested solutions.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="0b220-107">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="0b220-107">Software versions</span></span>
> 
> 
> - <span data-ttu-id="0b220-108">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="0b220-108">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="0b220-109">이 자습서는 ASP.NET 웹 페이지 2 및 ASP.NET 웹 페이지 1.0 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-109">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>

<span data-ttu-id="0b220-110">이 항목에는 다음과 같은 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-110">This topic contains the following sections:</span></span>

- [<span data-ttu-id="0b220-111">페이지 실행 문제</span><span class="sxs-lookup"><span data-stu-id="0b220-111">Issues with Running Pages</span></span>](#Issues_Running_.cshtml_Pages)
- [<span data-ttu-id="0b220-112">Razor 코드 문제</span><span class="sxs-lookup"><span data-stu-id="0b220-112">Issues with Razor Code</span></span>](#IssuesWithRazorCode)
- [<span data-ttu-id="0b220-113">보안 및 멤버 자격과 관련 된 문제</span><span class="sxs-lookup"><span data-stu-id="0b220-113">Issues with Security and Membership</span></span>](#membership)
- [<span data-ttu-id="0b220-114">전자 메일 보내기 문제</span><span class="sxs-lookup"><span data-stu-id="0b220-114">Issues with Sending Email</span></span>](#email)
- [<span data-ttu-id="0b220-115">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0b220-115">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="0b220-116">일반적인 질문은 [ASP.NET 웹 페이지 (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0b220-116">For general questions, see [ASP.NET Web Pages (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000).</span></span>

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a><span data-ttu-id="0b220-117">페이지 실행 문제</span><span class="sxs-lookup"><span data-stu-id="0b220-117">Issues with Running Pages</span></span>

<span data-ttu-id="0b220-118">여러 가지 문제로 인해 *. cshtml* 및 *.* t o l s 페이지가 제대로 실행 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-118">A variety of issues can prevent *.cshtml* and *.vbhtml* pages from running properly.</span></span> <span data-ttu-id="0b220-119">이 섹션에는 일반적인 오류 메시지 및 가능한 원인이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-119">This section lists common error messages and likely causes.</span></span>

### <a name="http-error-403---forbidden-access-is-denied"></a><span data-ttu-id="0b220-120">HTTP 오류 403-사용 권한 없음: 액세스가 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-120">HTTP Error 403 - Forbidden: Access is denied</span></span>

<span data-ttu-id="0b220-121">*제공한 자격 증명을 사용 하 여이 디렉터리 또는 페이지를 볼 수 있는 권한이 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="0b220-121">*You do not have permission to view this directory or page using the credentials that you supplied.*</span></span>

<span data-ttu-id="0b220-122">이 오류는 서버에서 올바른 버전의 .NET Framework를 실행 하지 않는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-122">This error can occur if the server is not running the correct version of the .NET Framework.</span></span> <span data-ttu-id="0b220-123">서버를 실행 하는 컴퓨터 (로컬 또는 원격)에 적어도 .NET Framework 4가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-123">Make sure that the computer that's running the server (locally or remotely) has at least the .NET Framework 4 installed.</span></span> <span data-ttu-id="0b220-124">또한 응용 프로그램 자체가 올바른 버전을 실행 하도록 구성 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-124">Also make sure that the application itself is configured to run the right version.</span></span>

<span data-ttu-id="0b220-125">WebMatrix에서 작업 하는 동안이 문제가 로컬로 표시 되 면 **사이트** 작업 영역을 클릭 한 다음 Treeview에서 **설정**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-125">If you see this problem locally while working in WebMatrix, click the **Site** workspace, and then in the treeview click **Settings**.</span></span> <span data-ttu-id="0b220-126">**.NET Framework 버전 선택** 목록에서 **.Net 4 (통합)** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-126">In the **Select .NET Framework Version** list, select **.NET 4 (Integrated)**.</span></span> <span data-ttu-id="0b220-127">이 버전이 이미 설정 되어 있는 경우 관리자 권한으로 WebMatrix를 실행 해 보세요.</span><span class="sxs-lookup"><span data-stu-id="0b220-127">If this version is already set, try running WebMatrix as an administrator.</span></span>

<span data-ttu-id="0b220-128">웹 사이트의 루트에 하나 이상의 *cshtml* 파일이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-128">Make sure that the root of your website has at least one *.cshtml* file in it.</span></span>

<span data-ttu-id="0b220-129">웹 서버가 원격 서버에 있는 경우이 오류가 표시 되 면 서버 관리자에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0b220-129">If you see this error when the web server is on a remote server, contact the server administrator.</span></span> <span data-ttu-id="0b220-130">서버에 .NET Framework 4 이상이 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-130">Make sure that the server has the .NET Framework 4 or later installed.</span></span> <span data-ttu-id="0b220-131">또한 해당 버전의 the.NET Framework를 사용 하도록 구성 된 응용 프로그램 풀에서 응용 프로그램이 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-131">Also make sure that the application is running in an application pool that's configured to use that version of the.NET Framework.</span></span>

<span data-ttu-id="0b220-132">서버에 대 한 제어 권한이 있는 경우 올바른 버전의 .NET Framework를 실행 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-132">If you have control over the server, make sure it's running the correct version of the .NET Framework.</span></span> <span data-ttu-id="0b220-133">`aspnet_regiis -iru` 명령을 실행 하 여 설치를 복구 해 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-133">You might also try repairing the installation by running the `aspnet_regiis -iru` command.</span></span> <span data-ttu-id="0b220-134">예를 들어 .NET Framework를 설치한 후 IIS를 설치 하는 경우 IIS는 ASP.NET 페이지를 실행 하도록 올바르게 구성 되지 않습니다. 자세한 내용은 [ASP.NET Iis 등록 도구 (Aspnet\_regiis .exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0b220-134">(For example, if you install IIS after you install the .NET Framework, IIS will not be correctly configured to run ASP.NET pages.) For more information, see [ASP.NET IIS Registration Tool (Aspnet\_regiis.exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx).</span></span>

### <a name="http-error-40314---forbidden"></a><span data-ttu-id="0b220-135">HTTP 오류 403.14-사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="0b220-135">HTTP Error 403.14 - Forbidden</span></span>

<span data-ttu-id="0b220-136">*웹 서버가이 디렉터리의 내용을 나열 하지 않도록 구성 되어 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="0b220-136">*The Web server is configured to not list the contents of this directory.*</span></span>

<span data-ttu-id="0b220-137">이 오류는 보호 되는 리소스 (예: *web.config* 파일) 또는 보호 되는 폴더 (예: *앱\_데이터* 또는 *앱\_코드*)에 있는 리소스를 요청 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-137">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="http-error-40417---not-found"></a><span data-ttu-id="0b220-138">HTTP 오류 404.17-찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="0b220-138">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="0b220-139">*요청 된 콘텐츠는 스크립트로 표시 되며 정적 파일 처리기에서 제공 되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="0b220-139">*The requested content appears to be script and will not be served by the static file handler.*</span></span>

<span data-ttu-id="0b220-140">이 오류는 .NET Framework 4 이상을 사용 하도록 서버가 올바르게 구성 되어 있지 않아 `@{ }` 블록의 코드를 인식 하지 못하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-140">This error can occur if the server is not configured correctly to use the .NET Framework 4 or later, and therefore does not recognize the code in `@{ }` blocks.</span></span> <span data-ttu-id="0b220-141">앞의 *HTTP 오류 403-사용 권한 없음: 액세스가 거부*됨에 대 한 설명을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0b220-141">See the description earlier for *HTTP Error 403 - Forbidden: Access is denied*.</span></span>

### <a name="http-error-4047---not-found"></a><span data-ttu-id="0b220-142">HTTP 오류 404.7-찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="0b220-142">HTTP Error 404.7 - Not Found</span></span>

<span data-ttu-id="0b220-143">*파일 확장명을 거부 하도록 요청 필터링 모듈이 구성 되어 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="0b220-143">*The request filtering module is configured to deny the file extension*</span></span>

<span data-ttu-id="0b220-144">이 오류는 서버가 서버에서 명시적으로 차단 *된 경우에* 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-144">This error can occur if *.cshtml* or *.vbhtml* extensions have been explicitly blocked on the server.</span></span> <span data-ttu-id="0b220-145">이 문제는 Url이 확장을 포함 하지 않는 경우에도 작동 하지만 *.* a u 또는 *.*</span><span class="sxs-lookup"><span data-stu-id="0b220-145">A symptom of this problem is that URLs work when they do not include the extension, but URLs that include *.cshtml* or *.vbhtml* do not work.</span></span> <span data-ttu-id="0b220-146">가능한 해결 방법은 사이트의 *web.config* 파일에서 확장을 다시 사용 하도록 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-146">A possible solution is to re-enable the extensions in the site's *Web.config* file.</span></span> <span data-ttu-id="0b220-147">다음 예제에서는 *. cshtml* 확장명을 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-147">The following example shows how to enable the *.cshtml* extension.</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a><span data-ttu-id="0b220-148">HTTP 오류 404.8-찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="0b220-148">HTTP Error 404.8 - Not Found</span></span>

<span data-ttu-id="0b220-149">*HiddenSegment 섹션을 포함 하는 URL의 경로를 거부 하도록 요청 필터링 모듈이 구성 되어 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="0b220-149">*The request filtering module is configured to deny a path in the URL that contains a hiddenSegment section.*</span></span>

<span data-ttu-id="0b220-150">이 오류는 보호 되는 리소스 (예: *web.config* 파일) 또는 보호 되는 폴더 (예: *앱\_데이터* 또는 *앱\_코드*)에 있는 리소스를 요청 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-150">This error can occur if you request a resource that's protected (like the *Web.config* file) or that's in a folder that's protected (like *App\_Data* or *App\_Code*).</span></span>

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a><span data-ttu-id="0b220-151">이 유형의 페이지는 제공 되지 않습니다 ('/' 응용 프로그램의 서버 오류).</span><span class="sxs-lookup"><span data-stu-id="0b220-151">This type of page is not served (Server Error in '/' Application)</span></span>

<span data-ttu-id="0b220-152">HTTP 오류 404.17에 대 한 앞부분의 설명을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0b220-152">See the description earlier for HTTP Error 404.17.</span></span>

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a><span data-ttu-id="0b220-153">Razor 코드 문제</span><span class="sxs-lookup"><span data-stu-id="0b220-153">Issues with Razor code</span></span>

### <a name="the-name-class-does-not-exist-in-the-current-context"></a><span data-ttu-id="0b220-154">'*Class*' 이름이 현재 컨텍스트에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-154">The name '*class*' does not exist in the current context</span></span>

<span data-ttu-id="0b220-155">이 오류가 표시 되는 이유는 `class` 도우미를 참조 하지만 도우미가 설치 되어 있지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-155">Often, a reason you see this error is that `class` references a helper, but the helper is not installed.</span></span> <span data-ttu-id="0b220-156">예를 들어 도우미를 사용 하려고 하지만 NuGet에서 패키지를 설치 하지 않은 경우이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-156">For example, if you try to use a helper, but if you haven't installed the package from NuGet, you'll see this error.</span></span> <span data-ttu-id="0b220-157">WebMatrix의 갤러리를 사용 하 여 도우미를 찾아서 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-157">Use the Gallery in WebMatrix to find and install the helper.</span></span>

<span data-ttu-id="0b220-158">도우미가 설치 되어 있지만 페이지에서 인식 되지 않는 경우 코드에 `using` 문 추가를 추가 해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-158">If the helper is installed, but the page still doesn't recognize it, try adding add a `using` statement to the code.</span></span> <span data-ttu-id="0b220-159">`using` 문에서 도우미가 포함 된 네임 스페이스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-159">In the `using` statement, reference the namespace that includes the helper.</span></span> <span data-ttu-id="0b220-160">예를 들어, ASP.NET 웹 도우미 패키지에 있는 기본 도우미는 `System.Web.Helpers` 네임 스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-160">For example, the basic helpers that are in the ASP.NET Web Helpers package are in the `System.Web.Helpers` namespace.</span></span> <span data-ttu-id="0b220-161">도우미를 사용 하려는 페이지 맨 위에 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-161">At the top of the page where you want to use the helper, add this line:</span></span>

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a><span data-ttu-id="0b220-162">보안 및 멤버 자격과 관련 된 문제</span><span class="sxs-lookup"><span data-stu-id="0b220-162">Issues with Security and Membership</span></span>

<span data-ttu-id="0b220-163">ASP.NET 웹 페이지 (Razor)에서 기본 제공 보안 (멤버 자격) 시스템을 사용 하는 경우 다음과 같은 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-163">If you are using the built-in security (membership) system in ASP.NET Web Pages (Razor), you might encounter the following issues.</span></span>

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a><span data-ttu-id="0b220-164">이 메서드를 호출 하려면 "Membership. Provider" 속성이 "ExtendedMembershipProvider"의 인스턴스여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-164">To call this method, the "Membership.Provider" property must be an instance of "ExtendedMembershipProvider"</span></span>

<span data-ttu-id="0b220-165">이 오류는 `AspNetSqlMembershipProvider` 클래스가 구성 되지 않았음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-165">This error can indicate that no `AspNetSqlMembershipProvider` class is configured.</span></span> <span data-ttu-id="0b220-166">증상은 사이트가 로컬에서 제대로 작동 하지만 호스팅 공급자의 서버에 게시할 때이 오류를 throw 한다는 것입니다. 이 문제에 대 한 한 가지 해결 방법은 사이트의 *web.config* 파일에 다음을 추가 하 여 명시적 멤버 자격을 명시적으로 사용 하도록 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-166">(A symptom is that the site works fine locally but throws this error when you publish it to a hosting provider's server.) One fix for this problem is to explicitly enable simple membership by adding the following to the site's *Web.config* file:</span></span>

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a><span data-ttu-id="0b220-167">전자 메일 보내기 문제</span><span class="sxs-lookup"><span data-stu-id="0b220-167">Issues with Sending Email</span></span>

<span data-ttu-id="0b220-168">전자 메일을 보낼 때 발생 하는 문제는 디버깅 하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-168">Problems with sending email can be challenging to debug.</span></span> <span data-ttu-id="0b220-169">초기 문제는 SMTP 서버에 연결할 수 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-169">An initial problem can be that you can't connect to the SMTP server.</span></span> <span data-ttu-id="0b220-170">연결에 성공 하면 ASP.NET는 메시지를 SMTP 서버에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-170">If the connection is successful, ASP.NET hands the message off to the SMTP server.</span></span> <span data-ttu-id="0b220-171">그러나 메시지 자체에는 SMTP 서버에서 메시지를 보내지 못하도록 하는 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-171">However, there can be problems with the message itself that prevents the SMTP server from sending it.</span></span>

<span data-ttu-id="0b220-172">응용 프로그램에서 전자 메일을 성공적으로 보내지 않는 경우 다음을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-172">If your application does not successfully send email, try the following:</span></span>

- <span data-ttu-id="0b220-173">SMTP 서버 이름은 `smtp.provider.com` 또는 `smtp.provider.net`와 같은 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-173">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="0b220-174">그러나 호스팅 공급자에 사이트를 게시 하는 경우 해당 지점에서 SMTP 서버 이름이 `localhost`될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-174">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="0b220-175">이 문제는 게시 하 고 사이트를 공급자 서버에서 실행 한 후 SMTP 서버가 응용 프로그램의 관점에서 로컬 일 수 있기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-175">This situation occurs because after you've published and your site is running on the provider's server, the SMTP server might be local from the perspective of your application.</span></span> <span data-ttu-id="0b220-176">서버 이름을 변경 하면 게시 프로세스의 일부로 SMTP 서버 이름을 변경 해야 하는 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-176">This change in server names might mean that you have to change the SMTP server name as part of your publishing process.</span></span>
- <span data-ttu-id="0b220-177">포트 번호는 일반적으로 25입니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-177">The port number is usually 25.</span></span> <span data-ttu-id="0b220-178">그러나 일부 공급자는 포트 587 또는 다른 포트를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-178">However, some providers require you to use port 587 or some other port.</span></span> <span data-ttu-id="0b220-179">SMTP 서버의 소유자에 게 사용할 포트 번호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-179">Check with the owner of the SMTP server what port number they expect you to use.</span></span>
- <span data-ttu-id="0b220-180">올바른 자격 증명을 사용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-180">Make sure that you use the right credentials.</span></span> <span data-ttu-id="0b220-181">호스팅 공급자에 사이트를 게시 한 경우 공급자가 특별히 표시 한 자격 증명을 전자 메일에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-181">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="0b220-182">이러한 자격 증명은 게시 하는 데 사용 하는 자격 증명과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-182">These credentials might be different from the credentials you use to publish.</span></span>
- <span data-ttu-id="0b220-183">자격 증명이 필요 하지 않은 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-183">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="0b220-184">개인 ISP를 사용 하 여 전자 메일을 전송 하는 경우 전자 메일 공급자가 이미 자격 증명을 알고 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-184">If you're sending email by using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="0b220-185">게시 한 후 로컬 컴퓨터에서 테스트 하는 경우와 다른 자격 증명을 사용 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-185">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
- <span data-ttu-id="0b220-186">전자 메일 공급자가 암호화를 사용 하는 경우 `WebMail.EnableSsl`를 `true`로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-186">If your email provider uses encryption, set `WebMail.EnableSsl` to `true`.</span></span>

<span data-ttu-id="0b220-187">전자 메일을 보내는 동안 오류가 발생 하는 경우 다음과 같은 표준 ASP.NET 오류 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-187">If there is an error sending email, you might see a standard ASP.NET error message, which looks like this:</span></span>

![전자 메일에 문제가 있는 경우 ASP.NET 오류 메시지](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

<span data-ttu-id="0b220-189">다음 예제와 같이 `try-catch` 블록을 사용 하 여 전자 메일 보내기와 관련 된 문제를 디버그할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-189">You can also debug problems with sending email by using a `try-catch` block, as in the following example.</span></span> <span data-ttu-id="0b220-190">`try-catch` 블록을 사용 하는 경우 ASP.NET는 표준 오류 메시지를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-190">When you use a `try-catch` block, ASP.NET does not display its standard error messages.</span></span> <span data-ttu-id="0b220-191">대신 블록의 `catch` 부분에서 오류를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-191">Instead, you can capture the error in the `catch` portion of the block.</span></span>

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

<span data-ttu-id="0b220-192">`your-SMTP-server-name`에 대 한 적절 한 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-192">Substitute the appropriate values for `your-SMTP-server-name`, and so on.</span></span> <span data-ttu-id="0b220-193">이러한 방식으로 표시 될 수 있는 오류 메시지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-193">Some of the error messages you might see this way include the following:</span></span>

- <span data-ttu-id="0b220-194">*메일을 보내지 못했습니다.*</span><span class="sxs-lookup"><span data-stu-id="0b220-194">*Failure sending mail.*</span></span>

    <span data-ttu-id="0b220-195">또는</span><span class="sxs-lookup"><span data-stu-id="0b220-195">-or-</span></span>

    <span data-ttu-id="0b220-196">*시간이 지난 후 연결 된 파티가 적절 하 게 응답 하지 않거나 연결 된 호스트가 응답 하지 않아 연결을 설정 하지 못하여 연결 하지 못했습니다.*</span><span class="sxs-lookup"><span data-stu-id="0b220-196">*A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond*</span></span>

    <span data-ttu-id="0b220-197">이 오류는 일반적으로 응용 프로그램이 SMTP 서버에 연결할 수 없음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-197">This error usually means that the application could not connect to the SMTP server.</span></span> <span data-ttu-id="0b220-198">서버 이름 및 포트 번호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-198">Check the server name and port number.</span></span>
- <span data-ttu-id="0b220-199">*사서함을 사용할 수 없습니다. 서버 응답: 5.1.0 &lt;someuser@invaliddomain&gt; 발신자가 거부 됨: 발신자 도메인이 잘못 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="0b220-199">*Mailbox unavailable. The server response was: 5.1.0 &lt;someuser@invaliddomain&gt; sender rejected : invalid sender domain*</span></span>

    <span data-ttu-id="0b220-200">이 메시지는 `From` 주소가 올바르지 않거나 누락 된 것을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-200">This message can indicate that the `From` address is not correct or is missing.</span></span>
- <span data-ttu-id="0b220-201">*지정 된 문자열이 전자 메일 주소에 필요한 형식이 아닙니다.*</span><span class="sxs-lookup"><span data-stu-id="0b220-201">*The specified string is not in the form required for an email address.*</span></span>

    <span data-ttu-id="0b220-202">이 오류는 `To` 또는 `From` 속성의 값이 전자 메일 주소로 인식 되지 않음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-202">This error might indicate that the value of the `To` or `From` properties are not recognized as email addresses.</span></span> <span data-ttu-id="0b220-203">ASP.NET 전자 메일 주소가 유효한 지, *name@domain.com* 와 같은 올바른 형식 인지 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-203">(ASP.NET cannot check that the email address is valid, only that it's in the correct format, like *name@domain.com*.)</span></span>

> [!NOTE]
> <span data-ttu-id="0b220-204">라이브 사이트에 페이지를 게시 하기 전에 오류 (`@errorMessage`)를 표시 하는 태그를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-204">Remove the markup that displays the error (`@errorMessage`) before you publish the page to a live site.</span></span> <span data-ttu-id="0b220-205">사용자가 서버에서 가져오는 오류 메시지를 볼 수 있도록 하는 것은 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b220-205">It's not a good idea to let users see error messages that you get from a server.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="0b220-206">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0b220-206">Additional Resources</span></span>

[<span data-ttu-id="0b220-207">ASP.NET 웹 페이지(Razor) FAQ</span><span class="sxs-lookup"><span data-stu-id="0b220-207">ASP.NET Web Pages (Razor) FAQ</span></span>](https://go.microsoft.com/fwlink/?LinkId=253000)

<span data-ttu-id="0b220-208">ASP.NET 웹 사이트의 [WebMatrix 및 ASP.NET 웹 페이지](https://forums.asp.net/1224.aspx/1?WebMatrix) 포럼</span><span class="sxs-lookup"><span data-stu-id="0b220-208">[WebMatrix and ASP.NET Web Pages](https://forums.asp.net/1224.aspx/1?WebMatrix) forum on the ASP.NET website</span></span>
