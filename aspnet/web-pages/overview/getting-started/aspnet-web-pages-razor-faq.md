---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET 웹 페이지 (Razor) FAQ | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Razor (ASP.NET 웹 페이지) 및 WebMatrix에 대 한 몇 가지 질문과 대답을 제공 합니다. 자습서에서 사용 되는 소프트웨어 버전 ASP.NET 웹 페이지 (R ...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 6fa1b668e915af856a693e79eafb7180ed504dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520655"
---
# <a name="aspnet-web-pages-razor-faq"></a><span data-ttu-id="ac40b-104">ASP.NET 웹 페이지(Razor) FAQ</span><span class="sxs-lookup"><span data-stu-id="ac40b-104">ASP.NET Web Pages (Razor) FAQ</span></span>

<span data-ttu-id="ac40b-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ac40b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > <span data-ttu-id="ac40b-106">WebMatrix는 ASP.NET 웹 페이지을 위한 통합 개발 환경으로 더 이상 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-106">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="ac40b-107">[Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) 또는 [Visual Studio Code](https://code.visualstudio.com/)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-107">Use [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
>
> <span data-ttu-id="ac40b-108">이 문서에서는 Razor (ASP.NET 웹 페이지) 및 WebMatrix에 대 한 몇 가지 질문과 대답을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-108">This article lists some frequently asked questions about ASP.NET Web Pages (Razor) and WebMatrix.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ac40b-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="ac40b-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="ac40b-110">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="ac40b-110">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="ac40b-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="ac40b-111">Visual Studio 2013</span></span>
> - <span data-ttu-id="ac40b-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="ac40b-112">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="ac40b-113">이 자습서는 ASP.NET 웹 페이지 2, WebMatrix 2 및 Visual Studio 2012 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-113">This tutorial also works with ASP.NET Web Pages 2, WebMatrix 2, and Visual Studio 2012.</span></span>

- [<span data-ttu-id="ac40b-114">ASP.NET 웹 페이지, ASP.NET Web Forms 및 ASP.NET MVC의 차이점은 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-114">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [<span data-ttu-id="ac40b-115">웹 페이지 작업을 위해 WebMatrix가 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-115">Do I need WebMatrix in order to work with Web Pages?</span></span>](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [<span data-ttu-id="ac40b-116">웹 페이지 페이지에서 ASP.NET Web Forms 컨트롤을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-116">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [<span data-ttu-id="ac40b-117">WebMatrix를 사용 하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-117">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [<span data-ttu-id="ac40b-118">로그인을 지원 하기 위해 WebSecurity 도우미를 사용 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-118">Do I have to use the WebSecurity helper to support logins?</span></span>](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [<span data-ttu-id="ac40b-119">HTML5를 지원할 ASP.NET 웹 페이지 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-119">Does ASP.NET Web Pages support HTML5?</span></span>](#Does_ASP.NET_Web_Pages_support_HTML5)
- [<span data-ttu-id="ac40b-120">웹 페이지에서 JavaScript 및 jQuery를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-120">Can I use JavaScript and jQuery with Web Pages?</span></span>](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [<span data-ttu-id="ac40b-121">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ac40b-121">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="ac40b-122">오류 및 기타 문제에 대 한 질문은 [Razor (ASP.NET 웹 페이지) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac40b-122">For questions about errors and other issues, see the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a><span data-ttu-id="ac40b-123">ASP.NET 웹 페이지, ASP.NET Web Forms 및 ASP.NET MVC의 차이점은 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-123">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>

<span data-ttu-id="ac40b-124">세 가지 모두 동적 웹 응용 프로그램을 만들기 위한 ASP.NET 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-124">All three are ASP.NET technologies for creating dynamic web applications:</span></span>

- <span data-ttu-id="ac40b-125">ASP.NET 웹 페이지 HTML 페이지에 대 한 동적 (서버 쪽) 코드 및 데이터베이스 액세스를 추가 하는 데 중점을 둔 단순 및 간단한 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-125">ASP.NET Web Pages focuses on adding dynamic (server-side) code and database access to HTML pages, and features simple and lightweight syntax.</span></span>
- <span data-ttu-id="ac40b-126">ASP.NET Web Forms는 페이지 개체 모델 및 기존 창 형식 컨트롤 (단추, 목록 등)을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-126">ASP.NET Web Forms is based on a page object model and traditional window-type controls (buttons, lists, etc.).</span></span> <span data-ttu-id="ac40b-127">Web Forms은 클라이언트 기반 (Windows Forms) 개발 작업을 수행 하는 사용자에 게 친숙 한 이벤트 기반 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-127">Web Forms uses an event-based model that's familiar to those who've worked with client-based (Windows forms) development.</span></span>
- <span data-ttu-id="ac40b-128">ASP.NET MVC는 ASP.NET에 대 한 모델-뷰-컨트롤러 패턴을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-128">ASP.NET MVC implements the model-view-controller pattern for ASP.NET.</span></span> <span data-ttu-id="ac40b-129">"문제 분리" (처리, 데이터 및 UI 계층)에 중점을 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-129">The emphasis is on "separation of concerns" (processing, data, and UI layers).</span></span>

<span data-ttu-id="ac40b-130">모든 세 프레임 워크는 완전히 지원 되며 ASP.NET 팀에서 계속 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-130">All three frameworks are fully supported and continue to be developed by the ASP.NET team.</span></span> <span data-ttu-id="ac40b-131">일반적으로 사용할 프레임 워크는 ASP.NET의 배경 및 환경에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-131">In general, the choice of which framework to use depends on your background and experience with ASP.NET.</span></span>

<span data-ttu-id="ac40b-132">특히 ASP.NET 웹 페이지는 HTML을 이미 알고 있는 사용자가 페이지에 서버 처리를 추가할 수 있도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-132">ASP.NET Web Pages in particular was designed to make it easy for people who already know HTML to add server processing to their pages.</span></span> <span data-ttu-id="ac40b-133">일반적으로 프로그래밍을 처음 접하는 학생, 취미 직원에 게 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-133">It's a good choice for students, hobbyists, people in general who are new to programming.</span></span> <span data-ttu-id="ac40b-134">Non-ASP.NET 웹 기술을 사용 하는 개발자에 게 적합 한 선택도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-134">It can also be a good choice for developers who have experience with non-ASP.NET web technologies.</span></span>

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a><span data-ttu-id="ac40b-135">웹 페이지 작업을 위해 WebMatrix가 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-135">Do I need WebMatrix in order to work with Web Pages?</span></span>

<span data-ttu-id="ac40b-136">아니요.</span><span class="sxs-lookup"><span data-stu-id="ac40b-136">No.</span></span> <span data-ttu-id="ac40b-137">WebMatrix는 ASP.NET 웹 페이지을 위한 통합 개발 환경으로 더 이상 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-137">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="ac40b-138">[Visual Studio](program-asp-net-web-pages-in-visual-studio.md) 또는 [Visual Studio Code](https://code.visualstudio.com/)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-138">Use [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>

<span data-ttu-id="ac40b-139">Visual Studio 또는 Visual Studio Code을 사용 하지 않으려는 경우 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)를 사용 하 여 구성 요소 제품을 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-139">If you don't want to use either Visual Studio or Visual Studio Code, you can install the component products individually using [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span> <span data-ttu-id="ac40b-140">다음 제품이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-140">You need the following products:</span></span>

- <span data-ttu-id="ac40b-141">Microsoft .NET Framework 4.5도 필요합니다</span><span class="sxs-lookup"><span data-stu-id="ac40b-141">Microsoft .NET Framework 4.5</span></span>
- <span data-ttu-id="ac40b-142">ASP.NET MVC 5 (ASP.NET 웹 페이지 프레임 워크도 설치)</span><span class="sxs-lookup"><span data-stu-id="ac40b-142">ASP.NET MVC 5 (which installs the ASP.NET Web Pages framework as well)</span></span>
- <span data-ttu-id="ac40b-143">IIS Express (웹 서버)</span><span class="sxs-lookup"><span data-stu-id="ac40b-143">IIS Express (the web server)</span></span>
- <span data-ttu-id="ac40b-144">Microsoft SQL Server Compact 4.0 (데이터베이스)</span><span class="sxs-lookup"><span data-stu-id="ac40b-144">Microsoft SQL Server Compact 4.0 (the database)</span></span>

<span data-ttu-id="ac40b-145">텍스트 편집기를 사용 하 여 *. cshtml* (또는 *vbhtml*) 페이지를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-145">You can use a text editor to edit *.cshtml* (or *.vbhtml*) pages.</span></span>

<span data-ttu-id="ac40b-146">도구 없이 SQL Server Compact 데이터베이스 ( *.sdf* 파일)를 관리 하는 것은 약간 더 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-146">Managing SQL Server Compact databases (*.sdf* files) without a tool is a bit harder.</span></span> <span data-ttu-id="ac40b-147">*.Sdf* 데이터베이스를 관리 하기 위한 Visual Studio containds 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-147">Visual Studio containds tools for managing *.sdf* databases.</span></span> <span data-ttu-id="ac40b-148">코드에서 SQL 명령을 실행 하 여 많은 SQL Server 관리 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-148">You can also run SQL commands in code to perform many SQL Server management tasks.</span></span>

<span data-ttu-id="ac40b-149">IDE (통합 개발 환경)를 사용 하지 않고 *cshtml* 페이지를 테스트 하려면 라이브 서버에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-149">To test *.cshtml* pages without using an integrated development environment (IDE), you can deploy them to a live server.</span></span> <span data-ttu-id="ac40b-150">( [WebMatrix를 사용 하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)를 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="ac40b-150">(See [Can I deploy an ASP.NET Web Pages site without using WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))</span></span>

### <a name="running-iis-express-without-using-an-ide"></a><span data-ttu-id="ac40b-151">IDE를 사용 하지 않고 IIS Express 실행</span><span class="sxs-lookup"><span data-stu-id="ac40b-151">Running IIS Express without using an IDE</span></span>

<span data-ttu-id="ac40b-152">컴퓨터에 IIS Express를 웹 서버로 설치 하는 경우이를 사용 하 여 페이지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-152">If you install IIS Express on your computer as a web server, you can use that to test the pages.</span></span> <span data-ttu-id="ac40b-153">명령줄에서 IIS Express를 실행 하 고 특정 포트 번호와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-153">You can run IIS Express from the command line and associate it with a specific port number.</span></span> <span data-ttu-id="ac40b-154">그런 다음 브라우저에서. cshtml 파일을 요청할 때 해당 포트를 지정 *합니다.*</span><span class="sxs-lookup"><span data-stu-id="ac40b-154">You then specify that port when you request *.cshtml* files in your browser.</span></span>

<span data-ttu-id="ac40b-155">Windows에서 관리자 권한으로 명령 프롬프트를 열고 *C:\Program Files\IIS Express로 변경 합니다.*</span><span class="sxs-lookup"><span data-stu-id="ac40b-155">In Windows, open a command prompt with administrator privileges and change to *C:\Program Files\IIS Express.*</span></span> <span data-ttu-id="ac40b-156">64 비트 시스템의 경우 *C:\Program files (x86) \IIS Express* 폴더를 사용 합니다. 그런 후 사이트의 실제 경로를 사용 하 여 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-156">(For 64-bit systems, use the folder *C:\Program Files (x86)\IIS Express.)* Then enter the following command, using the actual path to your site:</span></span>

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

<span data-ttu-id="ac40b-157">다른 프로세스에서 아직 예약 되지 않은 모든 포트 번호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-157">You can use any port number that isn't already reserved by some other process.</span></span> <span data-ttu-id="ac40b-158">1024 이상의 포트 번호는 일반적으로 무료입니다. `path` 값에 대해 파일의 경로를 사용 합니다 *.*</span><span class="sxs-lookup"><span data-stu-id="ac40b-158">(Port numbers above 1024 are typically free.) For the `path` value, use the path of the website folder where the *.cshtml* files are.</span></span>

<span data-ttu-id="ac40b-159">이 명령을 실행 하 여 페이지를 제공 하 IIS Express를 설정한 후에는 브라우저를 열고 *cshtml* 파일로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-159">After you run this command to set up IIS Express to serve your pages, you can open a browser and browse to a *.cshtml* file.</span></span> <span data-ttu-id="ac40b-160">다음과 같은 URL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-160">Use a URL like the following:</span></span>

`http://localhost:35896/default.cshtml`

<span data-ttu-id="ac40b-161">IIS Express 명령줄 옵션에 대 한 도움말을 보려면 명령줄에 `iisexpress.exe /?`를 입력 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ac40b-161">For help with IIS Express command line options, enter `iisexpress.exe /?` at the command line.</span></span>

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a><span data-ttu-id="ac40b-162">웹 페이지 페이지에서 ASP.NET Web Forms 컨트롤을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-162">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>

<span data-ttu-id="ac40b-163">아니요.</span><span class="sxs-lookup"><span data-stu-id="ac40b-163">No.</span></span> <span data-ttu-id="ac40b-164">[CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) 컨트롤, [유효성 검사 컨트롤](https://msdn.microsoft.com/library/bwd43d0x)및 [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) 컨트롤과 같은 Web Forms 컨트롤은 Web Forms 페이지 ( *.aspx* 파일) 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-164">Web Forms controls like the [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) control, the [validation controls](https://msdn.microsoft.com/library/bwd43d0x), and the [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) control only work in Web Forms pages (*.aspx* files).</span></span> <span data-ttu-id="ac40b-165">이러한 컨트롤에는 Web Forms 페이지 프레임 워크가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-165">These controls require the Web Forms page framework.</span></span>

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a><span data-ttu-id="ac40b-166">WebMatrix를 사용 하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-166">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>

<span data-ttu-id="ac40b-167">예.</span><span class="sxs-lookup"><span data-stu-id="ac40b-167">Yes.</span></span> <span data-ttu-id="ac40b-168">웹 사이트 파일을 서버에 수동으로 복사할 수 있습니다 (일반적으로 FTP를 사용 하 여).</span><span class="sxs-lookup"><span data-stu-id="ac40b-168">You can manually copy website files to a server (typically by using FTP).</span></span> <span data-ttu-id="ac40b-169">수동 복사를 수행 하는 경우에는 SQL Server Compact (데이터베이스)를 지 원하는 파일도 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-169">If you perform a manual copy, you also have to copy the files that support SQL Server Compact (the database).</span></span> <span data-ttu-id="ac40b-170">자세한 내용은 [도구 없이 웹 페이지 응용 프로그램 배포](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)블로그 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac40b-170">For details, see the blog entry [Deploying Web Pages applications without a tool](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).</span></span>

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a><span data-ttu-id="ac40b-171">로그인을 지원 하기 위해 WebSecurity 도우미를 사용 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-171">Do I have to use the WebSecurity helper to support logins?</span></span>

<span data-ttu-id="ac40b-172">아니요.</span><span class="sxs-lookup"><span data-stu-id="ac40b-172">No.</span></span> <span data-ttu-id="ac40b-173">ASP.NET 웹 페이지의 일부인 `SimpleMembership` 공급자는 한 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-173">The `SimpleMembership` provider that is part of ASP.NET Web Pages is one option.</span></span> <span data-ttu-id="ac40b-174">ASP.NET의 일부인 보안 공급자 (Web Forms에서 작업 하는 데 사용할 수 있음)도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-174">The security providers that are part of ASP.NET (that you might be used to working with in Web Forms) are also available.</span></span> <span data-ttu-id="ac40b-175">예를 들어 Web Forms에서와 마찬가지로 ASP.NET 웹 페이지에서 폼 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-175">For example, you can use forms authentication in ASP.NET Web Pages just as you would in Web Forms.</span></span> <span data-ttu-id="ac40b-176">폼 인증을 사용 하는 방법의 한 가지 예는 .Net을 [사용 C#하 여 ASP.NET 응용 프로그램에서 폼 기반 인증을 구현 하는 방법](https://support.microsoft.com/kb/301240)Microsoft 지원 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac40b-176">For one example of how to use forms authentication, see the Microsoft Support article [How To Implement Forms-Based Authentication in Your ASP.NET Application by Using C#.NET](https://support.microsoft.com/kb/301240).</span></span> <span data-ttu-id="ac40b-177">간단한 예제를 다운로드 하려면 [ASP.NET version of "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ac40b-177">To download a simple example, see [ASP.NET version of "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).</span></span>

<span data-ttu-id="ac40b-178">Windows 인증을 사용 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 페이지에서 windows 인증을 사용 하](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)는 블로그 게시물을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ac40b-178">For information about how to use Windows authentication, see the blog post [Using Windows authentication in ASP.NET Web Pages](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).</span></span>

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a><span data-ttu-id="ac40b-179">HTML5를 지원할 ASP.NET 웹 페이지 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-179">Does ASP.NET Web Pages support HTML5?</span></span>

<span data-ttu-id="ac40b-180">예.</span><span class="sxs-lookup"><span data-stu-id="ac40b-180">Yes.</span></span> <span data-ttu-id="ac40b-181">ASP.NET 웹 페이지 (*cshtml* 또는 *.* a s l 페이지)를 사용 하 여 만드는 페이지는 기본적으로 페이지가 렌더링 되기 전에 서버에서 실행 되는 코드를 포함 하는 HTML 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-181">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are essentially HTML pages that also contain code that runs on the server, before the page is rendered.</span></span> <span data-ttu-id="ac40b-182">사용자의 브라우저에서 HTML5를 지 원하는 경우에는 *.* s i t 또는 *.* a s l 페이지에서 html5 요소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-182">As long as the user's browser supports HTML5, you can use HTML5 elements in a *.cshtml* or *.vbhtml* page.</span></span>

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a><span data-ttu-id="ac40b-183">웹 페이지에서 JavaScript 및 jQuery를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ac40b-183">Can I use JavaScript and jQuery with Web Pages?</span></span>

<span data-ttu-id="ac40b-184">그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-184">Absolutely.</span></span> <span data-ttu-id="ac40b-185">ASP.NET 웹 페이지 (*cshtml* 또는 *.* a s l 페이지)를 사용 하 여 만든 페이지는 서버 코드를 포함 하는 HTML 페이지 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-185">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are just HTML pages with server code in them.</span></span> <span data-ttu-id="ac40b-186">따라서 JavaScript 또는 jQuery를 사용 하 여 일반 HTML 페이지에서 수행할 수 있는 모든 작업은 *cshtml* 또는 *.* a l l 페이지에서 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-186">Therefore, anything you can do in a normal HTML page by using JavaScript or jQuery you can also do in a *.cshtml* or *.vbhtml* page.</span></span>

<span data-ttu-id="ac40b-187">WebMatrix의 **시작 사이트** 템플릿에는 여러 jQuery 라이브러리가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-187">The **Starter Site** template in WebMatrix contains a number of jQuery libraries.</span></span> <span data-ttu-id="ac40b-188">해당 템플릿을 사용 하 여 사이트를 만드는 경우 *Scripts* 폴더에는 jquery core 라이브러리 (*jquery-1.10.2.min.js 1.6.2)* 와 jquery 유효성 검사를 위한 라이브러리 (*jquery. js*등)가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-188">If you create a site by using that template, the *Scripts* folder contains a jQuery core library (*jquery-1.6.2.js)* and libraries for jQuery validation (*jquery.validate.js*, etc.).</span></span>

<span data-ttu-id="ac40b-189">다음은 ASP.NET 웹 페이지에서 jQuery를 사용 하는 방법을 설명 하는 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="ac40b-189">Here are some blog posts that illustrate ways to use jQuery with ASP.NET Web Pages:</span></span>

- <span data-ttu-id="ac40b-190">[JQuery를 사용 하 여 ASP.NET 웹 페이지에 대 한 JQuery 추가-](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) Rachel Appel에서 WebMatrix 사용</span><span class="sxs-lookup"><span data-stu-id="ac40b-190">[Adding jQuery Goodness to ASP.NET Web Pages using WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) by Rachel Appel</span></span>
- <span data-ttu-id="ac40b-191">[5 분: WebMatrix + JQUERY UI + json + jquery template](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) By Jonas Eriksson</span><span class="sxs-lookup"><span data-stu-id="ac40b-191">[5 min: WebMatrix + jQuery UI + json + jQuery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) by Jonas Eriksson</span></span>
- <span data-ttu-id="ac40b-192">Mike Brind의 [WebMatrix 및 JQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)</span><span class="sxs-lookup"><span data-stu-id="ac40b-192">[WebMatrix And jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) by Mike Brind</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="ac40b-193">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ac40b-193">Additional Resources</span></span>

[<span data-ttu-id="ac40b-194">ASP.NET 웹 페이지(Razor) 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="ac40b-194">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)

<span data-ttu-id="ac40b-195">ASP.NET 웹 사이트의 [WebMatrix 및 ASP.NET 웹 페이지 포럼](https://forums.asp.net/1224.aspx/1?WebMatrix)</span><span class="sxs-lookup"><span data-stu-id="ac40b-195">[WebMatrix and ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix) on the ASP.NET website</span></span>
