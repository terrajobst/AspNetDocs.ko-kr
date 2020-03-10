---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005의 향상 된 기능 | Microsoft Docs
author: microsoft
description: Visual Studio 2005는 웹 프로젝트의 향상 된 기능 및 향상 된 기능 목록을 제공 하는 웹 응용 프로그램 개발자를 제공 합니다.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 64215d556ded0850537a13856fe69b094116ebca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464651"
---
# <a name="improvements-in-visual-studio-2005"></a><span data-ttu-id="e4aaf-103">Visual Studio 2005의 개선 사항</span><span class="sxs-lookup"><span data-stu-id="e4aaf-103">Improvements in Visual Studio 2005</span></span>

<span data-ttu-id="e4aaf-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="e4aaf-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e4aaf-105">Visual Studio 2005는 웹 프로젝트의 향상 된 기능 및 향상 된 기능 목록을 제공 하는 웹 응용 프로그램 개발자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-105">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span>

<span data-ttu-id="e4aaf-106">Visual Studio 2005는 웹 프로젝트의 향상 된 기능 및 향상 된 기능 목록을 제공 하는 웹 응용 프로그램 개발자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-106">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span> <span data-ttu-id="e4aaf-107">Visual Studio .NET 2002 및 2003의 장점은 웹 프로젝트를 처리 하는 방식에 많은 불만 사항이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-107">As powerful as Visual Studio .NET 2002 and 2003 are, there were many complaints in the way that Web projects were handled.</span></span> <span data-ttu-id="e4aaf-108">Visual Studio 2005는 이러한 불만을 해결 하기 위해 많은 수의 새로운 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-108">Visual Studio 2005 adds a significant number of new features in order to address these complaints.</span></span> <span data-ttu-id="e4aaf-109">Visual Studio .NET 2003에서 웹 응용 프로그램의 컴파일을 처리 하는 방법을 선호 하는 경우 [웹 응용 프로그램 프로젝트](https://go.microsoft.com/fwlink/?LinkId=57870)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-109">For those who prefer the way that Visual Studio .NET 2003 handled compilation of Web applications, see [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span></span>

<span data-ttu-id="e4aaf-110">이 모듈에서는 웹 프로젝트 작성, 관리 및 개발에 대 한 향상 된 기능을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-110">In this module, well cover improvements in Web project creation, management, and development.</span></span> <span data-ttu-id="e4aaf-111">이후 모듈에서는 웹 프로젝트 빌드 및 배포의 향상 된 기능을 잘 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-111">In a later module, well cover improvements in building Web projects and deploying them.</span></span>

## <a name="frontpage-server-extensions"></a><span data-ttu-id="e4aaf-112">FrontPage Server Extensions</span><span class="sxs-lookup"><span data-stu-id="e4aaf-112">FrontPage Server Extensions</span></span>

<span data-ttu-id="e4aaf-113">웹 프로젝트를 만들거나 빌드하기 위해 Visual Studio .NET 2002 및 2003이 상자에 FrontPage Server Extensions.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-113">Visual Studio .NET 2002 and 2003 required FrontPage Server Extensions on the box in order to create or build Web projects.</span></span> <span data-ttu-id="e4aaf-114">개발자는 두 가지 액세스 모드 (FrontPage Server Extensions 또는 파일 액세스 모드) 중에서 선택 하 여 IIS에서 응용 프로그램 루트를 설정 하는 등의 작업을 수행 하는 데 FrontPage Server Extensions 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-114">Developers did have a choice between two different access modes (FrontPage Server Extensions or File access mode), both used FrontPage Server Extensions to perform tasks such as setting the application root in IIS, etc.</span></span>

<span data-ttu-id="e4aaf-115">Visual Studio 2005는 로컬 프로젝트에 대 한 FrontPage Server Extensions의 의존도를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-115">Visual Studio 2005 removes the reliance on FrontPage Server Extensions for local projects.</span></span> <span data-ttu-id="e4aaf-116">이제 Visual Studio 2005은 FrontPage Server Extensions를 사용 하는 대신 IIS 메타 베이스에 직접 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-116">Visual Studio 2005 now accesses the IIS metabase directly instead of using the FrontPage Server Extensions.</span></span> <span data-ttu-id="e4aaf-117">Visual Studio 2005에는 FrontPage Server Extensions 없이 원격 프로젝트에 액세스할 수 있도록 하는 FTP에 대 한 지원도 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-117">Visual Studio 2005 also adds support for FTP which allows for remote project access without requiring FrontPage Server Extensions.</span></span>

<span data-ttu-id="e4aaf-118">프로젝트에서 FrontPage Server Extensions를 사용 하려는 개발자의 경우에도 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-118">For those developers who want to use FrontPage Server Extensions in their projects, the option is still available.</span></span> <span data-ttu-id="e4aaf-119">그러나 ASP.NET 개발자 커뮤니티의 강력한 피드백을 기반으로 하는 것은 요구 사항이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-119">However, based upon strong feedback from the ASP.NET developer community, it is not a requirement.</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-120">원격 프로젝트를 만들고 여는 등의 경우에도 FrontPage Server Extensions 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-120">FrontPage Server Extensions are still required for remote project creation, opening, etc.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="e4aaf-121">ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="e4aaf-121">ASP.NET Development Server</span></span>

<span data-ttu-id="e4aaf-122">Visual Studio 2005는 ASP.NET 개발 서버 라는 새 웹 서버와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-122">Visual Studio 2005 ships with a new Web server called ASP.NET Development Server.</span></span> <span data-ttu-id="e4aaf-123">이 웹 서버는 이전에 Cassini로 알려져 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-123">(This Web server was previously known as Cassini.)</span></span>

<span data-ttu-id="e4aaf-124">ASP.NET 개발 서버에는 여러 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-124">There are several benefits of the ASP.NET Development Server.</span></span>

- <span data-ttu-id="e4aaf-125">이제 관리자가 아닌 관리자가 웹 서버에 대해 개발 하 고 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-125">It is now possible for non-Administrators to develop and debug against a Web server.</span></span>
- <span data-ttu-id="e4aaf-126">ASP.NET 개발 서버은 유연한 프로젝트 위치를 허용 하는 파일 시스템의 임의 위치에 가상 디렉터리를 동적으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-126">The ASP.NET Development Server dynamically maps virtual directories to any location in the file system allowing for flexible project locations.</span></span>
- <span data-ttu-id="e4aaf-127">이미 IIS를 사용 하 고 있는 Windows XP Professional의 사용자는 IIS에서 기본 웹 사이트의 파일 또는 폴더 구조에 영향을 주지 않는 새 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-127">Users on Windows XP Professional who are already using IIS will now be able to create new Web applications that will not affect the file or folder structure of their Default Web Site in IIS.</span></span>

<span data-ttu-id="e4aaf-128">ASP.NET 개발 서버를 활용 하기 위해 특별 한 구성이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-128">No special configuration is required to take advantage of the ASP.NET Development Server.</span></span> <span data-ttu-id="e4aaf-129">파일 시스템에서 호스팅되는 웹 프로젝트를 디버깅 하거나 검색할 때 Visual Studio 2005는 요청을 처리 하기 위해 임의의 포트에서 ASP.NET 개발 서버의 인스턴스를 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-129">When a Web project that is hosted on the file system is debugged or browsed, Visual Studio 2005 will automatically start an instance of the ASP.NET Development Server on a random port to service the request.</span></span>

<span data-ttu-id="e4aaf-130">자세한 내용은이 모듈의 뒷부분에 나오는 ASP.NET 개발 서버에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-130">More information will be covered on the ASP.NET Development Server later in this module.</span></span>

## <a name="improved-file-management"></a><span data-ttu-id="e4aaf-131">향상 된 파일 관리</span><span class="sxs-lookup"><span data-stu-id="e4aaf-131">Improved File Management</span></span>

<span data-ttu-id="e4aaf-132">Visual Studio 2002 및 2003에서는 웹 응용 프로그램의 모든 파일에 대 한 정보를 저장 하 C#는 프로젝트 파일 (VB.NET 및 .csproj의 경우 .vbproj)이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-132">In Visual Studio 2002 and 2003, a project file (.vbproj for VB.NET and .csproj for C#) stored information on all files in the Web application.</span></span> <span data-ttu-id="e4aaf-133">솔루션 탐색기 표시는 프로젝트 파일의 파일 정보를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-133">The Solution Explorer display is based upon the file information in the project file.</span></span> <span data-ttu-id="e4aaf-134">이로 인해 솔루션 탐색기는 외부 편집기를 사용한 경우에 부정확 한 정보를 표시 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-134">Because of this, the Solution Explorer would often display inaccurate information in cases where external editors were used.</span></span> <span data-ttu-id="e4aaf-135">Visual Studio 2002 및 2003은 파일 변경 내용을 덮어쓰거나 파일의 최신 버전을 표시 하지 않는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-135">Visual Studio 2002 and 2003 would often overwrite file changes or not display the most recent version of files.</span></span>

<span data-ttu-id="e4aaf-136">Visual Studio 2005는 프로젝트 파일을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-136">Visual Studio 2005 does away with the project file.</span></span> <span data-ttu-id="e4aaf-137">대신 디스크에서 직접 파일 및 폴더 정보를 읽고 프로젝트의 파일을 정확 하 게 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-137">Instead, it reads the file and folder information directly from the disk, resulting in an accurate display of the files in your project.</span></span> <span data-ttu-id="e4aaf-138">Visual Studio 2002 및 2003의 참조 폴더는 웹 응용 프로그램의 실제 폴더를 나타내지 않으므로 Visual Studio 2005는 솔루션 탐색기에서 참조 폴더를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-138">Because the References folder in Visual Studio 2002 and 2003 does not represent an actual folder in your Web application, Visual Studio 2005 also removes the References folder from Solution Explorer.</span></span> <span data-ttu-id="e4aaf-139">Visual Studio 2005에서 프로젝트에 대 한 참조에 액세스 하려면 프로젝트의 속성 페이지를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-139">To access the references for your project in Visual Studio 2005, you should use the Property pages for the project.</span></span>

## <a name="creating-web-projects"></a><span data-ttu-id="e4aaf-140">웹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-140">Creating Web Projects</span></span>

<span data-ttu-id="e4aaf-141">웹 개발자는 Visual Studio 2005에서 프로젝트를 만드는 데 사용할 수 있는 여러 가지 새로운 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-141">Web developers have many new options available for project creation in Visual Studio 2005.</span></span> <span data-ttu-id="e4aaf-142">이제 파일 시스템의 모든 위치에서 웹 사이트를 만들 수 있으며, 새 ASP.NET 개발 서버를 사용 하 여 디버깅 하거나 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-142">Web sites can now be created anywhere in the file system and can then be debugged or browsed using the new ASP.NET Development Server.</span></span> <span data-ttu-id="e4aaf-143">또한 개발자는 FTP를 사용 하 여 새 웹 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-143">Developers can also create new Web sites using FTP.</span></span>

<span data-ttu-id="e4aaf-144">Visual Studio 2005에서 웹 프로젝트를 만드는 비디오 연습을 보려면 여기를 클릭 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-144">Click here to view a video walkthrough of creating Web projects in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image1.png)

[<span data-ttu-id="e4aaf-145">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-145">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a><span data-ttu-id="e4aaf-146">파일 시스템 프로젝트</span><span class="sxs-lookup"><span data-stu-id="e4aaf-146">File System Projects</span></span>

<span data-ttu-id="e4aaf-147">비디오 연습에서 살펴본 것 처럼 로컬 컴퓨터 또는 파일 공유를 통해 원격 위치에서 파일 시스템에 웹 사이트를 만들도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-147">As you saw in the video walkthrough, you can choose to create Web sites on the file system either on the local machine or on a remote location via a file share.</span></span> <span data-ttu-id="e4aaf-148">ASP.NET 개발 서버를 사용 하 여 파일 시스템에 생성 된 웹 사이트를 검색 하 고 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-148">Web sites that are created on the file system are browsed and debugged using the ASP.NET Development Server.</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-149">ASP.NET 개발 서버는 고객이 일부 혼동을 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-149">The ASP.NET Development Server may cause some confusion for customers.</span></span> <span data-ttu-id="e4aaf-150">웹 프로젝트가 IISs 디렉터리 구조 (예: c:/inetpub/wwwroot)에서 파일 시스템에 생성 되는 경우 Visual Studio 2005 내에서 시작할 때 웹 사이트는 ASP.NET 개발 서버를 통해 계속 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-150">If a Web project is created on the file system in IISs directory structure (i.e. c:/inetpub/wwwroot), the Web site will still be browsed via the ASP.NET Development Server when launched from within Visual Studio 2005.</span></span> <span data-ttu-id="e4aaf-151">따라서 모든 IIS 구성 (즉, 인증 방법)은 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-151">Therefore, any IIS configuration (i.e. authentication methods) is not applicable.</span></span>

<span data-ttu-id="e4aaf-152">또한 기본 웹 프로젝트는 default.aspx 페이지, default.cs 파일 및 App/_Data 폴더만 포함 하 여 많은 오버 헤드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-152">The default web project also removes a lot of the overhead by only includes a Default.aspx page, default.cs file, and an App/_Data folder.</span></span> <span data-ttu-id="e4aaf-153">Web.config와 특수 폴더 (즉, 앱/_code)가 필요에 따라 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-153">The web.config and special folders (i.e. app/_code) are added as they are needed.</span></span> <span data-ttu-id="e4aaf-154">웹 프로젝트에는 필요한 파일과 폴더만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-154">Your web project only includes the files and folders that you need.</span></span>

### <a name="http-projects"></a><span data-ttu-id="e4aaf-155">HTTP 프로젝트</span><span class="sxs-lookup"><span data-stu-id="e4aaf-155">HTTP Projects</span></span>

<span data-ttu-id="e4aaf-156">HTTP 프로젝트는 로컬 IIS 웹 사이트 또는 원격 웹 사이트에 생성 되는 프로젝트 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-156">HTTP projects can either be projects that are created on a local IIS Web site or on a remote Web site.</span></span> <span data-ttu-id="e4aaf-157">기본 프로젝트 위치는 `http://localhost`입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-157">The default project location is `http://localhost`.</span></span> <span data-ttu-id="e4aaf-158">찾아보기 단추를 클릭 하면 두 가지 HTTP 옵션인 로컬 IIS와 원격 사이트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-158">If you click the Browse button, there are two HTTP options: Local IIS and Remote Site.</span></span> <span data-ttu-id="e4aaf-159">이러한 두 옵션의 주요 차이점은 위치 선택 대화 상자와 웹 서버에 파일을 복사 하는 방법에 웹 사이트 정보가 표시 되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-159">The main difference in these two options is the method in which the web site information is displayed in the Choose Location dialog and in how the files are copied to the Web server.</span></span>

<span data-ttu-id="e4aaf-160">로컬 IIS 옵션은 로컬 컴퓨터의 메타 베이스에서 사이트 정보를 읽고 파일 시스템을 사용 하 여 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-160">The Local IIS option reads the site information from the metabase on the local machine and files are copied using the file system.</span></span> <span data-ttu-id="e4aaf-161">원격 사이트 옵션은 FrontPage Server Extensions를 사용 하 고 사이트 정보 및 파일은 HTTP 및 FrontPage Server Extensions RPC 호출을 사용 하 여 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-161">The Remote Site option uses the FrontPage Server Extensions and the site information and files are copied using HTTP and FrontPage Server Extensions RPC calls.</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-162">Vs # # #/_tmp .htm 파일 및 get/_aspx/_ver는 더 이상 버전 정보를 확인 하는 데 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-162">The vs###/_tmp.htm file and get/_aspx/_ver.aspx are no longer used to determine version information.</span></span>

<span data-ttu-id="e4aaf-163">기본 HTTP 옵션은 로컬 IIS입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-163">The default HTTP option is Local IIS.</span></span> <span data-ttu-id="e4aaf-164">이 옵션은 IIS 메타 베이스를 읽어 사용 가능한 사이트와 콘텐츠를 만들 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-164">This option reads the IIS Metabase to determine which sites are available and the location in which to create content.</span></span> <span data-ttu-id="e4aaf-165">트리 보기에서 선택 하 여 다른 폴더 또는 가상 디렉터리를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-165">You can select a different folder or virtual directory by selecting it in the tree view.</span></span> <span data-ttu-id="e4aaf-166">새 가상 디렉터리를 만들고, 폴더를 응용 프로그램으로 표시 하 고,이 대화 상자에서 기존 가상 디렉터리를 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-166">You can also create a new virtual directory, mark folders as applications, as well as delete existing virtual directories from this dialog box.</span></span>

![위치 선택 대화 상자](improvements-in-visual-studio-2005/_static/image1.gif)

<span data-ttu-id="e4aaf-168">**그림 1**: 위치 선택 대화 상자</span><span class="sxs-lookup"><span data-stu-id="e4aaf-168">**Figure 1**: The Choose Location Dialog</span></span>

<span data-ttu-id="e4aaf-169">이전 버전의 Visual Studio와 달리 **SSL(Secure Sockets Layer) 사용** 확인란을 선택 하 고 SSL 인증서가 검색 중인 URL과 일치 하지 않는 경우 계속할지 여부를 묻는 보안 경고 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-169">Unlike in earlier versions of Visual Studio, if you check the **Use Secure Sockets Layer** checkbox and the SSL certificate does not match the URL you are browsing, you will be presented with a Security Alert dialog asking you if you would like to proceed.</span></span> <span data-ttu-id="e4aaf-170">Visual Studio .NET 2003을 사용 하 여 인증서가 일치 하는 인증서가 아닌 경우 프로젝트를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-170">Using Visual Studio .NET 2003, if the certificate was not a matching one, creating the project would fail.</span></span>

![SSL 인증서에 대 한 보안 경고](improvements-in-visual-studio-2005/_static/image2.gif)

<span data-ttu-id="e4aaf-172">**그림 2**: SSL 인증서에 대 한 보안 경고</span><span class="sxs-lookup"><span data-stu-id="e4aaf-172">**Figure 2**: Security Alert Regarding SSL Certificate</span></span>

### <a name="note-on-host-headers"></a><span data-ttu-id="e4aaf-173">호스트 헤더에 대 한 참고</span><span class="sxs-lookup"><span data-stu-id="e4aaf-173">Note on Host Headers</span></span>

<span data-ttu-id="e4aaf-174">특정 IP에 바인딩된 사이트에서 웹 응용 프로그램을 만드는 경우 호스트 헤더가 구성 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-174">If you are creating a Web application on a site bound to a specific IP, you will need to ensure that a host header is configured.</span></span> <span data-ttu-id="e4aaf-175">그렇지 않으면 Visual Studio는 `http://localhost`에서 사이트를 만들지만 IDE 내에서 사이트를 검색 하거나 디버그할 때 IP 주소는 올바르게 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-175">Otherwise, Visual Studio will create the site at `http://localhost`, but the IP address will not resolve correctly when the site is browsed or debugged from within the IDE.</span></span>

<span data-ttu-id="e4aaf-176">원격 사이트 옵션을 선택 하는 경우 대화 상자를 변경 하 여 새 웹 사이트의 대상 URL을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-176">If you select the Remote Site option, the dialog changes to allow you to enter the destination URL for the new Web site.</span></span> <span data-ttu-id="e4aaf-177">이 URL은 FrontPage Server Extensions 사용 하도록 설정 된 서버에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-177">This URL must be on a server that has the FrontPage Server Extensions enabled.</span></span> <span data-ttu-id="e4aaf-178">FrontPage Server Extensions를 사용 하 여 로컬 웹 서버를 사용 하려는 경우 원격 사이트 옵션을 사용 하 고 로컬 URL을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-178">If you want to work with your local Web server using the FrontPage Server Extensions, you can use the Remote Site option and specify a local URL.</span></span>

![원격 서버에서 웹 사이트 만들기](improvements-in-visual-studio-2005/_static/image1.jpg)

<span data-ttu-id="e4aaf-180">**그림 3**: 원격 서버에 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-180">**Figure 3**: Creating a Web Site on a Remote Server</span></span>

<span data-ttu-id="e4aaf-181">SSL을 통해 원격 사이트에서 응용 프로그램을 만들 때 SSL 인증서가 일치 하지 않으면 로컬 IIS 옵션을 사용할 때 표시 되는 대화 상자와는 확인 대화 상자가 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-181">When creating an application on a remote site via SSL, if the SSL certificate does not match, the confirmation dialog is slightly different than the dialog displayed when using the Local IIS option.</span></span>

![원격 사이트 보안 경고](improvements-in-visual-studio-2005/_static/image3.gif)

<span data-ttu-id="e4aaf-183">**그림 4**: 원격 사이트 보안 경고</span><span class="sxs-lookup"><span data-stu-id="e4aaf-183">**Figure 4**: The Remote Site Security Alert</span></span>

<a id="_Toc116100243"></a>

#### <a name="ftp"></a><span data-ttu-id="e4aaf-184">FTP</span><span class="sxs-lookup"><span data-stu-id="e4aaf-184">FTP</span></span>

<span data-ttu-id="e4aaf-185">Visual Studio 2005에서는 FTP를 통해 웹 사이트를 만드는 옵션을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-185">Visual Studio 2005 introduces the option to create Web sites via FTP.</span></span> <span data-ttu-id="e4aaf-186">이 옵션을 사용 하는 경우 IDE는 사용자 임시 폴더에 로컬로 파일을 만든 다음 FTP를 사용 하 여 FTP 위치로 파일을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-186">When you use this option, the IDE creates the files locally in the users temp folder and then uses FTP to move the files to the FTP location.</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-187">임시 폴더 위치는 c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;응용 프로그램 이름&gt;</span><span class="sxs-lookup"><span data-stu-id="e4aaf-187">The temp folder location is c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="e4aaf-188">FTP 옵션을 사용 하는 경우 위치 선택 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-188">When using the FTP option, you will be presented with a Choose Location dialog.</span></span> <span data-ttu-id="e4aaf-189">아래와 같이 필요한 FTP 연결 정보를이 대화 상자에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-189">You enter the required FTP connection information into this dialog as shown below.</span></span>

![FTP에 대 한 위치 선택 대화 상자](improvements-in-visual-studio-2005/_static/image2.jpg)

<span data-ttu-id="e4aaf-191">**그림 5**: FTP에 대 한 위치 선택 대화 상자</span><span class="sxs-lookup"><span data-stu-id="e4aaf-191">**Figure 5**: The Choose Location Dialog for FTP</span></span>

## <a name="lab-setup-ftp-site-and-create-a-project"></a><span data-ttu-id="e4aaf-192">랩: FTP 사이트를 설정 하 고 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-192">Lab: Setup FTP site and create a project</span></span>

<span data-ttu-id="e4aaf-193">다음 단계는 ftp 사이트를 구성 하 여 사용자가 FTP를 통해 업로드할 수 있는 위치를 갖도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-193">The following steps configure the FTP site so that a user has a location that only they can upload to via FTP.</span></span>

### <a name="install-the-ftp-service"></a><span data-ttu-id="e4aaf-194">FTP 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="e4aaf-194">Install the FTP Service</span></span>

1. <span data-ttu-id="e4aaf-195">프로그램 추가/제거를 열고 Windows 구성 요소 추가/제거를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-195">Open Add Remove Programs, select Add/Remove Windows Components</span></span>
2. <span data-ttu-id="e4aaf-196">인터넷 정보 서비스 (Windows 2003의 응용 프로그램 서버)를 선택 하 고 **세부 정보**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-196">Select Internet Information Services (Application Server on Windows 2003) and click **Details**.</span></span>
3. <span data-ttu-id="e4aaf-197">**파일 전송 프로토콜 (FTP) 서비스** 를 확인 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-197">Check **File Transfer Protocol (FTP) Service** and click **OK**.</span></span>
4. <span data-ttu-id="e4aaf-198">**다음** 을 클릭 하 여 FTP 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-198">Click **Next** to install the FTP service.</span></span>

### <a name="create-a-new-folder-for-content"></a><span data-ttu-id="e4aaf-199">콘텐츠에 대 한 새 폴더 만들기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-199">Create a New Folder for Content</span></span>

1. <span data-ttu-id="e4aaf-200">Windows 탐색기에서 c:/inetpub/wwwroot 내부에 **User1** 이라는 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-200">In Windows Explorer, create a new folder called **User1** inside of c:/inetpub/wwwroot.</span></span>

#### <a name="configure-folders-and-permissions-on-folders"></a><span data-ttu-id="e4aaf-201">폴더 및 폴더에 대 한 사용 권한을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-201">Configure folders and permissions on folders.</span></span>

1. <span data-ttu-id="e4aaf-202">관리 도구에서 인터넷 정보 서비스 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-202">Open the Internet Information Services snap-in from Administrative Tools.</span></span> <span data-ttu-id="e4aaf-203">이제 컴퓨터 이름 노드 아래에 FTP 사이트 폴더가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-203">You will now have an FTP Sites folder under the computer name node.</span></span>
2. <span data-ttu-id="e4aaf-204">**FTP 사이트**를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-204">Expand **FTP Sites**.</span></span>
3. <span data-ttu-id="e4aaf-205">**기본 FTP 사이트**를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**, **가상 디렉터리**를 차례로 선택한 후 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-205">Right-click the **Default FTP Site**, select **New**, then **Virtual Directory**, then click **Next**.</span></span>
4. <span data-ttu-id="e4aaf-206">가상 디렉터리 이름으로 **User1** 을 입력 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-206">Enter **User1** for the virtual directory name and click **Next**.</span></span>
5. <span data-ttu-id="e4aaf-207">경로에 **c:/inetpub/wwwroot/User1** 을 입력 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-207">Enter **c:/inetpub/wwwroot/User1** for the path and click **Next**.</span></span>
6. <span data-ttu-id="e4aaf-208">**다음** 을 클릭 하 고 **마침** 을 클릭 하 여 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-208">Click **Next** and then **Finish** to complete the wizard.</span></span>
7. <span data-ttu-id="e4aaf-209">기본 FTP 사이트에서 **User1** 가상 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-209">Right-click the **User1** virtual directory under Default FTP Site and select **Properties**.</span></span>
8. <span data-ttu-id="e4aaf-210">**쓰기** 확인란을 선택 하 고 **확인** 을 클릭 하 여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-210">Check the **Write** checkbox and click **OK** to close the dialog.</span></span>
9. <span data-ttu-id="e4aaf-211">**기본 FTP 사이트** 를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-211">Right-click **Default FTP Site** and select **Properties**.</span></span>
10. <span data-ttu-id="e4aaf-212">**보안 계정** 탭에서 **익명 연결 허용**을 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-212">On the **Security Accounts** tab, uncheck **Allow Anonymous Connections**.</span></span>
11. <span data-ttu-id="e4aaf-213">계속할 것인지 묻는 대화 상자에서 **예** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-213">Click **Yes** in the dialog asking if you want to continue.</span></span>
12. <span data-ttu-id="e4aaf-214">**확인**을 클릭하여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-214">Click **OK** to close the dialog.</span></span>
13. <span data-ttu-id="e4aaf-215">**웹 사이트** 노드 아래에서 **기본 웹 사이트** 를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-215">Expand the **Default Web Site** under the **Web Sites** node.</span></span>
14. <span data-ttu-id="e4aaf-216">**User1** 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-216">Right-click the **User1** directory and select **Properties**</span></span>
15. <span data-ttu-id="e4aaf-217">**응용 프로그램 설정** 섹션에서 **만들기** 를 클릭 하 여 폴더를 응용 프로그램으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-217">In the **Application Settings** section, click **Create** to mark the folder as an application.</span></span>
16. <span data-ttu-id="e4aaf-218">**확인**을 클릭하여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-218">Click **OK** to close the dialog.</span></span>
17. <span data-ttu-id="e4aaf-219">인터넷 정보 서비스 스냅인을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-219">Close the Internet Information Services snap-in.</span></span>

### <a name="create-web-project"></a><span data-ttu-id="e4aaf-220">웹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-220">Create web project</span></span>

1. <span data-ttu-id="e4aaf-221">Visual Studio 2005을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-221">Open Visual Studio 2005.</span></span>
2. <span data-ttu-id="e4aaf-222">**파일** 메뉴에서 **새 웹 사이트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-222">From the **File** menu, select **New Web Site**.</span></span>
3. <span data-ttu-id="e4aaf-223">**위치** 드롭다운에서 **FTP**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-223">In the **Location** dropdown, select **FTP**.</span></span>
4. <span data-ttu-id="e4aaf-224">**찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-224">Click **Browse**.</span></span>
5. <span data-ttu-id="e4aaf-225">**서버** 텍스트 상자에 **localhost** 를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-225">Enter **localhost** in the **Server** textbox.</span></span>
6. <span data-ttu-id="e4aaf-226">디렉터리 텍스트 상자에 **User1** 을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-226">Enter **User1** in the Directory textbox.</span></span>
7. <span data-ttu-id="e4aaf-227">**열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-227">Click **Open**.</span></span> <span data-ttu-id="e4aaf-228">FTP 위치가 새 웹 사이트 대화 상자에 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-228">The FTP location will be entered into the New Web Site dialog.</span></span>
8. <span data-ttu-id="e4aaf-229">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-229">Click **OK**.</span></span>
9. <span data-ttu-id="e4aaf-230">FTP 로그온 대화 상자에서 **익명 로그온** 을 선택 취소 하 고 자격 증명을 입력 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-230">Uncheck **Anonymous log on** in the FTP Log On dialog, enter your credentials, and click **OK**.</span></span>
10. <span data-ttu-id="e4aaf-231">프로젝트에 대 한 URL은 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="e4aaf-231">What is the URL for the project?</span></span> <span data-ttu-id="e4aaf-232">프로젝트에 대 한 URL은 솔루션 탐색기 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-232">(The URL for the project will be displayed in Solution Explorer.)</span></span>
11. <span data-ttu-id="e4aaf-233">**빌드** 메뉴에서 **웹 사이트 빌드** 또는 **솔루션 빌드**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-233">From the **Build** menu, select **Build Web Site** or **Build Solution**.</span></span>
12. <span data-ttu-id="e4aaf-234">솔루션 탐색기에서 default.aspx를 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-234">Right-click on Default.aspx in Solution Explorer and select **View in Browser**.</span></span>
13. <span data-ttu-id="e4aaf-235">웹 사이트 URL 필요 대화 상자에서 URL에 `http://localhost/user1`를 입력 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-235">In the Web Site URL Required dialog, enter `http://localhost/user1` for the URL and click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-236">형식/_Default를 로드할 수 없음을 나타내는 오류가 발생 하는 경우 웹 사이트에서 ASP.NET 2.0를 실행 하 고 있고 이전 버전은 실행 하 고 있지 않은지 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-236">If you get a error indicating an inability to load the type /_Default, make sure that you are running ASP.NET 2.0 on your Web site and not an earlier version.</span></span> <span data-ttu-id="e4aaf-237">인터넷 정보 서비스의 ASP.NET 탭에서이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-237">You can do that from the ASP.NET tab in Internet Information Services.</span></span>

## <a name="opening-web-projects"></a><span data-ttu-id="e4aaf-238">웹 프로젝트 열기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-238">Opening Web Projects</span></span>

<span data-ttu-id="e4aaf-239">웹 프로젝트를 여는 것은 프로젝트를 만드는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-239">Opening Web projects is similar to creating projects.</span></span> <span data-ttu-id="e4aaf-240">다음 섹션에서는 IDE 내에서 작업 하는 동안에 대 한 영역을 유지 하기 위한 영역을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-240">The following sections call out areas to keep an eye out for while working within the IDE.</span></span> <span data-ttu-id="e4aaf-241">또한 HTTP 및 FTP를 사용 하 여 웹 프로젝트 작업을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-241">It also covers working with Web projects using HTTP and FTP.</span></span>

<span data-ttu-id="e4aaf-242">웹 프로젝트를 열려면 파일 메뉴에서 웹 사이트 열기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-242">To open a Web project, select Open Web Site from the File menu.</span></span> <span data-ttu-id="e4aaf-243">이전에 설명한 것과 동일한 위치 선택 대화 상자가 표시 되며, 파일 시스템, 로컬 IIS, FTP 및 원격 사이트와 같은 네 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-243">You will be prompted with the same Choose Location dialog covered previously and you have the same four options available to you: File System, Local IIS, FTP, and Remote Site.</span></span>

<a id="_Toc116100245"></a>

## <a name="file-system"></a><span data-ttu-id="e4aaf-244">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="e4aaf-244">File System</span></span>

<span data-ttu-id="e4aaf-245">이 모듈의 앞에서 설명한 것 처럼 Visual Studio에서는 더 이상 프로젝트 파일을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-245">As indicated previously in this module, Visual Studio no longer uses a project file.</span></span> <span data-ttu-id="e4aaf-246">따라서 파일 시스템에서 웹 사이트를 열도록 선택 하는 경우에는 선택한 폴더가 Visual Studio에서 처음에 웹 프로젝트로 생성 되지 않은 경우에도 원하는 폴더를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-246">Therefore, if you choose to open a Web site from the file system, you actually have the option of choosing any folder that you wish, even if the folder you choose was not created as a Web project initially in Visual Studio.</span></span> <span data-ttu-id="e4aaf-247">예를 들어 내 문서 폴더를 웹 사이트로 열도록 선택할 수 있습니다. 그러면 Visual Studio에서 해당 폴더를 열고 아래와 같이 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-247">For example, you can choose to open the My Documents folder as a Web site and Visual Studio will happily open it and display your files as shown below.</span></span>

![웹 사이트로 열린 내 문서](improvements-in-visual-studio-2005/_static/image3.jpg)

<span data-ttu-id="e4aaf-249">**그림 6**: 웹 사이트로 열린 *내 문서*</span><span class="sxs-lookup"><span data-stu-id="e4aaf-249">**Figure 6**: *My Documents* Opened As a Web Site</span></span>

<span data-ttu-id="e4aaf-250">Visual Studio는 필요한 경우에만 추가 파일 및 폴더를 만들기 때문에 사용자가 여는 위치에 추가 파일이 나 폴더가 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-250">Because Visual Studio only creates additional files and folders when necessary, no additional files or folders are added to the location you open.</span></span> <span data-ttu-id="e4aaf-251">이 아키텍처의 부작용은 파일 시스템에서 웹 사이트를 중첩 하지 못하도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-251">A side-effect of this architecture is that it prevents you from nesting Web sites on the file system.</span></span> <span data-ttu-id="e4aaf-252">예를 들어 다음 디렉터리 구조를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-252">For example, consider the following directory structure.</span></span>

<span data-ttu-id="e4aaf-253">C:/MyWebSite의 웹 프로젝트</span><span class="sxs-lookup"><span data-stu-id="e4aaf-253">Web project at C:/MyWebSite</span></span>

<span data-ttu-id="e4aaf-254">C:/MyWebSite/Nested의 다른 웹 프로젝트</span><span class="sxs-lookup"><span data-stu-id="e4aaf-254">Another web project at C:/MyWebSite/Nested</span></span>

<span data-ttu-id="e4aaf-255">C:/MyWebSite에서 웹 사이트를 열면 중첩 된 폴더가 해당 응용 프로그램의 하위 폴더로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-255">When you open the Web site at c:/MyWebSite, the Nested folder will appear as a sub-folder of that application.</span></span>

<a id="_Toc116100246"></a>

## <a name="http"></a><span data-ttu-id="e4aaf-256">HTTP</span><span class="sxs-lookup"><span data-stu-id="e4aaf-256">HTTP</span></span>

<span data-ttu-id="e4aaf-257">HTTP를 통해 웹 사이트를 열 때 IIS 메타 베이스 (로컬 IIS) 또는 FrontPage Server Extensions (원격 사이트)를 사용 하 여 설정을 읽습니다. 중첩 된 웹 응용 프로그램이 있는 경우 이러한 응용 프로그램을 응용 프로그램으로 식별 하는 아이콘으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-257">When opening Web sites via HTTP, settings are read either from the IIS metabase (Local IIS) or using FrontPage Server Extensions (Remote Site.) If there are nested web applications, these are displayed as well with an icon identifying them as an application.</span></span> <span data-ttu-id="e4aaf-258">FrontPage에서 웹 응용 프로그램을 사용 하는 방법을 잘 알고 있다면 Visual Studio 2005의 동작이 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-258">If you are familiar with working with web applications in FrontPage, the behavior in Visual Studio 2005 is similar.</span></span>

<span data-ttu-id="e4aaf-259">Visual Studio는 현재 IDE 내에서 열려 있는 응용 프로그램 아래에 중첩 된 응용 프로그램에 대 한 아이콘을 표시 하지만 해당 콘텐츠를 볼 수 있도록 확장할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-259">Even though Visual Studio will display an icon for applications that are nested beneath the application that is currently opened within the IDE, it will not allow you to expand them to see their content.</span></span> <span data-ttu-id="e4aaf-260">그러나 해당 항목을 두 번 클릭 하 여 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-260">You can, however, double-click on them to open them.</span></span> <span data-ttu-id="e4aaf-261">이렇게 하면 웹 응용 프로그램을 열 수 있는 대화 상자가 표시 되 고 (현재 열려 있는 솔루션을 대체 함) 웹 응용 프로그램을 현재 솔루션에 추가 하 라는 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-261">When you do, you will be presented with a dialog prompting you to either open the web application (and replace the currently open solution) or add the Web application to your current solution.</span></span>

![중첩 된 응용 프로그램 아이콘을 두 번 클릭 하면이 대화 상자가 표시 됩니다.](improvements-in-visual-studio-2005/_static/image4.jpg)

<span data-ttu-id="e4aaf-263">**그림 7**: 중첩 된 응용 프로그램 아이콘을 두 번 클릭 하면이 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-263">**Figure 7**: Double-clicking a nested application icon presents you with this dialog</span></span>

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a><span data-ttu-id="e4aaf-264">FTP 사이트</span><span class="sxs-lookup"><span data-stu-id="e4aaf-264">FTP Site</span></span>

<span data-ttu-id="e4aaf-265">FTP를 통해 사이트를 열 때 파일은 모두 임시 폴더에 로컬로 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-265">When you open a site via FTP, the files are all copied locally to your temp folder.</span></span> <span data-ttu-id="e4aaf-266">로컬 저장소 위치의 전체 경로는 프로젝트에 대 한 속성 창에 표시 되며 다음 형식을 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-266">The full path for the local storage location is displayed in the Properties pane for the project and is created using the following format.</span></span>

<span data-ttu-id="e4aaf-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;응용 프로그램 이름&gt;</span><span class="sxs-lookup"><span data-stu-id="e4aaf-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="e4aaf-268">FTP를 사용 하는 경우 Visual Studio는 아래와 같이 찾아볼 수 있도록 프로젝트의 기본 URL을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-268">When using FTP, Visual Studio will need to specify the base URL for your project so that you can browse it as shown below.</span></span> <span data-ttu-id="e4aaf-269">기본 URL을 지정 하지 않으면 웹 사이트의 페이지를 처음으로 탐색 하려고 할 때 Visual Studio에서 해당 URL을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-269">If you do not specify a base URL, Visual Studio will ask you for it the first time you attempt to browse a page in the Web site.</span></span>

![FTP 사이트에 대 한 기본 URL 지정](improvements-in-visual-studio-2005/_static/image5.jpg)

<span data-ttu-id="e4aaf-271">**그림 8**: FTP 사이트에 대 한 기본 URL 지정</span><span class="sxs-lookup"><span data-stu-id="e4aaf-271">**Figure 8**: Specifying a Base URL for FTP Sites</span></span>

## <a name="improvements-in-compilation"></a><span data-ttu-id="e4aaf-272">컴파일의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="e4aaf-272">Improvements in Compilation</span></span>

<span data-ttu-id="e4aaf-273">Visual Studio 2005에서 웹 응용 프로그램을 사용 하는 것은 이전 버전 보다 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-273">Working with Web applications in Visual Studio 2005 is noticeably faster than previous versions.</span></span> <span data-ttu-id="e4aaf-274">이는 컴파일 아키텍처의 변경 내용에 대 한 부분이 많지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-274">This is due in no small part to the changes in compilation architecture.</span></span>

<span data-ttu-id="e4aaf-275">Visual Studio 2002 및 2003에서 웹 응용 프로그램은 웹 응용 프로그램 폴더에 상주 하는 하나의 주 어셈블리로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-275">In Visual Studio 2002 and 2003, Web applications were compiled into one primary assembly residing in the /bin folder.</span></span> <span data-ttu-id="e4aaf-276">Visual Studio 2005에서 앱/_Code 폴더가 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-276">In Visual Studio 2005, an App/_Code folder was added.</span></span> <span data-ttu-id="e4aaf-277">클래스 및 기타 비 UI 코드는 App/_Code 폴더에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-277">Classes and other non-UI code are added to the App/_Code folder.</span></span> <span data-ttu-id="e4aaf-278">Visual Studio에서 프로젝트를 빌드하면 App/_Code 폴더의 모든 파일이 단일 앱/_Code .dll 파일로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-278">When Visual Studio builds the project, all files in the App/_Code folder are compiled into a single App/_Code.dll file.</span></span> <span data-ttu-id="e4aaf-279">이러한 변경으로 인해 이후 빌드는 이전 버전 보다 훨씬 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-279">The result of this change is that subsequent builds are much faster than in previous versions.</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-280">MSBuild 명령줄 유틸리티를 사용 하 여 ASP.NET 웹 응용 프로그램을 빌드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-280">The MSBuild command line utility can also be used to build ASP.NET Web applications.</span></span> <span data-ttu-id="e4aaf-281">이 도구는 모듈 9에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-281">That tool will be covered in module 9.</span></span>

<span data-ttu-id="e4aaf-282">또 다른 컴파일 기능은 빌드 메뉴의 새 빌드 페이지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-282">Another compilation enhancement is the new Build Page option on the Build menu.</span></span> <span data-ttu-id="e4aaf-283">이 기능을 사용 하면 개발자는 변경 내용을 보다 신속 하 게 컴파일할 수 있도록 현재 페이지 (물론, 및 종속성)만 다시 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-283">This feature allows a developer to rebuild only the current page (along with, of course, and dependencies) so that changes can be compiled more quickly.</span></span> <span data-ttu-id="e4aaf-284">는 C# intellisense를 업데이트할 목적으로 백그라운드 컴파일을 제공 하지 않기 때문에이 기능을 사용 하면 단일 페이지를 간단 하 게 다시 작성 하 여 intellisense를 빠르게 업데이트할 수 있으므로이 기능을 사용 하는 것은 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-284">Because C# does not offer background compilation for purposes of updating IntelliSense, etc., they will benefit immensely from this feature because it will allow for IntelliSense to be updated quickly by simply rebuilding a single page.</span></span>

<span data-ttu-id="e4aaf-285">프로젝트에 대 한 빌드 속성을 사용 하 여 시작 페이지를 실행 하기 전에 발생 하는 빌드 유형을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-285">The Build properties for a project allow you to configure the type of build that occurs before the startup page is executed.</span></span> <span data-ttu-id="e4aaf-286">개발자는 Visual Studio에서 코드 변경 후 더 빠르게 응용 프로그램 디버깅을 시작할 수 있도록 현재 페이지만 빌드하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-286">Developers can choose to only build the current page so that Visual Studio can start debugging applications more quickly after code changes.</span></span>

![빌드 페이지 시작 작업](improvements-in-visual-studio-2005/_static/image6.jpg)

<span data-ttu-id="e4aaf-288">**그림 9**: 빌드 페이지 시작 작업</span><span class="sxs-lookup"><span data-stu-id="e4aaf-288">**Figure 9**: The Build Page Start Action</span></span>

<span data-ttu-id="e4aaf-289">Visual Studio 및 ASP.NET 아키텍처의 또 다른 향상 된 기능은 편집 하며 계속 하기 영역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-289">Another great enhancement to Visual Studio and the ASP.NET architecture is in the area of edit and continue.</span></span> <span data-ttu-id="e4aaf-290">Visual Studio 2005에서 개발자는 프로젝트 디버깅을 시작 하 고 디버거를 분리 하지 않고 프로젝트에서 코드를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-290">In Visual Studio 2005, developers can start debugging a project and make code changes on the project without detaching the debugger.</span></span> <span data-ttu-id="e4aaf-291">실제로 디버거를 분리 하지 않고 프로젝트 디버깅을 시작 하 고, 새 클래스를 추가 하 고, 해당 클래스에 코드를 추가 하 고, 해당 클래스의 새 인스턴스를 만들고 클래스의 메서드를 실행 하는 코드를 페이지에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-291">In fact, you can literally start debugging a project, add a new class, add code to that class, add code to your page that creates a new instance of that class and execute a method of the class, all without detaching the debugger.</span></span> <span data-ttu-id="e4aaf-292">새 코드를 실행 하는 것은 브라우저를 새로 고치는 것 만큼 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-292">Executing the new code is literally as easy as refreshing the browser!</span></span>

<span data-ttu-id="e4aaf-293">Visual Studio 2005에서 편집 하며 계속 하기 기능의 비디오 연습을 보려면 여기를 클릭 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-293">Click here to see a video walkthrough of the edit and continue feature in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image2.png)

[<span data-ttu-id="e4aaf-294">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-294">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

<span data-ttu-id="e4aaf-295">ASP.NET 2.0 및 Visual Studio 2005의 강력한 편집 및 계속 기능은 ASP.NET 응용 프로그램에 대 한 아키텍처 변경 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-295">The robust edit and continue functionality in ASP.NET 2.0 and Visual Studio 2005 is due to an architectural change for ASP.NET applications.</span></span> <span data-ttu-id="e4aaf-296">ASP.NET 1.x에서 Visual Studio 2002/2003에서 만든 응용 프로그램은 해당 응용 프로그램 폴더에 저장 된 주 어셈블리로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-296">In ASP.NET 1.x, applications created in Visual Studio 2002/2003 were compiled into a primary assembly that was stored in the /bin folder.</span></span> <span data-ttu-id="e4aaf-297">응용 프로그램의 모든 클래스, 페이지 등은 해당 DLL로 컴파일 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-297">All classes, pages, etc. for the application were compiled into that one DLL.</span></span> <span data-ttu-id="e4aaf-298">그런 다음 런타임에 ASP.NET는 모든 컨트롤, 태그 및 ASP.NET 코드를 페이지 내에서 컴파일하고 이러한 Dll을 ASP.NET 임시 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-298">Then at runtime, ASP.NET would compile all of the controls, markup, and ASP.NET code within pages and copy those DLLs into the ASP.NET temporary folder.</span></span>

<span data-ttu-id="e4aaf-299">Visual Studio 2005에서 ASP.NET 2.0을 사용 하는 경우 위의 두 가지 컴파일 모델 개요 (Visual Studio 용 one 개와 런타임에 하나는 ASP.NET)가 하나의 일반적인 컴파일 모델에 병합 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-299">In Visual Studio 2005 using ASP.NET 2.0, the two compilation models outline above (one for Visual Studio and one for ASP.NET at runtime) have been merged into one common compilation model.</span></span> <span data-ttu-id="e4aaf-300">즉, 모든 컴파일 문제는 이제 런타임 대신 개발 단계에서 catch 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-300">That means that all compilation issues are now caught during the development stage instead of at runtime.</span></span> <span data-ttu-id="e4aaf-301">또한 사용자 컨트롤 및 마스터 페이지와 같은 기능에 대 한 디자이너 및 IntelliSense 지원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-301">It also allows for designer and IntelliSense support for features such as user controls and master pages.</span></span>

<span data-ttu-id="e4aaf-302">사용자 정의 컨트롤에 대 한 디자이너 지원 비디오 연습을 보려면 여기를 클릭 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-302">Click here to see a video walkthrough of designer support for user controls.</span></span>

![](improvements-in-visual-studio-2005/_static/image3.png)

[<span data-ttu-id="e4aaf-303">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-303">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> <span data-ttu-id="e4aaf-304">사용자 정의 컨트롤이 페이지에서 제거 되 면 @Register 지시문은 태그에 남아 있으므로 사용자 정의 컨트롤이 웹 사이트에서 삭제 되는 경우 파서 오류를 방지 하기 위해 수동으로 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-304">When a user control is removed from a page, the @Register directive remains in the markup and should be removed manually in order to avoid parser errors if the user control is deleted from the Web site.</span></span>

<span data-ttu-id="e4aaf-305">Visual Studio 컴파일 모델의 또 다른 향상 된 기능은 웹 사이트 게시 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-305">Another improvement in the Visual Studio compilation model is the Publish Web Site feature.</span></span> <span data-ttu-id="e4aaf-306">게시 기능은 웹 사이트를 미리 컴파일하 므로 개발자는 필요에 따라 아무것도 컴파일하지 않고도 추가 된 성능을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-306">Because the Publish feature precompiles the Web site, developers can enjoy the added performance of not having to compile anything on demand.</span></span> <span data-ttu-id="e4aaf-307">또한 응용 프로그램/_Code 폴더의 모든 소스 코드를 DLL로 미리 컴파일하며 소스 코드를 배포할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-307">It also precompiles all source code in the App/_Code folder into a DLL so that no source code has to be deployed.</span></span>

![웹 사이트 게시 대화 상자](improvements-in-visual-studio-2005/_static/image7.jpg)

<span data-ttu-id="e4aaf-309">**그림 10**: 웹 사이트 게시 대화 상자</span><span class="sxs-lookup"><span data-stu-id="e4aaf-309">**Figure 10**: The Publish Web Site Dialog</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-310">Aspnet/_compile 유틸리티를 사용 하 여 ASP.NET 웹 응용 프로그램을 미리 컴파일할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-310">The aspnet/_compile.exe utility can also be used to pre-compile an ASP.NET Web application.</span></span> <span data-ttu-id="e4aaf-311">이 도구는 모듈 9에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-311">That tool will be covered in module 9.</span></span>

<span data-ttu-id="e4aaf-312">웹 사이트를 게시할 때 미리 컴파일된 파일은 아래와 같이 임시 ASP.NET Files 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-312">When you Publish a Web site, the precompiled files are stored in the Temporary ASP.NET Files folder as shown below.</span></span> <span data-ttu-id="e4aaf-313">파일 확장명이 *.compiled* 인 파일은 특정 dll에 대 한 종속성을 정의 하는 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-313">Files with a *.compiled* file extension are XML files that define dependencies for particular DLLs.</span></span> <span data-ttu-id="e4aaf-314">모든 Webform 또는 사용자 정의 컨트롤은 *App/_Web/_* 로 시작 하는 임의의 dll로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-314">Any Webform or user controls are compiled into random DLLs that begin with *App/_Web/_*.</span></span>

<span data-ttu-id="e4aaf-315">*미리 컴파일된이 사이트를 업데이트할 수 있도록 허용* 확인란을 선택 하지 않으면 Webforms 및 사용자 정의 컨트롤 내부의 태그가 DLL로 미리 컴파일되지 않으므로 배포 후에 변경 내용을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-315">If you leave the *Allow this precompiled site to be updatable* checkbox checked, markup inside of your Webforms and user controls will not be pre-compiled into a DLL allowing you to make changes after deployment.</span></span> <span data-ttu-id="e4aaf-316">배포 된 콘텐츠를 변경할 수 없도록 태그를 잠그려면이 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-316">If you would prefer to lock down the markup so that changes to the deployed content are not allowed, uncheck this box.</span></span>

<span data-ttu-id="e4aaf-317">*고정 이름 지정 및 단일 페이지 어셈블리 사용* 확인란을 사용 하면 각 페이지가 고정 된 이름의 어셈블리로 컴파일되도록 일괄 컴파일을 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-317">The *Use fixed naming and single page assemblies* checkbox allows you to disable batch compilation so that each page is compiled into a fixed-named assembly.</span></span> <span data-ttu-id="e4aaf-318">이 확인란을 선택 하지 않은 상태로 두면 일괄 컴파일을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-318">Leaving this box unchecked allows you to take advantage of batch compilation.</span></span>

<span data-ttu-id="e4aaf-319">*미리 컴파일된 어셈블리에서 강력한 이름 지정* 확인란을 사용 하면 미리 컴파일된 어셈블리를 강력한 이름으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-319">The *Enable strong naming on precompiled assemblies* checkbox allows you to strong-name your precompiled assemblies.</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-320">ASP.NET 1.x에서 강력한 이름의 어셈블리는 GAC (전역 어셈블리 캐시)에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-320">In ASP.NET 1.x, strong-named assemblies had to be installed into the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="e4aaf-321">ASP.NET 2.0에서는 강력한 이름의 어셈블리를 GAC에 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-321">In ASP.NET 2.0, you are not required to install strong-named assemblies into the GAC.</span></span>

![ASP.NET 응용 프로그램 미리 컴파일된 파일](improvements-in-visual-studio-2005/_static/image8.jpg)

<span data-ttu-id="e4aaf-323">**그림 11**: 미리 컴파일된 파일 ASP.NET 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e4aaf-323">**Figure 11**: An ASP.NET Applications Pre-Compiled Files</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-324">위의 응용 프로그램에 web.config 파일이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-324">In the application above, there was no web.config file.</span></span> <span data-ttu-id="e4aaf-325">웹 사이트를 게시 한 후에는 *PrecompiledApp* 가 호출 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-325">If there had been, it would have been called *PrecompiledApp.config* after the Publish Web site process.</span></span>

## <a name="improvements-in-deployment"></a><span data-ttu-id="e4aaf-326">배포의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="e4aaf-326">Improvements in Deployment</span></span>

<span data-ttu-id="e4aaf-327">Visual Studio 2002 및 2003와 마찬가지로 Visual Studio 2005는 프로젝트 복사 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-327">As with Visual Studio 2002 and 2003, Visual Studio 2005 offers a Copy Project feature.</span></span> <span data-ttu-id="e4aaf-328">그러나이 기능은 Visual Studio 2005에 포함 되어 있으며 이제 웹 사이트 복사 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-328">However, the feature has been beefed up in Visual Studio 2005 and is now called Copy Web Site.</span></span>

<span data-ttu-id="e4aaf-329">웹 사이트 복사 대화 상자는 왼쪽 프레임 및 오른쪽 프레임으로 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-329">The Copy Web Site dialog is split into a left frame and a right frame.</span></span> <span data-ttu-id="e4aaf-330">왼쪽 프레임을 원본 웹 사이트 라고 하며, 오른쪽 프레임을 원격 웹 사이트 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-330">The left frame is called the Source Web Site and the right frame is called the Remote Web Site.</span></span> <span data-ttu-id="e4aaf-331">일부 개발자와 혼동 될 수 있는 한 가지는 오른쪽 프레임에 표시 되는 사이트가 반드시 원격 사이트 일 필요는 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-331">One thing that may confuse some developers is that the site displayed in the right frame is not necessarily a remote site.</span></span> <span data-ttu-id="e4aaf-332">로컬 파일 시스템 또는 IIS의 로컬 인스턴스에 있는 사이트 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-332">It could be a site on the local file system or on the local instance of IIS.</span></span> <span data-ttu-id="e4aaf-333">또한 대화 상자를 사용 하 여 원격 *웹 사이트에서* 원본 웹 사이트로 게시할 수 있으므로 왼쪽 프레임에 표시 되는 사이트는 반드시 원본 웹 사이트가 될 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-333">Additionally, the site displayed in the left frame is not necessarily the source Web site because the dialog allows you to publish from the remote Web site *to* the source Web site.</span></span>

<span data-ttu-id="e4aaf-334">프로젝트를 원격 웹 사이트에 복사 하는 경우 해당 사이트에 FrontPage Server Extensions 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-334">If you are copying a project to a remote Web site, that site must have the FrontPage Server Extensions installed on it.</span></span> <span data-ttu-id="e4aaf-335">그렇지 않은 경우 FTP를 사용 하 여 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-335">If it does not, you will need to connect using FTP.</span></span> <span data-ttu-id="e4aaf-336">반면, 프로젝트를 로컬 IIS 인스턴스에 복사 하는 경우 FrontPage Server Extensions 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-336">On the other hand, if you are copying a project to the local IIS instance, FrontPage Server Extensions are not required.</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-337">로컬 IIS 인스턴스에서 새 웹 사이트를 만들려고 하 고 FrontPage 2002 Server Extensions가 설치 된 경우 SharePoint 서버에서 웹 사이트를 만드는 것이 지원 되지 않음을 알리는 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-337">If you try to create a new Web site on the local IIS instance and the FrontPage 2002 Server Extensions are installed, you will get an error message telling you that creating Web sites is not supported on a SharePoint server.</span></span> <span data-ttu-id="e4aaf-338">이 경우 FrontPage 2000 서버 확장을 설치 하거나 FrontPage Server Extensions를 제거 하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-338">In that case, you have the option of installing the FrontPage 2000 Server Extensions or removing the FrontPage Server Extensions.</span></span>

<span data-ttu-id="e4aaf-339">웹 사이트 복사 기능의 비디오 연습을 보려면 여기를 클릭 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-339">Click here for a video walkthrough of the Copy Web Site feature.</span></span>

![](improvements-in-visual-studio-2005/_static/image4.png)

[<span data-ttu-id="e4aaf-340">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-340">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a><span data-ttu-id="e4aaf-341">디버깅의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="e4aaf-341">Improvements in Debugging</span></span>

<span data-ttu-id="e4aaf-342">Visual Studio 2005의 디버깅에는 네 가지 주요 향상 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-342">There are four key improvements in debugging in Visual Studio 2005.</span></span>

- <span data-ttu-id="e4aaf-343">관리자가 아닌 관리자로 로컬로 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-343">Debugging locally as a non-administrator is possible out of the box.</span></span>
- <span data-ttu-id="e4aaf-344">컴파일 요소의 Debug 특성은 이제 기본적으로 false입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-344">The Debug attribute for the Compilation element is now false by default.</span></span>
- <span data-ttu-id="e4aaf-345">원격 디버깅을 설치 하 고 구성 하는 것이 이전 보다 쉬워졌습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-345">Remote debugging setup and configuration is easier than before.</span></span>
- <span data-ttu-id="e4aaf-346">이제 FTP 위치를 통해 열린 웹 사이트를 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-346">You can now debug a Web site opened via an FTP location.</span></span>

## <a name="debugging-as-a-non-administrator"></a><span data-ttu-id="e4aaf-347">비관리자로 디버깅</span><span class="sxs-lookup"><span data-stu-id="e4aaf-347">Debugging as a Non-Administrator</span></span>

<span data-ttu-id="e4aaf-348">ASP.NET 개발 서버를 추가 하 여 관리자가 아닌 ASP.NET 응용 프로그램을 즉시 쉽게 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-348">The addition of the ASP.NET Development Server allows non-administrators to easily debug ASP.NET applications right out of the box.</span></span> <span data-ttu-id="e4aaf-349">로컬 파일 시스템에서 실행 되는 ASP.NET 응용 프로그램을 디버그 하는 경우 Visual Studio는 로그온 한 사용자의 컨텍스트에서 ASP.NET 개발 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-349">When an ASP.NET application running on the local file system is debugged, Visual Studio launches the ASP.NET Development Server under the context of the logged-on user.</span></span> <span data-ttu-id="e4aaf-350">그러면 해당 사용자가 추가 구성 없이 해당 응용 프로그램을 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-350">That user can then debug that application without any additional configuration.</span></span>

## <a name="debug-is-false-by-default"></a><span data-ttu-id="e4aaf-351">디버그는 기본적으로 False입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-351">Debug is False by Default</span></span>

<span data-ttu-id="e4aaf-352">ASP.NET 1.x에서 web.config 파일의 *컴파일* 요소에 있는 *debug* 특성은 기본적으로 *true* 로 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-352">In ASP.NET 1.x, the *debug* attribute in the *compilation* element of the web.config file was set to *true* by default.</span></span> <span data-ttu-id="e4aaf-353">개발자는 응용 프로그램을 프로덕션에 배포 하기 전에이 특성을 *false* 로 설정 하는 것이 항상 권장 됩니다. 그러나 대부분의 개발자는 debug 특성을 true로 설정 된 상태로 유지 하는 결과를 완전히 이해 하지 못하기 때문에 단순히 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-353">It has always been recommended that developers set this attribute to *false* before deploying an application to production, but because most developers don't fully understand the consequences of leaving the debug attribute set to true, they simply left it as-is.</span></span>

<span data-ttu-id="e4aaf-354">Debug 특성을 true로 설정 하는 경우 가장 심각한 문제는 안전망 batch 컴파일 모델을 사용 하지 않도록 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-354">The most severe problem with having the debug attribute set to true is that it disables ASP.NETs batch compilation model.</span></span> <span data-ttu-id="e4aaf-355">따라서 각 페이지는 별도의 DLL로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-355">Therefore, each page is compiled into a separate DLL.</span></span> <span data-ttu-id="e4aaf-356">웹 응용 프로그램이 수천 개의 페이지로 구성 된 경우 (어떤 방법으로도 적도 되지 않음) 해당 응용 프로그램에서 수천 개의 작은 Dll이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-356">If a Web application consists of thousands of pages (not unheard of by any means), that means several thousand small DLLs will be created by that application.</span></span> <span data-ttu-id="e4aaf-357">이러한 Dll의 크기는 작지만 메모리의 특정 위치로 로드 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-357">While these DLLs are small in size, they are not loaded into any particular location in memory.</span></span> <span data-ttu-id="e4aaf-358">따라서 시스템 메모리에서 조각화를 발생 하 고 OutOfMemoryException 발생에 기여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-358">Therefore, they cause fragmentation in system memory and can contribute to OutOfMemoryException occurrences.</span></span>

<span data-ttu-id="e4aaf-359">ASP.NET 2.0에서 debug 특성은 기본적으로 false로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-359">In ASP.NET 2.0, the debug attribute is set to false by default.</span></span> <span data-ttu-id="e4aaf-360">앞서 살펴본 바와 같이 개발자가 Visual Studio 2005에서 ASP.NET 응용 프로그램을 디버그할 때 디버깅을 사용 하도록 설정 된 web.config 파일을 추가 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-360">As you have already seen, when a developer debugs an ASP.NET application in Visual Studio 2005, they are prompted to add a web.config file with debugging enabled.</span></span> <span data-ttu-id="e4aaf-361">이렇게 하면 ASP.NET 1.x에 있는 것과 동일한 단점이 발생 하지만, 이제 응용 프로그램을 프로덕션 환경으로 이동 하기 전에 개발자에 게 특성을 false로 다시 설정 해야 한다는 경고 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-361">Doing so incurs the same drawbacks that were present in ASP.NET 1.x, but now the developer is clearly warned that the attribute should be reset to false before moving the application to production.</span></span>

## <a name="remote-debugging-setup-and-configuration"></a><span data-ttu-id="e4aaf-362">원격 디버깅 설정 및 구성</span><span class="sxs-lookup"><span data-stu-id="e4aaf-362">Remote Debugging Setup and Configuration</span></span>

<span data-ttu-id="e4aaf-363">Visual Studio 2002/2003에서 원격 디버깅은 컴퓨터 디버그 관리자 (mdm .exe) 및 vs7jit 프로세스에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-363">In Visual Studio 2002/2003, remote debugging relied on the Machine Debug Manager (mdm.exe) and the vs7jit.exe process.</span></span> <span data-ttu-id="e4aaf-364">이로 인해 원격 디버깅 문제를 해결 하는 것은 종종 고객을 위한 블랙 박스 이며 PSS의 경우 훨씬 더 좋은 경우가 많았습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-364">Because of that, troubleshooting remote debugging problems was often a black box for customers and it was often not much better for PSS.</span></span>

<span data-ttu-id="e4aaf-365">Visual Studio 2005는 mdm .exe 및 vs7jit 프로세스에 대 한 의존도를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-365">Visual Studio 2005 removes the reliance on the mdm.exe and vs7jit.exe processes.</span></span> <span data-ttu-id="e4aaf-366">대신, 이제 원격 디버그 모니터 서비스 (msvsmon.exe)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-366">Instead, it now uses the Remote Debug Monitor service (msvsmon.exe.)</span></span>

<span data-ttu-id="e4aaf-367">Visual Studio 2005 원격으로 디버깅 하는 데 필요한 요구 사항은 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-367">The requirement for debugging in Visual Studio 2005 remotely is quite simple.</span></span> <span data-ttu-id="e4aaf-368">디버깅 하기 전에 원격 서버에서 msvsmon.exe를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-368">You need to run msvsmon.exe on the remote server prior to debugging.</span></span> <span data-ttu-id="e4aaf-369">Visual Studio CD에서 원격 디버그 모니터를 설치 하거나, 웹 서버에 아무것도 설치 하지 않고 공유에서 msvsmon.exe를 실행 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-369">You can install the Remote Debug Monitor from the Visual Studio CD or you can simply run msvsmon.exe from a share without installing anything at all on the Web server.</span></span>

<span data-ttu-id="e4aaf-370">Msvsmon.exe를 실행 하는 경우 원격 디버깅을 위해 차단 되는 포트에 대 한 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-370">When you run msvsmon.exe, it is likely that it will complain about ports being blocked for remote debugging.</span></span> <span data-ttu-id="e4aaf-371">다행히 아래와 같이 경고 대화 상자 내에서 적절 한 포트를 쉽게 차단 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-371">Fortunately, you can easily unblock the ports from right within the warning dialog as shown below.</span></span>

![Windows 방화벽이 원격 디버깅을 차단 하 고 있음을 알립니다.](improvements-in-visual-studio-2005/_static/image9.jpg)

<span data-ttu-id="e4aaf-373">**그림 12**: Windows 방화벽이 원격 디버깅을 차단 한다는 알림</span><span class="sxs-lookup"><span data-stu-id="e4aaf-373">**Figure 12**: Notification that Windows Firewall is Blocking Remote Debugging</span></span>

<span data-ttu-id="e4aaf-374">디버깅에 필요한 포트를 차단 해제 한 후에는 아래와 같이 원격 디버깅 모니터 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-374">Once you have unblocked the ports necessary for debugging, you will see the Remote Debugging Monitor as shown below.</span></span> <span data-ttu-id="e4aaf-375">이 인터페이스에서 연결을 모니터링 하 고 디버깅 권한을 쉽게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-375">From this interface, you can monitor connections and change debugging permissions easily.</span></span>

![원격 디버깅 모니터](improvements-in-visual-studio-2005/_static/image10.jpg)

<span data-ttu-id="e4aaf-377">**그림 13**: 원격 디버깅 모니터</span><span class="sxs-lookup"><span data-stu-id="e4aaf-377">**Figure 13**: The Remote Debugging Monitor</span></span>

<span data-ttu-id="e4aaf-378">FTP를 통해 열린 웹 응용 프로그램을 원격으로 디버그할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-378">It is also possible to remotely debug a Web application opened via FTP.</span></span> <span data-ttu-id="e4aaf-379">단계는 앞에서 설명한 것과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-379">The steps are the same as those previously covered.</span></span> <span data-ttu-id="e4aaf-380">그러나이 모듈의 앞부분에서 설명한 대로 FTP 프로젝트를 검색 하는 데 사용할 기본 URL을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-380">However, you will need to specify a base URL for browsing the FTP project as outlined earlier in this module.</span></span>

## <a name="lab-2"></a><span data-ttu-id="e4aaf-381">랩 2</span><span class="sxs-lookup"><span data-stu-id="e4aaf-381">Lab 2</span></span>

## <a name="remote-debugging-with-visual-studio-2005"></a><span data-ttu-id="e4aaf-382">Visual Studio 2005을 사용 하 여 원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="e4aaf-382">Remote Debugging with Visual Studio 2005</span></span>

<span data-ttu-id="e4aaf-383">이 랩에서는 Visual Studio 2005을 사용 하 여 원격으로 디버깅 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-383">This lab will walk you through remote debugging with Visual Studio 2005.</span></span>

<span data-ttu-id="e4aaf-384">이 랩의 비디오 연습을 보려면 여기를 클릭 하세요.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-384">Click here for a video walkthrough of this lab.</span></span>

![](improvements-in-visual-studio-2005/_static/image5.png)

[<span data-ttu-id="e4aaf-385">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="e4aaf-385">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

<span data-ttu-id="e4aaf-386">이 랩에서는 두 대의 컴퓨터가 있어야 합니다. 하나는 Visual Studio 2005를 실행 하 고 다른 하나는 IIS를 실행 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-386">This lab requires you to have two machines, one running Visual Studio 2005 and the other running IIS 5 or greater.</span></span>

1. <span data-ttu-id="e4aaf-387">Visual Studio 2005을 열고 원격 서버에 새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-387">Open Visual Studio 2005 and create a new Web site on the remote server.</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-388">원격 IIS 인스턴스나 FTP를 통해 웹 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-388">You can create the Web site on a remote IIS instance or via FTP.</span></span>

1. <span data-ttu-id="e4aaf-389">원격 웹 서버에서 UNC 경로를 사용 하 여 개발 컴퓨터의 msvsmon.exe를 찾아 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-389">From the remote Web server, locate msvsmon.exe on the development machine using a UNC path and execute it.</span></span>  
 <span data-ttu-id="e4aaf-390">Msvsmon.exe의 기본 위치는 server/c $/Program Files/Microsoft Visual Studio 8/Common7/IDE/원격 디버거/x86입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-390">The default location for msvsmon.exe is //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.</span></span>
2. <span data-ttu-id="e4aaf-391">원격 디버깅을 위해 포트를 차단 해제 하 라는 메시지가 표시 되 면이를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-391">If prompted to unblock ports for remote debugging, do so.</span></span>
3. <span data-ttu-id="e4aaf-392">개발 컴퓨터에서 default.aspx에 대 한 코드 숨김으로 열고 페이지/_Load 메서드에서 중단점을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-392">From the development machine, open the code-behind for Default.aspx and set a breakpoint in the Page/_Load method.</span></span>
4. <span data-ttu-id="e4aaf-393">개발 컴퓨터에서 디버깅을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-393">Start debugging from the development machine.</span></span>

<span data-ttu-id="e4aaf-394">중단점은 예상 대로 적중 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-394">You should hit the breakpoint as expected.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="e4aaf-395">ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="e4aaf-395">ASP.NET Development Server</span></span>

<span data-ttu-id="e4aaf-396">이미 논의 한 대로 Visual Studio 2005는 ASP.NET 개발 서버 라는 웹 서버와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-396">As we've already discussed, Visual Studio 2005 ships with a Web server called the ASP.NET Development Server.</span></span> <span data-ttu-id="e4aaf-397">ASP.NET 개발 서버는 경우에 따라 Cassini 라고도 합니다. 이 웹 서버는 파일 시스템에서 실행 되는 웹 응용 프로그램을 찾아보고 디버그 하는 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-397">(The ASP.NET Development Server is sometimes referred to as Cassini.) This Web server is a convenient means to browse and debug Web applications running on the file system.</span></span>

<span data-ttu-id="e4aaf-398">ASP.NET 개발 서버 제한 된 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-398">The ASP.NET Development Server is a restricted Web server.</span></span> <span data-ttu-id="e4aaf-399">원격 연결을 허용 하지 않습니다. 웹 서버를 시작한 사용자가 아닌 다른 사용자의 요청은 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-399">It does not allow remote connections, it does not allow any requests from any user other than the user who started the Web server.</span></span> <span data-ttu-id="e4aaf-400">또한 ASP 페이지를 제공할 수 있는 기능이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-400">It also does not have the capability of serving ASP pages.</span></span> <span data-ttu-id="e4aaf-401">ASP.NET 리소스와 HTML 리소스 (이미지, CSS 파일 등 포함)만 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-401">Only ASP.NET resources and HTML resources (including images, CSS files, etc.) are served.</span></span>

<span data-ttu-id="e4aaf-402">C:/Windows/Microsoft .NET/Framework/v2.0/ */* / */* /\*에 있는 webdev .exe 파일을 실행 하 여 명령줄을 통해 ASP.NET 개발 서버를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-402">The ASP.NET Development Server can be launched via the command line by running the WebDev.WebServer.exe file located at c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*.</span></span> <span data-ttu-id="e4aaf-403">다음 대화 상자에는 사용할 수 있는 매개 변수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-403">The following dialog displays the parameters that are available.</span></span>

![](improvements-in-visual-studio-2005/_static/image11.jpg)

<span data-ttu-id="e4aaf-404">**그림 14**</span><span class="sxs-lookup"><span data-stu-id="e4aaf-404">**Figure 14**</span></span>

> [!NOTE]
> <span data-ttu-id="e4aaf-405">명령줄을 통해 명시적으로 시작 된 경우에는 ASP.NET 개발 서버 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4aaf-405">The ASP.NET Development Server is not supported when launched explicitly via the command line.</span></span>
