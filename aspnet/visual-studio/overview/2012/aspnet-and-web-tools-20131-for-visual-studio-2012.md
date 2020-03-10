---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Visual Studio 2012 ASP.NET 및 Web Tools 2013.1에 대 한 릴리스 정보 | Microsoft Docs
author: microsoft
description: 이 문서에서는 Visual Studio 2012의 ASP.NET 및 Web Tools 2013.1 릴리스를 설명 합니다.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467105"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="c5567-103">Visual Studio 2012용 ASP.NET 및 Web Tools 2013.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="c5567-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="c5567-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="c5567-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c5567-105">이 문서에서는 Visual Studio 2012의 ASP.NET 및 Web Tools 2013.1 릴리스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="c5567-106">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="c5567-106">Contents</span></span>

- [<span data-ttu-id="c5567-107">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="c5567-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="c5567-108">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c5567-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="c5567-109">Visual Studio 2012 ASP.NET 및 Web Tools 2013.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="c5567-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="c5567-110">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="c5567-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="c5567-111">템플릿</span><span class="sxs-lookup"><span data-stu-id="c5567-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="c5567-112">ASP.NET MVC 5 템플릿</span><span class="sxs-lookup"><span data-stu-id="c5567-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="c5567-113">ASP.NET Web API 2 템플릿</span><span class="sxs-lookup"><span data-stu-id="c5567-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="c5567-114">항목 템플릿</span><span class="sxs-lookup"><span data-stu-id="c5567-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="c5567-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="c5567-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="c5567-116">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="c5567-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="c5567-117">Razor 편집기</span><span class="sxs-lookup"><span data-stu-id="c5567-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="c5567-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="c5567-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="c5567-119">알려진 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="c5567-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="c5567-120">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="c5567-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="c5567-121">MVC 및 Web API 스 캐 폴딩-HTTP 404, 찾을 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="c5567-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="c5567-122">스 캐 폴드 항목을 추가한 후 웹에 대 한 Visual Studio Express 2012의 작동이 중지 됨</span><span class="sxs-lookup"><span data-stu-id="c5567-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="c5567-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="c5567-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="c5567-124">With 또는 F5를 사용 하 여 cshtml 파일을 보면 서버 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="c5567-125">Url 재작성 및 물결표 (~)</span><span class="sxs-lookup"><span data-stu-id="c5567-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="c5567-126">템플릿</span><span class="sxs-lookup"><span data-stu-id="c5567-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="c5567-127">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="c5567-127">Installation Notes</span></span>

<span data-ttu-id="c5567-128">[설치](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) Visual Studio 2012의 ASP.NET 및 Web Tools 2013.1입니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="c5567-129">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c5567-129">Software Requirements</span></span>

<span data-ttu-id="c5567-130">웹에 대해 Visual Studio 2012 또는 Visual Studio Express 2012이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="c5567-131">Visual Studio 2012 ASP.NET 및 Web Tools 2013.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="c5567-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="c5567-132">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="c5567-132">Bootstrap</span></span>

<span data-ttu-id="c5567-133">MVC 5 컨트롤러 및 뷰를 스 캐 폴드 뷰의 태그는 [부트스트랩](http://getbootstrap.com/)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="c5567-134">템플릿</span><span class="sxs-lookup"><span data-stu-id="c5567-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="c5567-135">ASP.NET MVC 5 템플릿</span><span class="sxs-lookup"><span data-stu-id="c5567-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="c5567-136">새 MVC 5 템플릿을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="c5567-137">최신 MVC 5 NuGet 패키지를 참조 하 고 스 캐 폴딩을 사용 하 여 컨트롤러 및 뷰를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="c5567-138">ASP.NET Web API 2 템플릿</span><span class="sxs-lookup"><span data-stu-id="c5567-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="c5567-139">새 Web API 2 템플릿을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="c5567-140">최신 Web API 2 NuGet 패키지를 참조 하 고 스 캐 폴딩을 사용 하 여 컨트롤러 및 뷰를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="c5567-141">항목 템플릿</span><span class="sxs-lookup"><span data-stu-id="c5567-141">Item Templates</span></span>

<span data-ttu-id="c5567-142">MVC 5 뷰, 웹 페이지 (Razor 3) 및 Web API 2 컨트롤러에 대 한 새 항목 템플릿을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="c5567-143">새 항목을 추가 하는 동안 프로젝트에 관련 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="c5567-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="c5567-144">Entity Framework 6</span></span>

<span data-ttu-id="c5567-145">Entity Framework를 사용 하 여 MVC 또는 Web API 컨트롤러를 스 캐 폴드 때 프레임 워크 6을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="c5567-146">Entity Framework에 대 한 자세한 내용은 [Entity Framework 버전 기록](https://msdn.com/data/jj574253)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c5567-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="c5567-147">Visual Studio 2012에 대 한 Entity Framework 6 도구를 다운로드 하 여 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="c5567-148">[Get Entity Framework](https://msdn.com/data/ee712906#tooling)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c5567-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="c5567-149">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="c5567-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="c5567-150">ASP.NET 스 캐 폴딩은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="c5567-151">이를 통해 데이터 모델과 상호 작용 하는 상용구 코드를 프로젝트에 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="c5567-152">이전 버전의 Visual Studio에서 스 캐 폴딩은 ASP.NET MVC 프로젝트로 제한 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="c5567-153">이 업데이트를 통해 이제 Web Forms를 포함 하 여 모든 ASP.NET 프로젝트에 스 캐 폴딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="c5567-154">이 업데이트는 Web Forms 프로젝트에 대 한 페이지 생성을 지원 하지 않지만 프로젝트에 MVC 종속성을 추가 하 여 Web Forms에서 스 캐 폴딩을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="c5567-155">Web Forms에 대 한 페이지 생성 지원은 향후 업데이트에서 추가 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="c5567-156">스 캐 폴딩을 사용 하는 경우 모든 필수 종속성이 프로젝트에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="c5567-157">예를 들어 ASP.NET Web Forms 프로젝트로 시작한 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가 하는 경우 필요한 NuGet 패키지와 참조가 프로젝트에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="c5567-158">Web Forms 프로젝트에 MVC 스 캐 폴딩을 추가 하려면 **새 스 캐 폴드 항목** 을 추가 하 고 대화 상자 창에서 **mvc 5 종속성** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="c5567-159">MVC 스 캐 폴딩에 대 한 두 가지 옵션이 있습니다. 최소 및 전체.</span><span class="sxs-lookup"><span data-stu-id="c5567-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="c5567-160">최소를 선택 하면 ASP.NET MVC에 대 한 NuGet 패키지 및 참조만 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="c5567-161">전체 옵션을 선택 하는 경우 최소 종속성 뿐만 아니라 MVC 프로젝트에 필요한 콘텐츠 파일이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="c5567-162">비동기 컨트롤러 스 캐 폴딩에 대 한 지원은 Entity Framework 6의 새로운 비동기 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="c5567-163">자세한 내용 및 자습서는 [ASP.NET 스 캐 폴딩 개요](../2013/aspnet-scaffolding-overview.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c5567-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="c5567-164">이러한 자습서는 Visual Studio 2013를 사용 하 여 스 캐 폴딩을 보여 주지만 Visual Studio 2012 용 ASP.NET 및 Web Tools 2013.1에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="c5567-165">Razor 편집기</span><span class="sxs-lookup"><span data-stu-id="c5567-165">Razor Editor</span></span>

<span data-ttu-id="c5567-166">이 업데이트를 사용 하면 이제 Visual Studio 2012에서 Razor 3 도구/편집을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="c5567-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="c5567-167">NuGet 2.7</span></span>

<span data-ttu-id="c5567-168">NuGet 2.7에는 [nuget 2.7 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.7)에 자세히 설명 되어 있는 다양 한 새 기능 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="c5567-169">이 버전의 NuGet은 사용자가 NuGet이 누락 된 패키지를 복원 하는 것을 명시적으로 허용 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="c5567-170">NuGet 2.7을 설치 하는 경우 사용자는 누락 된 패키지를 자동으로 복원 하도록 암시적으로 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="c5567-171">사용자는 Visual Studio의 NuGet 설정을 통해 패키지 복원을 명시적으로 옵트아웃 (opt out) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="c5567-172">이렇게 변경 하면 패키지 복원의 작동 방식이 간소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="c5567-173">알려진 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="c5567-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="c5567-174">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="c5567-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="c5567-175">MVC 및 Web API 스 캐 폴딩-HTTP 404, 찾을 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="c5567-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="c5567-176">프로젝트에 스 캐 폴드 항목을 추가할 때 오류가 발생 하는 경우 프로젝트가 일관 되지 않은 상태로 남아 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="c5567-177">스 캐 폴딩의 변경 내용 중 일부는 롤백되고, 설치 된 NuGet 패키지와 같은 다른 변경 내용은 롤백되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="c5567-178">라우팅 구성 변경 내용이 롤백되면 사용자는 스 캐 폴드 항목으로 이동할 때 HTTP 404 오류를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="c5567-179">MVC에 대 한이 오류를 해결 하려면 새 스 캐 폴드 항목을 추가 하 고 MVC 5 종속성 (최소 또는 전체)을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="c5567-180">이 프로세스는 프로젝트에 필요한 모든 변경 내용을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="c5567-181">Web API에 대해이 오류를 해결 하려면:</span><span class="sxs-lookup"><span data-stu-id="c5567-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="c5567-182">다음 WebApiConfig 클래스를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="c5567-183">다음과 같이 Global.asax의 응용 프로그램\_Start 메서드에서 WebApiConfig을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="c5567-184">스 캐 폴드 항목을 추가한 후 웹에 대 한 Visual Studio Express 2012의 작동이 중지 됨</span><span class="sxs-lookup"><span data-stu-id="c5567-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="c5567-185">Entity Framework를 사용 하 여 스 캐 폴드 항목 (예: 작업을 사용 하는 웹 API 2 컨트롤러, Entity Framework을 사용 하는 웹 API 2 컨트롤러)을 추가한 후 2012 Visual Studio Express 웹에 대 한 작업을 중지 하는 경우 어셈블리의 네이티브 이미지를 로드 하지 못할 수 Visual Studio Express 있습니다 System.web. 확장명에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="c5567-186">이 문제를 해결 하려면 Visual Studio Express를 구성 하 여 system.string의 MSIL 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="c5567-187">관리자 모드에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="c5567-188">%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE 또는% ProgramFiles (x86)% \ Microsoft Visual Studio 11.0 \ Common7\IDE (64 비트 Windows의 경우)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="c5567-189">텍스트 편집기에서 VWDExpress을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="c5567-190">&lt;구성&gt;/&lt;runtime&gt; 요소 아래에 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="c5567-191">웹에 대해 Visual Studio Express 2012을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="c5567-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="c5567-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="c5567-193">With 또는 F5를 사용 하 여 cshtml 파일을 보면 서버 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="c5567-194">Visual Studio 2012 (또는 Visual Studio 2012에서 Visual Studio 2013 만든 MVC 5 프로젝트를 사용 하 여)에서 MVC 5 프로젝트를 만들 때 Browse With 또는 F5 키를 사용 하 여 cshtml 파일을 보려고 하면 **'/' 응용 프로그램에서 상태-서버 오류가**발생 한다는 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="c5567-195">서버에서 `http://localhost:XXXX/Views/../XXXX.cshtml`로 이동 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="c5567-196">이 문제를 해결 하려면 프로젝트의 **시작 작업** 설정을 **특정 페이지로**변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="c5567-197">페이지에 대 한 값을 제공할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="c5567-198">이렇게 변경한 후에는 F5 키를 선택 하 여 응용 프로그램의 루트 (`http://localhost:XXXX`)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="c5567-199">이 동작은 **현재 페이지** 설정이 열린 페이지를 시작 하는 VISUAL STUDIO 2013의 MVC 5 프로젝트 동작과 동일 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="c5567-200">Url 재작성 및 물결표 (~)</span><span class="sxs-lookup"><span data-stu-id="c5567-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="c5567-201">ASP.NET Razor 3 또는 ASP.NET MVC 5로 업그레이드 한 후에는 URL 다시 쓰기를 사용 하는 경우 물결표 (~) 표기법이 더 이상 제대로 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="c5567-202">URL 재작성은 &lt;/&gt;, &lt;스크립트/&gt;&lt;링크/&gt;와 같은 HTML 요소의 물결표 (~) 표기법에 영향을 주므로 물결표는 더 이상 루트 디렉터리에 매핑되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="c5567-203">예를 들어 **asp.net/content** 에 대 한 요청을 **asp.net**에 다시 작성 하는 경우 href = "~/content/"/&gt; &lt;의 href 특성은 **/** 대신 **/content/content/** 로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="c5567-204">이러한 변경을 방지 하기 위해 각 웹 페이지나 global.asax의 **응용 프로그램\_BeginRequest** 에서 **IIS\_WasUrlRewritten** context를 false로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="c5567-205">템플릿</span><span class="sxs-lookup"><span data-stu-id="c5567-205">Templates</span></span>

<span data-ttu-id="c5567-206">Windows 8.1 또는 Windows Server 2012 r 2에서 Visual Studio 2012을 사용 하 여 ASP.NET MVC 프로젝트를 만들 때 Visual Studio에는 "ASP.NET 4.5에 대 한 웹 구성 [url]이 실패 했습니다." 라는 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![구성 오류](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="c5567-208">Visual Studio 2012은 이러한 Windows 릴리스에 설치 될 때 ASP.NET 4.5 기능을 사용 하도록 설정 하지 않기 때문에이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="c5567-209">ASP.NET 4.5를 사용 하도록 설정 하려면 [Windows 기능 사용/사용 안 함](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)에 설명 된 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![Windows 기능 설정 또는 해제](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="c5567-211">또는 명령줄을 통해 ASP.NET 4.5을 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="c5567-212">관리자 모드에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="c5567-213">ASP.NET 4.5를 사용 하도록 설정 하려면 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5567-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
