---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 Visual Studio 2010 용 ASP.NET MVC 4 Beta 릴리스에 대해 설명 합니다.
ms.author: riande
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: 17800dfe091bbb7afb25f7f41e3bd885b882edb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419843"
---
# <a name="aspnet-mvc-4"></a><span data-ttu-id="8e4a0-103">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="8e4a0-103">ASP.NET MVC 4</span></span>

> <span data-ttu-id="8e4a0-104">이 문서에서는 Visual Studio 2010 용 ASP.NET MVC 4 Beta 릴리스에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-104">This document describes the release of ASP.NET MVC 4 Beta for Visual Studio 2010.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="8e4a0-105">이는 최신 릴리스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-105">This is not the most current release.</span></span> <span data-ttu-id="8e4a0-106">ASP.NET MVC 4 RC 릴리스 정보는 [여기](mvc4-release-notes.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-106">The ASP.NET MVC 4 RC release notes are available [here](mvc4-release-notes.md).</span></span>

- [<span data-ttu-id="8e4a0-107">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="8e4a0-107">Installation Notes</span></span>](#_Toc303253802)
- [<span data-ttu-id="8e4a0-108">설명서</span><span class="sxs-lookup"><span data-stu-id="8e4a0-108">Documentation</span></span>](#_Toc303253803)
- [<span data-ttu-id="8e4a0-109">지원</span><span class="sxs-lookup"><span data-stu-id="8e4a0-109">Support</span></span>](#_Toc303253804)
- [<span data-ttu-id="8e4a0-110">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="8e4a0-110">Software Requirements</span></span>](#_Toc303253805)
- [<span data-ttu-id="8e4a0-111">ASP.NET MVC 3 프로젝트를 ASP.NET MVC 4로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="8e4a0-111">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>](#_Toc303253806)
- [<span data-ttu-id="8e4a0-112">ASP.NET MVC 4 Beta의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="8e4a0-112">New Features in ASP.NET MVC 4 Beta</span></span>](#_Toc303253807)

    - [<span data-ttu-id="8e4a0-113">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="8e4a0-113">ASP.NET Web API</span></span>](#_Toc317096197)
    - [<span data-ttu-id="8e4a0-114">ASP.NET 단일 페이지 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8e4a0-114">ASP.NET Single Page Application</span></span>](#_Toc317096198)
    - [<span data-ttu-id="8e4a0-115">기본 프로젝트 템플릿에 대 한 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="8e4a0-115">Enhancements to Default Project Templates</span></span>](#_Toc303253808)
    - [<span data-ttu-id="8e4a0-116">모바일 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="8e4a0-116">Mobile Project Template</span></span>](#_Toc303253809)
    - [<span data-ttu-id="8e4a0-117">디스플레이 모드</span><span class="sxs-lookup"><span data-stu-id="8e4a0-117">Display Modes</span></span>](#_Toc303253810)
    - [<span data-ttu-id="8e4a0-118">jQuery Mobile, 뷰 전환기 및 브라우저 재정의</span><span class="sxs-lookup"><span data-stu-id="8e4a0-118">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>](#_Toc303253811)
    - [<span data-ttu-id="8e4a0-119">Visual Studio에서 코드 생성을 위한 조리법</span><span class="sxs-lookup"><span data-stu-id="8e4a0-119">Recipes for Code Generation in Visual Studio</span></span>](#_Toc303253812)
    - [<span data-ttu-id="8e4a0-120">비동기 컨트롤러에 대 한 작업 지원</span><span class="sxs-lookup"><span data-stu-id="8e4a0-120">Task Support for Asynchronous Controllers</span></span>](#_Toc303253813)
    - [<span data-ttu-id="8e4a0-121">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="8e4a0-121">Azure SDK</span></span>](#_Toc303253814)
    - [<span data-ttu-id="8e4a0-122">알려진 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="8e4a0-122">Known Issues and Breaking Changes</span></span>](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a><span data-ttu-id="8e4a0-123">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="8e4a0-123">Installation Notes</span></span>

<span data-ttu-id="8e4a0-124">ASP.NET MVC 4 Beta for Visual Studio 2010는 웹 플랫폼 설치 관리자를 사용 하 여 [ASP.NET mvc 4 홈 페이지](../mvc/mvc4.md) 에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-124">ASP.NET MVC 4 Beta for Visual Studio 2010 can be installed from the [ASP.NET MVC 4 home page](../mvc/mvc4.md) using the Web Platform Installer.</span></span>

<span data-ttu-id="8e4a0-125">ASP.NET MVC 4 Beta를 설치 하기 전에 ASP.NET MVC 4의 이전에 설치 된 미리 보기를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-125">You must uninstall any previously installed previews of ASP.NET MVC 4 prior to installing ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="8e4a0-126">이 릴리스는 .NET Framework 4.5 Developer Preview와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-126">This release is not compatible with the .NET Framework 4.5 Developer Preview.</span></span> <span data-ttu-id="8e4a0-127">ASP.NET MVC 4 Beta를 설치 하기 전에 .NET 4.5 Developer Preview를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-127">You must uninstall the .NET 4.5 Developer Preview before installing the ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="8e4a0-128">ASP.NET MVC 4는 설치 될 수 있으며 ASP.NET MVC 3과 함께 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-128">ASP.NET MVC 4 can be installed and can run side-by-side with ASP.NET MVC 3.</span></span>

<a id="_Toc303253803"></a>
## <a name="documentation"></a><span data-ttu-id="8e4a0-129">문서화</span><span class="sxs-lookup"><span data-stu-id="8e4a0-129">Documentation</span></span>

<span data-ttu-id="8e4a0-130">ASP.NET MVC 문서는 다음 URL의 MSDN 웹사이트에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-130">Documentation for ASP.NET MVC is available on the MSDN website at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

<span data-ttu-id="8e4a0-131">ASP.NET MVC에 대 한 자습서 및 기타 정보는[https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)(ASP.NET) 웹 사이트의 MVC 4 페이지 (영문)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-131">Tutorials and other information about ASP.NET MVC are available on the MVC 4 page of the ASP.NET website ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)).</span></span>

<a id="_Toc303253804"></a>
## <a name="support"></a><span data-ttu-id="8e4a0-132">지원</span><span class="sxs-lookup"><span data-stu-id="8e4a0-132">Support</span></span>

<span data-ttu-id="8e4a0-133">이 릴리스는 미리 보기 릴리스 이며 공식적으로 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-133">This is a preview release and is not officially supported.</span></span> <span data-ttu-id="8e4a0-134">이 릴리스를 사용 하는 방법에 대 한 질문이 있는 경우 ASP.NET MVC 포럼 ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx))에 게시 합니다. ASP.NET 커뮤니티의 구성원이 비공식적 지원을 제공할 수 있는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-134">If you have questions about working with this release, post them to the ASP.NET MVC forum ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a><span data-ttu-id="8e4a0-135">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="8e4a0-135">Software Requirements</span></span>

<span data-ttu-id="8e4a0-136">Visual Studio 용 ASP.NET MVC 4 구성 요소에는 PowerShell 2.0 및 Visual Studio 2010 서비스 팩 1 또는 Visual Web Developer Express 2010 서비스 팩 1이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-136">The ASP.NET MVC 4 components for Visual Studio require PowerShell 2.0 and either Visual Studio 2010 with Service Pack 1 or Visual Web Developer Express 2010 with Service Pack 1.</span></span>

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a><span data-ttu-id="8e4a0-137">ASP.NET MVC 3 프로젝트를 ASP.NET MVC 4로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="8e4a0-137">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>

<span data-ttu-id="8e4a0-138">ASP.NET MVC 4는 동일한 컴퓨터에 ASP.NET MVC 3과 함께 설치할 수 있습니다. 그러면 ASP.NET MVC 3 응용 프로그램을 ASP.NET MVC 4로 업그레이드할 시기를 유연 하 게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-138">ASP.NET MVC 4 can be installed side by side with ASP.NET MVC 3 on the same computer, which gives you flexibility in choosing when to upgrade an ASP.NET MVC 3 application to ASP.NET MVC 4.</span></span>

<span data-ttu-id="8e4a0-139">가장 간단한 업그레이드 방법은 새 ASP.NET MVC 4 프로젝트를 만들고 기존 MVC 3 프로젝트의 모든 뷰, 컨트롤러, 코드 및 콘텐츠 파일을 새 프로젝트에 복사한 다음 새 프로젝트의 어셈블리 참조를 이전 프로젝트와 일치 하도록 업데이트 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-139">The simplest way to upgrade is to create a new ASP.NET MVC 4 project and copy all the views, controllers, code, and content files from the existing MVC 3 project to the new project and then to update the assembly references in the new project to match the old project.</span></span> <span data-ttu-id="8e4a0-140">MVC 3 프로젝트에서 web.config 파일을 변경한 경우 이러한 변경 내용을 MVC 4 프로젝트의 web.config 파일에 병합 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-140">If you have made changes to the Web.config file in the MVC 3 project, you must also merge those changes into the Web.config file in the MVC 4 project.</span></span>

<span data-ttu-id="8e4a0-141">기존 ASP.NET MVC 3 응용 프로그램을 버전 4로 수동으로 업그레이드 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-141">To manually upgrade an existing ASP.NET MVC 3 application to version 4, do the following:</span></span>

1. <span data-ttu-id="8e4a0-142">프로젝트의 모든 Web.config 파일 (프로젝트의 루트에 있고, Views 폴더에 있고, 프로젝트의 각 영역에 대 한 Views 폴더에 있는 프로젝트)에서 다음 텍스트의 모든 인스턴스를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-142">In all Web.config files in the project (there is one in the root of the project, one in the Views folder, and one in the Views folder for each area in your project), replace every instance of the following text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    <span data-ttu-id="8e4a0-143">다음 텍스트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-143">with the following corresponding text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. <span data-ttu-id="8e4a0-144">루트 Web.config 파일에서 *웹 페이지: 버전* 요소를 "2.0.0.0"으로 업데이트 하 고 값이 "true" 인 새 *PreserveLoginUrl* 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-144">In the root Web.config file, update the *webPages:Version* element to "2.0.0.0" and add a new *PreserveLoginUrl* key that has the value "true":</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. <span data-ttu-id="8e4a0-145">솔루션 탐색기에서 버전 3 DLL을 가리키는 *system.web* 에 대 한 참조를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-145">In Solution Explorer, delete the reference to *System.Web.Mvc* (which points to the version 3 DLL).</span></span> <span data-ttu-id="8e4a0-146">그런 다음, *system.web* (v 4.0.0.0)에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-146">Then add a reference to *System.Web.Mvc* (v4.0.0.0).</span></span> <span data-ttu-id="8e4a0-147">특히, 어셈블리 참조를 업데이트 하려면 다음과 같이 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-147">In particular, make the following changes to update the assembly references.</span></span> <span data-ttu-id="8e4a0-148">세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-148">Here are the details:</span></span>

    1. <span data-ttu-id="8e4a0-149">솔루션 탐색기에서 다음 어셈블리에 대 한 참조를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-149">In Solution Explorer, delete the references to the following assemblies:</span></span> 

        - <span data-ttu-id="8e4a0-150">*System.web*(v 3.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-150">*System.Web.Mvc*(v3.0.0.0)</span></span>
        - <span data-ttu-id="8e4a0-151">*System.web. 웹 페이지*(v 1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-151">*System.Web.WebPages*(v1.0.0.0)</span></span>
        - <span data-ttu-id="8e4a0-152">*System.web. Razor*(v 1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-152">*System.Web.Razor*(v1.0.0.0)</span></span>
        - <span data-ttu-id="8e4a0-153">*System.web. 배포*(v 1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-153">*System.Web.WebPages.Deployment*(v1.0.0.0)</span></span>
        - <span data-ttu-id="8e4a0-154">*System.web. 웹 페이지. Razor*(v 1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-154">*System.Web.WebPages.Razor*(v1.0.0.0)</span></span>
    2. <span data-ttu-id="8e4a0-155">다음 어셈블리에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-155">Add a references to the following assemblies:</span></span> 

        - <span data-ttu-id="8e4a0-156">*System.web*(v 4.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-156">*System.Web.Mvc*(v4.0.0.0)</span></span>
        - <span data-ttu-id="8e4a0-157">*System.web. 웹 페이지*(v 2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-157">*System.Web.WebPages*(v2.0.0.0)</span></span>
        - <span data-ttu-id="8e4a0-158">*System.web*(v 2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-158">*System.Web.Razor*(v2.0.0.0)</span></span>
        - <span data-ttu-id="8e4a0-159">*System.web. 배포*(v 2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-159">*System.Web.WebPages.Deployment*(v2.0.0.0)</span></span>
        - <span data-ttu-id="8e4a0-160">*System.web. 웹 페이지. Razor*(v 2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-160">*System.Web.WebPages.Razor*(v2.0.0.0)</span></span>
4. <span data-ttu-id="8e4a0-161">솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 프로젝트 언로드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-161">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="8e4a0-162">그런 다음 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 *ProjectName*.csproj 편집을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-162">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
5. <span data-ttu-id="8e4a0-163">*Projecttypeguids* 요소를 찾아서 {E53F8FEA-EAE0-44A6-8774-FFD645390401}을 {E3E379DF-F4C6-4180-9B81-6769533ABE47}로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-163">Locate the *ProjectTypeGuids* element and replace {E53F8FEA-EAE0-44A6-8774-FFD645390401} with {E3E379DF-F4C6-4180-9B81-6769533ABE47}.</span></span>
6. <span data-ttu-id="8e4a0-164">변경 내용을 저장 하 고 편집 중인 프로젝트 (.csproj) 파일을 닫은 다음 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 프로젝트 다시 로드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-164">Save the changes, close the project (.csproj) file you were editing, right-click the project, and then select Reload Project.</span></span>
7. <span data-ttu-id="8e4a0-165">프로젝트가 이전 버전의 ASP.NET MVC를 사용 하 여 컴파일된 타사 라이브러리를 참조 하는 경우 루트 Web.config 파일을 열고 *구성* 섹션 아래에 다음 세 가지 *bindingRedirect* 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-165">If the project references any third-party libraries that are compiled using previous versions of ASP.NET MVC, open the root Web.config file and add the following three *bindingRedirect* elements under the *configuration* section:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a><span data-ttu-id="8e4a0-166">ASP.NET MVC 4 Beta의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="8e4a0-166">New Features in ASP.NET MVC 4 Beta</span></span>

<span data-ttu-id="8e4a0-167">이 섹션에서는 ASP.NET MVC 4 베타 릴리스에 도입 된 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-167">This section describes features that have been introduced in the ASP.NET MVC 4 Beta release.</span></span>

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="8e4a0-168">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="8e4a0-168">ASP.NET Web API</span></span>

<span data-ttu-id="8e4a0-169">이제 ASP.NET MVC 4에는 브라우저 및 모바일 장치를 비롯 한 광범위 한 클라이언트에 연결할 수 있는 HTTP 서비스를 만들기 위한 새로운 프레임 워크인 ASP.NET Web API 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-169">ASP.NET MVC 4 now includes ASP.NET Web API, a new framework for creating HTTP services that can reach a broad range of clients including browsers and mobile devices.</span></span> <span data-ttu-id="8e4a0-170">또한 ASP.NET Web API는 RESTful services를 빌드하기 위한 이상적인 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-170">ASP.NET Web API is also an ideal platform for building RESTful services.</span></span>

<span data-ttu-id="8e4a0-171">ASP.NET Web API에는 다음 기능에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-171">ASP.NET Web API includes support for the following features:</span></span>

- <span data-ttu-id="8e4a0-172">**최신 HTTP 프로그래밍 모델:** 강력한 형식의 새 HTTP 개체 모델을 사용 하 여 웹 Api에서 HTTP 요청 및 응답을 직접 액세스 하 고 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-172">**Modern HTTP programming model:** Directly access and manipulate HTTP requests and responses in your Web APIs using a new, strongly typed HTTP object model.</span></span> <span data-ttu-id="8e4a0-173">동일한 프로그래밍 모델 및 HTTP 파이프라인은 새 HttpClient 형식을 통해 클라이언트에서 대칭적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-173">The same programming model and HTTP pipeline is symmetrically available on the client through the new HttpClient type.</span></span>
- <span data-ttu-id="8e4a0-174">**경로에 대 한 완전 한 지원**: 이제 웹 api는 경로 매개 변수 및 제약 조건을 포함 하 여 항상 웹 스택의 일부가 되는 전체 경로 기능 집합을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-174">**Full support for routes**: Web APIs now support the full set of route capabilities that have always been a part of the Web stack, including route parameters and constraints.</span></span> <span data-ttu-id="8e4a0-175">또한 작업에 대 한 매핑에는 규칙에 대 한 모든 지원이 있으므로 클래스 및 메서드에 [HttpPost]와 같은 특성을 더 이상 적용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-175">Additionally, mapping to actions has full support for conventions, so you no longer need to apply attributes such as [HttpPost] to your classes and methods.</span></span>
- <span data-ttu-id="8e4a0-176">**콘텐츠 협상**: 클라이언트와 서버가 함께 작동 하 여 API에서 반환 되는 데이터의 올바른 형식을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-176">**Content negotiation**: The client and server can work together to determine the right format for data being returned from an API.</span></span> <span data-ttu-id="8e4a0-177">XML, JSON 및 폼 URL로 인코딩된 형식에 대 한 기본 지원을 제공 하며, 사용자 고유의 포맷터를 추가 하거나 기본 콘텐츠 협상 전략을 대체 하 여이 지원을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-177">We provide default support for XML, JSON, and Form URL-encoded formats, and you can extend this support by adding your own formatters, or even replace the default content negotiation strategy.</span></span>
- <span data-ttu-id="8e4a0-178">**모델 바인딩 및 유효성 검사:** 모델 바인더는 HTTP 요청의 다양 한 부분에서 데이터를 추출 하 고 이러한 메시지 부분을 웹 API 작업에서 사용할 수 있는 .NET 개체로 변환 하는 쉬운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-178">**Model binding and validation:** Model binders provide an easy way to extract data from various parts of an HTTP request and convert those message parts into .NET objects which can be used by the Web API actions.</span></span>
- <span data-ttu-id="8e4a0-179">**필터:** 이제 Web Api는 [권한 부여] 특성과 같은 잘 알려진 필터를 포함 하 여 필터를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-179">**Filters:** Web APIs now supports filters, including well-known filters such as the [Authorize] attribute.</span></span> <span data-ttu-id="8e4a0-180">작업, 권한 부여 및 예외 처리에 대 한 사용자 고유의 필터를 작성 하 고 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-180">You can author and plug in your own filters for actions, authorization and exception handling.</span></span>
- <span data-ttu-id="8e4a0-181">**쿼리 컴퍼지션:** IQueryable&lt;T&gt;반환 하기만 하면 Web API는 OData URL 규칙을 통한 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-181">**Query composition:** By simply returning IQueryable&lt;T&gt;, your Web API will support querying via the OData URL conventions.</span></span>
- <span data-ttu-id="8e4a0-182">**향상 된 HTTP 정보 테스트:** 정적 컨텍스트 개체에서 HTTP 세부 정보를 설정 하는 대신, 이제 HttpRequestMessage 및 HttpResponseMessage의 인스턴스를 사용 하 여 Web API 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-182">**Improved testability of HTTP details:** Rather than setting HTTP details in static context objects, Web API actions can now work with instances of HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="8e4a0-183">이러한 개체의 제네릭 버전은 HTTP 형식 외에 사용자 지정 형식으로 작업 하는 데에도 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-183">Generic versions of these objects also exist to let you work with your custom types in addition to the HTTP types.</span></span>
- <span data-ttu-id="8e4a0-184">**DependencyResolver를 통한 제어 반전 (IoC) 향상:** Web API는 이제 MVC의 종속성 확인자에서 구현 된 서비스 로케이터 패턴을 사용 하 여 다양 한 기능에 대 한 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-184">**Improved Inversion of Control (IoC) via DependencyResolver:** Web API now uses the service locator pattern implemented by MVC's dependency resolver to obtain instances for many different facilities.</span></span>
- <span data-ttu-id="8e4a0-185">**코드 기반 구성:** 웹 API 구성은 코드를 통해서만 수행 되며 구성 파일이 깨끗 하 게 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-185">**Code-based configuration:** Web API configuration is accomplished solely through code, leaving your config files clean.</span></span>
- <span data-ttu-id="8e4a0-186">**자체 호스트:** 웹 api는 전체 경로 및 Web API의 다른 기능을 계속 사용 하면서 IIS 외에도 자체 프로세스에서 호스팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-186">**Self-host:** Web APIs can be hosted in your own process in addition to IIS while still using the full power of routes and other features of Web API.</span></span>

<span data-ttu-id="8e4a0-187">ASP.NET Web API에 대 한 자세한 내용은 [https://www.asp.net/web-api](../web-api/index.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-187">For more details on ASP.NET Web API please visit [https://www.asp.net/web-api](../web-api/index.md).</span></span>

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a><span data-ttu-id="8e4a0-188">ASP.NET 단일 페이지 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8e4a0-188">ASP.NET Single Page Application</span></span>

<span data-ttu-id="8e4a0-189">ASP.NET MVC 4에는 이제 JavaScript 및 Web Api를 사용 하 여 중요 한 클라이언트 쪽 상호 작용으로 단일 페이지 응용 프로그램을 빌드하는 환경에 대 한 초기 미리 보기가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-189">ASP.NET MVC 4 now includes an early preview of the experience for building single page applications with significant client-side interactions using JavaScript and Web APIs.</span></span> <span data-ttu-id="8e4a0-190">이 지원에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-190">This support includes:</span></span>

- <span data-ttu-id="8e4a0-191">캐시 된 데이터와의 더 많은 로컬 상호 작용을 위한 JavaScript 라이브러리 집합</span><span class="sxs-lookup"><span data-stu-id="8e4a0-191">A set of JavaScript libraries for richer local interactions with cached data</span></span>
- <span data-ttu-id="8e4a0-192">작업 단위 및 DAL 지원에 대 한 추가 웹 API 구성 요소</span><span class="sxs-lookup"><span data-stu-id="8e4a0-192">Additional Web API components for unit of work and DAL support</span></span>
- <span data-ttu-id="8e4a0-193">신속 하 게 시작 하기 위해 스 캐 폴딩이 포함 된 MVC 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="8e4a0-193">An MVC project template with scaffolding to get started quickly</span></span>

<span data-ttu-id="8e4a0-194">ASP.NET MVC 4의 단일 페이지 응용 프로그램 지원에 대 한 자세한 내용은 [https://www.asp.net/single-page-application](../single-page-application/index.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-194">For more details on the Single Page Application support in ASP.NET MVC 4 please visit [https://www.asp.net/single-page-application](../single-page-application/index.md).</span></span>

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a><span data-ttu-id="8e4a0-195">기본 프로젝트 템플릿에 대 한 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="8e4a0-195">Enhancements to Default Project Templates</span></span>

<span data-ttu-id="8e4a0-196">새 ASP.NET MVC 4 프로젝트를 만드는 데 사용 되는 템플릿이 최신 웹 사이트를 만들기 위해 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-196">The template that is used to create new ASP.NET MVC 4 projects has been updated to create a more modern-looking website:</span></span>

![](mvc4-beta-release-notes/_static/image1.png)

<span data-ttu-id="8e4a0-197">외관 향상 외에도 새 템플릿에서 향상 된 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-197">In addition to cosmetic improvements, there's improved functionality in the new template.</span></span> <span data-ttu-id="8e4a0-198">템플릿에서는 적응 렌더링 이라는 기술을 사용 하 여 사용자 지정 없이 데스크톱 브라우저와 모바일 브라우저 모두에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-198">The template employs a technique called adaptive rendering to look good in both desktop browsers and mobile browsers without any customization.</span></span>

![](mvc4-beta-release-notes/_static/image2.png)

<span data-ttu-id="8e4a0-199">작동 중인 적응 렌더링을 보려면 모바일 에뮬레이터를 사용 하거나 데스크톱 브라우저 창의 크기를 작게 조정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-199">To see adaptive rendering in action, you can use a mobile emulator or just try resizing the desktop browser window to be smaller.</span></span> <span data-ttu-id="8e4a0-200">브라우저 창이 충분히 작으면 페이지 레이아웃이 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-200">When the browser window gets small enough, the layout of the page will change.</span></span>

<span data-ttu-id="8e4a0-201">기본 프로젝트 템플릿에 대 한 또 다른 향상 된 기능은 JavaScript를 사용 하 여 보다 풍부한 UI를 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-201">Another enhancement to the default project template is the use of JavaScript to provide a richer UI.</span></span> <span data-ttu-id="8e4a0-202">템플릿에 사용 되는 로그인 및 등록 링크는 jQuery UI 대화 상자를 사용 하 여 다양 한 로그인 화면을 표시 하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-202">The Login and Register links that are used in the template are examples of how to use the jQuery UI Dialog to present a rich login screen:</span></span>

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a><span data-ttu-id="8e4a0-203">모바일 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="8e4a0-203">Mobile Project Template</span></span>

<span data-ttu-id="8e4a0-204">새 프로젝트를 시작 하 고 모바일 및 태블릿 브라우저용으로 특정 사이트를 만들려는 경우 새 모바일 응용 프로그램 프로젝트 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-204">If you're starting a new project and want to create a site specifically for mobile and tablet browsers, you can use the new Mobile Application project template.</span></span> <span data-ttu-id="8e4a0-205">이는 터치 최적화 UI를 빌드하기 위한 오픈 소스 라이브러리인 jQuery Mobile을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-205">This is based on jQuery Mobile, an open-source library for building touch-optimized UI:</span></span>

![](mvc4-beta-release-notes/_static/image4.png)

<span data-ttu-id="8e4a0-206">이 템플릿은 인터넷 응용 프로그램 템플릿과 동일한 응용 프로그램 구조를 포함 하 고 컨트롤러 코드는 거의 동일 하지만, jQuery Mobile을 사용 하 여 양호한 것으로 확인 하 고 터치 기반 모바일 장치에서 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-206">This template contains the same application structure as the Internet Application template (and the controller code is virtually identical), but it's styled using jQuery Mobile to look good and behave well on touch-based mobile devices.</span></span> <span data-ttu-id="8e4a0-207">모바일 UI를 구조화 하 고 스타일을 만드는 방법에 대 한 자세한 내용은 [JQuery mobile project 웹 사이트](http://jquerymobile.com/)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-207">To learn more about how to structure and style mobile UI, see the [jQuery Mobile project website](http://jquerymobile.com/).</span></span>

<span data-ttu-id="8e4a0-208">모바일에 최적화 된 보기를 추가할 데스크톱 기반 사이트가 이미 있는 경우 또는 데스크톱 및 모바일 브라우저에 대해 다르게 스타일 지정 된 보기를 제공 하는 단일 사이트를 만들려는 경우에는 새 디스플레이 모드 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-208">If you already have a desktop-oriented site that you want to add mobile-optimized views to, or if you want to create a single site that serves differently styled views to desktop and mobile browsers, you can use the new Display Modes feature.</span></span> <span data-ttu-id="8e4a0-209">(다음 섹션을 참조하십시오.)</span><span class="sxs-lookup"><span data-stu-id="8e4a0-209">(See the next section.)</span></span>

<a id="_Toc303253810"></a>
### <a name="display-modes"></a><span data-ttu-id="8e4a0-210">디스플레이 모드</span><span class="sxs-lookup"><span data-stu-id="8e4a0-210">Display Modes</span></span>

<span data-ttu-id="8e4a0-211">새 디스플레이 모드 기능을 사용 하면 응용 프로그램에서 요청을 수행 하는 브라우저에 따라 보기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-211">The new Display Modes feature lets an application select views depending on the browser that's making the request.</span></span> <span data-ttu-id="8e4a0-212">예를 들어 데스크톱 브라우저에서 홈 페이지를 요청 하는 경우 응용 프로그램은 Views\Home\Index.cshtml 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-212">For example, if a desktop browser requests the Home page, the application might use the Views\Home\Index.cshtml template.</span></span> <span data-ttu-id="8e4a0-213">모바일 브라우저에서 홈 페이지를 요청 하는 경우 응용 프로그램에서 Views\Home\Index.mobile.cshtml 템플릿이 반환 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-213">If a mobile browser requests the Home page, the application might return the Views\Home\Index.mobile.cshtml template.</span></span>

<span data-ttu-id="8e4a0-214">레이아웃 및 부분 특정 브라우저 유형에 대해 재정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-214">Layouts and partials can also be overridden for particular browser types.</span></span> <span data-ttu-id="8e4a0-215">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-215">For example:</span></span>

- <span data-ttu-id="8e4a0-216">Views\Shared 폴더에 \_\_레이아웃을 모두 포함 하는 경우에는 기본적으로 응용 프로그램에서 \_Layout을 사용 합니다. 모바일 브라우저 및 \_레이아웃에서 요청 하는 동안에는 응용 프로그램에서 Layout을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-216">If your Views\Shared folder contains both the \_Layout.cshtml and \_Layout.mobile.cshtml templates, by default the application will use \_Layout.mobile.cshtml during requests from mobile browsers and \_Layout.cshtml during other requests.</span></span>
- <span data-ttu-id="8e4a0-217">폴더에 \_MyPartial 및 \_MyPartial이 모두 포함 되어 있으면 명령 @Html.Partial("\_MyPartial")는 모바일 브라우저에서 요청 하는 동안 MyPartial를 렌더링 하 고 다른 요청 중에는 \_MyPartial를 렌더링 합니다.\_</span><span class="sxs-lookup"><span data-stu-id="8e4a0-217">If a folder contains both \_MyPartial.cshtml and \_MyPartial.mobile.cshtml, the instruction @Html.Partial("\_MyPartial") will render \_MyPartial.mobile.cshtml during requests from mobile browsers, and \_MyPartial.cshtml during other requests.</span></span>

<span data-ttu-id="8e4a0-218">다른 장치에 대 한 보기, 레이아웃 또는 부분 보기를 더 많이 만들려는 경우 새 *DefaultDisplayMode* 인스턴스를 등록 하 여 요청이 특정 조건에 부합 될 때 검색할 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-218">If you want to create more specific views, layouts, or partial views for other devices, you can register a new *DefaultDisplayMode* instance to specify which name to search for when a request satisfies particular conditions.</span></span> <span data-ttu-id="8e4a0-219">예를 들어, Global.asax 파일의 *응용 프로그램\_Start* 메서드에 다음 코드를 추가 하 여 Apple iPhone 브라우저가 요청할 때 적용 되는 표시 모드로 문자열 "iPhone"을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-219">For example, you could add the following code to the *Application\_Start* method in the Global.asax file to register the string "iPhone" as a display mode that applies when the Apple iPhone browser makes a request:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

<span data-ttu-id="8e4a0-220">이 코드가 실행 된 후 Apple iPhone 브라우저가 요청을 만들면 응용 프로그램은 Views\Shared\\_Layout (있는 경우)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-220">After this code runs, when an Apple iPhone browser makes a request, your application will use the Views\Shared\\_Layout.iPhone.cshtml layout (if it exists).</span></span>

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a><span data-ttu-id="8e4a0-221">jQuery Mobile, 뷰 전환기 및 브라우저 재정의</span><span class="sxs-lookup"><span data-stu-id="8e4a0-221">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>

<span data-ttu-id="8e4a0-222">jQuery Mobile은 터치에 최적화 된 웹 UI를 빌드하기 위한 오픈 소스 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-222">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="8e4a0-223">ASP.NET MVC 4 응용 프로그램에서 jQuery Mobile을 사용 하려는 경우 시작 하는 데 도움이 되는 NuGet 패키지를 다운로드 하 여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-223">If you want to use jQuery Mobile with an ASP.NET MVC 4 application, you can download and install a NuGet package that helps you get started.</span></span> <span data-ttu-id="8e4a0-224">Visual Studio 패키지 관리자 콘솔에서 설치 하려면 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-224">To install it from the Visual Studio Package Manager Console, type the following command:</span></span>

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

<span data-ttu-id="8e4a0-225">다음을 포함 하 여 jQuery Mobile 및 일부 도우미 파일을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-225">This installs jQuery Mobile and some helper files, including the following:</span></span>

- <span data-ttu-id="8e4a0-226">Views/Shared/\_레이아웃. Mobile. cshtml는 jQuery 모바일 기반 레이아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-226">Views/Shared/\_Layout.Mobile.cshtml, which is a jQuery Mobile-based layout.</span></span>
- <span data-ttu-id="8e4a0-227">Views/Shared/\_ViewSwitcher로 구성 된 뷰-전환기 구성 요소입니다. cshtml 부분 뷰와 ViewSwitcherController.cs controller.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-227">A view-switcher component, which consists of the Views/Shared/\_ViewSwitcher.cshtml partial view and the ViewSwitcherController.cs controller.</span></span>

<span data-ttu-id="8e4a0-228">패키지를 설치한 후 모바일 브라우저를 사용 하 여 응용 프로그램을 실행 하거나 (예: Firefox [사용자 에이전트 전환기](http://chrispederick.com/work/user-agent-switcher/) 추가 기능) 해당 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-228">After you install the package, run your application using a mobile browser (or equivalent, like the Firefox [User Agent Switcher](http://chrispederick.com/work/user-agent-switcher/) add-on).</span></span> <span data-ttu-id="8e4a0-229">JQuery Mobile은 레이아웃 및 스타일을 처리 하므로 페이지가 크게 달라 보입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-229">You'll see that your pages look quite different, because jQuery Mobile handles layout and styling.</span></span> <span data-ttu-id="8e4a0-230">이를 활용 하려면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-230">To take advantage of this, you can do the following:</span></span>

- <span data-ttu-id="8e4a0-231">이전 [표시 모드](#_Toc303253810) (예: 모바일 브라우저용 Views\Home\Index.cshtml를 재정의 하는 Views\Home\Index.mobile.cshtml 만들기)에 설명 된 대로 모바일 관련 뷰 재정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-231">Create mobile-specific view overrides as described under [Display Modes](#_Toc303253810) earlier (for example, create Views\Home\Index.mobile.cshtml to override Views\Home\Index.cshtml for mobile browsers).</span></span>
- <span data-ttu-id="8e4a0-232">[JQuery 모바일 설명서](http://jquerymobile.com/) 를 읽고 모바일 보기에서 터치 최적화 UI 요소를 추가 하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-232">Read the [jQuery Mobile documentation](http://jquerymobile.com/) to learn more about how to add touch-optimized UI elements in mobile views.</span></span>

<span data-ttu-id="8e4a0-233">모바일 최적화 웹 페이지의 규칙은 사용자가 페이지의 데스크톱 버전으로 전환할 수 있는 바탕 화면 보기 또는 전체 사이트 모드와 같은 텍스트를 포함 하는 링크를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-233">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="8e4a0-234">JQuery. Mobile. i n a. i n a.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-234">The jQuery.Mobile.MVC package includes a sample view-switcher component for this purpose.</span></span> <span data-ttu-id="8e4a0-235">이는 기본 Views\Shared\\_Layout에 사용 되며 페이지가 렌더링 될 때 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-235">It's used in the default Views\Shared\\_Layout.Mobile.cshtml view, and it looks like this when the page is rendered:</span></span>

![](mvc4-beta-release-notes/_static/image5.png)

<span data-ttu-id="8e4a0-236">방문자가 링크를 클릭 하면 동일한 페이지의 데스크톱 버전으로 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-236">If visitors click the link, they're switched to the desktop version of the same page.</span></span>

<span data-ttu-id="8e4a0-237">바탕 화면 레이아웃에는 기본적으로 보기 전환기가 포함 되어 있지 않으므로 방문자는 모바일 모드로 전환 하는 방법을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-237">Because your desktop layout will not include a view switcher by default, visitors won't have a way to get to mobile mode.</span></span> <span data-ttu-id="8e4a0-238">이를 사용 하도록 설정 하려면 *ViewSwitcher\_* 에 대 한 다음 참조를 *&lt;body&gt;* 요소 내에서 바탕 화면 레이아웃에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-238">To enable this, add the following reference to *\_ViewSwitcher* to your desktop layout, just inside the *&lt;body&gt;* element:</span></span>

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

<span data-ttu-id="8e4a0-239">뷰 전환기는 브라우저 재정의 라는 새로운 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-239">The view switcher uses a new feature called Browser Overriding.</span></span> <span data-ttu-id="8e4a0-240">이 기능을 통해 응용 프로그램은 요청을 실제로 사용 하는 것과 다른 브라우저 (사용자 에이전트)에서 가져온 것 처럼 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-240">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they're actually from.</span></span> <span data-ttu-id="8e4a0-241">다음 표에서는 브라우저 재정의에서 제공 하는 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-241">The following table lists the methods that Browser Overriding provides.</span></span>

| `HttpContext.SetOverriddenBrowser(userAgentString)` | <span data-ttu-id="8e4a0-242">지정된 사용자 에이전트를 사용하여 요청의 실제 사용자 에이전트 값을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-242">Overrides the request's actual user agent value using the specified user agent.</span></span> |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | <span data-ttu-id="8e4a0-243">요청의 사용자 에이전트 재정의 값 또는 재정의가 지정 되지 않은 경우 실제 사용자 에이전트 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-243">Returns the request's user agent override value, or the actual user agent string if no override has been specified.</span></span> |
| `HttpContext.GetOverriddenBrowser()` | <span data-ttu-id="8e4a0-244">현재 요청에 대해 설정 된 (실제 또는 재정의) 사용자 에이전트에 해당 하는 *HttpBrowserCapabilitiesBase* 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-244">Returns an *HttpBrowserCapabilitiesBase* instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="8e4a0-245">이 값을 사용 하 여 *IsMobileDevice*등의 속성을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-245">You can use this value to get properties such as *IsMobileDevice*.</span></span> |
| `HttpContext.ClearOverriddenBrowser()` | <span data-ttu-id="8e4a0-246">현재 요청에 대해 재정의된 사용자 에이전트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-246">Removes any overridden user agent for the current request.</span></span> |

<span data-ttu-id="8e4a0-247">브라우저 재정의는 ASP.NET MVC 4의 핵심 기능이 며, jQuery를 설치 하지 않은 경우에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-247">Browser Overriding is a core feature of ASP.NET MVC 4 and is available even if you don't install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="8e4a0-248">그러나 뷰, 레이아웃 및 부분 뷰 선택에만 영향을 *줍니다. ASP.NET 개체에* 종속 되는 다른 모든 기능에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-248">However, it affects only view, layout, and partial-view selection — it does not affect any other ASP.NET feature that depends on the *Request.Browser* object.</span></span>

<span data-ttu-id="8e4a0-249">기본적으로 사용자 에이전트 재정의는 쿠키를 사용 하 여 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-249">By default, the user-agent override is stored using a cookie.</span></span> <span data-ttu-id="8e4a0-250">데이터베이스의 경우와 같이 다른 곳에서 재정의를 저장 하려는 경우 기본 공급자 (*Browseroverridestores. Current*)를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-250">If you want to store the override elsewhere (for example, in a database), you can replace the default provider (*BrowserOverrideStores.Current*).</span></span> <span data-ttu-id="8e4a0-251">이 공급자에 대 한 설명서는 이후 버전의 ASP.NET MVC와 함께 제공 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-251">Documentation for this provider will be available to accompany a later release of ASP.NET MVC.</span></span>

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a><span data-ttu-id="8e4a0-252">Visual Studio에서 코드 생성을 위한 조리법</span><span class="sxs-lookup"><span data-stu-id="8e4a0-252">Recipes for Code Generation in Visual Studio</span></span>

<span data-ttu-id="8e4a0-253">새로운 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 여</span><span class="sxs-lookup"><span data-stu-id="8e4a0-253">The new Recipes feature enables Visual Studio to generate solution-specific code based on packages that you can install using NuGet.</span></span> <span data-ttu-id="8e4a0-254">레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 레 피가 프레임 워크</span><span class="sxs-lookup"><span data-stu-id="8e4a0-254">The Recipes framework makes it easy for developers to write code-generation plugins, which you can also use to replace the built-in code generators for Add Area, Add Controller, and Add View.</span></span> <span data-ttu-id="8e4a0-255">조리법은 NuGet 패키지로 배포 되기 때문에 쉽게 소스 제어에 체크 인하고 프로젝트의 모든 개발자와 자동으로 공유 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-255">Because recipes are deployed as NuGet packages, they can easily be checked into source control and shared with all developers on the project automatically.</span></span> <span data-ttu-id="8e4a0-256">솔루션 별로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-256">They are also available on a per-solution basis.</span></span>

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a><span data-ttu-id="8e4a0-257">비동기 컨트롤러에 대 한 작업 지원</span><span class="sxs-lookup"><span data-stu-id="8e4a0-257">Task Support for Asynchronous Controllers</span></span>

<span data-ttu-id="8e4a0-258">이제 비동기 작업 메서드를 *task* 또는 task 형식의 개체를 반환 하는 단일 메서드 *&lt;actionresult&gt;* 에 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-258">You can now write asynchronous action methods as single methods that return an object of type *Task* or *Task&lt;ActionResult&gt;*.</span></span>

<span data-ttu-id="8e4a0-259">예를 들어, Visual C# 5를 사용 하는 경우 (또는 [비동기 CTP](https://msdn.microsoft.com/vstudio/async.aspx)를 사용 하는 경우) 다음과 같은 비동기 작업 메서드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-259">For example, if you're using Visual C# 5 (or using the [Async CTP](https://msdn.microsoft.com/vstudio/async.aspx)), you can create an asynchronous action method that looks like the following:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

<span data-ttu-id="8e4a0-260">이전 동작 메서드에서 *newsService* 에 *대 한 호출* 은 비동기적으로 호출 되며 스레드 풀에서 스레드를 차단 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-260">In the previous action method, the calls to *newsService.GetHeadlinesAsync* and *sportsService.GetScoresAsync* are called asynchronously and do not block a thread from the thread pool.</span></span>

<span data-ttu-id="8e4a0-261">*작업* 인스턴스를 반환 하는 비동기 작업 메서드는 시간 제한을 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-261">Asynchronous action methods that return *Task* instances can also support timeouts.</span></span> <span data-ttu-id="8e4a0-262">작업 메서드를 취소 가능한 하려면 *CancellationToken* 형식의 매개 변수를 동작 메서드 시그니처에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-262">To make your action method cancellable, add a parameter of type *CancellationToken* to the action method signature.</span></span> <span data-ttu-id="8e4a0-263">다음 예제에서는 시간 제한이 2500 밀리초이 고 시간 제한이 발생 하는 경우 클라이언트에 *TimedOut* 뷰를 표시 하는 비동기 작업 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-263">The following example shows an asynchronous action method that has a timeout of 2500 milliseconds and that displays a *TimedOut* view to the client if a timeout occurs.</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a><span data-ttu-id="8e4a0-264">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="8e4a0-264">Azure SDK</span></span>

<span data-ttu-id="8e4a0-265">ASP.NET MVC 4 Beta는 Microsoft Azure SDK의 9 월 2011 1.5 릴리스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-265">ASP.NET MVC 4 Beta supports the September 2011 1.5 release of the Windows Azure SDK.</span></span>

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="8e4a0-266">알려진 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="8e4a0-266">Known Issues and Breaking Changes</span></span>

- <span data-ttu-id="8e4a0-267">**ASP.NET MVC 4 Beta를 설치한 후에는 코드 조각 또는 형식 파일에 코드 조각 또는 JavaScript를 입력 한 후 Visual Studio 2010 서비스 팩 1 CSHTML/VBHTML 편집기의 CSHTML/VBHTML editor가 오랫동안 일시 중지 될 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="8e4a0-267">**After installing ASP.NET MVC 4 Beta, the CSHTML/VBHTML editor in Visual Studio 2010 Service Pack 1 CSHTML/VBHTML editor may pause for a long time after typing snippet or JavaScript inside cshtml or vbhtml files.**</span></span> <span data-ttu-id="8e4a0-268">이는 생성 되었으며 아직 컴파일되지 않은 ASP.NET MVC 4 응용 프로그램 에서만 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-268">This occurs only in ASP.NET MVC 4 applications which have just been created and have not yet been compiled.</span></span>

    <span data-ttu-id="8e4a0-269">해결 방법은 프로젝트를 컴파일하여 bin 폴더의 어셈블리를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-269">The workaround is to compile the project to get the assemblies in the bin folder.</span></span> <span data-ttu-id="8e4a0-270">Bin 폴더에서 어셈블리를 제거 하는 프로젝트를 정리 하면 편집기 문제가 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-270">Note, if you clean the project which removes the assemblies from the bin folder, the editor problem will come back.</span></span>

    <span data-ttu-id="8e4a0-271">이는 다음 릴리스에서 수정 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-271">This will be corrected in the next release.</span></span>
- <span data-ttu-id="8e4a0-272">**C#Visual Studio 11 Beta 용 프로젝트 템플릿의 Global.asax.cs에 잘못 된 연결 문자열이 포함 되어 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="8e4a0-272">**C# Project templates for Visual Studio 11 Beta contain an incorrect connection string in Global.asax.cs.**</span></span> <span data-ttu-id="8e4a0-273">Visual Studio 11 Beta에서 만든 프로젝트에 대 한 응용 프로그램\_Start 메서드에 지정 된 기본 연결에는 이스케이프 되지 않은 백슬래시 (\) 문자를 포함 하는 LocalDB 연결 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-273">The default connection specified in the Application\_Start method for projects created in Visual Studio 11 Beta contain a LocalDB connection string which contains an unescaped backslash (\) character.</span></span> <span data-ttu-id="8e4a0-274">이로 인해 SqlException을 생성 하는 Entity Framework DbContext에 대 한 액세스를 시도할 때 연결 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-274">This results in a connection error upon attempts to access a Entity Framework DbContext, which generates a SqlException.</span></span>

    <span data-ttu-id="8e4a0-275">이 문제를 해결 하려면 Global.asax.cs의 App\_Start 메서드에서 백슬래시 문자를 이스케이프 하 여 다음과 같이 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-275">To correct this issue, escape the backslash character in the App\_Start method of Global.asax.cs so that it reads as follows:</span></span>

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- <span data-ttu-id="8e4a0-276">**.Net 4.5를 대상으로 하는 ASP.NET MVC 4 응용 프로그램은 .NET 4.0에서 실행 될 때 FileLoadException 어셈블리에 액세스 하려고 할 때을 throw 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8e4a0-276">**ASP.NET MVC 4 applications which target .NET 4.5 will throw a FileLoadException upon attempt to access the System.Net.Http.dll assembly when run under .NET 4.0.**</span></span> <span data-ttu-id="8e4a0-277">.NET 4.5에서 만든 ASP.NET MVC 4 응용 프로그램에는 "파일 또는 어셈블리를 로드할 수 없습니다. Http ' 또는 해당 종속성 중 하나를 로드할 수 없습니다." 라는 FileLoadException를 생성 하는 바인딩 리디렉션이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-277">ASP.NET MVC 4 applications created under .NET 4.5 contain a binding redirect that will result in a FileLoadException which that states "Could not load file or assembly 'System.Net.Http' or one of its dependencies."</span></span> <span data-ttu-id="8e4a0-278">응용 프로그램이 .NET 4.0이 설치 된 시스템에서 실행 되는 경우</span><span class="sxs-lookup"><span data-stu-id="8e4a0-278">when the application is executed on a system with .NET 4.0 installed.</span></span> <span data-ttu-id="8e4a0-279">이 문제를 해결 하려면 web.config에서 다음 바인딩 리디렉션을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-279">To correct this issue, remove the following binding redirect from web.config:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    <span data-ttu-id="8e4a0-280">수정 된 web.config의 어셈블리 바인딩 요소는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-280">The assembly binding element in the modified web.config should appear as follows:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <span data-ttu-id="8e4a0-281"><strong>Visual Basic 프로젝트의 "컨트롤러 추가" 항목 템플릿은</strong><strong>영역 내부에서</strong> 호출 될 때 잘못 된 네임 스페이스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-281"><strong>The "Add Controller" item template in Visual Basic projects generates an incorrect namespace when invoked</strong><strong>from inside an area.</strong></span></span> <span data-ttu-id="8e4a0-282">Visual Basic를 사용 하는 ASP.NET MVC 프로젝트의 영역에 컨트롤러를 추가 하면 항목 템플릿에서 잘못 된 네임 스페이스를 컨트롤러에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-282">When you add a controller to an area in an ASP.NET MVC project that uses Visual Basic, the item template inserts the wrong namespace into the controller.</span></span> <span data-ttu-id="8e4a0-283">컨트롤러에서 작업으로 이동할 때 결과는 "파일을 찾을 수 없습니다" 라는 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-283">The result is a "file not found" error when you navigate to any action in the controller.</span></span>  
  
  <span data-ttu-id="8e4a0-284">생성 된 네임 스페이스는 루트 네임 스페이스 이후의 모든 항목을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-284">The generated namespace omits everything after the root namespace.</span></span> <span data-ttu-id="8e4a0-285">예를 들어 생성 된 네임 스페이스는 *RootNamespace* 이지만 *RootNamespace AreaName* 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-285">For example, the namespace generated is *RootNamespace* but should be *RootNamespace.Areas.AreaName.Controllers* .</span></span>
- <span data-ttu-id="8e4a0-286">**Razor 뷰 엔진의 주요 변경 내용입니다.**</span><span class="sxs-lookup"><span data-stu-id="8e4a0-286">**Breaking changes in the Razor View Engine.**</span></span> <span data-ttu-id="8e4a0-287">Razor 파서를 다시 작성 하는 과정에서 다음과 같은 형식이 *system.web*에서 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-287">As part of a rewrite of the Razor parser, the following types were removed from *System.Web.Mvc.Razor*:</span></span> 

    - <span data-ttu-id="8e4a0-288">*ModelSpan*</span><span class="sxs-lookup"><span data-stu-id="8e4a0-288">*ModelSpan*</span></span>
    - <span data-ttu-id="8e4a0-289">*MvcVBRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="8e4a0-289">*MvcVBRazorCodeGenerator*</span></span>
    - <span data-ttu-id="8e4a0-290">*MvcCSharpRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="8e4a0-290">*MvcCSharpRazorCodeGenerator*</span></span>
    - <span data-ttu-id="8e4a0-291">*MvcVBRazorCodeParser*</span><span class="sxs-lookup"><span data-stu-id="8e4a0-291">*MvcVBRazorCodeParser*</span></span>

  <span data-ttu-id="8e4a0-292">다음 메서드도 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-292">The following methods were also removed:</span></span> 

    - <span data-ttu-id="8e4a0-293">*MvcCSharpRazorCodeParser (ParseInheritsStatement) ((System.web.*</span><span class="sxs-lookup"><span data-stu-id="8e4a0-293">*MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
    - <span data-ttu-id="8e4a0-294">*MvcWebPageRazorHost (DecorateCodeGenerator) (RazorCodeGenerator)*</span><span class="sxs-lookup"><span data-stu-id="8e4a0-294">*MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*</span></span>
    - <span data-ttu-id="8e4a0-295">*MvcVBRazorCodeParser (System.web. CodeBlockInfo)*</span><span class="sxs-lookup"><span data-stu-id="8e4a0-295">*MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
- <span data-ttu-id="8e4a0-296">**ASP.NET MVC 4 앱의 WebData 디렉터리에 WebMatrix를 포함 하는 경우 폼 인증에 대 한 URL을 사용 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8e4a0-296">**When WebMatrix.WebData.dll is included in the /bin directory of an ASP.NET MVC 4 apps, it takes over the URL for forms authentication.**</span></span> <span data-ttu-id="8e4a0-297">응용 프로그램에 WebData 어셈블리를 추가 하는 경우 (예를 들어, 배포 가능 종속성 추가 대화 상자를 사용할 때 "Razor 구문을 사용 하 여 ASP.NET 웹 페이지"을 선택 하는 경우)에는 기본 ASP.NET MVC 계정 컨트롤러에서 예상 하는/account/pvrn이 아닌/t r i n s/logon으로의 인증 로그인 리디렉션이 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-297">Adding the WebMatrix.WebData.dll assembly to your application (for example, by selecting "ASP.NET Web Pages with Razor Syntax" when using the Add Deployable Dependencies dialog) will override the authentication login redirect to /account/logon rather than /account/login as expected by the default ASP.NET MVC Account Controller.</span></span> <span data-ttu-id="8e4a0-298">이 동작을 방지 하 고 web.config의 인증 섹션에 이미 지정 된 URL을 사용 하려면 PreserveLoginUrl 라는 appSetting를 추가 하 고 true로 설정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-298">To prevent this behavior and use the URL specified already in the authentication section of web.config, you can add an appSetting called PreserveLoginUrl and set it to true:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- <span data-ttu-id="8e4a0-299">**Visual Studio 2010 및 Visual Web Developer 2010의 side-by-side 설치를 위해 ASP.NET MVC 4를 설치 하려고 하면 NuGet 패키지 관리자가 설치 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="8e4a0-299">**The NuGet package manager fails to install when attempting to install ASP.NET MVC 4 for side by side installations of Visual Studio 2010 and Visual Web Developer 2010.**</span></span> <span data-ttu-id="8e4a0-300">ASP.NET MVC 4를 사용 하 여 Visual Studio 2010 및 Visual Web Developer 2010을 함께 실행 하려면 두 버전의 Visual Studio가 이미 설치 된 후 ASP.NET MVC 4를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-300">To run Visual Studio 2010 and Visual Web Developer 2010 side by side with ASP.NET MVC 4 you must install ASP.NET MVC 4 after both versions of Visual Studio have already been installed.</span></span>
- <span data-ttu-id="8e4a0-301">**필수 구성 요소가 이미 제거 된 경우 ASP.NET MVC 4를 제거 하는 작업이 실패 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8e4a0-301">**Uninstalling ASP.NET MVC 4 fails if prerequisites have already been uninstalled.**</span></span> <span data-ttu-id="8e4a0-302">ASP.NET MVC 4를 완전히 제거 하려면 Visual Studio를 제거 하기 전에 ASP.NET MVC 4를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-302">To cleanly uninstall ASP.NET MVC 4you must uninstall ASP.NET MVC 4 prior to uninstalling Visual Studio.</span></span>
- <span data-ttu-id="8e4a0-303">**기본 Web API 프로젝트를 실행 하면 사용자가 존재 하지 않는 RegisterApis 메서드를 사용 하 여 경로를 추가 하도록 잘못 지시 하는 명령이 표시 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="8e4a0-303">**Running a default Web API project shows instructions that incorrectly direct the user to add routes using the RegisterApis method, which doesn't exist.**</span></span> <span data-ttu-id="8e4a0-304">ASP.NET 경로 테이블을 사용 하 여 RegisterRoutes 메서드에서 경로를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-304">Routes should be added in the RegisterRoutes method using the ASP.NET route table.</span></span>
- <span data-ttu-id="8e4a0-305">**ASP.NET MVC 4 Beta를 설치 하면 ASP.NET MVC 3 RTM 응용 프로그램이 중단 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="8e4a0-305">**Installing ASP.NET MVC 4 Beta breaks ASP.NET MVC 3 RTM applications.**</span></span> <span data-ttu-id="8e4a0-306">RTM 릴리스로 만든 ASP.NET MVC 3 응용 프로그램 (ASP.NET MVC 3 도구 업데이트 릴리스를 사용 하지 않음)은 ASP.NET MVC 4 Beta와 함께 작동 하기 위해 다음과 같이 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-306">ASP.NET MVC 3 applications that were created with the RTM release (not with the ASP.NET MVC 3 Tools Update release) require the following changes in order to work side-by-side with ASP.NET MVC 4 Beta.</span></span> <span data-ttu-id="8e4a0-307">이러한 업데이트를 수행 하지 않고 프로젝트를 빌드하면 컴파일 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-307">Building the project without making these updates results in compilation errors.</span></span> 

    <span data-ttu-id="8e4a0-308">**필수 업데이트**</span><span class="sxs-lookup"><span data-stu-id="8e4a0-308">**Required updates**</span></span>

  1. <span data-ttu-id="8e4a0-309">루트 Web.config 파일에서 키 *웹 페이지: 버전* 및 값 *1.0.0.0*을 사용 하 여 새 *&lt;appSettings&gt;* 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-309">In the root Web.config file, add a new *&lt;appSettings&gt;* entry with the key *webPages:Version* and the value *1.0.0.0*.</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. <span data-ttu-id="8e4a0-310">솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 프로젝트 언로드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-310">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="8e4a0-311">그런 다음 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 *ProjectName*.csproj 편집을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-311">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
  3. <span data-ttu-id="8e4a0-312">다음 어셈블리 참조를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-312">Locate the following assembly references:</span></span> 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      <span data-ttu-id="8e4a0-313">다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-313">Replace them with the following:</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. <span data-ttu-id="8e4a0-314">변경 내용을 저장 하 고 편집 중인 프로젝트 (.csproj) 파일을 닫은 다음 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 다시 로드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e4a0-314">Save the changes, close the project (.csproj) file you were editing, and then right-click the project and select Reload.</span></span>
