---
uid: web-pages/readme/beta3
title: 웹 행렬 및 ASP.NET 웹 페이지 (Razor) Beta 3 릴리스 추가 정보 | Microsoft Docs
author: rick-anderson
description: WebMatrix 및 ASP.NET 웹 페이지(Razor) 베타 3 릴리스 추가 정보
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510341"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="98281-103">WebMatrix 및 ASP.NET 웹 페이지(Razor) 베타 3 릴리스 추가 정보</span><span class="sxs-lookup"><span data-stu-id="98281-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

> <span data-ttu-id="98281-104">WebMatrix 및 ASP.NET 웹 페이지(Razor) 베타 3 릴리스 추가 정보</span><span class="sxs-lookup"><span data-stu-id="98281-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="98281-105">9 11 월 2010</span><span class="sxs-lookup"><span data-stu-id="98281-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="98281-106">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="98281-106">Contents</span></span>

- [<span data-ttu-id="98281-107">개요</span><span class="sxs-lookup"><span data-stu-id="98281-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="98281-108">설치</span><span class="sxs-lookup"><span data-stu-id="98281-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="98281-109">베타 3 릴리스의 새로운 기능, 변경 사항 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="98281-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="98281-110">WebMatrix 설치 문제</span><span class="sxs-lookup"><span data-stu-id="98281-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="98281-111">ASP.NET 웹 페이지 2</span><span class="sxs-lookup"><span data-stu-id="98281-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="98281-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="98281-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="98281-113">응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="98281-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="98281-114">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="98281-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="98281-115">기타 문제</span><span class="sxs-lookup"><span data-stu-id="98281-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="98281-116">자세한 내용</span><span class="sxs-lookup"><span data-stu-id="98281-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="98281-117">개요</span><span class="sxs-lookup"><span data-stu-id="98281-117">Overview</span></span>

> <span data-ttu-id="98281-118">Microsoft WebMatrix Beta는 몇 분 안에 설치 되는 무료 웹 개발 스택입니다.</span><span class="sxs-lookup"><span data-stu-id="98281-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="98281-119">웹 서버를 데이터베이스 및 프로그래밍 프레임 워크와 통합 하 여 통합 된 단일 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98281-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="98281-120">WebMatrix Beta를 사용 하 여 사용자 고유의 ASP.NET 또는 PHP 웹 사이트를 코딩, 테스트 및 게시 하는 방법을 간소화 하거나 WebMatrix Beta를 사용 하 여 DotNetNuke, Umbraco, WordPress 또는 Joomla와 같은 인기 있는 오픈 소스 앱을 사용 하 여 새 웹 사이트를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="98281-121">WebMatrix 베타는 인터넷에서 웹 사이트를 실행 하는 동일한 강력한 웹 서버, 데이터베이스 엔진 및 프레임 워크 환경을 사용 하며,이를 통해 개발 환경에서 프로덕션 환경으로 원활 하 고 원활 하 게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="98281-122">설치</span><span class="sxs-lookup"><span data-stu-id="98281-122">Installation</span></span>

> <span data-ttu-id="98281-123">WebMatrix 베타 3을 설치 하려면 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="98281-124">웹 플랫폼 설치 관리자를 설치한 후 WebMatrix 베타 3을 설치 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="98281-125">설치 하는 동안 문제가 발생 하는 경우 [Microsoft 웹 플랫폼 설치 관리자 문제 해결](https://go.microsoft.com/fwlink/?LinkId=196212)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="98281-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="98281-126">응용 프로그램 게시에 대 한 지침</span><span class="sxs-lookup"><span data-stu-id="98281-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="98281-127">[응용 프로그램 게시에 대 한 단계별 지침](https://go.microsoft.com/fwlink/?LinkID=196149) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="98281-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="98281-128">새로운 기능, 변경 사항 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="98281-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="98281-129">WebMatrix 베타 3 설치</span><span class="sxs-lookup"><span data-stu-id="98281-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="98281-130">문제: WebMatrix 베타 3은 Microsoft .NET Framework 4를 지 원하는 플랫폼 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="98281-131">WebMatrix 베타에 .NET Framework 버전 4가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="98281-132">경우에 따라 WebMatrix 베타 설치 관리자를 사용 하 여 지원 되는 구성 집합의 일부가 아닌 플랫폼에을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="98281-133">특히 SP1 업데이트가 설치 되지 않은 Windows Vista에서는 WebMatrix 베타 설치를 시작할 수 있지만 .NET Framework 4 구성 요소는 실패 하 고 설치를 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="98281-134">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-134">**Workaround**</span></span>  
> <span data-ttu-id="98281-135">지원 되는 플랫폼에을 설치 합니다. 여기에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="98281-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="98281-136">Windows 7</span></span>
> - <span data-ttu-id="98281-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="98281-137">Windows Server 2008</span></span>
> - <span data-ttu-id="98281-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="98281-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="98281-139">Windows Vista SP1 이상</span><span class="sxs-lookup"><span data-stu-id="98281-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="98281-140">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="98281-140">Windows XP SP3</span></span>
> - <span data-ttu-id="98281-141">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="98281-141">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="98281-142">문제: Microsoft Visual Studio 2008 s p 1 없이 Microsoft Visual Studio 2008가 설치 된 경우 WebMatrix 베타 3을 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="98281-143">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-143">**Workaround**</span></span>  
> <span data-ttu-id="98281-144">Microsoft 다운로드 센터에서 [Microsoft Visual Studio 2008](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) s p 1을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="98281-145">문제: SQL Server Compact 4.0에 대 한 일부 어셈블리가 GAC에 설치 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="98281-146">SQL Server Compact 4.0에 대 한 관리 되는 어셈블리는 64 비트 컴퓨터에 SQL Server Compact 4.0를 설치할 때 GAC (전역 어셈블리 캐시)에 배치 되지 않고 컴퓨터에 .NET Framework 3.5 SP1 클라이언트 프로필만 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="98281-147">GAC에 설치 되지 않은 관리 되는 어셈블리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="98281-148">*System.data.sqlserverce* (ADO.NET provider)</span><span class="sxs-lookup"><span data-stu-id="98281-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="98281-149">*System.data.sqlserverce* (ADO.NET Entity Framework).</span><span class="sxs-lookup"><span data-stu-id="98281-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="98281-150">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-150">**Workaround**</span></span>  
> <span data-ttu-id="98281-151">SQL Server Compact 4.0를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="98281-152">다음 위치에서 .NET Framework 3.5 s p 1의 전체 버전을 다운로드 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="98281-153">Microsoft .NET Framework 3.5 서비스 팩 1 (전체 패키지)</span><span class="sxs-lookup"><span data-stu-id="98281-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="98281-154">그런 다음 SQL Server Compact 4.0을 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-154">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="98281-155">문제: 명령줄을 사용 하 여 SQL Server Compact를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="98281-156">명령줄 옵션을 사용 하는 SQL Server Compact 제거는이 릴리스에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="98281-157">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-157">**Workaround**</span></span>  
> <span data-ttu-id="98281-158">Windows 제어판의 *프로그램 및 기능* 을 사용 하 여 Microsoft SQL Server Compact 4.0를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="98281-159">ASP.NET 웹 페이지</span><span class="sxs-lookup"><span data-stu-id="98281-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="98281-160">이 문서의 섹션에서는 Razor 구문와 함께 ASP.NET 웹 페이지 베타 3 릴리스의 새로운 기능, 변경 사항 및 알려진 문제에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="98281-161">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="98281-161">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="98281-162">변경</span><span class="sxs-lookup"><span data-stu-id="98281-162">Changes</span></span>](#Changes)
- [<span data-ttu-id="98281-163">문제</span><span class="sxs-lookup"><span data-stu-id="98281-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="98281-164">Razor 구문을 사용 하는 ASP.NET 웹 페이지에 대 한 Beta 3의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="98281-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="98281-165">New: "Html.actionlink" 메서드는 인코딩되지 않은 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="98281-166">새 `Html.Raw` 메서드를 사용 하면 인코딩된 출력을 렌더링 하는 대신 HTML 태그를 태그로 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="98281-167">기본적으로 ASP.NET Razor는 렌더링 하기 전에 문자열을 인코딩합니다. 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="98281-168">다음 예제에서는 `Html.Raw`을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98281-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="98281-169">Razor 구문을 사용 하는 ASP.NET 웹 페이지에 대 한 베타 3의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="98281-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="98281-170">변경: "HrefAttribute" 메서드가 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="98281-171">`WebPage` 클래스의 `HrefAttribute` 메서드가 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="98281-172">이 도우미는 Url에서 안전 하지 않은 문자를 인코딩하는 데 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="98281-173">ASP.NET Razor는 문자열을 자동으로 인코드 하므로 더 이상 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="98281-174">새 `Html.Raw` 메서드를 사용 하 여 인코딩되지 않은 문자열을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="98281-175">Change: 선언적 "@helper" 도우미의 구문이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="98281-176">Beta 3 릴리스에서 ASP.NET는 `@helper` 구문을 사용 하 여 만든 도우미를 구문 분석 하는 방법을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="98281-177">기본적으로 `@helper` 구문은 이제 코드를 포함할 수 있는 태그 블록이 아니라 코드 블록으로 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="98281-178">따라서 도우미 내의 코드는 `@{ }` 블록으로 묶을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="98281-179">반대로 도우미 내부의 태그는 HTML 요소나 ASP.NET Razor `<text></text>` 태그에 명시적으로 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="98281-180">예를 들어 베타 3 릴리스에서는 다음과 같은 `@helper` 구문이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="98281-181">베타 3 릴리스에서는 다음 예와 같이이 도우미를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="98281-182">도우미에서 초기 코드 주위의 `@{ }` 문자는 더 이상 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="98281-183">이는 도우미의 내용이 기본적으로 코드 블록으로 처리 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="98281-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="98281-184">도우미는 여는 `<a>` 태그로 시작 하는 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="98281-185">도우미가 닫는 태그 (예: `<meta>` 태그)를 포함 하지 않는 일반 텍스트 또는 태그를 렌더링 해야 하는 경우 렌더링할 콘텐츠가 `<text></text>` 태그에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>

#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="98281-186">변경: "WebPageContext" 제거 됨</span><span class="sxs-lookup"><span data-stu-id="98281-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="98281-187">`WebPageContext.HttpContext` 속성이 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="98281-188">대신 `HttpContext.Current`를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="98281-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="98281-189">`WebPageContext.HttpContext` 속성은 간단히이를 래핑 했습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>

#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="98281-190">변경: "Facebook" 도우미가 새 패키지로 이동 됨</span><span class="sxs-lookup"><span data-stu-id="98281-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="98281-191">`Facebook` 도우미가 `Facebook` 도우미 및 추가 기능을 포함 하는 *Facebook* 라이브러리로 이동 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="98281-192">[ASP.NET 시작 페이지](https://go.microsoft.com/fwlink/?LinkId=202889)의 "패키지 관리자를 사용 하 여 도우미 설치"에 설명 된 대로이 라이브러리를 별도의 패키지로 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="98281-193">변경: 멤버 자격, 역할 및 보안 유형이 새 어셈블리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="98281-194">다음 형식이 `WebMatrix.WebData` 어셈블리로 이동 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="98281-195">Change: "빌드하는 tagbuilder" 클래스가 System.object로 이동 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="98281-196">`TagBuilde` r 클래스가 System.web. 웹 페이지 .dll 어셈블리로 이동 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="98281-197">이전에는 ASP.NET MVC의 일부인 어셈블리에 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="98281-198">이 변경은 `TagBuilder` 클래스를 사용 하기 위해 ASP.NET MVC를 설치할 필요가 없음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="98281-199">그러나 클래스는 여전히 `System.Web.Mvc` 네임 스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="98281-200">사용자 지정 ASP.NET Razor 도우미와 같은 `TagBuilder` 클래스를 사용 하려면 네임 스페이스를 참조 해야 합니다. 예를 들어 코드에 `@using System.Web.Mvc`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="98281-201">변경: 요청 유효성 검사 구문이 변경 되었습니다. "유효성 검사" 클래스 제거 됨</span><span class="sxs-lookup"><span data-stu-id="98281-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="98281-202">베타 3 릴리스에서 개별 필드 또는 필드 집합에 대 한 유효성 검사를 사용 하지 않도록 설정 하려면 `Validation.Exclude` 메서드를 호출 하 여 유효성 검사에서 제외할 필드의 이름 또는 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="98281-203">베타 3 릴리스에서는 유효성 검사를 무시 하는 새 구문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="98281-204">Beta 3에서 사용 되는 `Validation` 메서드가 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="98281-205">요청 유효성 검사를 사용 하지 않도록 설정 하지 않으면 사용자가 HTML 태그를 업로드 하려고 할 때 (예: 페이지에서 서식 있는 텍스트 편집기 사용) 웹 사이트에서 잠재적으로 위험한 요청 등의 오류를 보고 *합니다. 클라이언트에서 양식 값이 검색* 되 고 사용자 입력이 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="98281-206">요청 유효성 검사를 사용 하지 않도록 설정 하는 경우 사용자 입력을 수동으로 확인 하 여 [Microsoft 사이트 간 스크립팅 라이브러리 v 4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)과 같은 기능을 사용 하는 잠재적으로 위험한 태그나 스크립트가 포함 되지 않았는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="98281-207">자동 요청 유효성 검사를 사용 하지 않도록 설정 하려면 `Request.Unvalidated` 메서드를 호출 하 여 요청 유효성 검사를 무시 하려는 필드 또는 다른 게시 개체의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="98281-208">이 메서드를 사용 하 여 `Form`, `QueryString`, `Cookies`및 `ServerVariables` 컬렉션에 있는 항목에 대 한 유효성 검사를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="98281-209">다음 예에서는 `Unvalidated` 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98281-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="98281-210">Razor 구문을 사용한 ASP.NET 웹 페이지의 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="98281-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="98281-211">문제: 멤버 자격에 사용자 지정 사용자 테이블을 사용할 때 예기치 않은 동작이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="98281-212">ASP.NET Razor 웹 사이트의 멤버 자격 공급자를 초기화 하려면 `WebSecurity.InitializeDatabaseConnection` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="98281-213">(WebMatrix에서 스타터 사이트 템플릿은 *\_AppStart* 파일에이 메서드에 대 한 호출을 포함 합니다.) 이 메서드의 `autoCreateTables` 매개 변수가 true로 설정 되어 있으면 (기본적으로 시작 사이트 템플릿에서 true로 설정 됨) 인식할 수 없는 테이블 이름이 메서드에 전달 되는 경우 (두 번째 매개 변수) 메서드는 오류를 throw 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="98281-214">대신 테이블을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98281-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="98281-215">멤버 자격에 사용자 지정 사용자 테이블을 사용 하지만 잘못 된 테이블 이름을 `WebSecurity.InitializeDatabaseConnection` 메서드에 전달 하려는 경우에이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="98281-216">사용자가 지정 하는 테이블이 존재 하지 않는 경우 메서드는 기본적으로 오류를 발생 시 키 지 않으며 대신 새 테이블을 만드는 경우 응용 프로그램이 작동 하는 것 처럼 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="98281-217">그러나 사용자 지정 사용자 테이블을 사용 하는 응용 프로그램 코드 (및 그 안에 포함 된 필드)는 결국 예기치 않은 오류로 인해 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="98281-218">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-218">**Workaround**</span></span>  
> <span data-ttu-id="98281-219">`InitializeDatabaseConnection` 메서드에 전달 된 이름이 멤버 자격 데이터베이스의 사용자 프로필 테이블과 일치 하는지 확인 하거나 `autoCreateTables` 매개 변수가 false로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="98281-220">문제: "SQL Server 사용자 인스턴스를 생성 하지 못했습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="98281-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="98281-221">WebMatrix 웹 응용 프로그램이 SQL Server Express를 사용 하 고 Windows 7 또는 Windows Server 2008 r 2에서 IIS 7.5를 실행 하는 경우 SQL Server에서 사용자의 로컬 응용 프로그램 경로를 런타임에 검색할 수 없음을 나타내는 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="98281-222">**해결 방법** 응용 프로그램이 실행 되는 Windows 계정 (일반적으로 NETWORK SERVICE)에 응용 프로그램의 루트 폴더와 *앱\_데이터*와 같은 하위 폴더에 대 한 읽기/쓰기 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="98281-223">자세한 내용은 기술 자료 문서 [SQL Server Express 사용자 인스턴스 및 ASP.net 웹 응용 프로그램 프로젝트 문제](https://support.microsoft.com/kb/2002980)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="98281-224">문제: Visual Studio에서 사용자 지정 어셈블리 (Dll)의 네임 스페이스를 자동으로 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="98281-225">Visual Studio의 프로젝트에서 사용자 지정 어셈블리를 사용 하는 경우 해당 어셈블리에 선언 된 네임 스페이스는 디자인 타임에 자동으로 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="98281-226">따라서 사용자 지정 형식에 대 한 참조가 디자인 타임에 인식 되지 않을 수 있으며 Visual Studio에서 인식 되지 않는 것으로 표시 됩니다 ("물결선" 사용).</span><span class="sxs-lookup"><span data-stu-id="98281-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="98281-227">이 문제는 Visual Studio의 디자인 타임에만 발생 합니다. 응용 프로그램 자체는 정상적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="98281-228">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-228">**Workaround**</span></span>  
> <span data-ttu-id="98281-229">디자인 타임에 인식 되지 않는 엔터티를 참조 하는 `using` 문 (Visual Basic의`imports`)을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="98281-230">문제: Visual Studio IntelliSense 및 프로젝트 템플릿은 ASP.NET MVC 버전 3 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="98281-231">ASP.NET 웹 페이지를 설치 해도 ASP.NET 웹 페이지 응용 프로그램용 IntelliSense 및 프로젝트 템플릿과 같은 Visual Studio 용 도구도 설치 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="98281-232">**해결 방법** Visual Studio에서 ASP.NET 웹 페이지 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿을 사용 하려면 웹 플랫폼 설치 관리자 또는 [독립 실행형 설치 관리자](https://go.microsoft.com/fwlink/?LinkID=191797)를 통해 ASP.NET MVC 3 RC를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="98281-233">문제: "&lt;도우미&gt; 클래스를 찾을 수 없습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="98281-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="98281-234">베타 3으로 업그레이드 한 후에는 도우미 클래스 (예: `Facebook` 클래스)를 찾을 수 없다는 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="98281-235">Beta 2부터 시작 하 여 베타 3에서 계속 하면 도우미가 명시적으로 설치 해야 하는 패키지로 이동 했습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="98281-236">기존 사이트는 이러한 패키지를 포함 하도록 업그레이드 되지 않습니다. 여기에는 *\My Documents\IISExpress* 또는 *\My Documents\My 웹 사이트* 폴더의 사이트가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="98281-237">특히 `Twitter` 도우미에 대 한 참조를 포함 하는 *내 사이트* (WebSite1)에서 기본 사이트를 사용 하는 경우이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="98281-238">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-238">**Workaround**</span></span>  
> <span data-ttu-id="98281-239">사이트의 모든 도우미에 대 한 호출을 주석으로 처리 하 고 *\_관리* 페이지를 실행 한 다음 사용 하려는 도우미가 포함 된 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="98281-240">패키지를 설치한 후에는 도우미를 참조 하는 줄의 주석 처리를 제거 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="98281-241">문제: 호스트 사이트에서 베타 3 ASP.NET Razor 어셈블리를 Bin 폴더에 배포 하는 작업이 작동 하지 않을 수 있음</span><span class="sxs-lookup"><span data-stu-id="98281-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="98281-242">호스팅 사이트에 ASP.NET 웹 페이지 웹 사이트를 배포 하 고 사이트의 *Bin* 폴더에 ASP.NET Razor Beta 3 어셈블리를 배포 하는 경우 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="98281-243">이 문제는 호스팅 공급자가 서버의 GAC (전역 응용 프로그램 캐시)에 ASP.NET 웹 페이지 Beta 1 어셈블리를 설치한 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="98281-244">GAC의 어셈블리는 *Bin* 폴더에 로컬로 설치 된 어셈블리 보다 우선적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="98281-245">**해결 방법** 호스팅 공급자에 게 문의 하 여 발생 한 오류가 공급자의 어셈블리 버전과 사용자의 어셈블리 버전 간 충돌로 인 한 것인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="98281-246">이 경우 호스팅 공급자가 서버의 GAC에서 어셈블리를 업데이트 하도록 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="98281-247">문제: 프록시 서버를 통해 피드 또는 기타 외부 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="98281-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="98281-248">사이트를 실행 하는 서버가 프록시 서버 뒤에 있는 경우 사이트 외부에서 제공 되는 정보를 읽을 수 있도록 *web.config 파일에서* 프록시 정보를 구성 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="98281-249">예를 들어 `ReCaptcha` 도우미를 사용 하는 경우 도우미가 reCAPTCHA 서비스와 통신 하지만 프록시 서버에 의해 차단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="98281-250">마찬가지로 패키지 관리자에서 사용 하는 피드와 같이 ASP.NET 웹 페이지에 사용 되는 피드에는 프록시 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="98281-251">외부 서비스를 사용 하거나 패키지 피드를 사용 하 여 작업 하는 데 문제가 발생 하는 경우 응용 프로그램의 루트 web.config 파일에 다음 요소를 *추가 합니다.*</span><span class="sxs-lookup"><span data-stu-id="98281-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="98281-252">프록시 서버를 구성 하는 방법에 대 한 자세한 내용은 MSDN 웹 사이트에서 [&lt;프록시&gt; 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) 를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="98281-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="98281-253">문제: "Microsoft web.config .dll을 로드할 수 없습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="98281-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="98281-254">이전에 Razor 구문를 사용 하 여 ASP.NET 웹 페이지 베타 1 버전을 설치 하 고 베타 3 버전을 설치 하는 경우에는 해당 하는 모든 어셈블리가 *Microsoft web.config*를 제외 하 고 GAC에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="98281-255">결과적으로 ASP.NET Razor 페이지를 실행할 때 *Microsoft web.config .dll* 을 로드할 수 없음을 나타내는 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="98281-256">클린 컴퓨터에서 베타 3 릴리스를 로드 한 경우에는이 문제가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="98281-257">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-257">**Workaround**</span></span>  
> <span data-ttu-id="98281-258">제어판에서 ASP.NET 웹 페이지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="98281-259">그런 다음 베타 3 릴리스를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-259">Then reinstall the Beta 3 release.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="98281-260">문제: .NET Framework 버전 4를 제거 하면 Razor 구문을 사용 하 여 ASP.NET 웹 페이지 사용 하지 않도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="98281-261">.NET Framework 버전 4를 제거한 후 다시 설치 하는 경우 Razor 구문 사용 하지 않도록 설정 된 ASP.NET 웹 페이지.</span><span class="sxs-lookup"><span data-stu-id="98281-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="98281-262">확장명이 *cshtml* 인 페이지는 올바르게 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="98281-263">ASP.NET 웹 페이지는 컴퓨터 루트 *web.config* 파일에 어셈블리를 등록 하 고 .NET Framework 제거 하면 해당 파일이 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="98281-264">.NET Framework를 다시 설치 하면 새 버전의 구성 파일이 설치 되지만 ASP.NET 웹 페이지 어셈블리에 대 한 참조는 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="98281-265">**해결 방법** .NET Framework를 다시 설치한 후 Razor 구문를 사용 하 여 ASP.NET 웹 페이지를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="98281-266">그러면 다음 요소가 컴퓨터 루트의 web.config *파일에* 추가 됩니다 .이 파일은 일반적으로 다음 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="98281-267">문제: Bin 폴더에 ASP.NET 어셈블리를 사용 하 여 이전에 배포한 응용 프로그램에서 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="98281-268">배포 하는 동안 ASP.NET 웹 페이지 어셈블리 (예: *Microsoft. 웹 페이지*)의 복사본은 서버에 있는 웹 사이트의 *Bin* 폴더에 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="98281-269">이는 배포 중에 자동으로 발생 하거나 개발자가 어셈블리를 명시적으로 복사한 경우에 발생할 수 있습니다. 그러나 베타 3 릴리스가 설치 될 때 특정 유형을 찾을 수 없다는 오류와 같은 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="98281-270">이는 여러 ASP.NET 웹 페이지 형식이 Beta 3 릴리스에 대 한 다른 네임 스페이스로 이동 되었기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="98281-271">**해결 방법** </span><span class="sxs-lookup"><span data-stu-id="98281-271">**Workaround** </span></span>  
> <span data-ttu-id="98281-272">배포 된 응용 프로그램의 *Bin* 폴더를 지우고 새 어셈블리를 폴더에 복사 하거나 응용 프로그램을 다시 배포 하 고 응용 프로그램을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="98281-273">문제: 확장명 없는 Url은 IIS 7 또는 IIS 7.5에 있는 cshtml/. a s d 파일을 찾지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="98281-274">IIS 7 또는 IIS 7.5에서는 다음과 같은 URL을 사용 하는 요청이 *확장명이. n e t 또는* *.* n e t 인 페이지를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="98281-275">URL 다시 쓰기는 IIS 7 또는 IIS 7.5에 대해 기본적으로 사용 되지 않기 때문에 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="98281-276">Likeliest를 사용 하 IIS Express 여 로컬로 테스트 하는 경우에는 문제가 표시 되지 않지만 호스팅 웹 사이트에 웹 사이트를 배포할 때이 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="98281-277">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="98281-278">서버 컴퓨터를 제어 하는 경우 서버 컴퓨터에서 업데이트에 설명 된 업데이트를 설치할 수 있습니다. [그러면 특정 iis 7.0 또는 iis 7.5 처리기에서 url이 마침표로 끝나지 않는 요청을 처리할 수 있습니다](https://support.microsoft.com/kb/980368).</span><span class="sxs-lookup"><span data-stu-id="98281-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="98281-279">서버 컴퓨터를 제어할 수 없는 경우 (예: 호스팅 웹 사이트에 배포 하는 경우) 웹 사이트의 *web.config* 파일에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="98281-280">문제: 웹 응용 프로그램 프로젝트 또는 ASP.NET MVC를 사용 하 고 동일한 응용 프로그램에서 웹 페이지 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="98281-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="98281-281">웹 응용 프로그램 프로젝트 또는 ASP.NET MVC 응용 프로그램에서 ASP.NET 웹 페이지를 사용 하는 경우 *WebPageHttpApplication* 를 찾을 수 없다는 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="98281-282">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-282">**Workaround**</span></span>  
> <span data-ttu-id="98281-283">이 오류가 발생 하는 경우 응용 프로그램이 파생 되는 기본 클래스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="98281-284">*Global.asax* 파일에서 다음 줄을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="98281-285">값:</span><span class="sxs-lookup"><span data-stu-id="98281-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="98281-286">이는 Razor 구문와 ASP.NET 웹 페이지 베타 1 릴리스에 대해 도입 된 변경 내용을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="98281-287">문제: SQL Server Compact 설치 되지 않은 컴퓨터에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="98281-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="98281-288">SQL Server Compact 데이터베이스를 포함 하는 응용 프로그램은 SQL Server Compact가 설치 되지 않은 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="98281-289">Microsoft WebMatrix 베타 3은 이러한 이진 파일을 자동으로 복사 하 고 *적절 한* web.config 파일 변환을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="98281-290">**해결 방법** 이러한 파일을 복사 하 고 *web.config 파일을* 수동으로 변경 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="98281-291">대상 컴퓨터에 있는 응용 프로그램의 *Bin* 폴더 (및 하위 폴더)에 데이터베이스 엔진 어셈블리를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="98281-292">*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **를** *\bin* 에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="98281-293">*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* \* **를** *\Bin\x86* 에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="98281-294">*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \* **를** *\Bin\amd64* 에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="98281-295">*웹* 사이트의 루트 폴더에서 web.config 파일을 만들거나 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98281-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="98281-296">(WebMatrix 베타 3에서는 **파일 형식 선택** 대화 상자에서 **모두** 를 클릭 하는 경우이 파일 형식을 사용할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="98281-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="98281-297">다음 요소를 **&lt;system.web&gt;** 요소 내부가 아닌 **&lt;구성&gt;** 요소의 자식으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="98281-298">문제: 데이터베이스 및 WebGrid 도우미가 Visual Basic의 보통 신뢰에서 작동 하지 않음</span><span class="sxs-lookup"><span data-stu-id="98281-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="98281-299">Visual Basic를 사용 하는 경우 ( *vbhtml* 파일 만들기) 응용 프로그램이 보통 신뢰를 사용 하도록 설정 된 경우 `Database` 및 `WebGrid` 도우미가 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="98281-300">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-300">**Workaround**</span></span>  
> <span data-ttu-id="98281-301">완전 신뢰를 사용 하도록 응용 프로그램을 일시적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="98281-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="98281-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="98281-303">문제: "Encrypt" 속성이 인식 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="98281-304">SQL Server Compact 4.0는 `SqlCeConnection` 클래스의 `Encrypt` 속성을 인식 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="98281-305">데이터베이스 파일을 암호화 하는 데이 속성을 사용 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="98281-306">`Encrypt` 속성은 SQL Server Compact 3.5 릴리스에서 사용 되지 않으며 이전 버전과의 호환성을 위해서만 유지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="98281-307">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-307">**Workaround**</span></span>  
> <span data-ttu-id="98281-308">`SqlCeConnection` 클래스의 `Encryption Mode` 속성을 사용 하 여 SQL Server Compact 4.0 데이터베이스 파일을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="98281-309">다음 예에서는 `Encryption Mode` 속성을 사용 하 여 암호화 된 SQL Server Compact 4.0 데이터베이스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98281-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="98281-310">기존 SQL Server Compact 4.0 데이터베이스의 암호화 모드를 변경 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="98281-311">암호화 되지 않은 SQL Server Compact 4.0 데이터베이스를 암호화 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="98281-312">문제: Microsoft Visual C++ 2008 런타임 라이브러리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="98281-313">SQL Server Compact 4.0의 네이티브 Dll에는 Microsoft Visual C++ 2008 런타임 라이브러리 (X86, IA64 및 X64) 서비스 팩 1이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="98281-314">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-314">**Workaround**</span></span>  
> <span data-ttu-id="98281-315">.NET Framework 3.5 SP1을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="98281-316">또한 Visual C++ 2008 런타임 라이브러리 s p 1을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="98281-317">다음 위치에서 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="98281-318">Microsoft Visual C++ 2008 서비스 팩 1 재배포 가능 패키지 ATL 보안 업데이트</span><span class="sxs-lookup"><span data-stu-id="98281-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="98281-319">2\.0, 3.0 또는 4 .NET Framework 설치 하는 경우 Visual C++ 2008 런타임 라이브러리 s p 1이 설치 *되지* 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="98281-320">문제: 컴퓨터에 .NET Framework를 설치 하기 전에 SQL Server Compact 설치 된 경우 공급자 고정 이름이 .NET Framework machine.config 파일에 등록 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="98281-321">SQL Server Compact에는 .NET Framework가 필요 하기 때문에 .NET Framework가 설치 되지 않은 컴퓨터에 SQL Server Compact를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="98281-322">SQL Server Compact를 설치 하기 전에 .NET Framework 버전 3.5 또는 4를 모두 설치 하지 않은 경우에는 SQL Server Compact 설치 프로그램이 *machine.config 파일에* 공급자 고정 이름을 등록 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="98281-323">*Machine.config 파일의* SQL Server Compact 항목에 의존 하는 모든 응용 프로그램은 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="98281-324">*Machine.config의 고정* 이름 등록 항목은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="98281-325">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-325">**Workaround**</span></span>  
> <span data-ttu-id="98281-326">SQL Server Compact 4.0 CTP1을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="98281-327">다음 위치에서 .NET Framework의 전체 버전을 다운로드 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="98281-328">Microsoft .NET Framework 3.5 서비스 팩 1 (전체 패키지)</span><span class="sxs-lookup"><span data-stu-id="98281-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="98281-329">Microsoft .NET Framework 4.0 릴리스 (전체 패키지)</span><span class="sxs-lookup"><span data-stu-id="98281-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="98281-330">그런 다음 [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="98281-331">애플리케이션 설치</span><span class="sxs-lookup"><span data-stu-id="98281-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="98281-332">문제: 사용자의 내 문서 폴더가 네트워크 공유로 리디렉션되는 경우 응용 프로그램을 설치 하는 데 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="98281-333">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-333">**Workaround**</span></span>  
> <span data-ttu-id="98281-334">없음</span><span class="sxs-lookup"><span data-stu-id="98281-334">None.</span></span> <span data-ttu-id="98281-335">응용 프로그램을 설치 하는 데 약간의 시간이 걸릴 수 있지만 제대로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-335">The application might take a while to install, but will install correctly.</span></span>

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="98281-336">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="98281-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="98281-337">문제: 사이트 "대상 URL" 필드는 http:// 또는 https:// 로 시작 하지 않는 경우 게시 한 후 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="98281-338">**게시 설정** 대화 상자에서 대상 URL이 `http://` 또는 `https://`으로 시작 하지 않는 경우 배포 후 사이트가 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="98281-339">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-339">**Workaround**</span></span>  
> <span data-ttu-id="98281-340">사이트를 게시 하기 전에 **게시 설정** 대화 상자의 대상 URL은 `http://` 또는 `https://`으로 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="98281-341">문제: "데이터베이스를 게시 하지 못했습니다." 오류가 발생 하 여 MySQL 데이터베이스를 게시 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="98281-342">이 문제는 원격 데이터베이스에서 스크립트를 실행할 수 없는 경우 발생할 수 있습니다. "</span><span class="sxs-lookup"><span data-stu-id="98281-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="98281-343">이 오류는 여러 가지 이유로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="98281-344">데이터베이스 스크립트에 작은따옴표 (')가 포함 되어 있고 대상 MySQL 데이터베이스의 기본 문자 집합이 u t f-8이 아닌 경우이 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="98281-345">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-345">**Workaround**</span></span>  
> <span data-ttu-id="98281-346">원격 MySQL 데이터베이스의 기본 문자 집합을 u t f-8로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="98281-347">기타 이슈</span><span class="sxs-lookup"><span data-stu-id="98281-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="98281-348">문제: 검색/필터가 Group By에 대 한 보고서: 문제 유형에서 작동 하지 않음</span><span class="sxs-lookup"><span data-stu-id="98281-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="98281-349">사이트에 대 한 보고서를 실행할 때 *URL로 필터링* 상자에 텍스트를 입력 하 고 *검색*을 클릭 하면 아무 일도 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="98281-350">이는 보고서의 *Group By* 상태가 *Issue 유형*(기본값)으로 설정 되어 있는 동안이 컨트롤이 작동 하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="98281-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="98281-351">**해결 방법** 리본 메뉴의 *그룹화* 방법 탭에서 *url* 을 클릭 하 여 원본 url로 항목을 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="98281-352">이 상태에서 항목을 필터링 하는 텍스트 상자와 단추가 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-352">The text box and button to filter the entries are functional while in this state.</span></span>

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="98281-353">문제: IIS Express 사용 하 여 WCF 응용 프로그램을 실행 하지 못함</span><span class="sxs-lookup"><span data-stu-id="98281-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="98281-354">WCF 응용 프로그램을 탐색 하면 다음과 같은 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="98281-355">*파일이 나 어셈블리 ' 7.0.0.0, Version =, Culture = 중립, PublicKeyToken = 31bf3856ad364e35 ' 또는 해당 종속성 중 하나를 로드할 수 없습니다. 시스템에서 지정 된 파일을 찾을 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="98281-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="98281-356">이는 IIS Express 베타 버전이 기본적으로 WCF를 지원 하지 않기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="98281-357">**해결 방법** 다음 해결 방법 중 하나를 사용 합니다 (해결 방법 #2 Microsoft Windows Vista 이상이 필요 함).</span><span class="sxs-lookup"><span data-stu-id="98281-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="98281-358">WebMatrix 설치 위치에서 WCF 응용 프로그램의 *bin* 디렉터리에 *Microsoft Web.config* 및 *microsoft web.config .dll* 어셈블리를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="98281-359">기본적으로 WebMatrix는 시스템의 *Program Files* 폴더 아래에 있는 *Microsoft webmatrix* 하위 폴더에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="98281-360">Microsoft Windows Vista 이상에서 다음 명령을 사용 하 여 *bin* 디렉터리의 어셈블리에 대 한 symlink를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98281-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="98281-361">이 방법은 어셈블리의 복사본을 만들지 않는다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="98281-362">GAC에 두 어셈블리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="98281-363">관리자 권한 프롬프트에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="98281-364">문제: WebMatrix 베타 3은 권한 상승이 필요한 특정 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="98281-365">WebMatrix 베타 3은 다음과 같은 상황에서 추가 구성 요소를 설치 하는 등 권한 상승이 필요한 특정 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="98281-366">Windows Vista 또는 Windows 7에서 관리 권한이 없고 UAC (사용자 계정 컨트롤)를 사용할 수 없는 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="98281-367">Microsoft Windows XP 또는 Microsoft Windows Server 2003를 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="98281-368">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-368">**Workaround**</span></span>  
> <span data-ttu-id="98281-369">WebMatrix 베타 3의 모든 작업에는 관리 권한이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="98281-370">이렇게 하려면 관리자 권한으로 작업을 수행 하거나 다음 단계를 수행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="98281-371">Windows Vista 또는 Windows 7에서 UAC를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="98281-372">Windows XP에서 관리자 보안 그룹에 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-372">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="98281-373">문제: "웹 갤러리에서 사이트"를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="98281-374">웹 플랫폼 설치 관리자 3.0가 설치 되어 있지 않으면 **웹 갤러리에서 사이트** 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="98281-375">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-375">**Workaround**</span></span>  
> <span data-ttu-id="98281-376">[Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="98281-377">문제: Windows Server 2003에서 관리자가 아닌 사용자에 대 한 IIS Express 시작 되지 않음</span><span class="sxs-lookup"><span data-stu-id="98281-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="98281-378">Windows Server 2003에서 페이지를 시작 하거나 IIS Express를 시작 하면 IIS Express 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="98281-379">웹 페이지의 경우 관리자가 아닌 사용자가 응용 프로그램을 시작 했음을 나타내는 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="98281-380">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-380">**Workaround**</span></span>  
> <span data-ttu-id="98281-381">관리자가 WebMatrix 베타 3를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="98281-382">자세한 내용은 다음 기술 자료 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="98281-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="98281-383">관리자가 아닌 사용자가 시작한 응용 프로그램은 Windows Vista, Windows Server 2003 또는 Windows XP에서 응용 프로그램이 실행 되 고 있는 컴퓨터의 HTTP 트래픽을 수신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="98281-384">문제: Google Chrome은 실행 옵션으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="98281-385">Google Chrome은 **홈** 탭에서 **실행** 중인 브라우저 목록에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="98281-386">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-386">**Workaround**</span></span>  
> <span data-ttu-id="98281-387">일부 Google Chrome 버전은 Windows의 기본 프로그램 기능을 사용 하 여 제대로 등록 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="98281-388">해결 방법으로 Google Chrome을 시작 하 *고 사용자 지정 및 제어 Google chrome* 메뉴를 클릭 한 다음 *옵션*을 클릭 하 고 *Google Chrome 내 기본 브라우저 만들기*를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="98281-389">문제: "외래 키" 대화 상자에서 기본 키 입력을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="98281-390">**외래 키** 대화 상자에서는 기본 키 테이블의 기본 키 이름을 입력할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="98281-391">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-391">**Workaround**</span></span>  
> <span data-ttu-id="98281-392">이것은 의도적인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98281-392">This is intentional.</span></span> <span data-ttu-id="98281-393">기본 키 테이블에서 기본 키의 이름을 입력할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-393">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="98281-394">문제: "관계" 단추를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="98281-395">**데이터베이스** 작업 영역의 **테이블** 탭에 있는 **관계** 단추는 SQL Server Compact 데이터베이스에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="98281-396">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-396">**Workaround**</span></span>  
> <span data-ttu-id="98281-397">없음</span><span class="sxs-lookup"><span data-stu-id="98281-397">None.</span></span> <span data-ttu-id="98281-398">SQL Server Compact은 테이블 간의 관계를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98281-398">SQL Server Compact does not support relationships between tables.</span></span>

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="98281-399">문제: 매개 변수가 있는 SQL 쿼리가 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="98281-400">SQL Server Compact 4.0에서 매개 변수가 있는 쿼리의 매개 변수에 대해 `SqlDbType` 또는 `DbType` 같은 데이터 형식을 지정 하지 않으면 쿼리가 실행 될 때 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98281-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="98281-401">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="98281-401">**Workaround**</span></span>  
> <span data-ttu-id="98281-402">`SqlDbType` 또는 `DbType`와 같은 매개 변수의 데이터 형식을 명시적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="98281-403">BLOB 데이터 형식 (`image` 및 `ntext`)의 경우이는 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="98281-404">다음과 같은 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98281-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="98281-405">참조 항목</span><span class="sxs-lookup"><span data-stu-id="98281-405">For More Information</span></span>

<span data-ttu-id="98281-406">WebMatrix 베타 3에 대 한 자세한 내용은 다음 웹 사이트를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="98281-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="98281-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="98281-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="98281-408">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="98281-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="98281-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="98281-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

---

<span data-ttu-id="98281-410">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="98281-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="98281-411">All Rights Reserved.</span><span class="sxs-lookup"><span data-stu-id="98281-411">All Rights Reserved.</span></span> <span data-ttu-id="98281-412">[사용 약관](https://msdn.microsoft.cos/cc300389.aspx).</span><span class="sxs-lookup"><span data-stu-id="98281-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
