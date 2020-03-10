---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 릴리스 정보에 대 한 ASP.NET 및 Web Tools | Microsoft Docs
author: microsoft
description: 이 문서에서는 Visual Studio 2013의 ASP.NET 및 Web Tools 릴리스에 대해 설명 합니다.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449525"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="daea0-103">Visual Studio 2013용 ASP.NET 및 Web Tools 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="daea0-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="daea0-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="daea0-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="daea0-105">이 문서에서는 Visual Studio 2013의 ASP.NET 및 Web Tools 릴리스에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="daea0-106">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="daea0-106">Contents</span></span>

- [<span data-ttu-id="daea0-107">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="daea0-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="daea0-108">설명서</span><span class="sxs-lookup"><span data-stu-id="daea0-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="daea0-109">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="daea0-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="daea0-110">Visual Studio 2013 ASP.NET 및 Web Tools의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="daea0-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="daea0-111">ASP.NET 1 개</span><span class="sxs-lookup"><span data-stu-id="daea0-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="daea0-112">새 웹 프로젝트 환경</span><span class="sxs-lookup"><span data-stu-id="daea0-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="daea0-113">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="daea0-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="daea0-114">브라우저 링크</span><span class="sxs-lookup"><span data-stu-id="daea0-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="daea0-115">Visual Studio 웹 편집기의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="daea0-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="daea0-116">Visual Studio에서 Web Apps 지원 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="daea0-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="daea0-117">웹 게시 향상</span><span class="sxs-lookup"><span data-stu-id="daea0-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="daea0-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="daea0-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="daea0-119">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="daea0-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="daea0-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="daea0-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="daea0-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="daea0-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="daea0-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="daea0-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="daea0-123">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="daea0-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="daea0-124">Microsoft OWIN 구성 요소</span><span class="sxs-lookup"><span data-stu-id="daea0-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="daea0-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="daea0-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="daea0-126">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="daea0-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="daea0-127">ASP.NET 앱 일시 중단</span><span class="sxs-lookup"><span data-stu-id="daea0-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="daea0-128">알려진 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="daea0-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="daea0-129">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="daea0-129">Installation Notes</span></span>

<span data-ttu-id="daea0-130">Visual Studio 2013에 대 한 ASP.NET 및 Web Tools는 기본 설치 관리자에 번들로 제공 되며 [여기](https://www.asp.net/downloads)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="daea0-131">문서화</span><span class="sxs-lookup"><span data-stu-id="daea0-131">Documentation</span></span>

<span data-ttu-id="daea0-132">Visual Studio 2013 ASP.NET 및 Web Tools에 대 한 자습서 및 기타 정보는 [ASP.NET 웹 사이트](https://www.asp.net/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="daea0-133">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="daea0-133">Software Requirements</span></span>

<span data-ttu-id="daea0-134">ASP.NET 및 Web Tools에는 Visual Studio 2013 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="daea0-135">Visual Studio 2013 ASP.NET 및 Web Tools의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="daea0-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="daea0-136">다음 섹션에서는 릴리스에 도입 된 기능에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="daea0-137">ASP.NET 1 개</span><span class="sxs-lookup"><span data-stu-id="daea0-137">One ASP.NET</span></span>

<span data-ttu-id="daea0-138">Visual Studio 2013 릴리스에서는 ASP.NET 기술을 사용 하는 환경을 통합 하는 단계를 수행 하 여 원하는 것을 쉽게 조합 하 고 일치 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="daea0-139">예를 들어 MVC를 사용 하 여 프로젝트를 시작 하 고 나중에 Web Forms 페이지를 프로젝트에 쉽게 추가 하거나 Web Forms 프로젝트에서 웹 Api를 스 캐 폴드 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="daea0-140">한 가지 ASP.NET는 개발자가 ASP.NET에서 선호 하는 작업을 수행 하는 데 도움이 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="daea0-141">선택한 기술에 관계 없이 하나의 ASP.NET 신뢰할 수 있는 기본 프레임 워크를 기반으로 하는 확신을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="daea0-142">새 웹 프로젝트 환경</span><span class="sxs-lookup"><span data-stu-id="daea0-142">New Web Project Experience</span></span>

<span data-ttu-id="daea0-143">Visual Studio 2013에서 새 웹 프로젝트를 만드는 환경을 향상 시켰습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="daea0-144">**새 ASP.NET 웹 프로젝트** 대화 상자에서 원하는 프로젝트 형식을 선택 하 고, 기술의 조합 (WEB FORMS, MVC, Web API)을 구성 하 고, 인증 옵션을 구성 하 고, 단위 테스트 프로젝트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![새 ASP.NET 프로젝트](release-notes/_static/image1.png)

<span data-ttu-id="daea0-146">새 대화 상자를 사용 하 여 많은 템플릿에 대 한 기본 인증 옵션을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="daea0-147">예를 들어 ASP.NET Web Forms 프로젝트를 만들 때 다음 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="daea0-148">인증 없음</span><span class="sxs-lookup"><span data-stu-id="daea0-148">No Authentication</span></span>
- <span data-ttu-id="daea0-149">개별 사용자 계정 (ASP.NET 멤버 자격 또는 소셜 공급자 로그인)</span><span class="sxs-lookup"><span data-stu-id="daea0-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="daea0-150">조직 계정 (인터넷 응용 프로그램의 Active Directory)</span><span class="sxs-lookup"><span data-stu-id="daea0-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="daea0-151">Windows 인증 (인트라넷 응용 프로그램의 Active Directory)</span><span class="sxs-lookup"><span data-stu-id="daea0-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![인증 옵션](release-notes/_static/image2.png)

<span data-ttu-id="daea0-153">웹 프로젝트를 만드는 새 프로세스에 대 한 자세한 내용은 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](creating-web-projects-in-visual-studio.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="daea0-154">새 인증 옵션에 대 한 자세한 내용은이 문서의 뒷부분에 나오는 [ASP.NET Identity](#TOC8) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="daea0-155">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="daea0-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="daea0-156">ASP.NET 스 캐 폴딩은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="daea0-157">이를 통해 데이터 모델과 상호 작용 하는 상용구 코드를 프로젝트에 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="daea0-158">이전 버전의 Visual Studio에서 스 캐 폴딩은 ASP.NET MVC 프로젝트로 제한 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="daea0-159">Visual Studio 2013를 사용 하 여 이제 Web Forms를 비롯 한 모든 ASP.NET 프로젝트에 스 캐 폴딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="daea0-160">Visual Studio 2013는 현재 Web Forms 프로젝트에 대 한 페이지 생성을 지원 하지 않지만 프로젝트에 MVC 종속성을 추가 하 여 Web Forms에서 스 캐 폴딩을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="daea0-161">Web Forms에 대 한 페이지 생성 지원은 향후 업데이트에서 추가 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="daea0-162">스 캐 폴딩을 사용 하는 경우 모든 필수 종속성이 프로젝트에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="daea0-163">예를 들어 ASP.NET Web Forms 프로젝트로 시작한 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가 하는 경우 필요한 NuGet 패키지와 참조가 프로젝트에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="daea0-164">Web Forms 프로젝트에 MVC 스 캐 폴딩을 추가 하려면 **새 스 캐 폴드 항목** 을 추가 하 고 대화 상자 창에서 **mvc 5 종속성** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="daea0-165">MVC 스 캐 폴딩에 대 한 두 가지 옵션이 있습니다. 최소 및 전체.</span><span class="sxs-lookup"><span data-stu-id="daea0-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="daea0-166">최소를 선택 하면 ASP.NET MVC에 대 한 NuGet 패키지 및 참조만 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="daea0-167">전체 옵션을 선택 하는 경우 최소 종속성 뿐만 아니라 MVC 프로젝트에 필요한 콘텐츠 파일이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="daea0-168">비동기 컨트롤러 스 캐 폴딩에 대 한 지원은 Entity Framework 6의 새로운 비동기 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="daea0-169">자세한 내용 및 자습서는 [ASP.NET 스 캐 폴딩 개요](aspnet-scaffolding-overview.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="daea0-170">브라우저 링크 – 브라우저와 Visual Studio 간 SignalR channel</span><span class="sxs-lookup"><span data-stu-id="daea0-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="daea0-171">새 [브라우저 링크](using-browser-link.md) 기능을 사용 하 여 여러 브라우저를 Visual Studio에 연결 하 고 도구 모음에서 단추를 클릭 하 여 모두 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="daea0-172">모바일 에뮬레이터를 포함 하 여 여러 브라우저를 개발 사이트에 연결 하 고 새로 고침을 클릭 하 여 모든 브라우저를 동시에 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="daea0-173">또한 브라우저 링크는 개발자가 브라우저 링크 확장을 작성할 수 있도록 API를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="daea0-174">개발자가 브라우저 링크 API를 활용할 수 있도록 하 여 Visual Studio와 연결 된 브라우저 간에 경계를 교차 하는 매우 고급 시나리오를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="daea0-175">Web Essentials는 API를 활용 하 여 Visual Studio와 브라우저의 개발자 도구 간에 통합 된 환경을 만듭니다. 원격으로 모바일 에뮬레이터를 제어 하 고 더 많은 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="daea0-176">Visual Studio 웹 편집기의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="daea0-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="daea0-177">Visual Studio 2013에는 웹 응용 프로그램의 Razor 파일 및 HTML 파일용 새 HTML 편집기가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="daea0-178">새 HTML 편집기는 HTML5를 기반으로 하는 단일 통합 스키마를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="daea0-179">자동 중괄호 완성, jQuery UI 및 AngularJS 특성 IntelliSense, 특성 IntelliSense 그룹화, ID 및 클래스 이름 Intellisense, 향상 된 성능, 형식 지정 및 스마트 태그를 비롯 한 기타 향상 된 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="daea0-180">다음 스크린샷에서는 HTML 편집기에서 부트스트랩 특성 IntelliSense를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML 편집기의 Intellisense](release-notes/_static/image4.png)

<span data-ttu-id="daea0-182">Visual Studio 2013는 CoffeeScript 및 LESS 편집기가 모두 내장 되어 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="daea0-183">LESS 편집기는 CSS 편집기의 모든 쿨 기능과 함께 제공 되며 @import 체인의 모든 LESS 문서에서 변수 및 mixin에 대 한 특정 Intellisense가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="daea0-184">Visual Studio에서 Web Apps 지원 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="daea0-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="daea0-185">Azure SDK for .NET 2.2을 사용 하 Visual Studio 2013에서는 **서버 탐색기** 를 사용 하 여 원격 웹 앱과 직접 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="daea0-186">Azure 계정에 로그인 하 고, 새 웹 앱을 만들고, 앱을 구성 하 고, 실시간 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="daea0-187">SDK 2.2이 출시 된 후 곧 Azure에서 원격으로 디버그 모드에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="daea0-188">Azure App Service Web Apps의 새로운 기능은 대부분 Azure SDK for .NET의 현재 릴리스를 설치할 때 Visual Studio 2012 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="daea0-189">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="daea0-190">Azure App Service에서 ASP.NET 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="daea0-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="daea0-191">Visual Studio를 사용하여 Azure App Service의 웹앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="daea0-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="daea0-192">웹 게시 향상</span><span class="sxs-lookup"><span data-stu-id="daea0-192">Web Publish Enhancements</span></span>

<span data-ttu-id="daea0-193">Visual Studio 2013에는 새롭고 향상 된 웹 게시 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="daea0-194">다음은 몇 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-194">Here are a few of them:</span></span>

- <span data-ttu-id="daea0-195">[Web.config 파일 암호화](https://go.microsoft.com/fwlink/?LinkId=325529)를 쉽게 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="daea0-196">(이 링크와 다음 두 가지는 MSDN에 대 한 설명서를 참조 하 여 10/17 년에 출시 될 때까지 사용 하지 못할 수 있음)</span><span class="sxs-lookup"><span data-stu-id="daea0-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="daea0-197">[배포 하는 동안 응용 프로그램을 오프 라인 상태로 만들기](https://go.microsoft.com/fwlink/?LinkId=325530)를 쉽게 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="daea0-198">서버에 복사할 파일을 결정 하기 위해 [마지막으로 변경 된 날짜 대신 파일 체크섬을 사용](https://go.microsoft.com/fwlink/?LinkId=325531) 하도록 웹 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="daea0-199">FTP 또는 파일 시스템 게시 방법과 웹 배포를 사용 하는 경우 선택한 개별 파일 (web.config 포함)을 신속 하 게 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="daea0-200">ASP.NET 웹 배포에 대 한 자세한 내용은 [ASP.NET 사이트](https://go.microsoft.com/fwlink/?LinkId=322027)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="daea0-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="daea0-201">NuGet 2.7</span></span>

<span data-ttu-id="daea0-202">NuGet 2.7에는 [nuget 2.7 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.7)에 자세히 설명 되어 있는 다양 한 새 기능 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="daea0-203">또한이 버전의 NuGet은 패키지를 다운로드 하기 위해 NuGet의 패키지 복원 기능에 대 한 명시적 동의를 제공 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="daea0-204">이제 NuGet을 설치 하 여 승인 (및 NuGet의 기본 설정 대화 상자에서 관련 된 확인란)이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="daea0-205">이제 패키지 복원은 기본적으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="daea0-206">ASP.NET 웹 양식</span><span class="sxs-lookup"><span data-stu-id="daea0-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="daea0-207">ASP.NET 1 개</span><span class="sxs-lookup"><span data-stu-id="daea0-207">One ASP.NET</span></span>

<span data-ttu-id="daea0-208">Web Forms 프로젝트 템플릿은 새로운 하나의 ASP.NET 환경과 원활 하 게 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="daea0-209">Web Forms 프로젝트에 MVC 및 Web API 지원을 추가할 수 있으며, 하나의 ASP.NET 프로젝트 만들기 마법사를 사용 하 여 인증을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="daea0-210">자세한 내용은 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](creating-web-projects-in-visual-studio.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="daea0-211">ASP.NET ID</span><span class="sxs-lookup"><span data-stu-id="daea0-211">ASP.NET Identity</span></span>

<span data-ttu-id="daea0-212">Web Forms 프로젝트 템플릿은 새로운 ASP.NET Identity 프레임 워크를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="daea0-213">또한 템플릿은 이제 Web Forms 인트라넷 프로젝트 만들기를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="daea0-214">자세한 내용은 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**의 [인증 방법](creating-web-projects-in-visual-studio.md#auth) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="daea0-215">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="daea0-215">Bootstrap</span></span>

<span data-ttu-id="daea0-216">Web Forms 템플릿은 [부트스트랩](http://twitter.github.io/bootstrap/) 을 사용 하 여 간단 하 고 응답성이 뛰어난 모양과 느낌을 제공 하 여 손쉽게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="daea0-217">자세한 내용은 [Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩](creating-web-projects-in-visual-studio.md#bootstrap)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="daea0-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="daea0-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="daea0-219">ASP.NET 1 개</span><span class="sxs-lookup"><span data-stu-id="daea0-219">One ASP.NET</span></span>

<span data-ttu-id="daea0-220">웹 MVC 프로젝트 템플릿은 새로운 하나의 ASP.NET 환경과 원활 하 게 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="daea0-221">ASP.NET 프로젝트 만들기 마법사 하나를 사용 하 여 MVC 프로젝트를 사용자 지정 하 고 인증을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="daea0-222">ASP.NET MVC 5에 대 한 소개 자습서는 [ASP.NET mvc 5 시작](../../../mvc/overview/getting-started/introduction/getting-started.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="daea0-223">MVC 4 프로젝트를 MVC 5로 업그레이드 하는 방법에 대 한 자세한 내용은 [ASP.NET mvc 4 및 WEB Api 프로젝트를 ASP.NET mvc 5 및 WEB api 2로 업그레이드 하는 방법](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="daea0-224">ASP.NET ID</span><span class="sxs-lookup"><span data-stu-id="daea0-224">ASP.NET Identity</span></span>

<span data-ttu-id="daea0-225">MVC 프로젝트 템플릿은 인증 및 id 관리를 위해 ASP.NET Identity를 사용 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="daea0-226">Facebook 및 Google 인증 및 새 멤버 자격 API를 사용 하는 자습서는 [facebook 및 Google OAuth2 및 Openid connect sign-on을 사용 하 여 ASP.NET mvc 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 및 [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱 만들기 및 Azure App Service에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="daea0-227">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="daea0-227">Bootstrap</span></span>

<span data-ttu-id="daea0-228">MVC 프로젝트 템플릿은 손쉽게 사용자 지정할 수 있는 슬림 하 고 응답성이 뛰어난 모양과 느낌을 제공 하기 위해 [부트스트랩](http://getbootstrap.com/) 을 사용 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="daea0-229">자세한 내용은 [Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩](creating-web-projects-in-visual-studio.md#bootstrap)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="daea0-230">인증 필터</span><span class="sxs-lookup"><span data-stu-id="daea0-230">Authentication filters</span></span>

<span data-ttu-id="daea0-231">인증 필터는 ASP.NET MVC 파이프라인에서 권한 부여 필터 전에 실행 되는 ASP.NET MVC의 새로운 종류의 필터 이며, 작업별, 컨트롤러당 또는 모든 컨트롤러에 대해 전역적으로 인증 논리를 지정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="daea0-232">인증 필터는 요청에서 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="daea0-233">인증 필터는 권한이 없는 요청에 대 한 응답으로 인증 문제를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="daea0-234">필터 재정의</span><span class="sxs-lookup"><span data-stu-id="daea0-234">Filter overrides</span></span>

<span data-ttu-id="daea0-235">이제 재정의 필터를 지정 하 여 지정 된 작업 메서드 또는 컨트롤러에 적용 되는 필터를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="daea0-236">재정의 필터는 지정 된 범위 (동작 또는 컨트롤러)에 대해 실행 하면 안 되는 필터 유형 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="daea0-237">이를 통해 전역적으로 적용 되는 필터를 구성한 다음 특정 작업 또는 컨트롤러에 적용 되는 특정 전역 필터를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="daea0-238">특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="daea0-238">Attribute routing</span></span>

<span data-ttu-id="daea0-239">ASP.NET MVC는 이제 [http://attributerouting.net](http://attributerouting.net)작성자 인 Tim mccall의 기여로 인해 특성 라우팅을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="daea0-240">특성 라우팅을 사용 하 여 작업 및 컨트롤러에 주석을 추가 하 여 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="daea0-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="daea0-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="daea0-242">특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="daea0-242">Attribute routing</span></span>

<span data-ttu-id="daea0-243">이제 ASP.NET Web API은 [http://attributerouting.net](http://attributerouting.net)의 작성자 인 Tim mccall의 기여로 인해 특성 라우팅을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="daea0-244">특성 라우팅을 사용 하 여 다음과 같이 작업 및 컨트롤러에 주석을 추가 하 여 Web API 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="daea0-245">특성 라우팅은 웹 API에서 Uri를 보다 강력 하 게 제어할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="daea0-246">예를 들어 단일 API 컨트롤러를 사용 하 여 리소스 계층을 쉽게 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="daea0-247">또한 특성 라우팅은 선택적 매개 변수, 기본값 및 경로 제약 조건을 지정 하는 편리한 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="daea0-248">특성 라우팅에 대 한 자세한 내용은 [WEB API 2에서 특성 라우팅](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="daea0-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="daea0-249">OAuth 2.0</span></span>

<span data-ttu-id="daea0-250">이제 Web API 및 단일 페이지 응용 프로그램 프로젝트 템플릿에서 OAuth 2.0을 사용한 권한 부여를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="daea0-251">OAuth 2.0은 보호 된 리소스에 대 한 클라이언트 액세스 권한을 부여 하기 위한 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="daea0-252">브라우저 및 모바일 장치를 비롯 한 다양 한 클라이언트에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="daea0-253">OAuth 2.0에 대 한 지원은 전달자 인증 및 권한 부여 서버 역할 구현에 Microsoft OWIN 구성 요소에서 제공 하는 새로운 보안 미들웨어를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="daea0-254">또는 Windows Server 2012 r 2에서 Azure Active Directory 또는 ADFS와 같은 조직 권한 부여 서버를 사용 하 여 클라이언트에 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="daea0-255">OData 개선 사항</span><span class="sxs-lookup"><span data-stu-id="daea0-255">OData Improvements</span></span>

<span data-ttu-id="daea0-256">**$Select, $expand, $batch 및 $value에 대 한 지원**</span><span class="sxs-lookup"><span data-stu-id="daea0-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="daea0-257">ASP.NET Web API OData는 이제 $select, $expand 및 $value에 대 한 완전 한 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="daea0-258">또한 요청 일괄 처리 및 변경 집합 처리에 $batch를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="daea0-259">$Select 및 $expand 옵션을 사용 하 여 OData 끝점에서 반환 되는 데이터의 모양을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="daea0-260">자세한 내용은 [WEB API OData에서 $Select 소개 및 $expand 지원](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="daea0-261">**향상 된 확장성**</span><span class="sxs-lookup"><span data-stu-id="daea0-261">**Improved extensibility**</span></span>

<span data-ttu-id="daea0-262">이제 OData 포맷터를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="daea0-263">Atom 항목 메타 데이터를 추가 하 고 명명 된 스트림 및 미디어 링크 항목을 지원 하 고 인스턴스 주석을 추가 하 고 링크가 생성 되는 방법을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="daea0-264">**지원 되지 않는 형식 지원**</span><span class="sxs-lookup"><span data-stu-id="daea0-264">**Type-less support**</span></span>

<span data-ttu-id="daea0-265">이제 엔터티 형식에 대 한 CLR 형식을 정의할 필요 없이 OData 서비스를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="daea0-266">대신 OData 컨트롤러는 OData 포맷터 직렬화/deserialize 인 **IEdmObject**인스턴스를 사용 하거나 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="daea0-267">**기존 모델 다시 사용**</span><span class="sxs-lookup"><span data-stu-id="daea0-267">**Reuse an existing model**</span></span>

<span data-ttu-id="daea0-268">기존 EDM (엔터티 데이터 모델)이 이미 있는 경우 새 EDM (엔터티 데이터 모델)을 빌드하는 대신 직접 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="daea0-269">예를 들어 Entity Framework를 사용 하는 경우 EF에서 작성 하는 EDM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="daea0-270">일괄 처리 요청</span><span class="sxs-lookup"><span data-stu-id="daea0-270">Request Batching</span></span>

<span data-ttu-id="daea0-271">요청 일괄 처리는 여러 작업을 단일 HTTP POST 요청으로 결합 하 여 네트워크 트래픽을 줄이고 더 부드럽고 번잡 사용자 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="daea0-272">ASP.NET Web API는 이제 요청 일괄 처리에 대 한 몇 가지 전략을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="daea0-273">OData 서비스의 $batch 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="daea0-274">단일 MIME 다중 파트 요청에 여러 요청을 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="daea0-275">사용자 지정 일괄 처리 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-275">Use a custom batching format.</span></span>

<span data-ttu-id="daea0-276">요청 일괄 처리를 사용 하도록 설정 하려면 일괄 처리 처리기가 있는 경로를 웹 API 구성에 추가 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="daea0-277">요청을 또는 순서에 관계 없이 실행할지 또는 실행할지를 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="daea0-278">이식 가능한 ASP.NET Web API 클라이언트</span><span class="sxs-lookup"><span data-stu-id="daea0-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="daea0-279">이제 ASP.NET Web API 클라이언트를 사용 하 여 Windows 스토어 및 Windows Phone 8 응용 프로그램에서 작동 하는 이식 가능한 클래스 라이브러리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="daea0-280">또한 클라이언트와 서버에서 공유할 수 있는 이식 가능한 포맷터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="daea0-281">향상 된 테스트 용이성</span><span class="sxs-lookup"><span data-stu-id="daea0-281">Improved Testability</span></span>

<span data-ttu-id="daea0-282">Web API 2를 사용 하면 API 컨트롤러를 더 쉽게 단위 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="daea0-283">요청 메시지 및 구성을 사용 하 여 API 컨트롤러를 인스턴스화한 다음 테스트할 동작 메서드를 호출 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="daea0-284">링크 생성을 수행 하는 작업 메서드에 대해서는 **Urlhelper** 클래스를 쉽게 모의으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="daea0-285">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="daea0-285">IHttpActionResult</span></span>

<span data-ttu-id="daea0-286">이제 IHttpActionResult을 구현 하 여 Web API 작업 메서드의 결과를 캡슐화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="daea0-287">웹 API 동작 메서드에서 반환 되는 IHttpActionResult는 ASP.NET Web API 런타임에 의해 실행 되어 결과 응답 메시지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="daea0-288">Web api 작업에서 IHttpActionResult를 반환 하 여 Web API 구현에 대 한 단위 테스트를 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="daea0-289">편의를 위해 특정 상태 코드, 서식이 지정 된 콘텐츠 또는 콘텐츠 협상 된 응답을 반환 하는 결과를 포함 하 여 다양 한 IHttpActionResult 구현이 기본적으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="daea0-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="daea0-290">HttpRequestContext</span></span>

<span data-ttu-id="daea0-291">새 **Httprequestcontext** 는 요청에 연결 되었지만 요청에서 즉시 사용할 수 없는 상태를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="daea0-292">예를 들어 **Httprequestcontext** 를 사용 하 여 경로 데이터, 요청에 연결 된 보안 주체, 클라이언트 인증서, **urlhelper** 및 가상 경로 루트를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="daea0-293">단위 테스트를 위해 **Httprequestcontext** 를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="daea0-294">요청에 대 한 보안 주체는 **system.threading.thread.currentprincipal**을 사용 하는 대신 요청으로 전달 되기 때문에 이제 웹 API 파이프라인에 있는 동안 요청 수명 내내 보안 주체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="daea0-295">CORS</span><span class="sxs-lookup"><span data-stu-id="daea0-295">CORS</span></span>

<span data-ttu-id="daea0-296">Brock Allen에서 좋은 다른 기여 덕분에 이제 ASP.NET는 CORS (원본 간 요청 공유)를 완벽 하 게 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="daea0-297">브라우저 보안은 웹 페이지에서 다른 도메인으로 AJAX 요청을 수행하지 못하도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="daea0-298">[CORS](http://www.w3.org/TR/cors/) 는 서버에서 동일한 원본 정책을 완화할 수 있게 해 주는 W3C 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="daea0-299">CORS를 사용하면 서버에서 명시적으로 일부 원본 간 요청을 허용하는 한편 다른 요청은 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="daea0-300">이제 Web API 2는 실행 전 요청의 자동 처리를 비롯 한 CORS를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="daea0-301">자세한 내용은 [ASP.NET 웹 API에서 크로스-원본 리소스 요청 사용](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="daea0-302">인증 필터</span><span class="sxs-lookup"><span data-stu-id="daea0-302">Authentication Filters</span></span>

<span data-ttu-id="daea0-303">인증 필터는 ASP.NET Web API 파이프라인의 권한 부여 필터 전에 실행 되는 ASP.NET Web API의 새로운 종류의 필터 이며, 모든 컨트롤러에 대해 작업당, 컨트롤러당 또는 전역 인증 논리를 지정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="daea0-304">인증 필터는 요청에서 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="daea0-305">인증 필터는 권한이 없는 요청에 대 한 응답으로 인증 문제를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="daea0-306">필터 재정의</span><span class="sxs-lookup"><span data-stu-id="daea0-306">Filter Overrides</span></span>

<span data-ttu-id="daea0-307">이제 재정의 필터를 지정 하 여 지정 된 작업 메서드 또는 컨트롤러에 적용 되는 필터를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="daea0-308">재정의 필터는 지정 된 범위 (동작 또는 컨트롤러)에 대해 실행 하면 안 되는 필터 유형 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="daea0-309">이렇게 하면 전역 필터를 추가할 수 있지만 특정 작업 또는 컨트롤러에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="daea0-310">OWIN 통합</span><span class="sxs-lookup"><span data-stu-id="daea0-310">OWIN Integration</span></span>

<span data-ttu-id="daea0-311">ASP.NET Web API은 이제 OWIN을 완벽 하 게 지원 하며 모든 OWIN 지원 호스트에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="daea0-312">OWIN 인증 시스템과의 통합을 제공 하는 **Hostauthenticationfilter** 도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="daea0-313">OWIN 통합을 사용 하면 SignalR와 같은 다른 OWIN 미들웨어와 함께 자체 프로세스에서 Web API를 자체 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="daea0-314">자세한 내용은 [OWIN를 사용 하 여 자체 호스트 ASP.NET Web API를](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="daea0-315">ASP.NET SignalR 2.0</span><span class="sxs-lookup"><span data-stu-id="daea0-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="daea0-316">다음 섹션에서는 SignalR 2.0의 기능에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="daea0-317">OWIN 기반</span><span class="sxs-lookup"><span data-stu-id="daea0-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="daea0-318">이제 MapHubs 및 Maphubs이 MapSignalR</span><span class="sxs-lookup"><span data-stu-id="daea0-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="daea0-319">도메인 간 지원</span><span class="sxs-lookup"><span data-stu-id="daea0-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="daea0-320">Monotouch.dialog 및 MonoDroid을 통한 iOS 및 Android 지원</span><span class="sxs-lookup"><span data-stu-id="daea0-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="daea0-321">이식 가능한 .NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="daea0-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="daea0-322">새 자체 호스트 패키지</span><span class="sxs-lookup"><span data-stu-id="daea0-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="daea0-323">이전 버전과 호환 되는 서버 지원</span><span class="sxs-lookup"><span data-stu-id="daea0-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="daea0-324">.NET 4.0에 대 한 서버 지원이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="daea0-325">클라이언트 및 그룹 목록에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="daea0-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="daea0-326">특정 사용자에 게 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="daea0-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="daea0-327">오류 처리 지원 향상</span><span class="sxs-lookup"><span data-stu-id="daea0-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="daea0-328">허브의 손쉬운 유닛 테스트</span><span class="sxs-lookup"><span data-stu-id="daea0-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="daea0-329">JavaScript 오류 처리</span><span class="sxs-lookup"><span data-stu-id="daea0-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="daea0-330">기존 1.x 프로젝트를 SignalR 2.0로 업그레이드 하는 방법에 대 한 예제는 SignalR 1.x [프로젝트 업그레이드](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="daea0-331">OWIN 기반</span><span class="sxs-lookup"><span data-stu-id="daea0-331">Built on OWIN</span></span>

<span data-ttu-id="daea0-332">SignalR 2.0는 완전히 [OWIN (.net 용 개방형 웹 인터페이스)](http://owin.org/)에서 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="daea0-333">이러한 변경으로 인해 SignalR는 웹 호스팅 및 자체 호스팅 SignalR 응용 프로그램 간에 훨씬 더 일관 되 게 설치할 수 있지만 많은 API 변경도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="daea0-334">이제 MapHubs 및 Maphubs이 MapSignalR</span><span class="sxs-lookup"><span data-stu-id="daea0-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="daea0-335">OWIN 표준과의 호환성을 위해 이러한 메서드의 이름이 `MapSignalR`로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="daea0-336">매개 변수 없이 호출 되는 `MapSignalR` 모든 허브를 매핑합니다 (`MapHubs` 버전 1.x에서). 개별 **PersistentConnection** 개체를 매핑하려면 연결 유형을 형식 매개 변수로 지정 하 고 연결에 대 한 URL 확장을 첫 번째 인수로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="daea0-337">`MapSignalR` 메서드는 Owin startup 클래스에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="daea0-338">Visual Studio 2013 Owin startup 클래스에 대 한 새 템플릿이 포함 되어 있습니다. 이 템플릿을 사용 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="daea0-339">프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-339">Right-click on the project</span></span>
2. <span data-ttu-id="daea0-340">**추가**, **새 항목** ...을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="daea0-341">**Owin 시작 클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="daea0-342">새 클래스의 이름을 **Startup.cs**로 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="daea0-343">**웹 응용 프로그램** 에서 `MapSignalR` 메서드를 포함 하는 Owin startup 클래스는 아래와 같이 web.config 파일의 응용 프로그램 설정 노드의 항목을 사용 하 여 Owin의 시작 프로세스에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="daea0-344">**자체 호스팅 응용 프로그램**에서 Startup 클래스는 `WebApp.Start` 메서드의 형식 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="daea0-345">**SignalR 1.x (웹 응용 프로그램의 전역 응용 프로그램 파일)에서 허브 및 연결 매핑:**</span><span class="sxs-lookup"><span data-stu-id="daea0-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="daea0-346">**SignalR 2.0 (Owin 시작 클래스 파일에서)의 허브 및 연결 매핑:**</span><span class="sxs-lookup"><span data-stu-id="daea0-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="daea0-347">**자체 호스팅 응용 프로그램**에서 Startup 클래스는 아래와 같이 `WebApp.Start` 메서드에 대 한 형식 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="daea0-348">도메인 간 지원</span><span class="sxs-lookup"><span data-stu-id="daea0-348">Cross-Domain Support</span></span>

<span data-ttu-id="daea0-349">SignalR 1.x에서 도메인 간 요청은 단일 EnableCrossDomain 플래그에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="daea0-350">이 플래그는 JSONP 및 CORS 요청을 모두 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="daea0-351">유연성을 높이기 위해 SignalR의 서버 구성 요소에서 모든 CORS 지원이 제거 되었습니다. JavaScript 클라이언트는 여전히 CORS를 사용 하 여 브라우저에서 지 원하는 경우에는 CORS를 정상적으로 사용 하 고, 이러한 시나리오를 지원 하기 위해 새로운 OWIN 미들웨어를 사용할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="daea0-352">SignalR 2.0에서 클라이언트에 JSONP가 필요한 경우 (이전 브라우저에서 도메인 간 요청을 지원 하려면 아래와 같이 `HubConfiguration` `true`개체에 대 한 `EnableJSONP`를 설정 하 여 명시적으로 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="daea0-353">JSONP는 CORS 보다 안전 하지 않으므로 기본적으로 사용 하지 않도록 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="daea0-354">SignalR 2.0에 새 CORS 미들웨어를 추가 하려면 프로젝트에 `Microsoft.Owin.Cors` 라이브러리를 추가 하 고 아래 섹션과 같이 SignalR 미들웨어 앞에 `UseCors`를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="daea0-355">**Owin을 프로젝트에 추가**:이 라이브러리를 설치 하려면 패키지 관리자 콘솔에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="daea0-356">이 명령은 2.0.0 버전의 패키지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="daea0-357">**UseCors 호출**</span><span class="sxs-lookup"><span data-stu-id="daea0-357">**Calling UseCors**</span></span>

<span data-ttu-id="daea0-358">다음 코드 조각에서는 SignalR 1.x 및 2.0에서 도메인 간 연결을 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="daea0-359">**SignalR 1.x (전역 응용 프로그램 파일)에서 도메인 간 요청 구현**</span><span class="sxs-lookup"><span data-stu-id="daea0-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="daea0-360">**SignalR 2.0에서 도메인 간 요청 구현 ( C# 코드 파일에서)**</span><span class="sxs-lookup"><span data-stu-id="daea0-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="daea0-361">다음 코드에서는 SignalR 2.0 프로젝트에서 CORS 또는 JSONP를 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="daea0-362">이 코드 샘플은 `MapSignalR`대신 `Map` 및 `RunSignalR`를 사용 하므로 CORS 미들웨어는 `MapSignalR`에 지정 된 경로의 모든 트래픽이 아닌 CORS를 지원 해야 하는 SignalR 요청에 대해서만 실행 됩니다. `Map`는 전체 응용 프로그램이 아닌 특정 URL 접두사에 대해 실행 해야 하는 다른 미들웨어에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="daea0-363">Monotouch.dialog 및 MonoDroid을 통한 iOS 및 Android 지원</span><span class="sxs-lookup"><span data-stu-id="daea0-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="daea0-364">[Xamarin 라이브러리](https://xamarin.com/)에서 Monotouch.dialog 및 MonoDroid 구성 요소를 사용 하 여 IOS 및 Android 클라이언트에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="daea0-365">사용 방법에 대 한 자세한 내용은 [Xamarin 구성 요소 사용](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="daea0-366">이러한 구성 요소는 SignalR RTW 릴리스를 사용할 수 있을 때 [Xamarin 스토어](https://store.xamarin.com/) 에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="daea0-367"># # # 이식 가능한 .NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="daea0-367">### Portable .NET client</span></span>

<span data-ttu-id="daea0-368">플랫폼 간 개발을 보다 효율적으로 수행할 수 있도록 Silverlight, WinRT 및 Windows Phone 클라이언트는 다음 플랫폼을 지 원하는 단일 휴대용 .NET 클라이언트로 대체 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="daea0-369">NET 4.5</span><span class="sxs-lookup"><span data-stu-id="daea0-369">NET 4.5</span></span>
- <span data-ttu-id="daea0-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="daea0-370">Silverlight 5</span></span>
- <span data-ttu-id="daea0-371">WinRT (Windows 스토어 앱 용 .NET)</span><span class="sxs-lookup"><span data-stu-id="daea0-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="daea0-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="daea0-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="daea0-373">새 자체 호스트 패키지</span><span class="sxs-lookup"><span data-stu-id="daea0-373">New Self-Host Package</span></span>

<span data-ttu-id="daea0-374">이제 NuGet 패키지를 사용 하면 웹 서버에서 호스트 되는 것이 아니라 프로세스 또는 다른 응용 프로그램에서 호스트 되는 SignalR 응용 프로그램을 SignalR 하 여 쉽게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="daea0-375">SignalR 1.x를 사용 하 여 빌드된 자체 호스트 프로젝트를 업그레이드 하려면 SignalR 패키지를 제거 하 고 SignalR 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="daea0-376">자체 호스트 패키지를 시작 하는 방법에 대 한 자세한 내용은 [자습서: SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="daea0-377">이전 버전과 호환 되는 서버 지원</span><span class="sxs-lookup"><span data-stu-id="daea0-377">Backward-compatible server support</span></span>

<span data-ttu-id="daea0-378">이전 버전의 SignalR에서는 클라이언트와 서버에서 사용 되는 SignalR 패키지의 버전이 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="daea0-379">업데이트 하기 어려운 굵고 클라이언트 응용 프로그램을 지원 하기 위해 SignalR 2.0는 이제 이전 클라이언트에서 최신 서버 버전을 사용할 수 있도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="daea0-380">**참고: SignalR 2.0는 최신 클라이언트를 사용 하 여 이전 버전으로 빌드된 서버를 지원 하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="daea0-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="daea0-381">.NET 4.0에 대 한 서버 지원이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="daea0-382">SignalR 2.0은 .NET 4.0과의 서버 상호 운용성에 대 한 지원을 삭제 했습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="daea0-383">.NET 4.5은 SignalR 2.0 서버와 함께 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="daea0-384">SignalR 2.0 용 .NET 4.0 클라이언트가 여전히 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="daea0-385">클라이언트 및 그룹 목록에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="daea0-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="daea0-386">SignalR 2.0에서는 클라이언트 및 그룹 Id 목록을 사용 하 여 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="daea0-387">다음 코드 조각에서는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="daea0-388">**PersistentConnection를 사용 하 여 클라이언트 및 그룹의 목록에 메시지 보내기**</span><span class="sxs-lookup"><span data-stu-id="daea0-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="daea0-389">**허브를 사용 하 여 클라이언트 및 그룹 목록에 메시지 보내기**</span><span class="sxs-lookup"><span data-stu-id="daea0-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="daea0-390">특정 사용자에 게 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="daea0-390">Sending a message to a specific user</span></span>

<span data-ttu-id="daea0-391">이 기능을 사용 하면 사용자가 새 인터페이스 IUserIdProvider를 통해 IRequest를 기반으로 하는 사용자 Id를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="daea0-392">**IUserIdProvider 인터페이스**</span><span class="sxs-lookup"><span data-stu-id="daea0-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="daea0-393">기본적으로 사용자의 IPrincipal.Identity.Name를 사용자 이름으로 사용 하는 구현이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="daea0-394">허브에서는 새 API를 통해 이러한 사용자에 게 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="daea0-395">**클라이언트 사용자 API 사용**</span><span class="sxs-lookup"><span data-stu-id="daea0-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="daea0-396">오류 처리 지원 향상</span><span class="sxs-lookup"><span data-stu-id="daea0-396">Better Error Handling Support</span></span>

<span data-ttu-id="daea0-397">이제 사용자가 모든 허브 호출에서 **HubException** 을 throw 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="daea0-398">**HubException** 의 생성자는 문자열 메시지와 개체 추가 오류 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="daea0-399">SignalR는 예외를 자동으로 직렬화 하 고 허브 메서드 호출을 거부/실패 하는 데 사용 되는 클라이언트에 게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="daea0-400">**자세한 허브 예외 표시** 설정은 클라이언트로 다시 전송 되는 **HubException** 에는 영향을 미치지 않습니다. 항상 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="daea0-401">**클라이언트에 HubException를 보내는 방법을 보여 주는 서버 쪽 코드**</span><span class="sxs-lookup"><span data-stu-id="daea0-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="daea0-402">**서버에서 보낸 HubException 응답을 보여 주는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="daea0-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="daea0-403">**서버에서 보낸 HubException 응답을 보여 주는 .NET 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="daea0-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="daea0-404">허브의 손쉬운 유닛 테스트</span><span class="sxs-lookup"><span data-stu-id="daea0-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="daea0-405">SignalR 2.0에는 모의 클라이언트 쪽 호출을 보다 쉽게 만들 수 있도록 하는 허브에 `IHubCallerConnectionContext` 라는 인터페이스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="daea0-406">다음 코드 조각은 인기 있는 테스트 장비 [xUnit.net](https://github.com/xunit/xunit) 및 [moq](https://code.google.com/p/moq/)로이 인터페이스를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="daea0-407">**XUnit.net를 사용 하 여 SignalR 유닛 테스트**</span><span class="sxs-lookup"><span data-stu-id="daea0-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="daea0-408">**Moq로 SignalR 유닛 테스트**</span><span class="sxs-lookup"><span data-stu-id="daea0-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="daea0-409">JavaScript 오류 처리</span><span class="sxs-lookup"><span data-stu-id="daea0-409">JavaScript error handling</span></span>

<span data-ttu-id="daea0-410">SignalR 2.0에서 모든 JavaScript 오류 처리 콜백은 원시 문자열 대신 JavaScript 오류 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="daea0-411">이렇게 하면 SignalR에서 오류 처리기에 대 한 다양 한 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="daea0-412">오류의 `source` 속성에서 내부 예외를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="daea0-413">**Start. Fail 예외를 처리 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="daea0-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="daea0-414">ASP.NET ID</span><span class="sxs-lookup"><span data-stu-id="daea0-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="daea0-415">새 ASP.NET 멤버 자격 시스템</span><span class="sxs-lookup"><span data-stu-id="daea0-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="daea0-416">ASP.NET Identity ASP.NET 응용 프로그램에 대 한 새 멤버 자격 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="daea0-417">ASP.NET Identity를 사용 하면 사용자 관련 프로필 데이터를 응용 프로그램 데이터와 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="daea0-418">ASP.NET Identity를 사용 하 여 응용 프로그램의 사용자 프로필에 대 한 지 속성 모델을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="daea0-419">Azure Storage 테이블과 같은 NoSQL 데이터 저장소를 포함 하 여 SQL Server 데이터베이스 또는 다른 데이터 저장소에 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="daea0-420">자세한 내용은 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**의 [개별 사용자 계정](creating-web-projects-in-visual-studio.md#indauth) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="daea0-421">클레임 기반 인증</span><span class="sxs-lookup"><span data-stu-id="daea0-421">Claims-based authentication</span></span>

<span data-ttu-id="daea0-422">이제 ASP.NET는 클레임 기반 인증을 지원 합니다. 여기서 사용자의 id는 신뢰할 수 있는 발급자의 클레임 집합으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="daea0-423">사용자는 응용 프로그램 데이터베이스에서 유지 관리 되는 사용자 이름 및 암호를 사용 하거나, 소셜 id 공급자 (예: Microsoft 계정, Facebook, Google, Twitter)를 사용 하거나, Azure Active Directory 또는을 통해 조직 계정을 사용 하 여 인증할 수 있습니다. Active Directory Federation Services (ADFS).</span><span class="sxs-lookup"><span data-stu-id="daea0-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="daea0-424">Azure Active Directory 및 Windows Server Active Directory와 통합</span><span class="sxs-lookup"><span data-stu-id="daea0-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="daea0-425">이제 인증을 위해 Azure Active Directory 또는 Windows Server Active Directory (AD)를 사용 하는 ASP.NET 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="daea0-426">자세한 내용은 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**의 [조직 계정](creating-web-projects-in-visual-studio.md#orgauth) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="daea0-427">OWIN 통합</span><span class="sxs-lookup"><span data-stu-id="daea0-427">OWIN Integration</span></span>

<span data-ttu-id="daea0-428">ASP.NET 인증은 이제 모든 OWIN 기반 호스트에서 사용할 수 있는 OWIN 미들웨어를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="daea0-429">OWIN에 대 한 자세한 내용은 다음 [MICROSOFT OWIN 구성 요소](#TOC7) 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="daea0-430">Microsoft OWIN 구성 요소</span><span class="sxs-lookup"><span data-stu-id="daea0-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="daea0-431">OWIN ( [Open Web Interface for .net](http://owin.org/) )는 .net 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="daea0-432">OWIN는 서버에서 웹 응용 프로그램을 분리 하 여 웹 응용 프로그램을 호스트 독립적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="daea0-433">예를 들어 IIS에서 OWIN 기반 웹 응용 프로그램을 호스트 하거나 사용자 지정 프로세스에서 자체 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="daea0-434">Microsoft OWIN 구성 요소 (Katana 프로젝트 라고도 함)에 도입 된 변경 내용에는 새로운 서버 및 호스트 구성 요소, 새 도우미 라이브러리 및 미들웨어, 새 인증 미들웨어가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="daea0-435">OWIN 및 Katana에 대 한 자세한 내용은 [OWIN 및 Katana의 새로운 기능](../../../aspnet/overview/owin-and-katana/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="daea0-436">**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램은 IIS 클래식 모드에서 실행할 수 없습니다. 통합 모드로 실행 해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="daea0-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="daea0-437">**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램은 완전 신뢰로 실행 해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="daea0-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="daea0-438">새 서버 및 호스트</span><span class="sxs-lookup"><span data-stu-id="daea0-438">New Servers and Hosts</span></span>

<span data-ttu-id="daea0-439">이 릴리스에서는 자체 호스트 시나리오를 사용할 수 있도록 새로운 구성 요소가 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="daea0-440">이러한 구성 요소에는 다음과 같은 NuGet 패키지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="daea0-441">**Owin. HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="daea0-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="daea0-442">**HttpListener** 를 사용 하 여 HTTP 요청을 수신 하 고이를 OWIN 파이프라인으로 전달 하는 OWIN 서버를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="daea0-443">**Owin** 는 콘솔 응용 프로그램 또는 Windows 서비스와 같은 사용자 지정 프로세스에서 Owin 파이프라인을 자체 호스트 하려는 개발자를 위한 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="daea0-444">**Owinhost**.</span><span class="sxs-lookup"><span data-stu-id="daea0-444">**OwinHost**.</span></span> <span data-ttu-id="daea0-445">`Microsoft.Owin.Hosting`를 래핑하는 독립 실행형 실행 파일을 제공 하며, 사용자 지정 호스트 응용 프로그램을 작성 하지 않고도 OWIN 파이프라인을 직접 호스팅할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="daea0-446">또한 `Microsoft.Owin.Host.SystemWeb` 패키지를 사용 하면 미들웨어가 **Systemweb** 서버에 힌트를 제공 하 여 특정 ASP.NET 파이프라인 단계에서 미들웨어를 호출 해야 함을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="daea0-447">이 기능은 ASP.NET 파이프라인의 초기에 실행 해야 하는 인증 미들웨어에 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="daea0-448">도우미 라이브러리 및 미들웨어</span><span class="sxs-lookup"><span data-stu-id="daea0-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="daea0-449">OWIN 사양의 함수 및 유형 정의만 사용 하 여 OWIN 구성 요소를 작성할 수 있지만, 새 `Microsoft.Owin` 패키지는 보다 사용자에 게 친숙 한 추상화 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="daea0-450">이 패키지는 여러 이전 패키지 (예: `Owin.Extensions`, `Owin.Types`)를 잘 구성 된 단일 개체 모델로 결합 하 여 다른 OWIN 구성 요소에서 쉽게 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="daea0-451">실제로 대부분의 Microsoft OWIN 구성 요소는이 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="daea0-452">[OWIN](http://www.owin.org) 응용 프로그램은 IIS 클래식 모드에서 실행할 수 없습니다. 통합 모드로 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="daea0-453">[OWIN](http://www.owin.org) 응용 프로그램은 완전 신뢰로 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="daea0-454">이 릴리스에는 실행 중인 OWIN 응용 프로그램의 유효성을 검사 하는 미들웨어와 오류를 조사 하는 데 도움이 되는 오류 페이지 미들웨어를 포함 하는 Owin 패키지도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="daea0-455">인증 구성 요소</span><span class="sxs-lookup"><span data-stu-id="daea0-455">Authentication Components</span></span>

<span data-ttu-id="daea0-456">다음 인증 구성 요소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-456">The following authentication components are available.</span></span>

- <span data-ttu-id="daea0-457">**Owin. ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="daea0-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="daea0-458">온-프레미스 또는 클라우드 기반 디렉터리 서비스를 사용 하 여 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="daea0-459">**Owin** 쿠키를 사용 하 여 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="daea0-460">이 패키지는 이전에 `Microsoft.Owin.Security.Forms`이름이 지정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="daea0-461">**Owin** Facebook의 OAuth 기반 서비스를 사용 하 여 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="daea0-462">**Owin** Google의 openid connect 기반 서비스를 사용 하 여 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="daea0-463">**Owin** 를 사용 하면 jwt 토큰을 사용 하 여 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="daea0-464">**Owin. MicrosoftAccount** 는 microsoft 계정을 사용 하 여 인증을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="daea0-465">**Owin**입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="daea0-466">전달자 토큰을 인증 하는 데 필요한 미들웨어 뿐만 아니라 OAuth 권한 부여 서버를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="daea0-467">**Owin** 를 사용 하면 Twitter의 OAuth 기반 서비스를 사용 하 여 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="daea0-468">이 릴리스에는 크로스-원본 HTTP 요청을 처리 하기 위한 미들웨어를 포함 하는 `Microsoft.Owin.Cors` 패키지도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="daea0-469">Visual Studio 2013의 최종 버전에서 JWT 서명 지원이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="daea0-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="daea0-470">Entity Framework 6</span></span>

<span data-ttu-id="daea0-471">Entity Framework 6의 새로운 기능 및 기타 변경 사항 목록은 [Entity Framework 버전 기록](https://msdn.com/data/jj574253)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="daea0-472">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="daea0-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="daea0-473">ASP.NET Razor 3에는 다음과 같은 새로운 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="daea0-474">탭 편집 지원.</span><span class="sxs-lookup"><span data-stu-id="daea0-474">Support for Tab editing.</span></span> <span data-ttu-id="daea0-475">이전에는 **탭 유지** 옵션을 사용 하는 경우 Visual Studio에서 **문서 서식 지정** 명령, 자동 들여쓰기 및 자동 서식 지정이 제대로 작동 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="daea0-476">이 변경 내용은 탭 서식 지정을 위한 Razor 코드의 Visual Studio 서식 지정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="daea0-477">링크를 생성할 때 URL 다시 쓰기 규칙을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="daea0-478">보안 투명 특성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="daea0-479">이는 주요 변경 내용으로, razor 3은 MVC4 및 이전 버전과 호환 되지 않지만 Razor 2는 MVC5에 대해 컴파일된 MVC5 또는 어셈블리와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="daea0-480">시험판 버전에서 Visual Studio 2013에서 해결 된 Razor 3 문제는 [여기](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="daea0-481">ASP.NET 앱 일시 중단</span><span class="sxs-lookup"><span data-stu-id="daea0-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="daea0-482">ASP.NET 앱 일시 중단은 단일 컴퓨터에서 많은 수의 ASP.NET 사이트를 호스트 하기 위한 사용자 환경 및 경제 모델을 완전히 변경 하는 .NET Framework 4.5.1의 게임 변경 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="daea0-483">자세한 내용은 [ASP.NET App Suspend – 응답성이 뛰어난 공유 .net 웹 호스팅](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="daea0-484">알려진 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="daea0-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="daea0-485">이 섹션에서는 Visual Studio 2013에 대 한 ASP.NET 및 Web Tools의 알려진 문제 및 주요 변경 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="daea0-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="daea0-486">NuGet</span></span>

- <span data-ttu-id="daea0-487">[새 패키지 복원이 SLN 파일을 사용 하는 경우 Mono에서 작동 하지 않음](https://nuget.codeplex.com/workitem/3596) – 예정 된 nuget.exe 다운로드 및 [nuget 명령줄 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트에서 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="daea0-488">[새 패키지 복원은 Wix 프로젝트에서 작동 하지 않습니다](https://nuget.codeplex.com/workitem/3598) . 예정 된 nuget.exe 다운로드 및 [nuget 명령줄 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트에서 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="daea0-489">[자동 패키지 복원은 솔루션 폴더의 프로젝트에 대해 작동 하지 않습니다](https://nuget.codeplex.com/workitem/3625) . NuGet 2.8에서 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="daea0-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="daea0-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="daea0-491">`$select` 및 `$expand`에 대 한 지원을 추가 했으므로 `ODataQueryOptions<T>.ApplyTo(IQueryable)` `IQueryable<T>` 항상 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="daea0-492">`ODataQueryOptions<T>`에 대 한 이전 예제는 항상 `ApplyTo`의 반환 값을 `IQueryable<T>`로 캐스트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="daea0-493">앞에서 설명한 쿼리 옵션 (`$filter`, `$orderby`, `$skip`, `$top`)은 쿼리 형태를 변경 하지 않으므로 앞에서 작업 했습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="daea0-494">이제 `$select`를 지원 하 고 `ApplyTo`의 반환 값 `$expand` 항상 `IQueryable<T>` 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="daea0-495">이전에 나온 샘플 코드를 사용 하는 경우 클라이언트가 `$select`를 전송 하지 않고 `$expand`경우 계속 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="daea0-496">그러나 `$select` 및 `$expand`를 지원 하려는 경우 해당 코드를로 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="daea0-497">**요청. Url 또는 RequestContext. 일괄 처리 요청 중 Url이 null입니다.**</span><span class="sxs-lookup"><span data-stu-id="daea0-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="daea0-498">일괄 처리 시나리오에서는 **요청 url** 또는 **RequestContext**에서 액세스할 때 **urlhelper** 가 null입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="daea0-499">이 문제는 현재 Batchrequestcontext에서 추적 됩니다. [일괄 처리 요청에 대 한 Url은 null](http://aspnetwebstack.codeplex.com/workitem/1301)입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="daea0-500">이 문제에 대 한 해결 방법은 다음 예제와 같이 **Urlhelper**의 새 인스턴스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="daea0-501">**UrlHelper의 새 인스턴스 만들기**</span><span class="sxs-lookup"><span data-stu-id="daea0-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="daea0-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="daea0-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="daea0-503">MVC5 및 OrgAuth를 사용 하는 경우 AntiForgerToken 유효성 검사를 수행 하는 보기가 있는 경우 뷰에 데이터를 게시할 때 다음 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="daea0-504">**오류**:</span><span class="sxs-lookup"><span data-stu-id="daea0-504">**Error**:</span></span>

    <span data-ttu-id="daea0-505">*'/' 응용 프로그램에서 서버 오류가 발생 했습니다.*</span><span class="sxs-lookup"><span data-stu-id="daea0-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="daea0-506"><em>'<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' 또는 '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' 형식의 클레임이 제공 된 ClaimsIdentity에 없습니다. 클레임 기반 인증을 사용 하 여 위조 방지 토큰 지원을 사용 하도록 설정 하려면 구성 된 클레임 공급자가 생성 하는 ClaimsIdentity 인스턴스에 대해 이러한 클레임을 모두 제공 하는지 확인 하세요. 구성 된 클레임 공급자에서 다른 클레임 유형을 고유 식별자로 사용 하는 경우에는 정적 속성인 AntiForgeryConfig를 설정 하 여 구성할 수 있습니다.</em></span><span class="sxs-lookup"><span data-stu-id="daea0-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="daea0-507">**해결 방법**:</span><span class="sxs-lookup"><span data-stu-id="daea0-507">**Workaround**:</span></span>

    <span data-ttu-id="daea0-508">Global.asax에 다음 줄을 추가 하 여 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="daea0-509">이 문제는 다음 릴리스에 대해 수정 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="daea0-510">MVC4 앱을 MVC5로 업그레이드 한 후 솔루션을 빌드하고 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="daea0-511">다음 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-511">You should see the following error:</span></span>

    <span data-ttu-id="daea0-512">은 [B] system.web. HostSection hostsection은 [B] System.web. HostSection HostSection으로 캐스트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="daea0-513">위치 ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35 \ '에 있는 ' Default ' 컨텍스트에서 ' 31bf3856ad364e35, Version = 2.0.0.0, Culture = 중립적인, PublicKeyToken = m A t i o n '을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="daea0-514">형식 B는 ' 31bf3856ad364e35 ', ' 3.0.0.0, Version =, Culture = 중립, PublicKeyToken = '의 ' Default ' 컨텍스트 (위치 ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_273ce1\ ')에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="daea0-515">위의 오류를 해결 하려면 프로젝트에서 *모든* web.config 파일 (Views 폴더의 항목 포함)을 열고 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="daea0-516">"4.0.0.0"의 모든 버전 ""를 "5.0.0.0"로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="daea0-517">"3.0.0.0"의 모든 버전 "2.0.0.0"을 업데이트 &quot;하 고, system.web. 웹 페이지&quot; 및 &quot;System.web. m i m&quot;를 ""으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="daea0-518">예를 들어 위의 내용을 변경 하 고 나면 어셈블리 바인딩이 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="daea0-519">MVC 4 프로젝트를 MVC 5로 업그레이드 하는 방법에 대 한 자세한 내용은 [ASP.NET mvc 4 및 WEB Api 프로젝트를 ASP.NET mvc 5 및 WEB api 2로 업그레이드 하는 방법](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="daea0-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="daea0-520">JQuery가 맞지 않는 유효성 검사를 사용 하 여 클라이언트 쪽 유효성 검사를 사용 하는 경우 유효성 검사 메시지는 경우에 따라 형식이 ' number ' 인 HTML input 요소에 대해 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="daea0-521">유효한 값이 필요한 올바른 메시지 대신 잘못 된 숫자를 입력 하는 경우에는 필요한 값에 대 한 유효성 검사 오류 ("Age 필드는 필수입니다.")가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="daea0-522">이 문제는 일반적으로 Create 및 Edit 뷰에서 정수 속성이 있는 모델에 대 한 스 캐 폴드 코드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="daea0-523">이 문제를 해결 하려면 편집기 도우미를 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="daea0-524">아래와 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="daea0-525">ASP.NET MVC 5는 더 이상 부분 신뢰를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="daea0-526">MVC 또는 WebAPI 이진 파일에 연결 하는 프로젝트는 [Securitytransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) 특성 및 [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) 특성을 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="daea0-527">이러한 특성을 제거 하면 다음과 같은 컴파일러 오류가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="daea0-528">이에 대 한 부작용으로 동일한 응용 프로그램에서 4.0 및 5.0 어셈블리를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="daea0-529">모든 항목을 5.0로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="daea0-530">웹 사이트가 인트라넷 영역에서 호스트 되는 동안 Facebook 권한 부여를 사용 하는 SPA 템플릿이 IE를 불안정 해질 수 있음</span><span class="sxs-lookup"><span data-stu-id="daea0-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="daea0-531">SPA 템플릿에서는 Facebook을 사용 하 여 외부 로그인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="daea0-532">템플릿을 사용 하 여 만든 프로젝트를 로컬로 실행 하는 경우 로그인 하면 IE의 작동이 중단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="daea0-533">해결 방법:</span><span class="sxs-lookup"><span data-stu-id="daea0-533">Solution:</span></span>

1. <span data-ttu-id="daea0-534">인터넷 영역에서 웹 사이트를 호스팅합니다. 디스크나</span><span class="sxs-lookup"><span data-stu-id="daea0-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="daea0-535">IE 이외의 브라우저에서 시나리오를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="daea0-536">Web Forms 스캐폴딩</span><span class="sxs-lookup"><span data-stu-id="daea0-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="daea0-537">Web Forms 스 캐 폴딩은 VS2013에서 제거 되었으며 Visual Studio에 대 한 향후 업데이트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="daea0-538">그러나 mvc 종속성을 추가 하 고 MVC에 대 한 스 캐 폴딩을 생성 하 여 Web Forms 프로젝트 내에서 스 캐 폴딩을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="daea0-539">프로젝트에 Web Forms 및 MVC의 조합이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="daea0-540">Web Forms 프로젝트에 MVC를 추가 하려면 새 스 캐 폴드 항목을 추가 하 고 **mvc 5 종속성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="daea0-541">스크립트와 같은 모든 콘텐츠 파일이 필요한 지 여부에 따라 최소 또는 전체를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="daea0-542">그런 다음 프로젝트에서 뷰와 컨트롤러를 만드는 MVC에 대 한 스 캐 폴드 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="daea0-543">MVC 및 Web API 스 캐 폴딩-HTTP 404, 찾을 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="daea0-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="daea0-544">프로젝트에 스 캐 폴드 항목을 추가할 때 오류가 발생 하는 경우 프로젝트가 일관 되지 않은 상태로 남아 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="daea0-545">스 캐 폴딩의 변경 내용 중 일부는 롤백되고, 설치 된 NuGet 패키지와 같은 다른 변경 내용은 롤백되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="daea0-546">라우팅 구성 변경 내용이 롤백되면 사용자는 스 캐 폴드 항목으로 이동할 때 HTTP 404 오류를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="daea0-547">해결 방법:</span><span class="sxs-lookup"><span data-stu-id="daea0-547">Workaround:</span></span>

- <span data-ttu-id="daea0-548">MVC에 대 한이 오류를 해결 하려면 새 스 캐 폴드 항목을 추가 하 고 MVC 5 종속성 (최소 또는 전체)을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="daea0-549">이 프로세스는 프로젝트에 필요한 모든 변경 내용을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="daea0-550">Web API에 대해이 오류를 해결 하려면:</span><span class="sxs-lookup"><span data-stu-id="daea0-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="daea0-551">WebApiConfig 클래스를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="daea0-552">다음과 같이 Global.asax의 응용 프로그램\_Start 메서드에서 WebApiConfig을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="daea0-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
