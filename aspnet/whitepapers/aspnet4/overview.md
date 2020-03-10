---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 및 Visual Studio 2010 웹 개발 개요 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 the.NET Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 여러 가지 새로운 기능에 대 한 개요를 제공 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: ecde48f6bd88ee5f569bfeb8b70c26a50bc869c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511433"
---
# <a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a><span data-ttu-id="e6592-103">ASP.NET 4 및 Visual Studio 2010 웹 개발 개요</span><span class="sxs-lookup"><span data-stu-id="e6592-103">ASP.NET 4 and Visual Studio 2010 Web Development Overview</span></span>

> <span data-ttu-id="e6592-104">이 문서에서는 the.NET Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 여러 가지 새로운 기능에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-104">This document provides an overview of many of the new features for ASP.NET that are included in the.NET Framework 4 and in Visual Studio 2010.</span></span>
> 
> [<span data-ttu-id="e6592-105">이 백서 다운로드</span><span class="sxs-lookup"><span data-stu-id="e6592-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)

<span data-ttu-id="e6592-106">**콘텐츠**</span><span class="sxs-lookup"><span data-stu-id="e6592-106">**Contents**</span></span>

<span data-ttu-id="e6592-107">**[핵심 서비스](#0.2__Toc253429238 "_Toc253429238")**</span><span class="sxs-lookup"><span data-stu-id="e6592-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span></span>  
[<span data-ttu-id="e6592-108">Web.config 파일 리팩터링</span><span class="sxs-lookup"><span data-stu-id="e6592-108">Web.config File Refactoring</span></span>](#0.2__Toc253429239 "_Toc253429239")  
[<span data-ttu-id="e6592-109">확장 가능한 출력 캐싱</span><span class="sxs-lookup"><span data-stu-id="e6592-109">Extensible Output Caching</span></span>](#0.2__Toc253429240 "_Toc253429240")  
[<span data-ttu-id="e6592-110">웹 응용 프로그램 자동 시작</span><span class="sxs-lookup"><span data-stu-id="e6592-110">Auto-Start Web Applications</span></span>](#0.2__Toc253429241 "_Toc253429241")  
[<span data-ttu-id="e6592-111">페이지를 영구적으로 리디렉션</span><span class="sxs-lookup"><span data-stu-id="e6592-111">Permanently Redirecting a Page</span></span>](#0.2__Toc253429242 "_Toc253429242")  
[<span data-ttu-id="e6592-112">세션 상태 축소</span><span class="sxs-lookup"><span data-stu-id="e6592-112">Shrinking Session State</span></span>](#0.2__Toc253429243 "_Toc253429243")  
[<span data-ttu-id="e6592-113">허용 되는 Url 범위 확장</span><span class="sxs-lookup"><span data-stu-id="e6592-113">Expanding the Range of Allowable URLs</span></span>](#0.2__Toc253429244 "_Toc253429244")  
[<span data-ttu-id="e6592-114">확장 가능한 요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e6592-114">Extensible Request Validation</span></span>](#0.2__Toc253429245 "_Toc253429245")  
[<span data-ttu-id="e6592-115">개체 캐싱 및 개체 캐싱 확장성</span><span class="sxs-lookup"><span data-stu-id="e6592-115">Object Caching and Object Caching Extensibility</span></span>](#0.2__Toc253429246 "_Toc253429246")  
[<span data-ttu-id="e6592-116">확장 가능한 HTML, URL 및 HTTP 헤더 인코딩</span><span class="sxs-lookup"><span data-stu-id="e6592-116">Extensible HTML, URL, and HTTP Header Encoding</span></span>](#0.2__Toc253429247 "_Toc253429247")  
[<span data-ttu-id="e6592-117">단일 작업자 프로세스의 개별 응용 프로그램에 대 한 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="e6592-117">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>](#0.2__Toc253429248 "_Toc253429248")  
[<span data-ttu-id="e6592-118">다중 대상 지정</span><span class="sxs-lookup"><span data-stu-id="e6592-118">Multi-Targeting</span></span>](#0.2__Toc253429249 "_Toc253429249")

<span data-ttu-id="e6592-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span><span class="sxs-lookup"><span data-stu-id="e6592-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span></span>  
[<span data-ttu-id="e6592-120">Web Forms 및 MVC에 포함 된 jQuery</span><span class="sxs-lookup"><span data-stu-id="e6592-120">jQuery Included with Web Forms and MVC</span></span>](#0.2__Toc253429251 "_Toc253429251")  
[<span data-ttu-id="e6592-121">지원 Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="e6592-121">Content Delivery Network Support</span></span>](#0.2__Toc253429252 "_Toc253429252")  
[<span data-ttu-id="e6592-122">ScriptManager 명시적 스크립트</span><span class="sxs-lookup"><span data-stu-id="e6592-122">ScriptManager Explicit Scripts</span></span>](#0.2__Toc253429253 "_Toc253429253")

<span data-ttu-id="e6592-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span><span class="sxs-lookup"><span data-stu-id="e6592-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span></span>  
[<span data-ttu-id="e6592-124">MetaKeywords 및 MetaDescription 속성을 사용 하 여 Meta 태그를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-124">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>](#0.2__Toc253429257 "_Toc253429257")  
[<span data-ttu-id="e6592-125">개별 컨트롤에 대 한 뷰 상태 설정</span><span class="sxs-lookup"><span data-stu-id="e6592-125">Enabling View State for Individual Controls</span></span>](#0.2__Toc253429258 "_Toc253429258")  
[<span data-ttu-id="e6592-126">브라우저 기능 변경 내용</span><span class="sxs-lookup"><span data-stu-id="e6592-126">Changes to Browser Capabilities</span></span>](#0.2__Toc253429259 "_Toc253429259")  
[<span data-ttu-id="e6592-127">ASP.NET 4의 라우팅</span><span class="sxs-lookup"><span data-stu-id="e6592-127">Routing in ASP.NET 4</span></span>](#0.2__Toc253429260 "_Toc253429260")  
[<span data-ttu-id="e6592-128">클라이언트 Id 설정</span><span class="sxs-lookup"><span data-stu-id="e6592-128">Setting Client IDs</span></span>](#0.2__Toc253429261 "_Toc253429261")  
[<span data-ttu-id="e6592-129">데이터 컨트롤에서 행 선택 유지</span><span class="sxs-lookup"><span data-stu-id="e6592-129">Persisting Row Selection in Data Controls</span></span>](#0.2__Toc253429262 "_Toc253429262")  
[<span data-ttu-id="e6592-130">ASP.NET Chart 컨트롤</span><span class="sxs-lookup"><span data-stu-id="e6592-130">ASP.NET Chart Control</span></span>](#0.2__Toc253429263 "_Toc253429263")  
[<span data-ttu-id="e6592-131">QueryExtender 컨트롤을 사용 하 여 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="e6592-131">Filtering Data with the QueryExtender Control</span></span>](#0.2__Toc253429264 "_Toc253429264")  
[<span data-ttu-id="e6592-132">Html로 인코딩된 코드 식</span><span class="sxs-lookup"><span data-stu-id="e6592-132">Html Encoded Code Expressions</span></span>](#0.2__Toc253429265 "_Toc253429265")  
[<span data-ttu-id="e6592-133">프로젝트 템플릿 변경</span><span class="sxs-lookup"><span data-stu-id="e6592-133">Project Template Changes</span></span>](#0.2__Toc253429266 "_Toc253429266")  
[<span data-ttu-id="e6592-134">CSS 개선 사항</span><span class="sxs-lookup"><span data-stu-id="e6592-134">CSS Improvements</span></span>](#0.2__Toc253429267 "_Toc253429267")  
[<span data-ttu-id="e6592-135">숨겨진 필드 주위의 div 요소 숨기기</span><span class="sxs-lookup"><span data-stu-id="e6592-135">Hiding div Elements Around Hidden Fields</span></span>](#0.2__Toc253429268 "_Toc253429268")  
[<span data-ttu-id="e6592-136">템플릿 기반 컨트롤에 대 한 외부 테이블 렌더링</span><span class="sxs-lookup"><span data-stu-id="e6592-136">Rendering an Outer Table for Templated Controls</span></span>](#0.2__Toc253429269 "_Toc253429269")  
[<span data-ttu-id="e6592-137">ListView 컨트롤의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="e6592-137">ListView Control Enhancements</span></span>](#0.2__Toc253429270 "_Toc253429270")  
[<span data-ttu-id="e6592-138">CheckBoxList 및 RadioButtonList 제어 기능 향상</span><span class="sxs-lookup"><span data-stu-id="e6592-138">CheckBoxList and RadioButtonList Control Enhancements</span></span>](#0.2__Toc253429271 "_Toc253429271")  
[<span data-ttu-id="e6592-139">메뉴 컨트롤 개선</span><span class="sxs-lookup"><span data-stu-id="e6592-139">Menu Control Improvements</span></span>](#0.2__Toc253429272 "_Toc253429272")  
[<span data-ttu-id="e6592-140">Wizard 및 CreateUserWizard 컨트롤 56</span><span class="sxs-lookup"><span data-stu-id="e6592-140">Wizard and CreateUserWizard Controls 56</span></span>](#0.2__Toc253429273 "_Toc253429273")

<span data-ttu-id="e6592-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span><span class="sxs-lookup"><span data-stu-id="e6592-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span></span>  
[<span data-ttu-id="e6592-142">영역 지원</span><span class="sxs-lookup"><span data-stu-id="e6592-142">Areas Support</span></span>](#0.2__Toc253429275 "_Toc253429275")  
[<span data-ttu-id="e6592-143">데이터 주석 특성 유효성 검사 지원</span><span class="sxs-lookup"><span data-stu-id="e6592-143">Data-Annotation Attribute Validation Support</span></span>](#0.2__Toc253429276 "_Toc253429276")  
[<span data-ttu-id="e6592-144">템플릿 기반 도우미</span><span class="sxs-lookup"><span data-stu-id="e6592-144">Templated Helpers</span></span>](#0.2__Toc253429277 "_Toc253429277")

<span data-ttu-id="e6592-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span><span class="sxs-lookup"><span data-stu-id="e6592-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span></span>  
[<span data-ttu-id="e6592-146">기존 프로젝트에 대 한 Dynamic Data 사용</span><span class="sxs-lookup"><span data-stu-id="e6592-146">Enabling Dynamic Data for Existing Projects</span></span>](#0.2__Toc253429279 "_Toc253429279")  
[<span data-ttu-id="e6592-147">선언적 DynamicDataManager 컨트롤 구문</span><span class="sxs-lookup"><span data-stu-id="e6592-147">Declarative DynamicDataManager Control Syntax</span></span>](#0.2__Toc253429280 "_Toc253429280")  
[<span data-ttu-id="e6592-148">엔터티 템플릿</span><span class="sxs-lookup"><span data-stu-id="e6592-148">Entity Templates</span></span>](#0.2__Toc253429281 "_Toc253429281")  
[<span data-ttu-id="e6592-149">Url 및 전자 메일 주소에 대 한 새 필드 템플릿</span><span class="sxs-lookup"><span data-stu-id="e6592-149">New Field Templates for URLs and E-mail Addresses</span></span>](#0.2__Toc253429282 "_Toc253429282")  
[<span data-ttu-id="e6592-150">DynamicHyperLink 컨트롤을 사용 하 여 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="e6592-150">Creating Links with the DynamicHyperLink Control</span></span>](#0.2__Toc253429283 "_Toc253429283")  
[<span data-ttu-id="e6592-151">데이터 모델의 상속에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="e6592-151">Support for Inheritance in the Data Model</span></span>](#0.2__Toc253429284 "_Toc253429284")  
[<span data-ttu-id="e6592-152">다 대 다 관계에 대 한 지원 (Entity Framework에만 해당)</span><span class="sxs-lookup"><span data-stu-id="e6592-152">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>](#0.2__Toc253429285 "_Toc253429285")  
[<span data-ttu-id="e6592-153">표시 및 지원 열거를 제어 하기 위한 새 특성</span><span class="sxs-lookup"><span data-stu-id="e6592-153">New Attributes to Control Display and Support Enumerations</span></span>](#0.2__Toc253429286 "_Toc253429286")  
[<span data-ttu-id="e6592-154">향상 된 필터 지원</span><span class="sxs-lookup"><span data-stu-id="e6592-154">Enhanced Support for Filters</span></span>](#0.2__Toc253429287 "_Toc253429287")

<span data-ttu-id="e6592-155">**[Visual Studio 2010 웹 개발 개선 사항](#0.2__Toc253429288 "_Toc253429288")**</span><span class="sxs-lookup"><span data-stu-id="e6592-155">**[Visual Studio 2010 Web Development Improvements](#0.2__Toc253429288 "_Toc253429288")**</span></span>  
[<span data-ttu-id="e6592-156">향상 된 CSS 호환성</span><span class="sxs-lookup"><span data-stu-id="e6592-156">Improved CSS Compatibility</span></span>](#0.2__Toc253429289 "_Toc253429289")  
[<span data-ttu-id="e6592-157">HTML 및 JavaScript 코드 조각</span><span class="sxs-lookup"><span data-stu-id="e6592-157">HTML and JavaScript Snippets</span></span>](#0.2__Toc253429290 "_Toc253429290")  
[<span data-ttu-id="e6592-158">JavaScript IntelliSense의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="e6592-158">JavaScript IntelliSense Enhancements</span></span>](#0.2__Toc253429291 "_Toc253429291")

<span data-ttu-id="e6592-159">**[Visual Studio 2010을 사용 하 여 웹 응용 프로그램 배포](#0.2__Toc253429292 "_Toc253429292")**</span><span class="sxs-lookup"><span data-stu-id="e6592-159">**[Web Application Deployment with Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span></span>  
[<span data-ttu-id="e6592-160">웹 패키징</span><span class="sxs-lookup"><span data-stu-id="e6592-160">Web Packaging</span></span>](#0.2__Toc253429293 "_Toc253429293")  
[<span data-ttu-id="e6592-161">Web.config 변환</span><span class="sxs-lookup"><span data-stu-id="e6592-161">Web.config Transformation</span></span>](#0.2__Toc253429294 "_Toc253429294")  
[<span data-ttu-id="e6592-162">데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="e6592-162">Database Deployment</span></span>](#0.2__Toc253429295 "_Toc253429295")  
[<span data-ttu-id="e6592-163">한 번 클릭으로 웹 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="e6592-163">One-Click Publish for Web Applications</span></span>](#0.2__Toc253429296 "_Toc253429296")  
[<span data-ttu-id="e6592-164">리소스</span><span class="sxs-lookup"><span data-stu-id="e6592-164">Resources</span></span>](#0.2__Toc253429297 "_Toc253429297")

<span data-ttu-id="e6592-165">**[내용을](#0.2__Toc253429298 "_Toc253429298")**</span><span class="sxs-lookup"><span data-stu-id="e6592-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span></span>

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a><span data-ttu-id="e6592-166">핵심 서비스</span><span class="sxs-lookup"><span data-stu-id="e6592-166">Core Services</span></span>

<span data-ttu-id="e6592-167">ASP.NET 4에서는 출력 캐싱 및 세션 상태 저장소와 같은 핵심 ASP.NET 서비스를 개선 하는 여러 가지 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-167">ASP.NET 4 introduces a number of features that improve core ASP.NET services such as output caching and session-state storage.</span></span>

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a><span data-ttu-id="e6592-168">Web.config 파일 리팩터링</span><span class="sxs-lookup"><span data-stu-id="e6592-168">Web.config File Refactoring</span></span>

<span data-ttu-id="e6592-169">Ajax, 라우팅 및 IIS 7과의 통합과 같은 새로운 기능이 추가 되 면 웹 응용 프로그램에 대 한 구성이 포함 된 `Web.config` 파일이 .NET Framework 크게 증가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-169">The `Web.config` file that contains the configuration for a Web application has grown considerably over the past few releases of the .NET Framework as new features have been added, such as Ajax, routing, and integration with IIS 7.</span></span> <span data-ttu-id="e6592-170">그러면 Visual Studio와 같은 도구를 사용 하지 않고 새 웹 응용 프로그램을 구성 하거나 시작 하기가 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-170">This has made it harder to configure or start new Web applications without a tool like Visual Studio.</span></span> <span data-ttu-id="e6592-171">.NET Framework 4에서 주요 구성 요소는 `machine.config` 파일로 이동 되었으며 이제 응용 프로그램에서 이러한 설정을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-171">In .the NET Framework 4, the major configuration elements have been moved to the `machine.config` file, and applications now inherit these settings.</span></span> <span data-ttu-id="e6592-172">이를 통해 ASP.NET 4 응용 프로그램의 `Web.config` 파일이 비어 있거나 응용 프로그램에서 대상으로 하는 프레임 워크의 버전을 지정 하는 다음 줄만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-172">This allows the `Web.config` file in ASP.NET 4 applications either to be empty or to contain just the following lines, which specify for Visual Studio what version of the framework the application is targeting:</span></span>

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a><span data-ttu-id="e6592-173">확장 가능한 출력 캐싱</span><span class="sxs-lookup"><span data-stu-id="e6592-173">Extensible Output Caching</span></span>

<span data-ttu-id="e6592-174">ASP.NET 1.0이 출시 된 이후에는 출력 캐싱이 개발자가 생성 된 페이지, 컨트롤 및 HTTP 응답 출력을 메모리에 저장할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-174">Since the time that ASP.NET 1.0 was released, output caching has enabled developers to store the generated output of pages, controls, and HTTP responses in memory.</span></span> <span data-ttu-id="e6592-175">이후 웹 요청에서 ASP.NET는 처음부터 출력을 다시 생성 하는 대신 메모리에서 생성 된 출력을 검색 하 여 콘텐츠를 더 신속 하 게 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-175">On subsequent Web requests, ASP.NET can serve content more quickly by retrieving the generated output from memory instead of regenerating the output from scratch.</span></span> <span data-ttu-id="e6592-176">그러나이 방법에는 제한이 있습니다. 생성 된 콘텐츠는 항상 메모리에 저장 되어야 하 고 많은 트래픽이 발생 하는 서버에서는 출력 캐싱에 사용 되는 메모리가 웹 응용 프로그램의 다른 부분에서 메모리 수요와 경쟁할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-176">However, this approach has a limitation — generated content always has to be stored in memory, and on servers that are experiencing heavy traffic, the memory consumed by output caching can compete with memory demands from other portions of a Web application.</span></span>

<span data-ttu-id="e6592-177">ASP.NET 4는 하나 이상의 사용자 지정 출력 캐시 공급자를 구성할 수 있도록 하는 확장 지점을 출력 캐싱에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-177">ASP.NET 4 adds an extensibility point to output caching that enables you to configure one or more custom output-cache providers.</span></span> <span data-ttu-id="e6592-178">출력 캐시 공급자는 모든 저장소 메커니즘을 사용 하 여 HTML 콘텐츠를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-178">Output-cache providers can use any storage mechanism to persist HTML content.</span></span> <span data-ttu-id="e6592-179">이렇게 하면 로컬 또는 원격 디스크, 클라우드 저장소 및 분산 캐시 엔진을 포함할 수 있는 다양 한 지 속성 메커니즘에 대 한 사용자 지정 출력 캐시 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-179">This makes it possible to create custom output-cache providers for diverse persistence mechanisms, which can include local or remote disks, cloud storage, and distributed cache engines.</span></span>

<span data-ttu-id="e6592-180">사용자 지정 출력 캐시 공급자를 새 *system.object* 에서 파생 되는 클래스로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-180">You create a custom output-cache provider as a class that derives from the new *System.Web.Caching.OutputCacheProvider* type.</span></span> <span data-ttu-id="e6592-181">그런 다음, 다음 예제와 같이 *outputCache* 요소의 new *providers* 하위 섹션을 사용 하 여 `Web.config` 파일에서 공급자를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-181">You can then configure the provider in the `Web.config` file by using the new *providers* subsection of the *outputCache* element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample2.xml)]

<span data-ttu-id="e6592-182">기본적으로 ASP.NET 4에서 모든 HTTP 응답, 렌더링 된 페이지 및 컨트롤은 이전 예제에 표시 된 것 처럼 메모리 내 출력 캐시를 사용 합니다. 여기서 *defaultProvider* 특성은 AspNetInternalProvider로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-182">By default in ASP.NET 4, all HTTP responses, rendered pages, and controls use the in-memory output cache, as shown in the previous example, where the *defaultProvider* attribute is set to AspNetInternalProvider.</span></span> <span data-ttu-id="e6592-183">*DefaultProvider*에 대해 다른 공급자 이름을 지정 하 여 웹 응용 프로그램에 사용 되는 기본 출력 캐시 공급자를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-183">You can change the default output-cache provider used for a Web application by specifying a different provider name for *defaultProvider*.</span></span>

<span data-ttu-id="e6592-184">또한 각 제어 및 요청당 다른 출력 캐시 공급자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-184">In addition, you can select different output-cache providers per control and per request.</span></span> <span data-ttu-id="e6592-185">다른 웹 사용자 컨트롤에 대해 다른 출력 캐시 공급자를 선택 하는 가장 쉬운 방법은 다음 예제와 같이 컨트롤 지시문에 새 *providerName* 특성을 사용 하 여 선언적으로 수행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-185">The easiest way to choose a different output-cache provider for different Web user controls is to do so declaratively by using the new *providerName* attribute in a control directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample3.aspx)]

<span data-ttu-id="e6592-186">HTTP 요청에 다른 출력 캐시 공급자를 지정 하려면 약간 더 많은 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-186">Specifying a different output cache provider for an HTTP request requires a little more work.</span></span> <span data-ttu-id="e6592-187">공급자를 선언적으로 지정 하는 대신 `Global.asax` 파일에서 새 *Getouputcacheprovidername* 메서드를 재정의 하 여 특정 요청에 사용할 공급자를 프로그래밍 방식으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-187">Instead of declaratively specifying the provider, you override the new *GetOuputCacheProviderName* method in the `Global.asax` file to programmatically specify which provider to use for a specific request.</span></span> <span data-ttu-id="e6592-188">다음 예제에 이 작업을 수행하는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-188">The following example shows how to do this.</span></span>

[!code-csharp[Main](overview/samples/sample4.cs)]

<span data-ttu-id="e6592-189">ASP.NET 4에 출력 캐시 공급자 확장성이 추가 되어 이제 웹 사이트에 더 적극적이 고 지능적인 출력 캐싱 전략을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-189">With the addition of output-cache provider extensibility to ASP.NET 4, you can now pursue more aggressive and more intelligent output-caching strategies for your Web sites.</span></span> <span data-ttu-id="e6592-190">예를 들어, 디스크에서 낮은 트래픽을 가져오는 페이지를 캐시 하는 동안 사이트의 "상위 10 개" 페이지를 메모리에 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-190">For example, it is now possible to cache the "Top 10" pages of a site in memory, while caching pages that get lower traffic on disk.</span></span> <span data-ttu-id="e6592-191">또는 렌더링 된 페이지에 대 한 모든 vary 조합을 캐시할 수 있지만 메모리 소비가 프런트 엔드 웹 서버에서 오프 로드 되도록 분산 캐시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-191">Alternatively, you can cache every vary-by combination for a rendered page, but use a distributed cache so that the memory consumption is offloaded from front-end Web servers.</span></span>

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a><span data-ttu-id="e6592-192">웹 응용 프로그램 자동 시작</span><span class="sxs-lookup"><span data-stu-id="e6592-192">Auto-Start Web Applications</span></span>

<span data-ttu-id="e6592-193">일부 웹 응용 프로그램은 첫 번째 요청을 처리 하기 전에 많은 양의 데이터를 로드 하거나 비용이 많이 드는 초기화 처리를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-193">Some Web applications need to load large amounts of data or perform expensive initialization processing before serving the first request.</span></span> <span data-ttu-id="e6592-194">이전 버전의 ASP.NET에서는 이러한 상황에서 ASP.NET 응용 프로그램을 "절전 모드 해제" 하는 사용자 지정 방법을 고안 한 다음 `Global.asax` 파일에서 *응용 프로그램\_Load* 메서드를 실행 하는 동안 초기화 코드를 실행 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-194">In earlier versions of ASP.NET, for these situations you had to devise custom approaches to "wake up" an ASP.NET application and then run initialization code during the *Application\_Load* method in the `Global.asax` file.</span></span>

<span data-ttu-id="e6592-195">이 시나리오를 직접 해결 하는 *자동 시작* 이라는 새로운 확장성 기능은 ASP.NET 4가 Windows Server 2008 r 2에서 IIS 7.5에서 실행 될 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-195">A new scalability feature named *auto-start* that directly addresses this scenario is available when ASP.NET 4 runs on IIS 7.5 on Windows Server 2008 R2.</span></span> <span data-ttu-id="e6592-196">자동 시작 기능은 응용 프로그램 풀을 시작 하 고, ASP.NET 응용 프로그램을 초기화 하 고, HTTP 요청을 수락 하는 제어 된 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-196">The auto-start feature provides a controlled approach for starting up an application pool, initializing an ASP.NET application, and then accepting HTTP requests.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e6592-197">Iis 7.5에 대 한 IIS 응용 프로그램 준비 모듈</span><span class="sxs-lookup"><span data-stu-id="e6592-197">IIS Application Warm-Up Module for IIS 7.5</span></span>
> 
> <span data-ttu-id="e6592-198">IIS 팀은 IIS 7.5에 대 한 응용 프로그램 준비 모듈의 첫 번째 베타 테스트 버전을 출시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-198">The IIS team has released the first beta test version of the Application Warm-Up Module for IIS 7.5.</span></span> <span data-ttu-id="e6592-199">이렇게 하면 이전에 설명한 것 보다 훨씬 더 쉽게 응용 프로그램을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-199">This makes warming up your applications even easier than previously described.</span></span> <span data-ttu-id="e6592-200">사용자 지정 코드를 작성 하는 대신, 웹 응용 프로그램이 네트워크에서 요청을 수락 하기 전에 실행할 리소스의 Url을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-200">Instead of writing custom code, you specify the URLs of resources to execute before the Web application accepts requests from the network.</span></span> <span data-ttu-id="e6592-201">이 준비는 iis 서비스를 시작 하는 동안 (IIS 응용 프로그램 풀을 *AlwaysRunning*로 구성한 경우) 및 iis 작업자 프로세스가 재활용 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-201">This warm-up occurs during startup of the IIS service (if you configured the IIS application pool as *AlwaysRunning*) and when an IIS worker process recycles.</span></span> <span data-ttu-id="e6592-202">재활용 중에 이전 IIS 작업자 프로세스는 새로 생성 된 작업자 프로세스가 완전히 준비 때까지 요청을 계속 실행 하므로 응용 프로그램에서 unprimed 캐시로 인 한 중단 또는 기타 문제가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-202">During recycle, the old IIS worker process continues to execute requests until the newly spawned worker process is fully warmed up, so that applications experience no interruptions or other issues due to unprimed caches.</span></span> <span data-ttu-id="e6592-203">이 모듈은 버전 2.0부터 모든 버전의 ASP.NET에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-203">Note that this module works with any version of ASP.NET, starting with version 2.0.</span></span>
> 
> <span data-ttu-id="e6592-204">자세한 내용은 IIS.net 웹 사이트에서 [응용 프로그램 준비](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-204">For more information, see [Application Warm-Up](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) on the IIS.net Web site.</span></span> <span data-ttu-id="e6592-205">준비 기능을 사용 하는 방법을 보여 주는 연습은 IIS.net 웹 사이트의 [IIS 7.5 응용 프로그램 준비 모듈 시작](https://www.iis.net/learn/manage) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-205">For a walkthrough that illustrates how to use the warm-up feature, see [Getting Started with the IIS 7.5 Application Warm-Up Module](https://www.iis.net/learn/manage) on the IIS.net Web site.</span></span>

<span data-ttu-id="e6592-206">자동 시작 기능을 사용 하기 위해 IIS 관리자는 `applicationHost.config` 파일에서 다음 구성을 사용 하 여 IIS 7.5의 응용 프로그램 풀을 자동으로 시작 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-206">To use the auto-start feature, an IIS administrator sets an application pool in IIS 7.5 to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample5.xml)]

<span data-ttu-id="e6592-207">단일 응용 프로그램 풀에 여러 응용 프로그램이 포함 될 수 있으므로 `applicationHost.config` 파일에서 다음 구성을 사용 하 여 개별 응용 프로그램을 자동으로 시작할 수 있도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-207">Because a single application pool can contain multiple applications, you specify individual applications to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample6.xml)]

<span data-ttu-id="e6592-208">IIS 7.5 서버가 콜드 시작 되거나 개별 응용 프로그램 풀이 재활용 될 때 IIS 7.5은 `applicationHost.config` 파일의 정보를 사용 하 여 자동으로 시작 해야 하는 웹 응용 프로그램을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-208">When an IIS 7.5 server is cold-started or when an individual application pool is recycled, IIS 7.5 uses the information in the `applicationHost.config` file to determine which Web applications need to be automatically started.</span></span> <span data-ttu-id="e6592-209">자동 시작으로 표시 된 각 응용 프로그램에 대해 IIS 7.5는 응용 프로그램이 일시적으로 HTTP 요청을 수락 하지 않는 상태에서 응용 프로그램을 시작 하기 위해 ASP.NET 4로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-209">For each application that is marked for auto-start, IIS7.5 sends a request to ASP.NET 4 to start the application in a state during which the application temporarily does not accept HTTP requests.</span></span> <span data-ttu-id="e6592-210">이 상태 이면 ASP.NET는 *Serviceautostartprovider* 특성 (이전 예제에 표시 된 것 처럼)에 정의 된 형식을 인스턴스화하고 해당 공용 진입점을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-210">When it is in this state, ASP.NET instantiates the type defined by the *serviceAutoStartProvider* attribute (as shown in the previous example) and calls into its public entry point.</span></span>

<span data-ttu-id="e6592-211">다음 예제와 같이 *IProcessHostPreloadClient* 인터페이스를 구현 하 여 필요한 진입점을 사용 하 여 관리 되는 자동 시작 유형을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-211">You create a managed auto-start type with the necessary entry point by implementing the *IProcessHostPreloadClient* interface, as shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample7.cs)]

<span data-ttu-id="e6592-212">*미리 로드* 메서드에서 초기화 코드를 실행 하 고 메서드를 반환 하면 ASP.NET 응용 프로그램은 요청을 처리할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-212">After your initialization code runs in the *Preload* method and the method returns, the ASP.NET application is ready to process requests.</span></span>

<span data-ttu-id="e6592-213">IIS .5와 ASP.NET 4를 자동으로 시작 하는 것을 추가 하 여, 이제는 첫 번째 HTTP 요청을 처리 하기 전에 비용이 많이 드는 응용 프로그램 초기화를 수행 하기 위한 잘 정의 된 접근 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-213">With the addition of auto-start to IIS .5 and ASP.NET 4, you now have a well-defined approach for performing expensive application initialization prior to processing the first HTTP request.</span></span> <span data-ttu-id="e6592-214">예를 들어 새 자동 시작 기능을 사용 하 여 응용 프로그램을 초기화 한 다음 응용 프로그램이 초기화 되었으며 HTTP 트래픽을 받아들일 준비가 되었음을 부하 분산 장치에 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-214">For example, you can use the new auto-start feature to initialize an application and then signal a load-balancer that the application was initialized and ready to accept HTTP traffic.</span></span>

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a><span data-ttu-id="e6592-215">페이지를 영구적으로 리디렉션</span><span class="sxs-lookup"><span data-stu-id="e6592-215">Permanently Redirecting a Page</span></span>

<span data-ttu-id="e6592-216">웹 응용 프로그램에서 시간이 지남에 따라 페이지 및 기타 콘텐츠를 이동 하는 것이 일반적입니다 .이 경우 검색 엔진에서 오래 된 링크가 누적 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-216">It is common practice in Web applications to move pages and other content around over time, which can lead to an accumulation of stale links in search engines.</span></span> <span data-ttu-id="e6592-217">ASP.NET에서 개발자는 일반적으로 Response 메서드를 사용 하 여 새 URL로 요청을 전달 함으로써 이전 Url에 대 한 요청을 처리 했습니다 *.*</span><span class="sxs-lookup"><span data-stu-id="e6592-217">In ASP.NET, developers have traditionally handled requests to old URLs by using by using the *Response.Redirect* method to forward a request to the new URL.</span></span> <span data-ttu-id="e6592-218">그러나 *리디렉션* 메서드는 Http 302 발견 (임시 리디렉션) 응답을 실행 하 여 사용자가 이전 url에 액세스 하려고 할 때 추가 http 왕복을 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-218">However, the *Redirect* method issues an HTTP 302 Found (temporary redirect) response, which results in an extra HTTP round trip when users attempt to access the old URLs.</span></span>

<span data-ttu-id="e6592-219">ASP.NET 4를 사용 하면 다음 예제와 같이 HTTP 301 이동한 영구적 응답을 쉽게 실행할 수 있도록 하는 새 *Redirectpermanent* 도우미 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-219">ASP.NET 4 adds a new *RedirectPermanent* helper method that makes it easy to issue HTTP 301 Moved Permanently responses, as in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample8.cs)]

<span data-ttu-id="e6592-220">영구 리디렉션을 인식 하는 검색 엔진 및 기타 사용자 에이전트는 콘텐츠와 연결 된 새 URL을 저장 하 여 임시 리디렉션의 브라우저에서 불필요 한 왕복을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-220">Search engines and other user agents that recognize permanent redirects will store the new URL that is associated with the content, which eliminates the unnecessary round trip made by the browser for temporary redirects.</span></span>

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a><span data-ttu-id="e6592-221">세션 상태 축소</span><span class="sxs-lookup"><span data-stu-id="e6592-221">Shrinking Session State</span></span>

<span data-ttu-id="e6592-222">ASP.NET은 웹 팜 전체에 세션 상태를 저장 하기 위한 두 가지 기본 옵션을 제공 합니다 .이는 out-of-process 세션 상태 서버를 호출 하는 세션 상태 공급자와 Microsoft SQL Server 데이터베이스에 데이터를 저장 하는 세션 상태 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-222">ASP.NET provides two default options for storing session state across a Web farm: a session-state provider that invokes an out-of-process session-state server, and a session-state provider that stores data in a Microsoft SQL Server database.</span></span> <span data-ttu-id="e6592-223">두 옵션 모두 웹 응용 프로그램의 작업자 프로세스 외부에 상태 정보를 저장 하기 때문에 세션 상태는 원격 저장소로 보내기 전에 serialize 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-223">Because both options involve storing state information outside a Web application's worker process, session state has to be serialized before it is sent to remote storage.</span></span> <span data-ttu-id="e6592-224">개발자가 세션 상태를 저장 하는 정보의 양에 따라 serialize 된 데이터의 크기가 상당히 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-224">Depending on how much information a developer saves in session state, the size of the serialized data can grow quite large.</span></span>

<span data-ttu-id="e6592-225">ASP.NET 4에서는 두 종류의 out-of-process 세션 상태 공급자에 대 한 새로운 압축 옵션을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-225">ASP.NET 4 introduces a new compression option for both kinds of out-of-process session-state providers.</span></span> <span data-ttu-id="e6592-226">다음 예제에 표시 된 *compressionEnabled* 구성 옵션을 *true*로 설정 하면 ASP.NET는 *GZipStream* 클래스를 사용 .NET Framework 하 여 직렬화 된 세션 상태를 압축 (및 압축 해제) 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-226">When the *compressionEnabled* configuration option shown in the following example is set to *true*, ASP.NET will compress (and decompress) serialized session state by using the .NET Framework *System.IO.Compression.GZipStream* class.</span></span>

[!code-xml[Main](overview/samples/sample9.xml)]

<span data-ttu-id="e6592-227">`Web.config` 파일에 새 특성을 간단히 추가 하면 웹 서버에서 예비 CPU 사이클이 있는 응용 프로그램은 serialize 된 세션 상태 데이터의 크기를 크게 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-227">With the simple addition of the new attribute to the `Web.config` file, applications with spare CPU cycles on Web servers can realize substantial reductions in the size of serialized session-state data.</span></span>

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a><span data-ttu-id="e6592-228">허용 되는 Url 범위 확장</span><span class="sxs-lookup"><span data-stu-id="e6592-228">Expanding the Range of Allowable URLs</span></span>

<span data-ttu-id="e6592-229">ASP.NET 4에서는 응용 프로그램 Url 크기를 확장 하는 새로운 옵션을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-229">ASP.NET 4 introduces new options for expanding the size of application URLs.</span></span> <span data-ttu-id="e6592-230">이전 버전의 ASP.NET 제한 된 URL 경로 길이는 NTFS 파일 경로 제한을 기반으로 260 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-230">Previous versions of ASP.NET constrained URL path lengths to 260 characters, based on the NTFS file-path limit.</span></span> <span data-ttu-id="e6592-231">ASP.NET 4에서는 두 개의 새로운 *httpRuntime* 구성 특성을 사용 하 여 응용 프로그램에 맞게이 제한을 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-231">In ASP.NET 4, you have the option to increase (or decrease) this limit as appropriate for your applications, using two new *httpRuntime* configuration attributes.</span></span> <span data-ttu-id="e6592-232">다음 예에서는 이러한 새 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-232">The following example shows these new attributes.</span></span>

[!code-xml[Main](overview/samples/sample10.xml)]

<span data-ttu-id="e6592-233">더 길거나 짧은 경로 (프로토콜, 서버 이름 및 쿼리 문자열을 포함 하지 않는 URL 부분)를 허용 하려면 *[Maxurllength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 특성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-233">To allow longer or shorter paths (the portion of the URL that does not include protocol, server name, and query string), modify the *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* attribute.</span></span> <span data-ttu-id="e6592-234">더 길거나 짧은 쿼리 문자열을 허용 하려면 *[Maxquerystringlength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 특성의 값을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-234">To allow longer or shorter query strings, modify the value of the *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* attribute.</span></span>

<span data-ttu-id="e6592-235">ASP.NET 4를 사용 하 여 URL 문자 검사에 사용 되는 문자를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-235">ASP.NET 4 also enables you to configure the characters that are used by the URL character check.</span></span> <span data-ttu-id="e6592-236">ASP.NET에서 URL의 경로 부분에 잘못 된 문자를 찾으면 요청을 거부 하 고 HTTP 400 오류를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-236">When ASP.NET finds an invalid character in the path portion of a URL, it rejects the request and issues an HTTP 400 error.</span></span> <span data-ttu-id="e6592-237">이전 버전의 ASP.NET에서 URL 문자 검사는 고정 문자 집합으로 제한 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-237">In previous versions of ASP.NET, the URL character checks were limited to a fixed set of characters.</span></span> <span data-ttu-id="e6592-238">ASP.NET 4에서 다음 예제와 같이 *httpRuntime* 구성 요소의 새 *requestpathinvalidcharacters* 특성을 사용 하 여 유효한 문자 집합을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-238">In ASP.NET 4, you can customize the set of valid characters using the new *requestPathInvalidCharacters* attribute of the *httpRuntime* configuration element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample11.xml)]

<span data-ttu-id="e6592-239">기본적으로 *Requestpathinvalidcharacters* 특성은 8 문자를 유효 하지 않은 것으로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-239">By default, the *requestPathInvalidCharacters* attribute defines eight characters as invalid.</span></span> <span data-ttu-id="e6592-240">(기본적으로 *Requestpathinvalidcharacters* 에 할당 된 문자열에서 `Web.config` 파일이 XML 파일 이므로 보다 작음 (&lt;), 보다 큼 (&gt;) 및 앰퍼샌드 (&amp;) 문자가 인코딩됩니다. 필요에 따라 잘못 된 문자 집합을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-240">(In the string that is assigned to *requestPathInvalidCharacters* by default, the less than (&lt;), greater than (&gt;), and ampersand (&amp;) characters are encoded, because the `Web.config` file is an XML file.) You can customize the set of invalid characters as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="e6592-241">참고 ASP.NET 4는 IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt))의 RFC 2396에 정의 된 잘못 된 URL 문자 이기 때문에 ASCII 범위 0X00에서 0x1F 문자를 포함 하는 url 경로를 항상 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-241">Note ASP.NET 4 always rejects URL paths that contain characters in the ASCII range of 0x00 to 0x1F, because those are invalid URL characters as defined in RFC 2396 of the IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)).</span></span> <span data-ttu-id="e6592-242">IIS 6 이상을 실행 하는 Windows Server 버전에서 http.sys 프로토콜 장치 드라이버는 이러한 문자를 포함 하는 Url을 자동으로 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-242">On versions of Windows Server that run IIS 6 or higher, the http.sys protocol device driver automatically rejects URLs with these characters.</span></span>

<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a><span data-ttu-id="e6592-243">확장 가능한 요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e6592-243">Extensible Request Validation</span></span>

<span data-ttu-id="e6592-244">ASP.NET 요청 유효성 검사는 들어오는 HTTP 요청 데이터에서 XSS (교차 사이트 스크립팅) 공격에 일반적으로 사용 되는 문자열을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-244">ASP.NET request validation searches incoming HTTP request data for strings that are commonly used in cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="e6592-245">잠재적 XSS 문자열이 발견 되 면 요청 유효성 검사에서 주의 대상 문자열에 플래그를 제공 하 고 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-245">If potential XSS strings are found, request validation flags the suspect string and returns an error.</span></span> <span data-ttu-id="e6592-246">기본 제공 요청 유효성 검사에서는 XSS 공격에 사용 되는 가장 일반적인 문자열을 찾은 경우에만 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-246">The built-in request validation returns an error only when it finds the most common strings used in XSS attacks.</span></span> <span data-ttu-id="e6592-247">이전에 XSS 유효성 검사를 더 적극적으로 수행 하려고 하면 가양성이 너무 많이 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-247">Previous attempts to make the XSS validation more aggressive resulted in too many false positives.</span></span> <span data-ttu-id="e6592-248">그러나 고객은 더 적극적인 요청 유효성 검사를 원할 수도 있고, 특정 페이지 또는 특정 유형의 요청에 대해 의도적으로 XSS 검사를 완화 하려고 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-248">However, customers might want request validation that is more aggressive, or conversely might want to intentionally relax XSS checks for specific pages or for specific types of requests.</span></span>

<span data-ttu-id="e6592-249">ASP.NET 4에서는 사용자 지정 요청-유효성 검사 논리를 사용할 수 있도록 요청 유효성 검사 기능이 확장 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-249">In ASP.NET 4, the request validation feature has been made extensible so that you can use custom request-validation logic.</span></span> <span data-ttu-id="e6592-250">요청 유효성 검사를 확장 *하려면 새 httpRuntime* 형식에서 파생 되는 클래스를 만들고 사용자 지정 형식을 사용 하도록 응용 프로그램 (`Web.config` 파일의 섹션에 있는)을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-250">To extend request validation, you create a class that derives from the new *System.Web.Util.RequestValidator* type, and you configure the application (in the *httpRuntime* section of the `Web.config` file) to use the custom type.</span></span> <span data-ttu-id="e6592-251">다음 예제에서는 사용자 지정 요청-유효성 검사 클래스를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-251">The following example shows how to configure a custom request-validation class:</span></span>

[!code-xml[Main](overview/samples/sample12.xml)]

<span data-ttu-id="e6592-252">새 *requestValidationType* 특성에는 사용자 지정 요청 유효성 검사를 제공 하는 클래스를 지정 하는 표준 .NET Framework 형식 식별자 문자열이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-252">The new *requestValidationType* attribute requires a standard .NET Framework type identifier string that specifies the class that provides custom request validation.</span></span> <span data-ttu-id="e6592-253">각 요청에 대해 ASP.NET는 들어오는 HTTP 요청 데이터의 각 부분을 처리 하기 위해 사용자 지정 형식을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-253">For each request, ASP.NET invokes the custom type to process each piece of incoming HTTP request data.</span></span> <span data-ttu-id="e6592-254">들어오는 URL, 모든 HTTP 헤더 (쿠키와 사용자 지정 헤더 모두) 및 엔터티 본문은 모두 다음 예제에 표시 된 것과 같이 사용자 지정 요청 유효성 검사 클래스에서 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-254">The incoming URL, all the HTTP headers (both cookies and custom headers), and the entity body are all available for inspection by a custom request validation class like that shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample13.cs)]

<span data-ttu-id="e6592-255">들어오는 HTTP 데이터를 검사 하지 않으려는 경우에는 base를 호출 하 여 ASP.NET 기본 요청 유효성 검사를 실행할 수 있도록 요청 유효성 검사 클래스가 대체 될 수 있습니다 *. Is유효한 Requeststring입니다.*</span><span class="sxs-lookup"><span data-stu-id="e6592-255">For cases where you do not want to inspect a piece of incoming HTTP data, the request-validation class can fall back to let the ASP.NET default request validation run by simply calling *base.IsValidRequestString.*</span></span>

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a><span data-ttu-id="e6592-256">개체 캐싱 및 개체 캐싱 확장성</span><span class="sxs-lookup"><span data-stu-id="e6592-256">Object Caching and Object Caching Extensibility</span></span>

<span data-ttu-id="e6592-257">첫 번째 릴리스 이후 ASP.NET은 강력한 메모리 내 개체 캐시 (*system.web*)를 포함 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-257">Since its first release, ASP.NET has included a powerful in-memory object cache (*System.Web.Caching.Cache*).</span></span> <span data-ttu-id="e6592-258">캐시 구현은 웹이 아닌 응용 프로그램에서 사용 되는 것으로 널리 사용 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-258">The cache implementation has been so popular that it has been used in non-Web applications.</span></span> <span data-ttu-id="e6592-259">그러나 Windows Forms 또는 WPF 응용 프로그램에서 ASP.NET 개체 캐시를 사용할 수 있도록 `System.Web.dll`에 대 한 참조를 포함 하는 것은 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-259">However, it is awkward for a Windows Forms or WPF application to include a reference to `System.Web.dll` just to be able to use the ASP.NET object cache.</span></span>

<span data-ttu-id="e6592-260">모든 응용 프로그램에서 캐싱을 사용할 수 있도록 하기 위해 .NET Framework 4에서는 새 어셈블리, 새 네임 스페이스, 몇 가지 기본 형식 및 구체적인 캐싱 구현을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-260">To make caching available for all applications, the .NET Framework 4 introduces a new assembly, a new namespace, some base types, and a concrete caching implementation.</span></span> <span data-ttu-id="e6592-261">새 `System.Runtime.Caching.dll` 어셈블리에는 *system.object* 네임 스페이스의 새로운 캐싱 API가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-261">The new `System.Runtime.Caching.dll` assembly contains a new caching API in the *System.Runtime.Caching* namespace.</span></span> <span data-ttu-id="e6592-262">네임 스페이스에는 클래스의 두 가지 핵심 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-262">The namespace contains two core sets of classes:</span></span>

- <span data-ttu-id="e6592-263">모든 형식의 사용자 지정 캐시 구현을 빌드하기 위한 토대를 제공 하는 추상 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-263">Abstract types that provide the foundation for building any type of custom cache implementation.</span></span>
- <span data-ttu-id="e6592-264">구체적인 메모리 내 개체 캐시 구현 ( *system.web. memorycache* 클래스)입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-264">A concrete in-memory object cache implementation (the *System.Runtime.Caching.MemoryCache* class).</span></span>

<span data-ttu-id="e6592-265">새 *memorycache* 클래스는 ASP.NET cache와 긴밀 하 게 모델링 되며 ASP.NET를 사용 하 여 내부 캐시 엔진 논리의 대부분을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-265">The new *MemoryCache* class is modeled closely on the ASP.NET cache, and it shares much of the internal cache engine logic with ASP.NET.</span></span> <span data-ttu-id="e6592-266">ASP.NET *Cache* 개체를 사용 하는 경우에는 Cache 개체를 사용 하 여 사용자 지정 캐시의 공용 캐싱 *api가 업데이트* 되었지만 새 api에서 친숙 한 개념을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-266">Although the public caching APIs in *System.Runtime.Caching* have been updated to support development of custom caches, if you have used the ASP.NET *Cache* object, you will find familiar concepts in the new APIs.</span></span>

<span data-ttu-id="e6592-267">새 *Memorycache* 클래스와 지원 기본 api에 대 한 자세한 내용은 전체 문서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-267">An in-depth discussion of the new *MemoryCache* class and supporting base APIs would require an entire document.</span></span> <span data-ttu-id="e6592-268">그러나 다음 예제에서는 새 캐시 API의 작동 방식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-268">However, the following example gives you an idea of how the new cache API works.</span></span> <span data-ttu-id="e6592-269">이 예제는 `System.Web.dll`에 대 한 종속성 없이 Windows Forms 응용 프로그램용으로 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-269">The example was written for a Windows Forms application, without any dependency on `System.Web.dll`.</span></span>

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a><span data-ttu-id="e6592-270">확장 가능한 HTML, URL 및 HTTP 헤더 인코딩</span><span class="sxs-lookup"><span data-stu-id="e6592-270">Extensible HTML, URL, and HTTP Header Encoding</span></span>

<span data-ttu-id="e6592-271">ASP.NET 4에서 다음과 같은 일반적인 텍스트 인코딩 작업에 대 한 사용자 지정 인코딩 루틴을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-271">In ASP.NET 4, you can create custom encoding routines for the following common text-encoding tasks:</span></span>

- <span data-ttu-id="e6592-272">HTML 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-272">HTML encoding.</span></span>
- <span data-ttu-id="e6592-273">URL 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-273">URL encoding.</span></span>
- <span data-ttu-id="e6592-274">HTML 특성 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-274">HTML attribute encoding.</span></span>
- <span data-ttu-id="e6592-275">아웃 바운드 HTTP 헤더를 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-275">Encoding outbound HTTP headers.</span></span>

<span data-ttu-id="e6592-276">다음 예제와 *같이 새 ASP.NET* 형식에서 파생 시킨 다음, `Web.config` 파일의 *httpRuntime* 섹션에서 사용자 지정 형식을 사용 하도록 구성 하 여 사용자 지정 인코더를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-276">You can create a custom encoder by deriving from the new *System.Web.Util.HttpEncoder* type and then configuring ASP.NET to use the custom type in the *httpRuntime* section of the `Web.config` file, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample15.xml)]

<span data-ttu-id="e6592-277">사용자 지정 인코더가 구성 된 후에는 ASP.NET 또는 *HttpServerUtility* 클래스의 공용 인코딩 메서드가 호출 될 때마다 사용자 지정 인코딩 구현을 자동으로 호출 *합니다.*</span><span class="sxs-lookup"><span data-stu-id="e6592-277">After a custom encoder has been configured, ASP.NET automatically calls the custom encoding implementation whenever public encoding methods of the *System.Web.HttpUtility* or *System.Web.HttpServerUtility* classes are called.</span></span> <span data-ttu-id="e6592-278">이렇게 하면 웹 개발 팀의 한 부분에서 적극적인 문자 인코딩을 구현 하는 사용자 지정 인코더를 만들 수 있으며, 나머지 웹 개발 팀은 계속 해 서 공용 ASP.NET encoding Api를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-278">This lets one part of a Web development team create a custom encoder that implements aggressive character encoding, while the rest of the Web development team continues to use the public ASP.NET encoding APIs.</span></span> <span data-ttu-id="e6592-279">*HttpRuntime* 요소에서 사용자 지정 인코더를 중앙에서 구성 하 여 공용 ASP.NET encoding api의 모든 텍스트 인코딩 호출이 사용자 지정 인코더를 통해 라우팅되도록 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-279">By centrally configuring a custom encoder in the *httpRuntime* element, you are guaranteed that all text-encoding calls from the public ASP.NET encoding APIs are routed through the custom encoder.</span></span>

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a><span data-ttu-id="e6592-280">단일 작업자 프로세스의 개별 응용 프로그램에 대 한 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="e6592-280">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>

<span data-ttu-id="e6592-281">단일 서버에서 호스팅될 수 있는 웹 사이트 수를 늘리기 위해 많은 호스팅 서비스 공급자는 단일 작업자 프로세스에서 여러 ASP.NET 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-281">In order to increase the number of Web sites that can be hosted on a single server, many hosters run multiple ASP.NET applications in a single worker process.</span></span> <span data-ttu-id="e6592-282">그러나 여러 응용 프로그램에서 단일 공유 작업자 프로세스를 사용 하는 경우 서버 관리자가 문제가 발생 한 개별 응용 프로그램을 식별 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-282">However, if multiple applications use a single shared worker process, it is difficult for server administrators to identify an individual application that is experiencing problems.</span></span>

<span data-ttu-id="e6592-283">ASP.NET 4는 CLR에서 도입 된 새로운 리소스 모니터링 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-283">ASP.NET 4 leverages new resource-monitoring functionality introduced by the CLR.</span></span> <span data-ttu-id="e6592-284">이 기능을 사용 하도록 설정 하려면 다음 XML 구성 코드 조각을 `aspnet.config` 구성 파일에 추가 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-284">To enable this functionality, you can add the following XML configuration snippet to the `aspnet.config` configuration file.</span></span>

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> <span data-ttu-id="e6592-285">`aspnet.config` 파일은 .NET Framework가 설치 된 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-285">Note The `aspnet.config` file is in the directory where the .NET Framework is installed.</span></span> <span data-ttu-id="e6592-286">`Web.config` 파일이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-286">It is not the `Web.config` file.</span></span>

<span data-ttu-id="e6592-287">*AppDomainResourceMonitoring* 기능을 사용 하는 경우 "ASP.NET 응용 프로그램" 성능 범주 *% 관리 되는 프로세서 시간* 및 *사용 된 관리*되는 메모리에서 두 개의 새로운 성능 카운터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-287">When the *appDomainResourceMonitoring* feature has been enabled, two new performance counters are available in the "ASP.NET Applications" performance category: *% Managed Processor Time* and *Managed Memory Used*.</span></span> <span data-ttu-id="e6592-288">이러한 성능 카운터는 모두 새로운 CLR 응용 프로그램 도메인 리소스 관리 기능을 사용 하 여 개별 ASP.NET 응용 프로그램의 예상 CPU 시간 및 관리 되는 메모리 사용률을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-288">Both of these performance counters use the new CLR application-domain resource management feature to track estimated CPU time and managed memory utilization of individual ASP.NET applications.</span></span> <span data-ttu-id="e6592-289">결과적으로, 관리자는 ASP.NET 4를 사용 하 여 단일 작업자 프로세스에서 실행 되는 개별 응용 프로그램의 리소스 소비에 대 한 보다 세분화 된 보기를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-289">As a result, with ASP.NET 4, administrators now have a more granular view into the resource consumption of individual applications running in a single worker process.</span></span>

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a><span data-ttu-id="e6592-290">멀티 타기팅</span><span class="sxs-lookup"><span data-stu-id="e6592-290">Multi-Targeting</span></span>

<span data-ttu-id="e6592-291">.NET Framework의 특정 버전을 대상으로 하는 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-291">You can create an application that targets a specific version of the .NET Framework.</span></span> <span data-ttu-id="e6592-292">ASP.NET 4에서는 `Web.config` 파일의 *컴파일* 요소에 있는 새 특성을 사용 하 여 .NET Framework 4 이상을 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-292">In ASP.NET 4, a new attribute in the *compilation* element of the `Web.config` file lets you target the .NET Framework 4 and later.</span></span> <span data-ttu-id="e6592-293">.NET Framework 4를 명시적으로 대상으로 지정 하 고 `Web.config` 파일에 *system.object*와 같은 선택적 요소를 포함 하는 경우 이러한 요소는 .NET Framework 4에 대해 정확 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-293">If you explicitly target the .NET Framework 4, and if you include optional elements in the `Web.config` file such as the entries for *system.codedom*, these elements must be correct for the .NET Framework 4.</span></span> <span data-ttu-id="e6592-294">.NET Framework 4를 명시적으로 대상으로 하지 않는 경우 대상 프레임 워크는 `Web.config` 파일에 항목이 부족 한 것으로 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-294">(If you do not explicitly target the .NET Framework 4, the target framework is inferred from the lack of an entry in the `Web.config` file.)</span></span>

<span data-ttu-id="e6592-295">다음 예제에서는 `Web.config` 파일의 *컴파일* 요소에 *targetframework* 특성을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-295">The following example shows the use of the *targetFramework* attribute in the *compilation* element of the `Web.config` file.</span></span>

[!code-xml[Main](overview/samples/sample17.xml)]

<span data-ttu-id="e6592-296">특정 버전의 .NET Framework를 대상으로 지정 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-296">Note the following about targeting a specific version of the .NET Framework:</span></span>

- <span data-ttu-id="e6592-297">.NET Framework 4 응용 프로그램 풀에서, `Web.config` 파일이 *Targetframework* 특성을 포함 하지 않거나 `Web.config` 파일이 없는 경우 ASP.NET 빌드 시스템은 .NET Framework 4를 대상으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-297">In a .NET Framework 4 application pool, the ASP.NET build system assumes the .NET Framework 4 as a target if the `Web.config` file does not include the *targetFramework* attribute or if the `Web.config` file is missing.</span></span> <span data-ttu-id="e6592-298">.NET Framework 4에서 실행 되도록 응용 프로그램에 대 한 코딩 변경 작업을 수행 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-298">(You might have to make coding changes to your application to make it run under the .NET Framework 4.)</span></span>
- <span data-ttu-id="e6592-299">*Targetframework* 특성을 포함 하 고, `Web.config` 파일에 *system.object* 요소가 정의 되어 있는 경우이 파일은 .NET Framework 4에 대 한 올바른 항목을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-299">If you do include the *targetFramework* attribute, and if the *system.codeDom* element is defined in the `Web.config` file, this file must contain the correct entries for the .NET Framework 4.</span></span>
- <span data-ttu-id="e6592-300">빌드 환경에서와 같이 *aspnet\_컴파일러* 명령을 사용 하 여 응용 프로그램을 미리 컴파일하는 경우 대상 프레임 워크에 대 한 올바른 버전의 *aspnet\_컴파일러* 명령을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-300">If you are using the *aspnet\_compiler* command to precompile your application (such as in a build environment), you must use the correct version of the *aspnet\_compiler* command for the target framework.</span></span> <span data-ttu-id="e6592-301">.NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727)과 함께 제공 된 컴파일러를 사용 하 여 .NET Framework 3.5 이전 버전을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-301">Use the compiler that shipped with the .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) to compile for the .NET Framework 3.5 and earlier versions.</span></span> <span data-ttu-id="e6592-302">.NET Framework 4와 함께 제공 되는 컴파일러를 사용 하 여 해당 프레임 워크를 사용 하거나 이후 버전을 사용 하 여 만든 응용 프로그램을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-302">Use the compiler that ships with the .NET Framework 4 to compile applications created using that framework or using later versions.</span></span>
- <span data-ttu-id="e6592-303">런타임에 컴파일러는 컴퓨터에 설치 된 최신 프레임 워크 어셈블리 (및 따라서 GAC)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-303">At run time, the compiler uses the latest framework assemblies that are installed on the computer (and therefore in the GAC).</span></span> <span data-ttu-id="e6592-304">가상 버전 4.1가 설치 된 경우와 같이 나중에 프레임 워크에 업데이트를 수행 하는 경우 *targetframework* 특성이 더 낮은 버전 (예: 4.0)을 대상으로 하더라도 최신 버전의 프레임 워크에서 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-304">If an update is made later to the framework (for example, a hypothetical version 4.1 is installed), you will be able to use features in the newer version of the framework even though the *targetFramework* attribute targets a lower version (such as 4.0).</span></span> <span data-ttu-id="e6592-305">그러나 Visual Studio 2010의 디자인 타임에 또는 *aspnet\_컴파일러* 명령을 사용 하는 경우 프레임 워크의 최신 기능을 사용 하면 컴파일러 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-305">(However, at design time in Visual Studio 2010 or when you use the *aspnet\_compiler* command, using newer features of the framework will cause compiler errors).</span></span>

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a><span data-ttu-id="e6592-306">Ajax</span><span class="sxs-lookup"><span data-stu-id="e6592-306">Ajax</span></span>

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a><span data-ttu-id="e6592-307">Web Forms 및 MVC에 포함 된 jQuery</span><span class="sxs-lookup"><span data-stu-id="e6592-307">jQuery Included with Web Forms and MVC</span></span>

<span data-ttu-id="e6592-308">Web Forms 및 MVC에 대 한 Visual Studio 템플릿은 오픈 소스 jQuery 라이브러리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-308">The Visual Studio templates for both Web Forms and MVC include the open-source jQuery library.</span></span> <span data-ttu-id="e6592-309">새 웹 사이트 또는 프로젝트를 만들 때 다음 세 개의 파일이 포함 된 Scripts 폴더가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-309">When you create a new website or project, a Scripts folder containing the following 3 files is created:</span></span>

- <span data-ttu-id="e6592-310">Jquery-1.10.2.min.js 1.4.1 – 사용자가 읽을 수 있는 jQuery 라이브러리의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-310">jQuery-1.4.1.js – The human-readable, unminified version of the jQuery library.</span></span>
- <span data-ttu-id="e6592-311">Jquery-1.10.2.min.js 14.1 – jQuery 라이브러리의 최소 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-311">jQuery-14.1.min.js – The minified version of the jQuery library.</span></span>
- <span data-ttu-id="e6592-312">Jquery-1.10.2.min.js 1.4.1-vsdoc – jQuery 라이브러리에 대 한 Intellisense 설명서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-312">jQuery-1.4.1-vsdoc.js – The Intellisense documentation file for the jQuery library.</span></span>

<span data-ttu-id="e6592-313">응용 프로그램을 개발 하는 동안 jQuery 버전의 jQuery를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-313">Include the unminified version of jQuery while developing an application.</span></span> <span data-ttu-id="e6592-314">프로덕션 응용 프로그램에 대 한 jQuery 버전을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-314">Include the minified version of jQuery for production applications.</span></span>

<span data-ttu-id="e6592-315">예를 들어 다음 Web Forms 페이지에서는 jQuery를 사용 하 여 포커스가 있을 때 ASP.NET TextBox 컨트롤의 배경색을 노란색으로 변경 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-315">For example, the following Web Forms page illustrates how you can use jQuery to change the background color of ASP.NET TextBox controls to yellow when they have focus.</span></span>

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a><span data-ttu-id="e6592-316">지원 Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="e6592-316">Content Delivery Network Support</span></span>

<span data-ttu-id="e6592-317">Microsoft Ajax Content Delivery Network (CDN)를 사용 하면 웹 응용 프로그램에 ASP.NET Ajax 및 jQuery 스크립트를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-317">The Microsoft Ajax Content Delivery Network (CDN) enables you to easily add ASP.NET Ajax and jQuery scripts to your Web applications.</span></span> <span data-ttu-id="e6592-318">예를 들어 페이지에 다음과 같이 Ajax.microsoft.com를 가리키는 `<script>` 태그를 추가 하 여 jQuery 라이브러리를 사용 하 여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-318">For example, you can start using the jQuery library simply by adding a `<script>` tag to your page that points to Ajax.microsoft.com like this:</span></span>

[!code-html[Main](overview/samples/sample19.html)]

<span data-ttu-id="e6592-319">Microsoft Ajax CDN을 사용하여 Ajax 응용 프로그램의 성능을 크게 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-319">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="e6592-320">Microsoft Ajax CDN의 콘텐츠는 전 세계에 있는 서버에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-320">The contents of the Microsoft Ajax CDN are cached on servers located around the world.</span></span> <span data-ttu-id="e6592-321">또한 Microsoft Ajax CDN을 통해 브라우저에서 다른 도메인에 있는 웹 사이트에 대한 캐시된 JavaScript 파일을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-321">In addition, the Microsoft Ajax CDN enables browsers to reuse cached JavaScript files for Web sites that are located in different domains.</span></span>

<span data-ttu-id="e6592-322">Microsoft Ajax Content Delivery Network는 SSL(Secure Sockets Layer)를 사용 하 여 웹 페이지를 제공 해야 하는 경우 SSL (HTTPS)을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-322">The Microsoft Ajax Content Delivery Network supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="e6592-323">CDN을 사용할 수 없는 경우 대체 (fallback)를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-323">Implement a fallback when the CDN is unavailable.</span></span> <span data-ttu-id="e6592-324">대체 (fallback)를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-324">Test the fallback.</span></span>

<span data-ttu-id="e6592-325">Microsoft Ajax CDN에 대 한 자세한 내용을 보려면 다음 웹 사이트를 방문 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-325">To learn more about the Microsoft Ajax CDN, visit the following website:</span></span>

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

<span data-ttu-id="e6592-326">ASP.NET ScriptManager는 Microsoft Ajax CDN을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-326">The ASP.NET ScriptManager supports the Microsoft Ajax CDN.</span></span> <span data-ttu-id="e6592-327">단일 속성인 EnableCdn 속성을 설정 하기만 하면 CDN에서 모든 ASP.NET framework JavaScript 파일을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-327">Simply by setting one property, the EnableCdn property, you can retrieve all ASP.NET framework JavaScript files from the CDN:</span></span>

[!code-aspx[Main](overview/samples/sample20.aspx)]

<span data-ttu-id="e6592-328">EnableCdn 속성을 true 값으로 설정 하면 ASP.NET framework는 유효성 검사 및 UpdatePanel에 사용 되는 모든 JavaScript 파일을 포함 하 여 CDN에서 모든 ASP.NET framework JavaScript 파일을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-328">After you set the EnableCdn property to the value true, the ASP.NET framework will retrieve all ASP.NET framework JavaScript files from the CDN including all JavaScript files used for validation and the UpdatePanel.</span></span> <span data-ttu-id="e6592-329">이 속성을 설정 하면 웹 응용 프로그램의 성능에 크게 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-329">Setting this one property can have a dramatic impact on the performance of your web application.</span></span>

<span data-ttu-id="e6592-330">Webresource.axd 특성을 사용 하 여 고유한 JavaScript 파일에 대 한 CDN 경로를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-330">You can set the CDN path for your own JavaScript files by using the WebResource attribute.</span></span> <span data-ttu-id="e6592-331">새 CdnPath 속성은 EnableCdn 속성을 true 값으로 설정할 때 사용 되는 CDN의 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-331">The new CdnPath property specifies the path to the CDN used when you set the EnableCdn property to the value true:</span></span>

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a><span data-ttu-id="e6592-332">ScriptManager 명시적 스크립트</span><span class="sxs-lookup"><span data-stu-id="e6592-332">ScriptManager Explicit Scripts</span></span>

<span data-ttu-id="e6592-333">이전에는 ASP.NET ScriptManger를 사용한 경우 전체 모놀리식 ASP.NET Ajax 라이브러리를 로드 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-333">In the past, if you used the ASP.NET ScriptManger then you were required to load the entire monolithic ASP.NET Ajax Library.</span></span> <span data-ttu-id="e6592-334">새 AjaxFrameworkMode 속성을 활용 하 여 ASP.NET Ajax 라이브러리의 구성 요소를 로드 하 고 필요한 ASP.NET Ajax 라이브러리의 구성 요소만 로드 하는 것을 정확 하 게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-334">By taking advantage of the new ScriptManager.AjaxFrameworkMode property, you can control exactly which components of the ASP.NET Ajax Library are loaded and load only the components of the ASP.NET Ajax Library that you need.</span></span>

<span data-ttu-id="e6592-335">AjaxFrameworkMode 속성은 다음 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-335">The ScriptManager.AjaxFrameworkMode property can be set to the following values:</span></span>

- <span data-ttu-id="e6592-336">Enabled-ScriptManager 컨트롤이 Microsoftajax.js 스크립트 파일을 자동으로 포함 하도록 지정 합니다 .이 파일은 모든 핵심 프레임 워크 스크립트 (레거시 동작)의 결합 된 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-336">Enabled -- Specifies that the ScriptManager control automatically includes the MicrosoftAjax.js script file, which is a combined script file of every core framework script (legacy behavior).</span></span>
- <span data-ttu-id="e6592-337">Disabled--모든 Microsoft Ajax 스크립트 기능을 사용 하지 않도록 지정 하 고 ScriptManager 컨트롤이 스크립트를 자동으로 참조 하지 않도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-337">Disabled -- Specifies that all Microsoft Ajax script features are disabled and that the ScriptManager control does not reference any scripts automatically.</span></span>
- <span data-ttu-id="e6592-338">Explicit--페이지에 필요한 개별 프레임 워크 핵심 스크립트 파일에 스크립트 참조를 명시적으로 포함 하 고 각 스크립트 파일에 필요한 종속성에 대 한 참조를 포함할 것을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-338">Explicit -- Specifies that you will explicitly include script references to individual framework core script file that your page requires, and that you will include references to the dependencies that each script file requires.</span></span>

<span data-ttu-id="e6592-339">예를 들어 AjaxFrameworkMode 속성을 Explicit 값으로 설정 하는 경우 필요한 특정 ASP.NET Ajax 구성 요소 스크립트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-339">For example, if you set the AjaxFrameworkMode property to the value Explicit then you can specify the particular ASP.NET Ajax component scripts that you need:</span></span>

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a><span data-ttu-id="e6592-340">웹 양식</span><span class="sxs-lookup"><span data-stu-id="e6592-340">Web Forms</span></span>

<span data-ttu-id="e6592-341">Web Forms ASP.NET 1.0 이후 ASP.NET의 핵심 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-341">Web Forms has been a core feature in ASP.NET since the release of ASP.NET 1.0.</span></span> <span data-ttu-id="e6592-342">ASP.NET 4의 경우 다음을 포함 하 여 다양 한 기능이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-342">Many enhancements have been in this area for ASP.NET 4, including the following:</span></span>

- <span data-ttu-id="e6592-343">*Meta* 태그를 설정 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-343">The ability to set *meta* tags.</span></span>
- <span data-ttu-id="e6592-344">뷰 상태에 대 한 제어 향상.</span><span class="sxs-lookup"><span data-stu-id="e6592-344">More control over view state.</span></span>
- <span data-ttu-id="e6592-345">브라우저 기능을 사용 하는 보다 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-345">Easier ways to work with browser capabilities.</span></span>
- <span data-ttu-id="e6592-346">Web Forms에서 ASP.NET routing 사용에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="e6592-346">Support for using ASP.NET routing with Web Forms.</span></span>
- <span data-ttu-id="e6592-347">생성 된 Id에 대 한 추가 제어.</span><span class="sxs-lookup"><span data-stu-id="e6592-347">More control over generated IDs.</span></span>
- <span data-ttu-id="e6592-348">데이터 컨트롤에서 선택 된 행을 유지 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-348">The ability to persist selected rows in data controls.</span></span>
- <span data-ttu-id="e6592-349">*FormView* 및 *ListView* 컨트롤에서 렌더링 된 HTML에 대 한 제어 향상</span><span class="sxs-lookup"><span data-stu-id="e6592-349">More control over rendered HTML in the *FormView* and *ListView* controls.</span></span>
- <span data-ttu-id="e6592-350">데이터 소스 컨트롤에 대 한 필터링 지원.</span><span class="sxs-lookup"><span data-stu-id="e6592-350">Filtering support for data source controls.</span></span>

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a><span data-ttu-id="e6592-351">MetaKeywords 및 MetaDescription 속성을 사용 하 여 Meta 태그를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-351">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>

<span data-ttu-id="e6592-352">ASP.NET 4는 *페이지* 클래스 *MetaKeywords* 및 *MetaDescription*에 두 개의 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-352">ASP.NET 4 adds two properties to the *Page* class, *MetaKeywords* and *MetaDescription*.</span></span> <span data-ttu-id="e6592-353">이러한 두 속성은 다음 예제와 같이 페이지의 해당 *meta* 태그를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-353">These two properties represent corresponding *meta* tags in your page, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample23.aspx)]

<span data-ttu-id="e6592-354">이러한 두 속성은 페이지의 *Title* 속성과 동일한 방식으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-354">These two properties work the same way that the page's *Title* property does.</span></span> <span data-ttu-id="e6592-355">이러한 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-355">They follow these rules:</span></span>

1. <span data-ttu-id="e6592-356">*Head* 요소에 속성 이름 ( *MetaKeywords* 의 경우 name = "keywords")과 일치 하는 *Meta* 태그가 없는 경우, *MetaDescription*에 대해 이러한 속성이 설정 되지 않은 것을 의미 합니다. 즉, 해당 속성이 설정 되지 않은 경우에는 *메타* 태그가 렌더링 될 때 해당 페이지에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-356">If there are no *meta* tags in the *head* element that match the property names (that is, name="keywords" for *Page.MetaKeywords* and name="description" for *Page.MetaDescription*, meaning that these properties have not been set), the *meta* tags will be added to the page when it is rendered.</span></span>
2. <span data-ttu-id="e6592-357">이러한 이름을 가진 *meta* 태그가 이미 있는 경우 이러한 속성은 기존 태그 내용에 대 한 get 및 set 메서드로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-357">If there are already *meta* tags with these names, these properties act as get and set methods for the contents of the existing tags.</span></span>

<span data-ttu-id="e6592-358">런타임에 이러한 속성을 설정 하 여 데이터베이스 또는 다른 소스에서 콘텐츠를 가져올 수 있으며, 특정 페이지의 용도를 설명 하도록 태그를 동적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-358">You can set these properties at run time, which lets you get the content from a database or other source, and which lets you set the tags dynamically to describe what a particular page is for.</span></span>

<span data-ttu-id="e6592-359">다음 예제와 같이 Web Forms 페이지 태그 위쪽의 *@ page* 지시문에서 *키워드* 및 *설명* 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-359">You can also set the *Keywords* and *Description* properties in the *@ Page* directive at the top of the Web Forms page markup, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample24.aspx)]

<span data-ttu-id="e6592-360">이렇게 하면 해당 페이지에 이미 선언 된 *meta* 태그 내용 (있는 경우)이 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-360">This will override the *meta* tag contents (if any) already declared in the page.</span></span>

<span data-ttu-id="e6592-361">설명 *메타* 태그의 내용은 Google에서 검색 목록 미리 보기를 개선 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-361">The contents of the description *meta* tag are used for improving search listing previews in Google.</span></span> <span data-ttu-id="e6592-362">자세한 내용은 Google 웹 마스터 중부 블로그에서 [메타 설명을 사용 하 여 코드 조각 개선 개조](https://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) 을 참조 하세요. Google 및 Windows 실시간 검색은 키워드의 내용을 어떤 것도 사용 하지 않지만 다른 검색 엔진은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-362">(For details, see [Improve snippets with a meta description makeover](https://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) on the Google Webmaster Central blog.) Google and Windows Live Search do not use the contents of the keywords for anything, but other search engines might.</span></span> <span data-ttu-id="e6592-363">자세한 내용은 검색 엔진 가이드 웹 사이트에서 [Meta 키워드 도움말](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-363">For more information, see [Meta Keywords Advice](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) on the Search Engine Guide Web site.</span></span>

<span data-ttu-id="e6592-364">이러한 새 속성은 간단한 기능 이지만 이러한 속성을 수동으로 추가 하거나 사용자 고유의 코드를 작성 하 여 *메타* 태그를 만드는 요구 사항에서 사용자를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-364">These new properties are a simple feature, but they save you from the requirement to add these manually or from writing your own code to create the *meta* tags.</span></span>

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a><span data-ttu-id="e6592-365">개별 컨트롤에 대 한 뷰 상태 설정</span><span class="sxs-lookup"><span data-stu-id="e6592-365">Enabling View State for Individual Controls</span></span>

<span data-ttu-id="e6592-366">기본적으로 페이지에 대 한 뷰 상태는 응용 프로그램에 필요 하지 않은 경우에도 페이지의 각 컨트롤이 뷰 상태를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-366">By default, view state is enabled for the page, with the result that each control on the page potentially stores view state even if it is not required for the application.</span></span> <span data-ttu-id="e6592-367">뷰 상태 데이터는 페이지가 생성 하는 태그에 포함 되며 페이지를 클라이언트에 전송 하 고 다시 게시 하는 데 걸리는 시간을 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-367">View state data is included in the markup that a page generates and increases the amount of time it takes to send a page to the client and post it back.</span></span> <span data-ttu-id="e6592-368">필요한 것 보다 더 많은 뷰 상태를 저장 하면 성능이 크게 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-368">Storing more view state than is necessary can cause significant performance degradation.</span></span> <span data-ttu-id="e6592-369">이전 버전의 ASP.NET에서는 개발자가 페이지 크기를 줄이기 위해 개별 컨트롤에 대 한 뷰 상태를 사용 하지 않도록 설정할 수 있지만 개별 컨트롤에 대해 명시적으로이 작업을 수행 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-369">In earlier versions of ASP.NET, developers could disable view state for individual controls in order to reduce page size, but had to do so explicitly for individual controls.</span></span> <span data-ttu-id="e6592-370">ASP.NET 4에서 웹 서버 컨트롤에는 기본적으로 뷰 상태를 사용 하지 않도록 설정한 다음 페이지에 필요한 컨트롤에 대해서만 사용 하도록 설정 하는 *Viewstatemode* 속성이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-370">In ASP.NET 4, Web server controls include a *ViewStateMode* property that lets you disable view state by default and then enable it only for the controls that require it in the page.</span></span>

<span data-ttu-id="e6592-371">*Viewstatemode* 속성은 3 개의 값이 *사용*, *사용 안 함*및 *상속*인 열거형을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-371">The *ViewStateMode* property takes an enumeration that has three values: *Enabled*, *Disabled*, and *Inherit*.</span></span> <span data-ttu-id="e6592-372">*사용* 을 설정 하면 해당 컨트롤 및 *상속* 하도록 설정 되었거나 아무것도 설정 하지 않은 모든 자식 컨트롤의 뷰 상태를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-372">*Enabled* enables view state for that control and for any child controls that are set to *Inherit* or that have nothing set.</span></span> <span data-ttu-id="e6592-373">*Disabled* 뷰 상태를 사용 하지 않도록 설정 하 고 *상속* 은 컨트롤이 부모 컨트롤의 *viewstatemode* 설정을 사용 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-373">*Disabled* disables view state, and *Inherit* specifies that the control uses the *ViewStateMode* setting from the parent control.</span></span>

<span data-ttu-id="e6592-374">다음 예에서는 *Viewstatemode* 속성이 작동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-374">The following example shows how the *ViewStateMode* property works.</span></span> <span data-ttu-id="e6592-375">다음 페이지의 컨트롤에 대 한 태그와 코드에는 *Viewstatemode* 속성의 값이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-375">The markup and code for the controls in the following page includes values for the *ViewStateMode* property:</span></span>

[!code-aspx[Main](overview/samples/sample25.aspx)]

<span data-ttu-id="e6592-376">여기에서 볼 수 있듯이 코드는 PlaceHolder1 컨트롤에 대 한 뷰 상태를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-376">As you can see, the code disables view state for the PlaceHolder1 control.</span></span> <span data-ttu-id="e6592-377">자식 label1 컨트롤은이 속성 값을 상속 합니다. 즉, 컨트롤에 대 한 *Viewstatemode* 의 기본값을*상속* 하므로 뷰 상태를 저장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-377">The child label1 control inherits this property value (*Inherit* is the default value for *ViewStateMode* for controls.) and therefore saves no view state.</span></span> <span data-ttu-id="e6592-378">PlaceHolder2 컨트롤에서 *Viewstatemode* 는 *Enabled*로 설정 되므로 label2는이 속성을 상속 하 고 뷰 상태를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-378">In the PlaceHolder2 control, *ViewStateMode* is set to *Enabled*, so label2 inherits this property and saves view state.</span></span> <span data-ttu-id="e6592-379">페이지가 처음 로드 될 때 두 *레이블* 컨트롤의 *Text* 속성은 문자열 "[DynamicValue]"로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-379">When the page is first loaded, the *Text* property of both *Label* controls is set to the string "[DynamicValue]".</span></span>

<span data-ttu-id="e6592-380">이러한 설정의 효과는 페이지가 처음 로드 될 때 브라우저에 다음 출력이 표시 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-380">The effect of these settings is that when the page loads the first time, the following output is displayed in the browser:</span></span>

<span data-ttu-id="e6592-381">사용 안 함 `: [DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="e6592-381">Disabled `: [DynamicValue]`</span></span>

<span data-ttu-id="e6592-382">사용:`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="e6592-382">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="e6592-383">그러나 포스트백 후에는 다음과 같은 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-383">After a postback, however, the following output is displayed:</span></span>

<span data-ttu-id="e6592-384">사용 안 함 `: [DeclaredValue]`</span><span class="sxs-lookup"><span data-stu-id="e6592-384">Disabled `: [DeclaredValue]`</span></span>

<span data-ttu-id="e6592-385">사용:`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="e6592-385">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="e6592-386">Label1 컨트롤 ( *Viewstatemode* 값이 *Disabled*로 설정 됨)이 코드에서 설정 된 값을 유지 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-386">The label1 control (whose *ViewStateMode* value is set to *Disabled*) has not preserved the value that it was set to in code.</span></span> <span data-ttu-id="e6592-387">그러나 *Viewstatemode* 값이 *사용*으로 설정 된 label2 컨트롤은 상태를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-387">However, the label2 control (whose *ViewStateMode* value is set to *Enabled*) has preserved its state.</span></span>

<span data-ttu-id="e6592-388">다음 예제와 같이 *@ Page* 지시문에 *viewstatemode* 를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-388">You can also set *ViewStateMode* in the *@ Page* directive, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample26.aspx)]

<span data-ttu-id="e6592-389">*페이지* 클래스는 다른 컨트롤 일 뿐입니다. 페이지의 다른 모든 컨트롤에 대 한 부모 컨트롤 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-389">The *Page* class is just another control; it acts as the parent control for all the other controls in the page.</span></span> <span data-ttu-id="e6592-390">*Page*인스턴스에 대해 *viewstatemode* 의 기본값을 *사용할 수* 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-390">The default value of *ViewStateMode* is *Enabled* for instances of *Page*.</span></span> <span data-ttu-id="e6592-391">컨트롤은를 기본적으로 *상속*하기 때문에 페이지 또는 컨트롤 수준에서 *viewstatemode* 를 설정 하지 않는 한, 컨트롤은 *Enabled* 속성 값을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-391">Because controls default to *Inherit*, controls will inherit the *Enabled* property value unless you set *ViewStateMode* at page or control level.</span></span>

<span data-ttu-id="e6592-392">*Viewstatemode* 속성의 값은 *enableviewstate* 속성이 *true*로 설정 된 경우에만 뷰 상태가 유지 되는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-392">The value of the *ViewStateMode* property determines if view state is maintained only if the *EnableViewState* property is set to *true*.</span></span> <span data-ttu-id="e6592-393">*Enableviewstate* 속성이 *false*로 설정 되어 있으면 *viewstatemode* 가 *Enabled*로 설정 된 경우에도 뷰 상태가 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-393">If the *EnableViewState* property is set to *false*, view state will not be maintained even if *ViewStateMode* is set to *Enabled*.</span></span>

<span data-ttu-id="e6592-394">이 기능을 사용 하는 경우 마스터 페이지의 *ContentPlaceHolder* 컨트롤을 사용 하는 것이 좋습니다 .이 경우 마스터 페이지에 대해 *Viewstatemode* 를 *Disabled* 로 설정한 다음 뷰 상태가 필요한 컨트롤이 포함 된 *ContentPlaceHolder* 컨트롤에 대해 개별적으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-394">A good use for this feature is with *ContentPlaceHolder* controls in master pages, where you can set *ViewStateMode* to *Disabled* for the master page and then enable it individually for *ContentPlaceHolder* controls that in turn contain controls that require view state.</span></span>

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a><span data-ttu-id="e6592-395">브라우저 기능 변경 내용</span><span class="sxs-lookup"><span data-stu-id="e6592-395">Changes to Browser Capabilities</span></span>

<span data-ttu-id="e6592-396">ASP.NET는 *브라우저 기능*이라는 기능을 사용 하 여 사용자가 사이트를 검색 하는 데 사용 하는 브라우저의 기능을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-396">ASP.NET determines the capabilities of the browser that a user is using to browse your site by using a feature called *browser capabilities*.</span></span> <span data-ttu-id="e6592-397">브라우저 기능은 *Httpbrowsercapabilities* 개체로 표시 됩니다 ( *요청. browser* 속성에 의해 노출 됨).</span><span class="sxs-lookup"><span data-stu-id="e6592-397">Browser capabilities are represented by the *HttpBrowserCapabilities* object (exposed by the *Request.Browser* property).</span></span> <span data-ttu-id="e6592-398">예를 들어 *Httpbrowsercapabilities* 개체를 사용 하 여 현재 브라우저의 형식 및 버전이 특정 버전의 JavaScript를 지원 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-398">For example, you can use the *HttpBrowserCapabilities* object to determine whether the type and version of the current browser supports a particular version of JavaScript.</span></span> <span data-ttu-id="e6592-399">또는 *Httpbrowsercapabilities* 개체를 사용 하 여 요청이 모바일 장치에서 시작 되었는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-399">Or, you can use the *HttpBrowserCapabilities* object to determine whether the request originated from a mobile device.</span></span>

<span data-ttu-id="e6592-400">*Httpbrowsercapabilities* 개체는 브라우저 정의 파일 집합에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-400">The *HttpBrowserCapabilities* object is driven by a set of browser definition files.</span></span> <span data-ttu-id="e6592-401">이러한 파일에는 특정 브라우저의 기능에 대 한 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-401">These files contain information about the capabilities of particular browsers.</span></span> <span data-ttu-id="e6592-402">ASP.NET 4에서는 이러한 브라우저 정의 파일이 최근에 도입 된 브라우저와 장치에 대 한 정보를 포함 하도록 업데이트 되었습니다. Google Chrome, 모션 BlackBerry 스마트폰의 연구 및 Apple iPhone.</span><span class="sxs-lookup"><span data-stu-id="e6592-402">In ASP.NET 4, these browser definition files have been updated to contain information about recently introduced browsers and devices such as Google Chrome, Research in Motion BlackBerry smartphones, and Apple iPhone.</span></span>

<span data-ttu-id="e6592-403">다음 목록에서는 새 브라우저 정의 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-403">The following list shows new browser definition files:</span></span>

- <span data-ttu-id="e6592-404">*blackberry. 브라우저*</span><span class="sxs-lookup"><span data-stu-id="e6592-404">*blackberry.browser*</span></span>
- <span data-ttu-id="e6592-405">*chrome. 브라우저*</span><span class="sxs-lookup"><span data-stu-id="e6592-405">*chrome.browser*</span></span>
- <span data-ttu-id="e6592-406">*기본값. 브라우저*</span><span class="sxs-lookup"><span data-stu-id="e6592-406">*Default.browser*</span></span>
- <span data-ttu-id="e6592-407">*firefox. 브라우저*</span><span class="sxs-lookup"><span data-stu-id="e6592-407">*firefox.browser*</span></span>
- <span data-ttu-id="e6592-408">*게이트웨이. 브라우저*</span><span class="sxs-lookup"><span data-stu-id="e6592-408">*gateway.browser*</span></span>
- <span data-ttu-id="e6592-409">*일반 브라우저*</span><span class="sxs-lookup"><span data-stu-id="e6592-409">*generic.browser*</span></span>
- <span data-ttu-id="e6592-410">*ie.browser*</span><span class="sxs-lookup"><span data-stu-id="e6592-410">*ie.browser*</span></span>
- <span data-ttu-id="e6592-411">*iemobile*</span><span class="sxs-lookup"><span data-stu-id="e6592-411">*iemobile.browser*</span></span>
- <span data-ttu-id="e6592-412">*iphone. 브라우저*</span><span class="sxs-lookup"><span data-stu-id="e6592-412">*iphone.browser*</span></span>
- <span data-ttu-id="e6592-413">*opera*</span><span class="sxs-lookup"><span data-stu-id="e6592-413">*opera.browser*</span></span>
- <span data-ttu-id="e6592-414">*safari. 브라우저*</span><span class="sxs-lookup"><span data-stu-id="e6592-414">*safari.browser*</span></span>

#### <a name="using-browser-capabilities-providers"></a><span data-ttu-id="e6592-415">브라우저 기능 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="e6592-415">Using Browser Capabilities Providers</span></span>

<span data-ttu-id="e6592-416">ASP.NET 버전 3.5 서비스 팩 1에서는 다음과 같은 방법으로 브라우저에 포함 되는 기능을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-416">In ASP.NET version 3.5 Service Pack 1, you can define the capabilities that a browser has in the following ways:</span></span>

- <span data-ttu-id="e6592-417">컴퓨터 수준에서 다음 폴더에 `.browser` XML 파일을 만들거나 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-417">At the computer level, you create or update a `.browser` XML file in the following folder:</span></span>

- [!code-console[Main](overview/samples/sample27.cmd)]

- <span data-ttu-id="e6592-418">브라우저 기능을 정의한 후에는 브라우저 기능 어셈블리를 다시 빌드하고 GAC에 추가 하기 위해 Visual Studio 명령 프롬프트에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-418">After you define the browser capability, you run the following command from the Visual Studio Command Prompt in order to rebuild the browser capabilities assembly and add it to the GAC:</span></span>

- [!code-console[Main](overview/samples/sample28.cmd)]

- <span data-ttu-id="e6592-419">개별 응용 프로그램의 경우 응용 프로그램의 `App_Browsers` 폴더에 `.browser` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-419">For an individual application, you create a `.browser` file in the application's `App_Browsers` folder.</span></span>

<span data-ttu-id="e6592-420">이러한 접근 방식에서는 XML 파일을 변경 해야 하며 컴퓨터 수준 변경의 경우에는 aspnet\_regbrowsers 프로세스를 실행 한 후 응용 프로그램을 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-420">These approaches require you to change XML files, and for computer-level changes, you must restart the application after you run the aspnet\_regbrowsers.exe process.</span></span>

<span data-ttu-id="e6592-421">ASP.NET 4에는 *브라우저 기능 공급자*라고 하는 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-421">ASP.NET 4 includes a feature referred to as *browser capabilities providers*.</span></span> <span data-ttu-id="e6592-422">이름에서 알 수 있듯이이를 통해 공급자를 빌드할 수 있습니다. 그러면 고유한 코드를 사용 하 여 브라우저 기능을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-422">As the name suggests, this lets you build a provider that in turn lets you use your own code to determine browser capabilities.</span></span>

<span data-ttu-id="e6592-423">실제로 개발자는 사용자 지정 브라우저 기능을 정의 하지 않는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-423">In practice, developers often do not define custom browser capabilities.</span></span> <span data-ttu-id="e6592-424">브라우저 파일은 업데이트 하기 어렵습니다. 이러한 파일을 업데이트 하는 프로세스는 매우 복잡 하며, `.browser` 파일의 XML 구문은를 사용 하 고 정의 하는 데 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-424">Browser files are hard to update, the process for updating them is fairly complicated, and the XML syntax for `.browser` files can be complex to use and define.</span></span> <span data-ttu-id="e6592-425">일반적인 브라우저 정의 구문이 나 최신 브라우저 정의를 포함 하는 데이터베이스 또는 이러한 데이터베이스에 대 한 웹 서비스를 사용 하는 경우이 프로세스를 훨씬 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-425">What would make this process much easier is if there were a common browser definition syntax, or a database that contained up-to-date browser definitions, or even a Web service for such a database.</span></span> <span data-ttu-id="e6592-426">새 브라우저 기능 공급자 기능을 사용 하면 타사 개발자가 이러한 시나리오를 가능 하 게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-426">The new browser capabilities providers feature makes these scenarios possible and practical for third-party developers.</span></span>

<span data-ttu-id="e6592-427">새로운 ASP.NET 4 브라우저 기능 공급자 기능을 사용 하는 방법에는 ASP.NET 브라우저 기능 정의 기능을 확장 하거나 완전히 대체 하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-427">There are two main approaches for using the new ASP.NET 4 browser capabilities provider feature: extending the ASP.NET browser capabilities definition functionality, or totally replacing it.</span></span> <span data-ttu-id="e6592-428">다음 섹션에서는 기능을 대체 하는 방법 및 확장 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-428">The following sections describe first how to replace the functionality, and then how to extend it.</span></span>

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="e6592-429">ASP.NET Browser 기능 대체 기능</span><span class="sxs-lookup"><span data-stu-id="e6592-429">Replacing the ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="e6592-430">ASP.NET browser 기능 정의 기능을 완전히 교체 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-430">To replace the ASP.NET browser capabilities definition functionality completely, follow these steps:</span></span>

1. <span data-ttu-id="e6592-431">다음 예제와 같이 *Getbrowsercapabilities* 메서드를 재정의 하는 *HttpCapabilitiesProvider* 에서 파생 되는 공급자 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-431">Create a provider class that derives from *HttpCapabilitiesProvider* and that overrides the *GetBrowserCapabilities* method, as in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    <span data-ttu-id="e6592-432">이 예제의 코드는 browser 라는 기능을 지정 하 고 해당 기능을 MyCustomBrowser로 설정 하 여 새 *Httpbrowsercapabilities* 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-432">The code in this example creates a new *HttpBrowserCapabilities* object, specifying only the capability named browser and setting that capability to MyCustomBrowser.</span></span>
2. <span data-ttu-id="e6592-433">응용 프로그램에 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-433">Register the provider with the application.</span></span> 

    <span data-ttu-id="e6592-434">응용 프로그램에서 공급자를 사용 하려면 `Web.config` 또는 `Machine.config` 파일의 *browserCaps* 섹션에 *공급자* 특성을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-434">In order to use a provider with an application, you must add the *provider* attribute to the *browserCaps* section in the `Web.config` or `Machine.config` files.</span></span> <span data-ttu-id="e6592-435">특정 모바일 장치에 대 한 폴더와 같이 응용 프로그램의 특정 디렉터리에 대 한 *location* 요소에서 공급자 특성을 정의할 수도 있습니다. 다음 예에서는 구성 파일에서 *공급자* 특성을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-435">(You can also define the provider attributes in a *location* element for specific directories in application, such as in a folder for a specific mobile device.) The following example shows how to set the *provider* attribute in a configuration file:</span></span>

    [!code-xml[Main](overview/samples/sample30.xml)]

    <span data-ttu-id="e6592-436">새 브라우저 기능 정의를 등록 하는 또 다른 방법은 다음 예제와 같이 코드를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-436">Another way to register the new browser capability definition is to use code, as shown in the following example:</span></span>

    [!code-csharp[Main](overview/samples/sample31.cs)]

    <span data-ttu-id="e6592-437">이 코드는 `Global.asax` 파일의 *응용 프로그램\_시작* 이벤트에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-437">This code must run in the *Application\_Start* event of the `Global.asax` file.</span></span> <span data-ttu-id="e6592-438">*BrowserCapabilitiesProvider* 클래스에 대 한 변경 내용은 응용 프로그램의 코드가 실행 되기 전에 발생 해야 캐시가 해결 된 *사용* 개체에 대 한 유효한 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-438">Any change to the *BrowserCapabilitiesProvider* class must occur before any code in the application executes, in order to make sure that the cache remains in a valid state for the resolved *HttpCapabilitiesBase* object.</span></span>

#### <a name="caching-the-httpbrowsercapabilities-object"></a><span data-ttu-id="e6592-439">HttpBrowserCapabilities 개체 캐시</span><span class="sxs-lookup"><span data-stu-id="e6592-439">Caching the HttpBrowserCapabilities Object</span></span>

<span data-ttu-id="e6592-440">앞의 예제에는 *Httpbrowsercapabilities* 개체를 가져오기 위해 사용자 지정 공급자가 호출 될 때마다 코드가 실행 되는 한 가지 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-440">The preceding example has one problem, which is that the code would run each time the custom provider is invoked in order to get the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="e6592-441">각 요청 중에 여러 번 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-441">This can happen multiple times during each request.</span></span> <span data-ttu-id="e6592-442">이 예제에서는 공급자의 코드에서 많은 작업을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-442">In the example, the code for the provider does not do much.</span></span> <span data-ttu-id="e6592-443">그러나 사용자 지정 공급자의 코드가 *Httpbrowsercapabilities* 개체를 가져오기 위해 중요 한 작업을 수행 하는 경우이는 성능에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-443">However, if the code in your custom provider performs significant work in order to get the *HttpBrowserCapabilities* object, this can affect performance.</span></span> <span data-ttu-id="e6592-444">이러한 상황이 발생 하지 않도록 하려면 *Httpbrowsercapabilities* 개체를 캐시 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-444">To prevent this from happening, you can cache the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="e6592-445">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-445">Follow these steps:</span></span>

1. <span data-ttu-id="e6592-446">다음 예제와 같이 *HttpCapabilitiesProvider*에서 파생 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-446">Create a class that derives from *HttpCapabilitiesProvider*, like the one in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    <span data-ttu-id="e6592-447">이 예제에서 코드는 사용자 지정 BuildCacheKey 메서드를 호출 하 여 캐시 키를 생성 하 고, 사용자 지정 GetCacheTime 메서드를 호출 하 여 캐시 하는 시간 길이를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-447">In the example, the code generates a cache key by calling a custom BuildCacheKey method, and it gets the length of time to cache by calling a custom GetCacheTime method.</span></span> <span data-ttu-id="e6592-448">그런 다음 코드는 확인 된 *Httpbrowsercapabilities* 개체를 캐시에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-448">The code then adds the resolved *HttpBrowserCapabilities* object to the cache.</span></span> <span data-ttu-id="e6592-449">캐시에서 개체를 검색 하 고 사용자 지정 공급자를 사용 하는 후속 요청에서 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-449">The object can be retrieved from the cache and reused on subsequent requests that make use of the custom provider.</span></span>
2. <span data-ttu-id="e6592-450">이전 절차에 설명 된 대로 응용 프로그램에 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-450">Register the provider with the application as described in the preceding procedure.</span></span>

#### <a name="extending-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="e6592-451">ASP.NET Browser 기능 확장 기능</span><span class="sxs-lookup"><span data-stu-id="e6592-451">Extending ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="e6592-452">이전 섹션에서는 ASP.NET 4에서 새 *Httpbrowsercapabilities* 개체를 만드는 방법을 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-452">The previous section described how to create a new *HttpBrowserCapabilities* object in ASP.NET 4.</span></span> <span data-ttu-id="e6592-453">ASP.NET에 이미 있는 브라우저에 새 브라우저 기능 정의를 추가 하 여 ASP.NET 브라우저 기능 기능을 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-453">You can also extend the ASP.NET browser capabilities functionality by adding new browser capabilities definitions to those that are already in ASP.NET.</span></span> <span data-ttu-id="e6592-454">XML 브라우저 정의를 사용 하지 않고이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-454">You can do this without using the XML browser definitions.</span></span> <span data-ttu-id="e6592-455">다음 절차에서는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-455">The following procedure shows how.</span></span>

1. <span data-ttu-id="e6592-456">다음 예제와 같이 *Getbrowsercapabilities* 메서드를 재정의 하는 *HttpCapabilitiesEvaluator* 에서 파생 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-456">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    <span data-ttu-id="e6592-457">이 코드는 먼저 ASP.NET browser 기능 기능을 사용 하 여 브라우저를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-457">This code first uses the ASP.NET browser capabilities functionality to try to identify the browser.</span></span> <span data-ttu-id="e6592-458">그러나 요청에 정의 된 정보를 기반으로 브라우저가 식별 되지 않는 경우 즉, *Httpbrowsercapabilities* 개체의 *browser* 속성이 문자열 "Unknown" 이면 코드에서 사용자 지정 공급자 (MyBrowserCapabilitiesEvaluator)를 호출 하 여 브라우저를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-458">However, if no browser is identified based on the information defined in the request (that is, if the *Browser* property of the *HttpBrowserCapabilities* object is the string "Unknown"), the code calls the custom provider (MyBrowserCapabilitiesEvaluator) to identify the browser.</span></span>
2. <span data-ttu-id="e6592-459">이전 예제에서 설명한 대로 응용 프로그램에 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-459">Register the provider with the application as described in the previous example.</span></span>

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a><span data-ttu-id="e6592-460">기존 기능 정의에 새 기능을 추가 하 여 브라우저 기능 기능 확장</span><span class="sxs-lookup"><span data-stu-id="e6592-460">Extending Browser Capabilities Functionality by Adding New Capabilities to Existing Capabilities Definitions</span></span>

<span data-ttu-id="e6592-461">사용자 지정 브라우저 정의 공급자를 만들고 동적으로 새 브라우저 정의를 만드는 것 외에도 추가 기능을 사용 하 여 기존 브라우저 정의를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-461">In addition to creating a custom browser definition provider and to dynamically creating new browser definitions, you can extend existing browser definitions with additional capabilities.</span></span> <span data-ttu-id="e6592-462">이렇게 하면 원하는 항목에 가까운 정의를 사용할 수 있지만 몇 가지 기능만 부족 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-462">This lets you use a definition that is close to what you want but lacks only a few capabilities.</span></span> <span data-ttu-id="e6592-463">이렇게 하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-463">To do this, use the following steps.</span></span>

1. <span data-ttu-id="e6592-464">다음 예제와 같이 *Getbrowsercapabilities* 메서드를 재정의 하는 *HttpCapabilitiesEvaluator* 에서 파생 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-464">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    <span data-ttu-id="e6592-465">예제 코드는 기존 ASP.NET *HttpCapabilitiesEvaluator* 클래스를 확장 하 고 다음 코드를 사용 하 여 현재 요청 정의와 일치 하는 *httpbrowsercapabilities* 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-465">The example code extends the existing ASP.NET *HttpCapabilitiesEvaluator* class and gets the *HttpBrowserCapabilities* object that matches the current request definition by using the following code:</span></span>

    [!code-csharp[Main](overview/samples/sample35.cs)]

    <span data-ttu-id="e6592-466">그러면 코드에서이 브라우저의 기능을 추가 하거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-466">The code can then add or modify a capability for this browser.</span></span> <span data-ttu-id="e6592-467">새 브라우저 기능을 지정 하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-467">There are two ways to specify a new browser capability:</span></span>

    - <span data-ttu-id="e6592-468">*사용* 개체의 *Capabilities* 속성에 의해 노출 되는 *IDictionary* 개체에 키/값 쌍을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-468">Add a key/value pair to the *IDictionary* object that is exposed by the *Capabilities* property of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="e6592-469">이전 예제에서 코드는 값이 *true*인 다중 터치 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-469">In the previous example, the code adds a capability named MultiTouch with a value of *true*.</span></span>
    - <span data-ttu-id="e6592-470">*사용* 개체의 기존 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-470">Set existing properties of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="e6592-471">이전 예제에서 코드는 *frame* 속성을 *true*로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-471">In the previous example, the code sets the *Frames* property to *true*.</span></span> <span data-ttu-id="e6592-472">이 속성은 *기능* 속성에 의해 노출 되는 *IDictionary* 개체에 대 한 접근자 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-472">This property is simply an accessor for the *IDictionary* object that is exposed by the *Capabilities* property.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="e6592-473">참고이 모델은 제어 어댑터를 포함 하 여 *Httpbrowsercapabilities*의 모든 속성에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-473">Note This model applies to any property of *HttpBrowserCapabilities*, including control adapters.</span></span>
2. <span data-ttu-id="e6592-474">이전 절차에 설명 된 대로 응용 프로그램에 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-474">Register the provider with the application as described in the earlier procedure.</span></span>

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a><span data-ttu-id="e6592-475">ASP.NET 4의 라우팅</span><span class="sxs-lookup"><span data-stu-id="e6592-475">Routing in ASP.NET 4</span></span>

<span data-ttu-id="e6592-476">ASP.NET 4는 Web Forms로 라우팅을 사용 하기 위한 기본 제공 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-476">ASP.NET 4 adds built-in support for using routing with Web Forms.</span></span> <span data-ttu-id="e6592-477">라우팅을 사용 하면 실제 파일에 매핑되지 않는 요청 Url을 허용 하도록 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-477">Routing lets you configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="e6592-478">대신 라우팅을 사용 하 여 사용자에 게 의미 있는 Url을 정의 하 고 응용 프로그램에 대 한 SEO (검색 엔진 최적화)를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-478">Instead, you can use routing to define URLs that are meaningful to users and that can help with search-engine optimization (SEO) for your application.</span></span> <span data-ttu-id="e6592-479">예를 들어 기존 응용 프로그램의 제품 범주를 표시 하는 페이지의 URL은 다음 예제와 같이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-479">For example, the URL for a page that displays product categories in an existing application might look like the following example:</span></span>

[!code-console[Main](overview/samples/sample36.cmd)]

<span data-ttu-id="e6592-480">라우팅을 사용 하 여 다음 URL을 허용 하도록 응용 프로그램을 구성 하 여 동일한 정보를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-480">By using routing, you can configure the application to accept the following URL to render the same information:</span></span>

[!code-console[Main](overview/samples/sample37.cmd)]

<span data-ttu-id="e6592-481">ASP.NET 3.5 SP1부터 라우팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-481">Routing has been available starting with ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="e6592-482">ASP.NET 3.5 s p 1에서 라우팅을 사용 하는 방법에 대 한 예제는 Phil Haack의 블로그에서 [WebForms를 사용 하 여 라우팅을](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "이 항목의 제목입니다.") 사용 하는 항목을 참조 하세요. 그러나 ASP.NET 4에는 다음을 포함 하 여 라우팅을 보다 쉽게 사용할 수 있도록 하는 몇 가지 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-482">(For an example of how to use routing in ASP.NET 3.5 SP1, see the entry [Using Routing With WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "Title of this entry.") on Phil Haack's blog.) However, ASP.NET 4 includes some features that make it easier to use routing, including the following:</span></span>

- <span data-ttu-id="e6592-483">*PageRouteHandler* 클래스는 경로를 정의할 때 사용 하는 간단한 HTTP 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-483">The *PageRouteHandler* class, which is a simple HTTP handler that you use when you define routes.</span></span> <span data-ttu-id="e6592-484">클래스는 요청을 라우팅하는 페이지로 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-484">The class passes data to the page that the request is routed to.</span></span>
- <span data-ttu-id="e6592-485">새 속성 *HttpRequest* 및 *RouteData* ( *HttpRequest* 개체에 대 한 프록시)입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-485">The new properties *HttpRequest.RequestContext* and *Page.RouteData* (which is a proxy for the *HttpRequest.RequestContext.RouteData* object).</span></span> <span data-ttu-id="e6592-486">이러한 속성을 통해 경로에서 전달 되는 정보에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-486">These properties make it easier to access information that is passed from the route.</span></span>
- <span data-ttu-id="e6592-487">*RouteUrlExpressionBuilder* 및 RouteValueExpressionBuilder에 정의 된 다음과 같은 새 식 작성기가 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="e6592-487">The following new expression builders, which are defined in *System.Web.Compilation.RouteUrlExpressionBuilder* and *System.Web.Compilation.RouteValueExpressionBuilder*:</span></span>
- <span data-ttu-id="e6592-488">*RouteUrl*는 ASP.NET 서버 컨트롤 내의 경로 url에 해당 하는 url을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-488">*RouteUrl*, which provides a simple way to create a URL that corresponds to a route URL within an ASP.NET server control.</span></span>
- <span data-ttu-id="e6592-489">*RouteValue*는 *RouteContext* 개체에서 정보를 추출 하는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-489">*RouteValue*, which provides a simple way to extract information from the *RouteContext* object.</span></span>
- <span data-ttu-id="e6592-490">*RouteParameter* 클래스를 사용 하면 *RouteContext* 개체에 포함 된 데이터를 데이터 소스 컨트롤에 대 한 쿼리에 더 쉽게 전달할 수 있습니다 ( [*formparameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)와 유사).</span><span class="sxs-lookup"><span data-stu-id="e6592-490">The *RouteParameter* class, which makes it easier to pass data contained in a *RouteContext* object to a query for a data source control (similar to [*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span></span>

#### <a name="routing-for-web-forms-pages"></a><span data-ttu-id="e6592-491">Web Forms 페이지에 대 한 라우팅</span><span class="sxs-lookup"><span data-stu-id="e6592-491">Routing for Web Forms Pages</span></span>

<span data-ttu-id="e6592-492">다음 예제에서는 *route* 클래스의 new *MapPageRoute* 메서드를 사용 하 여 Web Forms 경로를 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-492">The following example shows how to define a Web Forms route by using the new *MapPageRoute* method of the *Route* class:</span></span>

[!code-csharp[Main](overview/samples/sample38.cs)]

<span data-ttu-id="e6592-493">ASP.NET 4에서는 *MapPageRoute* 메서드를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-493">ASP.NET 4 introduces the *MapPageRoute* method.</span></span> <span data-ttu-id="e6592-494">다음 예제는 이전 예제에 표시 된 SearchRoute 정의와 동일 하지만 *PageRouteHandler* 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-494">The following example is equivalent to the SearchRoute definition shown in the previous example, but uses the *PageRouteHandler* class.</span></span>

[!code-csharp[Main](overview/samples/sample39.cs)]

<span data-ttu-id="e6592-495">예제의 코드는 경로를 첫 번째 경로의 실제 페이지에 매핑합니다 (`~/search.aspx`).</span><span class="sxs-lookup"><span data-stu-id="e6592-495">The code in the example maps the route to a physical page (in the first route, to `~/search.aspx`).</span></span> <span data-ttu-id="e6592-496">또한 첫 번째 경로 정의는 searchterm 이라는 매개 변수를 URL에서 추출 하 여 페이지에 전달 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-496">The first route definition also specifies that the parameter named searchterm should be extracted from the URL and passed to the page.</span></span>

<span data-ttu-id="e6592-497">*MapPageRoute* 메서드는 다음 메서드 오버 로드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-497">The *MapPageRoute* method supports the following method overloads:</span></span>

- <span data-ttu-id="e6592-498">*MapPageRoute (string routeName, string routeUrl, string Valfile, bool checkPhysicalUrlAccess)*</span><span class="sxs-lookup"><span data-stu-id="e6592-498">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*</span></span>
- <span data-ttu-id="e6592-499">*MapPageRoute (string routeName, string routeUrl, string Valfile, bool checkPhysicalUrlAccess, RouteValueDictionary 기본값)*</span><span class="sxs-lookup"><span data-stu-id="e6592-499">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults)*</span></span>
- <span data-ttu-id="e6592-500">*MapPageRoute (string routeName, string routeUrl, string Valfile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary 제약 조건)*</span><span class="sxs-lookup"><span data-stu-id="e6592-500">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary constraints)*</span></span>

<span data-ttu-id="e6592-501">*Check이상 Urlaccess* 매개 변수는 경로가 라우팅되는 실제 페이지의 보안 권한 (이 경우에는 .aspx) 및 들어오는 URL에 대 한 권한 (이 경우 검색/{searchterm})을 확인 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-501">The *checkPhysicalUrlAccess* parameter specifies whether the route should check the security permissions for the physical page being routed to (in this case, search.aspx) and the permissions on the incoming URL (in this case, search/{searchterm}).</span></span> <span data-ttu-id="e6592-502">*Checking Urlaccess* 값이 *FALSE*이면 들어오는 URL의 사용 권한만 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-502">If the value of *checkPhysicalUrlAccess* is *false*, only the permissions of the incoming URL will be checked.</span></span> <span data-ttu-id="e6592-503">이러한 권한은 다음과 같은 설정을 사용 하 여 `Web.config` 파일에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-503">These permissions are defined in the `Web.config` file using settings such as the following:</span></span>

[!code-xml[Main](overview/samples/sample40.xml)]

<span data-ttu-id="e6592-504">예제 구성에서는 관리자 역할에 속한 사용자를 제외한 모든 사용자에 대 한 실제 페이지 `search.aspx`에 대 한 액세스가 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-504">In the example configuration, access is denied to the physical page `search.aspx` for all users except those who are in the admin role.</span></span> <span data-ttu-id="e6592-505">*Check/search/{searchterm} Urlaccess* 매개 변수를 *true* (기본값)로 설정 하면 실제 페이지 검색은 해당 역할의 사용자로 제한 되기 때문에 admin 사용자만 URL에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-505">When the *checkPhysicalUrlAccess* parameter is set to *true* (which is its default value), only admin users are allowed to access the URL /search/{searchterm}, because the physical page search.aspx is restricted to users in that role.</span></span> <span data-ttu-id="e6592-506">*Check/search/{searchterm}. Urlaccess* 가 *false* 로 설정 되 고 사이트가 이전 예제와 같이 구성 된 경우 인증 된 모든 사용자는 URL에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-506">If *checkPhysicalUrlAccess* is set to *false* and the site is configured as shown in the previous example, all authenticated users are allowed to access the URL /search/{searchterm}.</span></span>

#### <a name="reading-routing-information-in-a-web-forms-page"></a><span data-ttu-id="e6592-507">Web Forms 페이지에서 라우팅 정보 읽기</span><span class="sxs-lookup"><span data-stu-id="e6592-507">Reading Routing Information in a Web Forms Page</span></span>

<span data-ttu-id="e6592-508">Web Forms 실제 페이지의 코드에서 *HttpRequest* 및 *RouteData*라는 두 개의 새 속성을 사용 하 여 라우팅에서 추출 된 정보 (또는 다른 개체가 *RouteData* 개체에 추가한 기타 정보)에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-508">In the code of the Web Forms physical page, you can access the information that routing has extracted from the URL (or other information that another object has added to the *RouteData* object) by using two new properties: *HttpRequest.RequestContext* and *Page.RouteData*.</span></span> <span data-ttu-id="e6592-509">(*RouteData* *HttpRequest RouteData*를 래핑합니다.) 다음 예제에서는 *RouteData*를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-509">(*Page.RouteData* wraps *HttpRequest.RequestContext.RouteData*.) The following example shows how to use *Page.RouteData*.</span></span>

[!code-csharp[Main](overview/samples/sample41.cs)]

<span data-ttu-id="e6592-510">이 코드는 앞의 예제 경로에 정의 된 대로 searchterm 매개 변수로 전달 된 값을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-510">The code extracts the value that was passed for the searchterm parameter, as defined in the example route earlier.</span></span> <span data-ttu-id="e6592-511">다음 요청 URL을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-511">Consider the following request URL:</span></span>

[!code-console[Main](overview/samples/sample42.cmd)]

<span data-ttu-id="e6592-512">이 요청을 수행 하면 "scott" 이라는 단어가 `search.aspx` 페이지에서 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-512">When this request is made, the word "scott" would be rendered in the `search.aspx` page.</span></span>

#### <a name="accessing-routing-information-in-markup"></a><span data-ttu-id="e6592-513">태그에서 라우팅 정보 액세스</span><span class="sxs-lookup"><span data-stu-id="e6592-513">Accessing Routing Information in Markup</span></span>

<span data-ttu-id="e6592-514">이전 섹션에서 설명 하는 메서드는 Web Forms 페이지에서 코드의 경로 데이터를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-514">The method described in the previous section shows how to get route data in code in a Web Forms page.</span></span> <span data-ttu-id="e6592-515">동일한 정보에 대 한 액세스를 제공 하는 태그에 식을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-515">You can also use expressions in markup that give you access to the same information.</span></span> <span data-ttu-id="e6592-516">식 작성기는 선언적 코드를 사용 하는 강력 하 고 세련 된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-516">Expression builders are a powerful and elegant way to work with declarative code.</span></span> <span data-ttu-id="e6592-517">자세한 내용은 Phil Haack의 블로그에서 [사용자 지정 식 작성기를 사용 하 여 명시적으로](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) 입력 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-517">(For more information, see the entry [Express Yourself With Custom Expression Builders](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) on Phil Haack's blog.)</span></span>

<span data-ttu-id="e6592-518">ASP.NET 4에는 Web Forms 라우팅을 위한 두 가지 새로운 식 작성기가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-518">ASP.NET 4 includes two new expression builders for Web Forms routing.</span></span> <span data-ttu-id="e6592-519">다음 예제에서는이를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-519">The following example shows how to use them.</span></span>

[!code-aspx[Main](overview/samples/sample43.aspx)]

<span data-ttu-id="e6592-520">이 예에서 *RouteUrl* 식은 경로 매개 변수를 기반으로 하는 URL을 정의 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-520">In the example, the *RouteUrl* expression is used to define a URL that is based on a route parameter.</span></span> <span data-ttu-id="e6592-521">이렇게 하면 전체 URL을 태그에 하드 코딩 하지 않아도 되며, 나중에이 링크를 변경할 필요 없이 URL 구조를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-521">This saves you from having to hard-code the complete URL into the markup, and lets you change the URL structure later without requiring any change to this link.</span></span>

<span data-ttu-id="e6592-522">이 태그는 앞에서 정의한 경로에 따라 다음 URL을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-522">Based on the route defined earlier, this markup generates the following URL:</span></span>

[!code-console[Main](overview/samples/sample44.cmd)]

<span data-ttu-id="e6592-523">ASP.NET는 입력 매개 변수를 기반으로 올바른 경로 (즉, 올바른 URL 생성)를 자동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-523">ASP.NET automatically works out the correct route (that is, it generates the correct URL) based on the input parameters.</span></span> <span data-ttu-id="e6592-524">사용할 경로를 지정할 수 있는 경로 이름을 식에 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-524">You can also include a route name in the expression, which lets you specify a route to use.</span></span>

<span data-ttu-id="e6592-525">다음 예에서는 *RouteValue* 식을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-525">The following example shows how to use the *RouteValue* expression.</span></span>

[!code-aspx[Main](overview/samples/sample45.aspx)]

<span data-ttu-id="e6592-526">이 컨트롤을 포함 하는 페이지가 실행 되 면 레이블에 "scott" 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-526">When the page that contains this control runs, the value "scott" is displayed in the label.</span></span>

<span data-ttu-id="e6592-527">*RouteValue* 식을 사용 하면 태그에서 경로 데이터를 간단 하 게 사용할 수 있으며, 태그에서 보다 복잡 한 RouteData ["x"] 구문을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-527">The *RouteValue* expression makes it simple to use route data in markup, and it avoids having to work with the more complex Page.RouteData["x"] syntax in markup.</span></span>

#### <a name="using-route-data-for-data-source-control-parameters"></a><span data-ttu-id="e6592-528">데이터 원본 제어 매개 변수에 대 한 경로 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="e6592-528">Using Route Data for Data Source Control Parameters</span></span>

<span data-ttu-id="e6592-529">*RouteParameter* 클래스를 사용 하면 경로 데이터를 데이터 소스 컨트롤의 쿼리에 대 한 매개 변수 값으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-529">The *RouteParameter* class lets you specify route data as a parameter value for queries in a data source control.</span></span> <span data-ttu-id="e6592-530">다음 예제와 같이 클래스와 [매우 유사](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-530">It [works much like the](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) class, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample46.aspx)]

<span data-ttu-id="e6592-531">이 경우 경로 매개 변수 searchterm의 값이 *Select* 문의 @companyname 매개 변수에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-531">In this case, the value of the route parameter searchterm will be used for the @companyname parameter in the *Select* statement.</span></span>

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a><span data-ttu-id="e6592-532">클라이언트 Id 설정</span><span class="sxs-lookup"><span data-stu-id="e6592-532">Setting Client IDs</span></span>

<span data-ttu-id="e6592-533">새 *Clientidmode* 속성은 ASP.NET에서 오래 된 문제를 해결 합니다. 즉, 컨트롤에서 렌더링 하는 요소에 대 한 *id* 특성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-533">The new *ClientIDMode* property addresses a long-standing issue in ASP.NET, namely how controls create the *id* attribute for elements that they render.</span></span> <span data-ttu-id="e6592-534">응용 프로그램에 이러한 요소를 참조 하는 클라이언트 스크립트가 포함 된 경우 렌더링 된 요소에 대 한 *id* 특성을 알고 있는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-534">Knowing the *id* attribute for rendered elements is important if your application includes client script that references these elements.</span></span>

<span data-ttu-id="e6592-535">웹 서버 컨트롤에 대해 렌더링 되는 HTML의 *id* 특성은 컨트롤의 *ClientID* 속성을 기반으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-535">The *id* attribute in HTML that is rendered for Web server controls is generated based on the *ClientID* property of the control.</span></span> <span data-ttu-id="e6592-536">ASP.NET 4 까지는 *ClientID* 속성에서 *id* 특성을 생성 하는 알고리즘이 id를 사용 하 여 명명 컨테이너 (있는 경우)를 연결 하 고 반복 되는 컨트롤 (데이터 컨트롤의 경우)에서 접두사와 일련 번호를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-536">Until ASP.NET 4, the algorithm for generating the *id* attribute from the *ClientID* property has been to concatenate the naming container (if any) with the ID, and in the case of repeated controls (as in data controls), to add a prefix and a sequential number.</span></span> <span data-ttu-id="e6592-537">이는 페이지의 컨트롤 Id가 항상 고유 하다는 것을 보장 하지만 알고리즘은 예측할 수 없는 컨트롤 Id를 가지 므로 클라이언트 스크립트에서 참조 하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-537">While this has always guaranteed that the IDs of controls in the page are unique, the algorithm has resulted in control IDs that were not predictable, and were therefore difficult to reference in client script.</span></span>

<span data-ttu-id="e6592-538">새 *Clientidmode* 속성을 사용 하면 컨트롤에 대 한 클라이언트 ID가 생성 되는 방식을 보다 정확 하 게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-538">The new *ClientIDMode* property lets you specify more precisely how the client ID is generated for controls.</span></span> <span data-ttu-id="e6592-539">페이지를 포함 하 여 모든 컨트롤에 대해 *Clientidmode* 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-539">You can set the *ClientIDMode* property for any control, including for the page.</span></span> <span data-ttu-id="e6592-540">가능한 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-540">Possible settings are the following:</span></span>

- <span data-ttu-id="e6592-541">*Autoid* – ASP.NET의 이전 버전에서 사용 된 *ClientID* 속성 값을 생성 하는 알고리즘과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-541">*AutoID* – This is equivalent to the algorithm for generating *ClientID* property values that was used in earlier versions of ASP.NET.</span></span>
- <span data-ttu-id="e6592-542">*정적* –이는 *ClientID* 값이 부모 명명 컨테이너의 id를 연결 하지 않고 id와 동일 하 게 지정 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-542">*Static* – This specifies that the *ClientID* value will be the same as the ID without concatenating the IDs of parent naming containers.</span></span> <span data-ttu-id="e6592-543">이는 웹 사용자 정의 컨트롤에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-543">This can be useful in Web user controls.</span></span> <span data-ttu-id="e6592-544">웹 사용자 정의 컨트롤은 다른 페이지와 다른 컨테이너 컨트롤에 있을 수 있으므로 ID 값을 예측할 수 없으므로 *Autoid* 알고리즘을 사용 하는 컨트롤에 대 한 클라이언트 스크립트를 작성 하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-544">Because a Web user control can be located on different pages and in different container controls, it can be difficult to write client script for controls that use the *AutoID* algorithm because you cannot predict what the ID values will be.</span></span>
- <span data-ttu-id="e6592-545">*예측* 가능-이 옵션은 주로 반복 템플릿을 사용 하는 데이터 컨트롤에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-545">*Predictable* – This option is primarily for use in data controls that use repeating templates.</span></span> <span data-ttu-id="e6592-546">컨트롤의 명명 컨테이너에 대 한 ID 속성을 연결 하지만 생성 된 *ClientID* 값은 "ctlxxx"와 같은 문자열을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-546">It concatenates the ID properties of the control's naming containers, but generated *ClientID* values do not contain strings like "ctlxxx".</span></span> <span data-ttu-id="e6592-547">이 설정은 컨트롤의 *Clientidrowsuffix* 속성과 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-547">This setting works in conjunction with the *ClientIDRowSuffix* property of the control.</span></span> <span data-ttu-id="e6592-548">*Clientidrowsuffix* 속성을 데이터 필드의 이름으로 설정 하 고 해당 필드의 값이 생성 된 *ClientID* 값의 접미사로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-548">You set the *ClientIDRowSuffix* property to the name of a data field, and the value of that field is used as the suffix for the generated *ClientID* value.</span></span> <span data-ttu-id="e6592-549">일반적으로 데이터 레코드의 기본 키를 *Clientidrowsuffix* 값으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-549">Typically you would use the primary key of a data record as the *ClientIDRowSuffix* value.</span></span>
- <span data-ttu-id="e6592-550">*Inherit* –이 설정은 컨트롤의 기본 동작입니다. 컨트롤의 ID 생성이 부모와 동일 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-550">*Inherit* – This setting is the default behavior for controls; it specifies that a control's ID generation is the same as its parent.</span></span>

<span data-ttu-id="e6592-551">페이지 수준에서 *Clientidmode* 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-551">You can set the *ClientIDMode* property at the page level.</span></span> <span data-ttu-id="e6592-552">이는 현재 페이지의 모든 컨트롤에 대 한 기본 *Clientidmode* 값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-552">This defines the default *ClientIDMode* value for all controls in the current page.</span></span>

<span data-ttu-id="e6592-553">페이지 수준에서 기본 *clientidmode* 값은 *autoid*이 고, 컨트롤 수준의 기본 *Clientidmode* 값은 *상속*됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-553">The default *ClientIDMode* value at the page level is *AutoID*, and the default *ClientIDMode* value at the control level is *Inherit*.</span></span> <span data-ttu-id="e6592-554">따라서 코드의 아무 곳에서 나이 속성을 설정 하지 않으면 모든 컨트롤이 *자동 id* 알고리즘으로 기본 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-554">As a result, if you do not set this property anywhere in your code, all controls will default to the *AutoID* algorithm.</span></span>

<span data-ttu-id="e6592-555">다음 예제와 같이 *@ page* 지시문에서 페이지 수준 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-555">You set the page-level value in the *@ Page* directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample47.aspx)]

<span data-ttu-id="e6592-556">컴퓨터 (컴퓨터) 수준이 나 응용 프로그램 수준에서 구성 파일에 *Clientidmode* 값을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-556">You can also set the *ClientIDMode* value in the configuration file, either at the computer (machine) level or at the application level.</span></span> <span data-ttu-id="e6592-557">응용 프로그램의 모든 페이지에 있는 모든 컨트롤에 대 한 기본 *Clientidmode* 설정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-557">This defines the default *ClientIDMode* setting for all controls in all pages in the application.</span></span> <span data-ttu-id="e6592-558">컴퓨터 수준에서 값을 설정 하는 경우 해당 컴퓨터의 모든 웹 사이트에 대해 기본 *Clientidmode* 설정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-558">If you set the value at the computer level, it defines the default *ClientIDMode* setting for all Web sites on that computer.</span></span> <span data-ttu-id="e6592-559">다음 예에서는 구성 파일에 있는 *Cli\mode* 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-559">The following example shows the *ClientIDMode* setting in the configuration file:</span></span>

[!code-xml[Main](overview/samples/sample48.xml)]

<span data-ttu-id="e6592-560">앞에서 설명한 것 처럼 *ClientID* 속성의 값은 컨트롤의 부모에 대 한 명명 컨테이너에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-560">As noted earlier, the value of the *ClientID* property is derived from the naming container for a control's parent.</span></span> <span data-ttu-id="e6592-561">마스터 페이지를 사용 하는 경우와 같은 일부 시나리오에서 컨트롤은 다음과 같이 렌더링 된 HTML과 같은 Id로 끝날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-561">In some scenarios, such as when you are using master pages, controls can end up with IDs like those in the following rendered HTML:</span></span>

[!code-html[Main](overview/samples/sample49.html)]

<span data-ttu-id="e6592-562">*텍스트 상자* 컨트롤의 태그에 표시 된 *input* 요소는 페이지 (중첩 된 *ContentPlaceholder* 컨트롤)에 있는 두 개의 명명 컨테이너에만 포함 되어 있지만 마스터 페이지가 처리 되는 방식 때문에 최종 결과는 다음과 같은 컨트롤 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-562">Even though the *input* element shown in the markup (from a *TextBox* control) is only two naming containers deep in the page (the nested *ContentPlaceholder* controls), because of the way master pages are processed, the end result is a control ID like the following:</span></span>

[!code-console[Main](overview/samples/sample50.cmd)]

<span data-ttu-id="e6592-563">이 ID는 페이지에서 고유 하지만 대부분의 용도로는 불필요 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-563">This ID is guaranteed to be unique in the page, but is unnecessarily long for most purposes.</span></span> <span data-ttu-id="e6592-564">렌더링 된 ID의 길이를 줄이고 ID 생성 방법을 보다 세밀 하 게 제어 하려는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-564">Imagine that you want to reduce the length of the rendered ID, and to have more control over how the ID is generated.</span></span> <span data-ttu-id="e6592-565">예를 들어 "ctlxxx" 접두사를 제거 하려고 합니다. 이 작업을 수행 하는 가장 쉬운 방법은 다음 예제에 표시 된 대로 *Clientidmode* 속성을 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-565">(For example, you want to eliminate "ctlxxx" prefixes.) The easiest way to achieve this is by setting the *ClientIDMode* property as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample51.aspx)]

<span data-ttu-id="e6592-566">이 샘플에서 *Clientidmode* 속성은 가장 바깥쪽 *namingpanel* 요소에 대해 *Static* 으로 설정 되 고 내부 *Namingpanel* 요소에 대해 *예측 가능한* 로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-566">In this sample, the *ClientIDMode* property is set to *Static* for the outermost *NamingPanel* element, and set to *Predictable* for the inner *NamingControl* element.</span></span> <span data-ttu-id="e6592-567">이러한 설정은 다음 태그를 생성 합니다. 페이지의 나머지 부분과 마스터 페이지는 이전 예제와 동일한 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-567">These settings result in the following markup (the rest of the page and the master page is assumed to be the same as in the previous example):</span></span>

[!code-html[Main](overview/samples/sample52.html)]

<span data-ttu-id="e6592-568">*정적* 설정은 가장 바깥쪽 *namingpanel* 요소 내의 모든 컨트롤에 대 한 명명 계층을 다시 설정 하 고 생성 된 ID에서 *ContentPlaceHolder* 및 *MasterPage* id를 제거 하는 효과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-568">The *Static* setting has the effect of resetting the naming hierarchy for any controls inside the outermost *NamingPanel* element, and of eliminating the *ContentPlaceHolder* and *MasterPage* IDs from the generated ID.</span></span> <span data-ttu-id="e6592-569">렌더링 된 요소의 *name* 특성에는 영향을 주지 않으므로 일반적인 ASP.NET 기능은 이벤트, 뷰 상태 등에 대해 유지 됩니다. 명명 계층을 다시 설정 하는 부작용은 *Namingpanel* 요소의 태그를 다른 *ContentPlaceholder* 컨트롤로 이동 하더라도 렌더링 된 클라이언트 id는 동일 하 게 유지 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-569">(The *name* attribute of rendered elements is unaffected, so the normal ASP.NET functionality is retained for events, view state, and so on.) A side effect of resetting the naming hierarchy is that even if you move the markup for the *NamingPanel* elements to a different *ContentPlaceholder* control, the rendered client IDs remain the same.</span></span>

> [!NOTE]
> <span data-ttu-id="e6592-570">렌더링 된 컨트롤 Id가 고유한 지 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-570">Note It is up to you to make sure that the rendered control IDs are unique.</span></span> <span data-ttu-id="e6592-571">그렇지 않으면 클라이언트 *document.getelementbyid* 함수와 같은 개별 HTML 요소에 대해 고유 id가 필요한 모든 기능을 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-571">If they are not, it can break any functionality that requires unique IDs for individual HTML elements, such as the client *document.getElementById* function.</span></span>

#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a><span data-ttu-id="e6592-572">데이터 바인딩된 컨트롤에서 예측 가능한 클라이언트 Id 만들기</span><span class="sxs-lookup"><span data-stu-id="e6592-572">Creating Predictable Client IDs in Data-Bound Controls</span></span>

<span data-ttu-id="e6592-573">레거시 알고리즘을 통해 데이터 바인딩된 목록 컨트롤의 컨트롤에 대해 생성 되는 *ClientID* 값은 길고 예측 가능 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-573">The *ClientID* values that are generated for controls in a data-bound list control by the legacy algorithm can be long and are not really predictable.</span></span> <span data-ttu-id="e6592-574">이러한 Id가 생성 되는 방식을 보다 *효과적으로 제어 하는 데* 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-574">The *ClientIDMode* functionality can help you have more control over how these IDs are generated.</span></span>

<span data-ttu-id="e6592-575">다음 예제의 태그는 *ListView* 컨트롤을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-575">The markup in the following example includes a *ListView* control:</span></span>

[!code-aspx[Main](overview/samples/sample53.aspx)]

<span data-ttu-id="e6592-576">이전 예제에서 *Clientidmode* 및 *Rowclientidrowsuffix* 속성은 태그에 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-576">In the previous example, the *ClientIDMode* and *RowClientIDRowSuffix* properties are set in markup.</span></span> <span data-ttu-id="e6592-577">*Clientidrowsuffix* 속성은 데이터 바인딩된 컨트롤에만 사용할 수 있으며 해당 동작은 사용 하는 컨트롤에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-577">The *ClientIDRowSuffix* property can be used only in data-bound controls, and its behavior differs depending on which control you are using.</span></span> <span data-ttu-id="e6592-578">차이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-578">The differences are these:</span></span>

- <span data-ttu-id="e6592-579">*GridView* 컨트롤-런타임에 결합 되어 클라이언트 id를 만드는 데이터 소스에 있는 하나 이상의 열 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-579">*GridView* control — You can specify the name of one or more columns in the data source, which are combined at run time to create the client IDs.</span></span> <span data-ttu-id="e6592-580">예를 들어 *Rowclientidrowsuffix* 를 "ProductName, ProductId"로 설정 하면 렌더링 된 요소의 컨트롤 id 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-580">For example, if you set *RowClientIDRowSuffix* to "ProductName, ProductId", control IDs for rendered elements will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample54.cmd)]

- <span data-ttu-id="e6592-581">*ListView* 컨트롤-클라이언트 ID에 추가 되는 데이터 원본의 단일 열을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-581">*ListView* control — You can specify a single column in the data source that is appended to the client ID.</span></span> <span data-ttu-id="e6592-582">예를 들어, *Clientidrowsuffix* 를 "ProductName"로 설정 하면 렌더링 된 컨트롤 id의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-582">For example, if you set *ClientIDRowSuffix* to "ProductName", the rendered control IDs will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample55.cmd)]

- <span data-ttu-id="e6592-583">이 경우 후행 1은 현재 데이터 항목의 제품 ID에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-583">In this case the trailing 1 is derived from the product ID of the current data item.</span></span>

- <span data-ttu-id="e6592-584">*Repeater* 컨트롤-이 컨트롤은 *Clientidrowsuffix* 속성을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-584">*Repeater* control— This control does not support the *ClientIDRowSuffix* property.</span></span> <span data-ttu-id="e6592-585">*Repeater* 컨트롤에서 현재 행의 인덱스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-585">In a *Repeater* control, the index of the current row is used.</span></span> <span data-ttu-id="e6592-586">*Repeater* 컨트롤에서 ClientIDMode = "예측 가능"을 사용 하는 경우 다음과 같은 형식의 클라이언트 id가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-586">When you use ClientIDMode="Predictable" with a *Repeater* control, client IDs are generated that have the following format:</span></span>

- [!code-console[Main](overview/samples/sample56.cmd)]

- <span data-ttu-id="e6592-587">후행 0은 현재 행의 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-587">The trailing 0 is the index of the current row.</span></span>

<span data-ttu-id="e6592-588">*FormView* 및 *DetailsView* 컨트롤은 여러 행을 표시 하지 않으므로 *clientidrowsuffix* 속성을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-588">The *FormView* and *DetailsView* controls do not display multiple rows, so they do not support the *ClientIDRowSuffix* property.</span></span>

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a><span data-ttu-id="e6592-589">데이터 컨트롤에서 행 선택 유지</span><span class="sxs-lookup"><span data-stu-id="e6592-589">Persisting Row Selection in Data Controls</span></span>

<span data-ttu-id="e6592-590">*GridView* 및 *ListView* 컨트롤을 사용 하면 사용자가 행을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-590">The *GridView* and *ListView* controls can let users select a row.</span></span> <span data-ttu-id="e6592-591">이전 버전의 ASP.NET에서 선택은 페이지의 행 인덱스를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-591">In previous versions of ASP.NET, selection has been based on the row index on the page.</span></span> <span data-ttu-id="e6592-592">예를 들어 1 페이지에서 세 번째 항목을 선택한 다음 2 페이지로 이동 하면 해당 페이지의 세 번째 항목이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-592">For example, if you select the third item on page 1 and then move to page 2, the third item on that page is selected.</span></span>

<span data-ttu-id="e6592-593">지속형 선택은 처음에는 .NET Framework 3.5 s p 1의 Dynamic Data 프로젝트 에서만 지원 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-593">Persisted selection was initially supported only in Dynamic Data projects in the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="e6592-594">이 기능을 사용 하도록 설정 하면 현재 선택한 항목이 항목의 데이터 키를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-594">When this feature is enabled, the current selected item is based on the data key for the item.</span></span> <span data-ttu-id="e6592-595">즉, 1 페이지에서 세 번째 행을 선택 하 고 2 페이지로 이동 하면 2 페이지에서 아무 것도 선택 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-595">This means that if you select the third row on page 1 and move to page 2, nothing is selected on page 2.</span></span> <span data-ttu-id="e6592-596">1 페이지를 다시 이동 하면 세 번째 행도 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-596">When you move back to page 1, the third row is still selected.</span></span> <span data-ttu-id="e6592-597">이제 다음 예제와 같이 *Enablepersistedselection* 속성을 사용 하 여 모든 프로젝트에서 *GridView* 및 *ListView* 컨트롤에 대해 지속형 선택이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-597">Persisted selection is now supported for the *GridView* and *ListView* controls in all projects by using the *EnablePersistedSelection* property, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a><span data-ttu-id="e6592-598">ASP.NET Chart 컨트롤</span><span class="sxs-lookup"><span data-stu-id="e6592-598">ASP.NET Chart Control</span></span>

<span data-ttu-id="e6592-599">ASP.NET *차트* 컨트롤은 .NET Framework에서 데이터 시각화 제공 기능을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-599">The ASP.NET *Chart* control expands the data-visualization offerings in the .NET Framework.</span></span> <span data-ttu-id="e6592-600">*차트* 컨트롤을 사용 하 여 복잡 한 통계 또는 재무 분석을 위해 직관적이 고 시각적으로 멋진 차트가 있는 ASP.NET 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-600">Using the *Chart* control, you can create ASP.NET pages that have intuitive and visually compelling charts for complex statistical or financial analysis.</span></span> <span data-ttu-id="e6592-601">ASP.NET *Chart* 컨트롤은 .NET Framework 버전 3.5 SP1 릴리스에 추가 된 기능으로 도입 되었으며 .NET Framework 4 릴리스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-601">The ASP.NET *Chart* control was introduced as an add-on to the .NET Framework version 3.5 SP1 release and is part of the .NET Framework 4 release.</span></span>

<span data-ttu-id="e6592-602">컨트롤에는 다음과 같은 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-602">The control includes the following features:</span></span>

- <span data-ttu-id="e6592-603">35가지 개별 차트 종류</span><span class="sxs-lookup"><span data-stu-id="e6592-603">35 distinct chart types.</span></span>
- <span data-ttu-id="e6592-604">차트 영역, 제목, 범례 및 주석의 수에 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-604">An unlimited number of chart areas, titles, legends, and annotations.</span></span>
- <span data-ttu-id="e6592-605">모든 차트 요소에 대 한 다양 한 모양 설정</span><span class="sxs-lookup"><span data-stu-id="e6592-605">A wide variety of appearance settings for all chart elements.</span></span>
- <span data-ttu-id="e6592-606">대부분의 차트 종류에 대 한 3 차원 지원</span><span class="sxs-lookup"><span data-stu-id="e6592-606">3-D support for most chart types.</span></span>
- <span data-ttu-id="e6592-607">데이터 요소 주위에 자동으로 맞출 수 있는 스마트 데이터 레이블</span><span class="sxs-lookup"><span data-stu-id="e6592-607">Smart data labels that can automatically fit around data points.</span></span>
- <span data-ttu-id="e6592-608">줄무늬 선, 배율 구분선 및 로그 눈금 크기 조정.</span><span class="sxs-lookup"><span data-stu-id="e6592-608">Strip lines, scale breaks, and logarithmic scaling.</span></span>
- <span data-ttu-id="e6592-609">데이터 분석 및 변환을 위한 50개가 넘는 재무 및 통계 수식</span><span class="sxs-lookup"><span data-stu-id="e6592-609">More than 50 financial and statistical formulas for data analysis and transformation.</span></span>
- <span data-ttu-id="e6592-610">차트 데이터의 단순 바인딩 및 조작</span><span class="sxs-lookup"><span data-stu-id="e6592-610">Simple binding and manipulation of chart data.</span></span>
- <span data-ttu-id="e6592-611">날짜, 시간 및 통화와 같은 공통 데이터 형식에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="e6592-611">Support for common data formats such as dates, times, and currency.</span></span>
- <span data-ttu-id="e6592-612">Ajax를 사용 하 여 클라이언트 클릭 이벤트를 비롯 한 대화형 작업 및 이벤트 구동 사용자 지정 지원.</span><span class="sxs-lookup"><span data-stu-id="e6592-612">Support for interactivity and event-driven customization, including client click events using Ajax.</span></span>
- <span data-ttu-id="e6592-613">상태 관리.</span><span class="sxs-lookup"><span data-stu-id="e6592-613">State management.</span></span>
- <span data-ttu-id="e6592-614">이진 스트리밍</span><span class="sxs-lookup"><span data-stu-id="e6592-614">Binary streaming.</span></span>

<span data-ttu-id="e6592-615">다음 그림에서는 ASP.NET 차트 컨트롤에 의해 생성 되는 재무 차트의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-615">The following figures show examples of financial charts that are produced by the ASP.NET Chart control.</span></span>

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

<span data-ttu-id="e6592-616">그림 2: ASP.NET Chart 컨트롤 예제</span><span class="sxs-lookup"><span data-stu-id="e6592-616">Figure 2: ASP.NET Chart control examples</span></span>

<span data-ttu-id="e6592-617">ASP.NET 차트 컨트롤을 사용 하는 방법에 대 한 추가 예제를 보려면 MSDN 웹 사이트의 [Microsoft Chart Controls 용 샘플 환경](https://go.microsoft.com/fwlink/?LinkId=128300) 페이지에서 샘플 코드를 다운로드 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e6592-617">For more examples of how to use the ASP.NET Chart control, download the sample code on the [Samples Environment for Microsoft Chart Controls](https://go.microsoft.com/fwlink/?LinkId=128300) page on the MSDN Web site.</span></span> <span data-ttu-id="e6592-618">커뮤니티 콘텐츠의 샘플은 [차트 컨트롤 포럼](https://go.microsoft.com/fwlink/?LinkId=128713)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-618">You can find more samples of community content at the [Chart Control Forum](https://go.microsoft.com/fwlink/?LinkId=128713).</span></span>

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a><span data-ttu-id="e6592-619">ASP.NET 페이지에 차트 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="e6592-619">Adding the Chart Control to an ASP.NET Page</span></span>

<span data-ttu-id="e6592-620">다음 예제에서는 태그를 사용 하 여 ASP.NET 페이지에 *차트* 컨트롤을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-620">The following example shows how to add a *Chart* control to an ASP.NET page by using markup.</span></span> <span data-ttu-id="e6592-621">이 예제에서 *차트* 컨트롤은 정적 데이터 요소에 대 한 세로 막대형 차트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-621">In the example, the *Chart* control produces a column chart for static data points.</span></span>

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a><span data-ttu-id="e6592-622">3 차원 차트 사용</span><span class="sxs-lookup"><span data-stu-id="e6592-622">Using 3-D Charts</span></span>

<span data-ttu-id="e6592-623">*차트* 컨트롤에는 차트 영역의 특징을 정의 하는 지 수 개체를 포함할 수 있는 *Chartareas* *컬렉션이 포함 되어* 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-623">The *Chart* control contains a *ChartAreas* collection, which can contain *ChartArea* objects that define characteristics of chart areas.</span></span> <span data-ttu-id="e6592-624">예를 들어 차트 영역에 3 차원을 사용 하려면 다음 예제와 같이 *있는 area3dstyle* 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-624">For example, to use 3-D for a chart area, use the *Area3DStyle* property as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample59.aspx)]

<span data-ttu-id="e6592-625">아래 그림에서는 *가로 막대형* 차트 종류의 4 가지 계열을 포함 하는 3 차원 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-625">The figure below shows a 3-D chart with four series of the *Bar* chart type.</span></span>

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

<span data-ttu-id="e6592-626">그림 3:3-D 가로 막대형 차트</span><span class="sxs-lookup"><span data-stu-id="e6592-626">Figure 3: 3-D Bar Chart</span></span>

#### <a name="using-scale-breaks-and-logarithmic-scales"></a><span data-ttu-id="e6592-627">배율 구분선 및 로그 눈금 간격 사용</span><span class="sxs-lookup"><span data-stu-id="e6592-627">Using Scale Breaks and Logarithmic Scales</span></span>

<span data-ttu-id="e6592-628">배율 구분선 및 로그 눈금 크기는 차트에 복잡성을 추가 하는 두 가지 추가 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-628">Scale breaks and logarithmic scales are two additional ways to add sophistication to the chart.</span></span> <span data-ttu-id="e6592-629">이러한 기능은 차트 영역의 각 축에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-629">These features are specific to each axis in a chart area.</span></span> <span data-ttu-id="e6592-630">예를 들어 차트 영역의 기본 Y 축에서 이러한 기능을 사용 하려면 *AxisY* 및 *ScaleBreakStyle* *속성을 영역 개체에* 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-630">For example, to use these features on the primary Y axis of a chart area, use the *AxisY.IsLogarithmic* and *ScaleBreakStyle* properties in a *ChartArea* object.</span></span> <span data-ttu-id="e6592-631">다음 코드 조각에서는 기본 Y 축에서 배율 구분선을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-631">The following snippet shows how to use scale breaks on the primary Y axis.</span></span>

[!code-aspx[Main](overview/samples/sample60.aspx)]

<span data-ttu-id="e6592-632">아래 그림은 배율 구분선이 설정 된 Y 축을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-632">The figure below shows the Y axis with scale breaks enabled.</span></span>

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

<span data-ttu-id="e6592-633">그림 4: 배율 구분선</span><span class="sxs-lookup"><span data-stu-id="e6592-633">Figure 4: Scale Breaks</span></span>

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a><span data-ttu-id="e6592-634">QueryExtender 컨트롤을 사용 하 여 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="e6592-634">Filtering Data with the QueryExtender Control</span></span>

<span data-ttu-id="e6592-635">데이터 기반 웹 페이지를 만드는 개발자를 위한 매우 일반적인 작업은 데이터를 필터링 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-635">A very common task for developers who create data-driven Web pages is to filter data.</span></span> <span data-ttu-id="e6592-636">일반적으로 데이터 소스 컨트롤의 *Where* 절을 빌드하여 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-636">This traditionally has been performed by building *Where* clauses in data source controls.</span></span> <span data-ttu-id="e6592-637">이 방법은 복잡할 수 있으며, 경우에 따라 *Where* 구문을 사용 하 여 기본 데이터베이스의 전체 기능을 활용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-637">This approach can be complicated, and in some cases the *Where* syntax does not let you take advantage of the full functionality of the underlying database.</span></span>

<span data-ttu-id="e6592-638">더 쉽게 필터링 하기 위해 ASP.NET 4에서 새 *Queryextender* 컨트롤이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-638">To make filtering easier, a new *QueryExtender* control has been added in ASP.NET 4.</span></span> <span data-ttu-id="e6592-639">이러한 컨트롤에서 반환 된 데이터를 필터링 하기 위해이 컨트롤을 *EntityDataSource* 또는 *LinqDataSource* 컨트롤에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-639">This control can be added to *EntityDataSource* or *LinqDataSource* controls in order to filter the data returned by these controls.</span></span> <span data-ttu-id="e6592-640">*Queryextender* 컨트롤이 LINQ를 사용 하기 때문에 데이터가 페이지에 전송 되기 전에 데이터베이스 서버에 필터가 적용 되므로 작업이 매우 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-640">Because the *QueryExtender* control relies on LINQ, the filter is applied on the database server before the data is sent to the page, which results in very efficient operations.</span></span>

<span data-ttu-id="e6592-641">*Queryextender* 컨트롤은 다양 한 필터 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-641">The *QueryExtender* control supports a variety of filter options.</span></span> <span data-ttu-id="e6592-642">다음 섹션에서는 이러한 옵션에 대해 설명 하 고이를 사용 하는 방법에 대 한 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-642">The following sections describe these options and provide examples of how to use them.</span></span>

#### <a name="search"></a><span data-ttu-id="e6592-643">검색</span><span class="sxs-lookup"><span data-stu-id="e6592-643">Search</span></span>

<span data-ttu-id="e6592-644">검색 옵션의 경우 *Queryextender* 컨트롤은 지정 된 필드에서 검색을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-644">For the search option, the *QueryExtender* control performs a search in specified fields.</span></span> <span data-ttu-id="e6592-645">다음 예제에서 컨트롤은 TextBoxSearch 컨트롤에 입력 된 텍스트를 사용 하 여 `ProductName`에서 해당 콘텐츠를 검색 하 고 *LinqDataSource* 컨트롤에서 반환 된 데이터의 `Supplier.CompanyName` 열을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-645">In the following example, the control uses the text that is entered in the TextBoxSearch control and searches for its contents in the `ProductName` and `Supplier.CompanyName` columns in the data that is returned from the *LinqDataSource* control.</span></span>

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a><span data-ttu-id="e6592-646">범위</span><span class="sxs-lookup"><span data-stu-id="e6592-646">Range</span></span>

<span data-ttu-id="e6592-647">범위 옵션은 검색 옵션과 비슷하지만 범위를 정의 하는 값 쌍을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-647">The range option is similar to the search option, but specifies a pair of values to define the range.</span></span> <span data-ttu-id="e6592-648">다음 예제에서 *Queryextender* 컨트롤은 *LinqDataSource* 컨트롤에서 반환 된 데이터의 `UnitPrice` 열을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-648">In the following example, the *QueryExtender* control searches the `UnitPrice` column in the data returned from the *LinqDataSource* control.</span></span> <span data-ttu-id="e6592-649">페이지의 TextBoxFrom 및 TextBoxTo 컨트롤에서 범위를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-649">The range is read from the TextBoxFrom and TextBoxTo controls on the page.</span></span>

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a><span data-ttu-id="e6592-650">PropertyExpression</span><span class="sxs-lookup"><span data-stu-id="e6592-650">PropertyExpression</span></span>

<span data-ttu-id="e6592-651">속성 식 옵션을 사용 하 여 속성 값에 대 한 비교를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-651">The property expression option lets you define a comparison to a property value.</span></span> <span data-ttu-id="e6592-652">식이 *true*로 평가 되 면 검사 중인 데이터가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-652">If the expression evaluates to *true*, the data that is being examined is returned.</span></span> <span data-ttu-id="e6592-653">다음 예제에서 *Queryextender* 컨트롤은 `Discontinued` 열의 데이터를 페이지의 CheckBoxDiscontinued 컨트롤 값과 비교 하 여 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-653">In the following example, the *QueryExtender* control filters data by comparing the data in the `Discontinued` column to the value from the CheckBoxDiscontinued control on the page.</span></span>

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a><span data-ttu-id="e6592-654">CustomExpression</span><span class="sxs-lookup"><span data-stu-id="e6592-654">CustomExpression</span></span>

<span data-ttu-id="e6592-655">마지막으로 *Queryextender* 컨트롤에 사용할 사용자 지정 식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-655">Finally, you can specify a custom expression to use with the *QueryExtender* control.</span></span> <span data-ttu-id="e6592-656">이 옵션을 사용 하면 사용자 지정 필터 논리를 정의 하는 페이지에서 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-656">This option lets you call a function in the page that defines custom filter logic.</span></span> <span data-ttu-id="e6592-657">다음 예제에서는 *Queryextender* 컨트롤에서 사용자 지정 식을 선언적으로 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-657">The following example shows how to declaratively specify a custom expression in the *QueryExtender* control.</span></span>

[!code-aspx[Main](overview/samples/sample64.aspx)]

<span data-ttu-id="e6592-658">다음 예제에서는 *Queryextender* 컨트롤에 의해 호출 되는 사용자 지정 함수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-658">The following example shows the custom function that is invoked by the *QueryExtender* control.</span></span> <span data-ttu-id="e6592-659">이 경우 *Where* 절을 포함 하는 데이터베이스 쿼리를 사용 하는 대신 코드는 LINQ 쿼리를 사용 하 여 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-659">In this case, instead of using a database query that includes a *Where* clause, the code uses a LINQ query to filter the data.</span></span>

[!code-csharp[Main](overview/samples/sample65.cs)]

<span data-ttu-id="e6592-660">이 예에서는 한 번에 하나의 식만 *Queryextender* 컨트롤에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-660">These examples show only one expression being used in the *QueryExtender* control at a time.</span></span> <span data-ttu-id="e6592-661">그러나 *Queryextender* 컨트롤 안에 여러 개의 식을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-661">However, you can include multiple expressions inside the *QueryExtender* control.</span></span>

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a><span data-ttu-id="e6592-662">Html로 인코딩된 코드 식</span><span class="sxs-lookup"><span data-stu-id="e6592-662">Html Encoded Code Expressions</span></span>

<span data-ttu-id="e6592-663">일부 ASP.NET 사이트 (특히 ASP.NET MVC)는 `<%`= `expression %>` 구문 (종종 "code 너 깃" 이라고 함)을 사용 하 여 응답에 텍스트를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-663">Some ASP.NET sites (especially with ASP.NET MVC) rely heavily on using `<%`= `expression %>` syntax (often called "code nuggets") to write some text to the response.</span></span> <span data-ttu-id="e6592-664">코드 식을 사용 하는 경우 텍스트를 HTML로 인코딩하는 것은 쉽지 않습니다. 텍스트를 사용자 입력에서 가져온 경우에는 페이지를 XSS (교차 사이트 스크립팅) 공격에 노출 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-664">When you use code expressions, it is easy to forget to HTML-encode the text, If the text comes from user input, it can leave pages open to an XSS (Cross Site Scripting) attack.</span></span>

<span data-ttu-id="e6592-665">ASP.NET 4에는 다음과 같은 코드 식에 대 한 새로운 구문이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-665">ASP.NET 4 introduces the following new syntax for code expressions:</span></span>

[!code-aspx[Main](overview/samples/sample66.aspx)]

<span data-ttu-id="e6592-666">이 구문은 응답에 쓸 때 기본적으로 HTML 인코딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-666">This syntax uses HTML encoding by default when writing to the response.</span></span> <span data-ttu-id="e6592-667">이 새 식은 다음과 같이 효과적으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-667">This new expression effectively translates to the following:</span></span>

[!code-aspx[Main](overview/samples/sample67.aspx)]

<span data-ttu-id="e6592-668">예를 들어 &lt;%: Request ["UserInput"]%&gt;는 *request ["userinput"]* 의 값에서 HTML 인코딩을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-668">For example, &lt;%: Request["UserInput"] %&gt; performs HTML encoding on the value of *Request["UserInput"]*.</span></span>

<span data-ttu-id="e6592-669">이 기능의 목표는 사용할 모든 단계를 강제로 결정 하지 않도록 이전 구문의 모든 인스턴스를 새 구문으로 바꿀 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-669">The goal of this feature is to make it possible to replace all instances of the old syntax with the new syntax so that you are not forced to decide at every step which one to use.</span></span> <span data-ttu-id="e6592-670">그러나 출력 되는 텍스트가 HTML 이거나 이미 인코딩된 경우가 있습니다 .이 경우에는 이중 인코딩이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-670">However, there are cases in which the text being output is meant to be HTML or is already encoded, in which case this could lead to double encoding.</span></span>

<span data-ttu-id="e6592-671">이러한 경우, ASP.NET 4에서는 구체적인 구현인 *Htmlstring*과 함께 *IHtmlString*새 인터페이스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-671">For those cases, ASP.NET 4 introduces a new interface, *IHtmlString*, along with a concrete implementation, *HtmlString*.</span></span> <span data-ttu-id="e6592-672">이러한 형식의 인스턴스를 사용 하면 반환 값이 HTML로 표시 하기 위해 이미 올바르게 인코딩 되었는지 아니면 검사 되었는지 확인할 수 있으며, 따라서이 값은 다시 HTML로 인코딩되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-672">Instances of these types let you indicate that the return value is already properly encoded (or otherwise examined) for displaying as HTML, and that therefore the value should not be HTML-encoded again.</span></span> <span data-ttu-id="e6592-673">예를 들어, 다음은 HTML로 인코딩되지 않고 인코딩되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-673">For example, the following should not be (and is not) HTML encoded:</span></span>

[!code-aspx[Main](overview/samples/sample68.aspx)]

<span data-ttu-id="e6592-674">ASP.NET MVC 2 도우미 메서드는 이중 인코딩되지 않고 ASP.NET 4를 실행 하는 경우에만이 새 구문에서 사용할 수 있도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-674">ASP.NET MVC 2 helper methods have been updated to work with this new syntax so that they are not double encoded, but only when you are running ASP.NET 4.</span></span> <span data-ttu-id="e6592-675">ASP.NET 3.5 s p 1을 사용 하 여 응용 프로그램을 실행 하는 경우이 새로운 구문이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-675">This new syntax does not work when you run an application using ASP.NET 3.5 SP1.</span></span>

<span data-ttu-id="e6592-676">이것은 XSS 공격 으로부터 보호를 보장 하지 않는다는 점에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e6592-676">Keep in mind that this does not guarantee protection from XSS attacks.</span></span> <span data-ttu-id="e6592-677">예를 들어 따옴표에 포함 되지 않은 특성 값을 사용 하는 HTML에는 여전히 취약 한 사용자 입력이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-677">For example, HTML that uses attribute values that are not in quotation marks can contain user input that is still susceptible.</span></span> <span data-ttu-id="e6592-678">ASP.NET 컨트롤 및 ASP.NET MVC 도우미의 출력에는 항상 따옴표 안에 특성 값이 포함 되며이는 권장 되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-678">Note that the output of ASP.NET controls and ASP.NET MVC helpers always includes attribute values in quotation marks, which is the recommended approach.</span></span>

<span data-ttu-id="e6592-679">마찬가지로이 구문은 사용자 입력을 기반으로 JavaScript 문자열을 만드는 경우와 같이 JavaScript 인코딩을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-679">Likewise, this syntax does not perform JavaScript encoding, such as when you create a JavaScript string based on user input.</span></span>

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a><span data-ttu-id="e6592-680">프로젝트 템플릿 변경</span><span class="sxs-lookup"><span data-stu-id="e6592-680">Project Template Changes</span></span>

<span data-ttu-id="e6592-681">이전 버전의 ASP.NET에서 Visual Studio를 사용 하 여 새 웹 사이트 프로젝트 또는 웹 응용 프로그램 프로젝트를 만드는 경우 결과 프로젝트에는 다음 그림과 같이 default.aspx 페이지, 기본 `Web.config` 파일 및 `App_Data` 폴더만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-681">In earlier versions of ASP.NET, when you use Visual Studio to create a new Web Site project or Web Application project, the resulting projects contain only a Default.aspx page, a default `Web.config` file, and the `App_Data` folder, as shown in the following illustration:</span></span>

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

<span data-ttu-id="e6592-682">Visual Studio는 다음 그림에 표시 된 것 처럼 파일을 전혀 포함 하지 않는 빈 웹 사이트 프로젝트 형식을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-682">Visual Studio also supports an Empty Web Site project type, which contains no files at all, as shown in the following figure:</span></span>

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

<span data-ttu-id="e6592-683">그 결과, 초보자의 경우 프로덕션 웹 응용 프로그램을 빌드하는 방법에 대 한 지침이 거의 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-683">The result is that for the beginner, there is very little guidance on how to build a production Web application.</span></span> <span data-ttu-id="e6592-684">따라서 ASP.NET 4에는 빈 웹 응용 프로그램 프로젝트용과 웹 응용 프로그램 및 웹 사이트 프로젝트에 각각 하나씩 세 개의 새 템플릿이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-684">Therefore, ASP.NET 4 introduces three new templates, one for an empty Web application project, and one each for a Web Application and Web Site project.</span></span>

#### <a name="empty-web-application-template"></a><span data-ttu-id="e6592-685">빈 웹 응용 프로그램 템플릿</span><span class="sxs-lookup"><span data-stu-id="e6592-685">Empty Web Application Template</span></span>

<span data-ttu-id="e6592-686">이름에서 알 수 있듯이, 빈 웹 응용 프로그램 템플릿은 제거 된 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-686">As the name suggests, the Empty Web Application template is a stripped-down Web Application project.</span></span> <span data-ttu-id="e6592-687">다음 그림에 표시 된 것 처럼 Visual Studio 새 프로젝트 대화 상자에서이 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-687">You select this project template from the Visual Studio New Project dialog box, as shown in the following figure:</span></span>

[![](overview/_static/image7.png)](overview/_static/image6.png)

<span data-ttu-id="e6592-688">([전체 크기 이미지를 보려면 클릭](overview/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="e6592-688">([Click to view full-size image](overview/_static/image8.png))</span></span>

<span data-ttu-id="e6592-689">빈 ASP.NET 웹 응용 프로그램을 만들면 Visual Studio에서 다음과 같은 폴더 레이아웃을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-689">When you create an Empty ASP.NET Web Application, Visual Studio creates the following folder layout:</span></span>

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

<span data-ttu-id="e6592-690">이는 한 가지 예외를 제외 하 고 이전 버전의 ASP.NET에서 가져온 빈 웹 사이트 레이아웃과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-690">This is similar to the Empty Web Site layout from earlier versions of ASP.NET, with one exception.</span></span> <span data-ttu-id="e6592-691">Visual Studio 2010에서 빈 웹 응용 프로그램 및 빈 웹 사이트 프로젝트에는 Visual Studio에서 프로젝트를 대상으로 하는 프레임 워크를 식별 하는 데 사용 하는 정보가 포함 된 다음과 같은 최소 `Web.config` 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-691">In Visual Studio 2010, Empty Web Application and Empty Web Site projects contain the following minimal `Web.config` file that contains information used by Visual Studio to identify the framework that the project is targeting:</span></span>

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

<span data-ttu-id="e6592-692">이 *Targetframework* 속성이 없는 경우 Visual Studio는 이전 응용 프로그램을 열 때 호환성을 유지 하기 위해 기본적으로 .NET Framework 2.0를 대상으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-692">Without this *targetFramework* property, Visual Studio defaults to targeting the .NET Framework 2.0 in order to preserve compatibility when opening older applications.</span></span>

#### <a name="web-application-and-web-site-project-templates"></a><span data-ttu-id="e6592-693">웹 응용 프로그램 및 웹 사이트 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="e6592-693">Web Application and Web Site Project Templates</span></span>

<span data-ttu-id="e6592-694">Visual Studio 2010와 함께 제공 되는 다른 두 개의 새 프로젝트 템플릿에는 주요 변경 내용이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-694">The other two new project templates that are shipped with Visual Studio 2010 contain major changes.</span></span> <span data-ttu-id="e6592-695">다음 그림은 새 웹 응용 프로그램 프로젝트를 만들 때 생성 되는 프로젝트 레이아웃을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-695">The following figure shows the project layout that is created when you create a new Web Application project.</span></span> <span data-ttu-id="e6592-696">웹 사이트 프로젝트의 레이아웃은 거의 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-696">(The layout for a Web Site project is virtually identical.)</span></span>

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

<span data-ttu-id="e6592-697">프로젝트에는 이전 버전에서 만들지 않은 많은 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-697">The project includes a number of files that were not created in earlier versions.</span></span> <span data-ttu-id="e6592-698">또한 새 웹 응용 프로그램 프로젝트는 새로운 응용 프로그램에 대 한 액세스 보안을 신속 하 게 시작할 수 있도록 하는 기본 멤버 자격 기능으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-698">In addition, the new Web Application project is configured with basic membership functionality, which lets you quickly get started in securing access to the new application.</span></span> <span data-ttu-id="e6592-699">이러한 포함으로 인해 새 프로젝트의 `Web.config` 파일에는 멤버 자격, 역할 및 프로필을 구성 하는 데 사용 되는 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-699">Because of this inclusion, the `Web.config` file for the new project includes entries that are used to configure membership, roles, and profiles.</span></span> <span data-ttu-id="e6592-700">다음 예제에서는 새 웹 응용 프로그램 프로젝트에 대 한 `Web.config` 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-700">The following example shows the `Web.config` file for a new Web Application project.</span></span> <span data-ttu-id="e6592-701">(이 경우 *roleManager* 은 사용 하지 않도록 설정 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="e6592-701">(In this case, *roleManager* is disabled.)</span></span>

[![](overview/_static/image13.png)](overview/_static/image12.png)

<span data-ttu-id="e6592-702">([전체 크기 이미지를 보려면 클릭](overview/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="e6592-702">([Click to view full-size image](overview/_static/image14.png))</span></span>

<span data-ttu-id="e6592-703">또한이 프로젝트는 `Account` 디렉터리에 두 번째 `Web.config` 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-703">The project also contains a second `Web.config` file in the `Account` directory.</span></span> <span data-ttu-id="e6592-704">두 번째 구성 파일은 로그인 하지 않은 사용자를 위해 ChangePassword 페이지에 대 한 액세스를 보호 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-704">The second configuration file provides a way to secure access to the ChangePassword.aspx page for non-logged in users.</span></span> <span data-ttu-id="e6592-705">다음 예에서는 두 번째 `Web.config` 파일의 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-705">The following example shows the contents of the second `Web.config` file.</span></span>

![](overview/_static/image15.png)

<span data-ttu-id="e6592-706">새 프로젝트 템플릿에는 기본적으로 만들어진 페이지에도 이전 버전 보다 더 많은 콘텐츠가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-706">The pages created by default in the new project templates also contain more content than in previous versions.</span></span> <span data-ttu-id="e6592-707">프로젝트에는 기본 마스터 페이지와 CSS 파일이 포함 되어 있으며 기본 페이지 (default.aspx)는 기본적으로 마스터 페이지를 사용 하도록 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-707">The project contains a default master page and CSS file, and the default page (Default.aspx) is configured to use the master page by default.</span></span> <span data-ttu-id="e6592-708">따라서 웹 응용 프로그램 또는 웹 사이트를 처음 실행 하는 경우 기본 (홈) 페이지가 이미 작동 하 고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-708">The result is that when you run the Web application or Web site for the first time, the default (home) page is already functional.</span></span> <span data-ttu-id="e6592-709">실제로 새 MVC 응용 프로그램을 시작할 때 표시 되는 기본 페이지와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-709">In fact, it is similar to the default page you see when you start up a new MVC application.</span></span>

[![](overview/_static/image17.png)](overview/_static/image16.png)

<span data-ttu-id="e6592-710">([전체 크기 이미지를 보려면 클릭](overview/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="e6592-710">([Click to view full-size image](overview/_static/image18.png))</span></span>

<span data-ttu-id="e6592-711">이러한 프로젝트 템플릿에 대 한 이러한 변경의 목적은 새 웹 응용 프로그램 빌드를 시작 하는 방법에 대 한 지침을 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-711">The intention of these changes to the project templates is to provide guidance on how to start building a new Web application.</span></span> <span data-ttu-id="e6592-712">의미 체계가 올바르고 엄격한 XHTML 1.0 호환 태그와 CSS를 사용 하 여 지정 된 레이아웃을 사용 하 여 템플릿의 페이지는 ASP.NET 4 웹 응용 프로그램을 빌드하기 위한 모범 사례를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-712">With semantically correct, strict XHTML 1.0-compliant markup and with layout that is specified using CSS, the pages in the templates represent best practices for building ASP.NET 4 Web applications.</span></span> <span data-ttu-id="e6592-713">기본 페이지에는 쉽게 사용자 지정할 수 있는 2 열 레이아웃도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-713">The default pages also have a two-column layout that you can easily customize.</span></span>

<span data-ttu-id="e6592-714">예를 들어, 새 웹 응용 프로그램의 경우 일부 색을 변경 하 고 My ASP.NET 응용 프로그램 로고 대신 회사 로고를 삽입 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-714">For example, imagine that for a new Web Application you want to change some of the colors and insert your company logo in place of the My ASP.NET Application logo.</span></span> <span data-ttu-id="e6592-715">이렇게 하려면 로고 이미지를 저장 하는 `Content` 아래에 새 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-715">To do this, you create a new directory under `Content` to store your logo image:</span></span>

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

<span data-ttu-id="e6592-716">페이지에 이미지를 추가 하려면 다음 예제와 같이 `Site.Master` 파일을 열고 내 ASP.NET 응용 프로그램 텍스트가 정의 된 위치를 찾은 다음 *src* 특성이 새 로고 이미지로 설정 된 *image* 요소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-716">To add the image to the page, you then open the `Site.Master` file, find where the My ASP.NET Application text is defined, and replace it with an *image* element whose *src* attribute is set to the new logo image, as in the following example:</span></span>

[![](overview/_static/image21.png)](overview/_static/image20.png)

<span data-ttu-id="e6592-717">([전체 크기 이미지를 보려면 클릭](overview/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="e6592-717">([Click to view full-size image](overview/_static/image22.png))</span></span>

<span data-ttu-id="e6592-718">그런 다음 사이트별로 이동 하 고 CSS 클래스 정의를 수정 하 여 페이지의 배경색 뿐만 아니라 헤더의 배경색을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-718">You can then go into the Site.css file and modify CSS class definitions to change the background color of the page as well as that of the header.</span></span>

<span data-ttu-id="e6592-719">이러한 변경의 결과로 사용자 지정 된 홈 페이지를 매우 적은 노력으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-719">The result of these changes is that you can display a customized home page with very little effort:</span></span>

[![](overview/_static/image24.png)](overview/_static/image23.png)

<span data-ttu-id="e6592-720">([전체 크기 이미지를 보려면 클릭](overview/_static/image25.png))</span><span class="sxs-lookup"><span data-stu-id="e6592-720">([Click to view full-size image](overview/_static/image25.png))</span></span>

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a><span data-ttu-id="e6592-721">CSS 개선 사항</span><span class="sxs-lookup"><span data-stu-id="e6592-721">CSS Improvements</span></span>

<span data-ttu-id="e6592-722">ASP.NET 4의 주요 작업 영역 중 하나는 최신 HTML 표준과 호환 되는 HTML을 렌더링 하는 데 도움을 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-722">One of the major areas of work in ASP.NET 4 has been to help render HTML that is compliant with the latest HTML standards.</span></span> <span data-ttu-id="e6592-723">여기에는 ASP.NET 웹 서버 컨트롤에서 CSS 스타일을 사용 하는 방법이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-723">This includes changes to how ASP.NET Web server controls use CSS styles.</span></span>

#### <a name="compatibility-setting-for-rendering"></a><span data-ttu-id="e6592-724">렌더링에 대 한 호환성 설정</span><span class="sxs-lookup"><span data-stu-id="e6592-724">Compatibility Setting for Rendering</span></span>

<span data-ttu-id="e6592-725">기본적으로 웹 응용 프로그램 또는 웹 사이트가 .NET Framework 4를 대상으로 하는 경우 *pages* 요소의 *controlRenderingCompatibilityVersion* 특성은 "4.0"로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-725">By default, when a Web application or Web site targets the .NET Framework 4, the *controlRenderingCompatibilityVersion* attribute of the *pages* element is set to "4.0".</span></span> <span data-ttu-id="e6592-726">이 요소는 컴퓨터 수준 `Web.config` 파일에 정의 되며 기본적으로 모든 ASP.NET 4 응용 프로그램에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-726">This element is defined in the machine-level `Web.config` file and by default applies to all ASP.NET 4 applications:</span></span>

[!code-xml[Main](overview/samples/sample69.xml)]

<span data-ttu-id="e6592-727">*ControlRenderingCompatibility* 에 대 한 값은 이후 릴리스에서 새 버전 정의를 잠재적으로 허용 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-727">The value for *controlRenderingCompatibility* is a string, which allows potential new version definitions in future releases.</span></span> <span data-ttu-id="e6592-728">현재 릴리스에서이 속성에 대해 지원 되는 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-728">In the current release, the following values are supported for this property:</span></span>

- <span data-ttu-id="e6592-729">"3.5".</span><span class="sxs-lookup"><span data-stu-id="e6592-729">"3.5".</span></span> <span data-ttu-id="e6592-730">이 설정은 레거시 렌더링 및 태그를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-730">This setting indicates legacy rendering and markup.</span></span> <span data-ttu-id="e6592-731">컨트롤에 의해 렌더링 된 태그는 100% 이전 버전과 호환 되며 *Xhtmlconformance* 속성의 설정이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-731">Markup rendered by controls is 100% backward compatible, and the setting of the *xhtmlConformance* property is honored.</span></span>
- <span data-ttu-id="e6592-732">"4.0".</span><span class="sxs-lookup"><span data-stu-id="e6592-732">"4.0".</span></span> <span data-ttu-id="e6592-733">속성에이 설정이 있으면 ASP.NET 웹 서버 컨트롤은 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-733">If the property has this setting, ASP.NET Web server controls do the following:</span></span>
- <span data-ttu-id="e6592-734">*Xhtmlconformance* 속성은 항상 "Strict"로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-734">The *xhtmlConformance* property is always treated as "Strict".</span></span> <span data-ttu-id="e6592-735">따라서 컨트롤은 XHTML 1.0 Strict 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-735">As a result, controls render XHTML 1.0 Strict markup.</span></span>
- <span data-ttu-id="e6592-736">비 입력 컨트롤을 사용 하지 않도록 설정 하면 더 이상 잘못 된 스타일이 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-736">Disabling non-input controls no longer renders invalid styles.</span></span>
- <span data-ttu-id="e6592-737">숨겨진 필드 주변의 *div* 요소는 이제 사용자가 만든 CSS 규칙을 방해 하지 않도록 스타일이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-737">*div* elements around hidden fields are now styled so they do not interfere with user-created CSS rules.</span></span>
- <span data-ttu-id="e6592-738">메뉴 컨트롤은 의미 체계가 올바르고 내게 필요한 옵션 지침을 준수 하는 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-738">Menu controls render markup that is semantically correct and compliant with accessibility guidelines.</span></span>
- <span data-ttu-id="e6592-739">유효성 검사 컨트롤은 인라인 스타일을 렌더링 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-739">Validation controls do not render inline styles.</span></span>
- <span data-ttu-id="e6592-740">이전에 렌더링 된 border = "0" (ASP.NET *Table* 컨트롤에서 파생 된 컨트롤 및 ASP.NET *Image* 컨트롤에서 파생 된 컨트롤)은 더 이상이 특성을 렌더링 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-740">Controls that previously rendered border="0" (controls that derive from the ASP.NET *Table* control, and the ASP.NET *Image* control) no longer render this attribute.</span></span>

#### <a name="disabling-controls"></a><span data-ttu-id="e6592-741">컨트롤 비활성화</span><span class="sxs-lookup"><span data-stu-id="e6592-741">Disabling Controls</span></span>

<span data-ttu-id="e6592-742">ASP.NET 3.5 SP1 및 이전 버전에서 프레임 워크는 *Enabled* 속성이 *false*로 설정 된 모든 컨트롤에 대해 HTML 태그에서 *disabled* 특성을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-742">In ASP.NET 3.5 SP1 and earlier versions, the framework renders the *disabled* attribute in the HTML markup for any control whose *Enabled* property set to *false*.</span></span> <span data-ttu-id="e6592-743">그러나 HTML 4.01 사양에 따라 *입력* 요소만이 특성을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-743">However, according to the HTML 4.01 specification, only *input* elements should have this attribute.</span></span>

<span data-ttu-id="e6592-744">ASP.NET 4에서 다음 예제와 같이 *controlRenderingCompatibilityVersion* 속성을 "3.5"로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-744">In ASP.NET 4, you can set the *controlRenderingCompatibilityVersion* property to "3.5", as in the following example:</span></span>

[!code-xml[Main](overview/samples/sample70.xml)]

<span data-ttu-id="e6592-745">컨트롤을 사용 하지 않도록 설정 하는 다음과 같은 *레이블* 컨트롤에 대 한 태그를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-745">You might create markup for a *Label* control like the following, which disables the control:</span></span>

[!code-aspx[Main](overview/samples/sample71.aspx)]

<span data-ttu-id="e6592-746">*레이블* 컨트롤은 다음 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-746">The *Label* control would render the following HTML:</span></span>

[!code-html[Main](overview/samples/sample72.html)]

<span data-ttu-id="e6592-747">ASP.NET 4에서는 *controlRenderingCompatibilityVersion* 를 "4.0"로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-747">In ASP.NET 4, you can set the *controlRenderingCompatibilityVersion* to "4.0".</span></span> <span data-ttu-id="e6592-748">이 경우 컨트롤의 *Enabled* 속성이 *false*로 설정 되어 있으면 *입력* 요소를 렌더링 하는 컨트롤만 *비활성화* 된 특성을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-748">In that case, only controls that render *input* elements will render a *disabled* attribute when the control's *Enabled* property is set to *false*.</span></span> <span data-ttu-id="e6592-749">HTML *입력* 요소를 렌더링 하지 않는 컨트롤은 컨트롤에 대해 사용 하지 않도록 설정 된 모양을 정의 하는 데 사용할 수 있는 CSS 클래스를 참조 하는 *클래스* 특성을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-749">Controls that do not render HTML *input* elements instead render a *class* attribute that references a CSS class that you can use to define a disabled look for the control.</span></span> <span data-ttu-id="e6592-750">예를 들어 앞의 예제에 표시 된 *레이블* 컨트롤은 다음 태그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-750">For example, the *Label* control shown in the earlier example would generate the following markup:</span></span>

[!code-html[Main](overview/samples/sample73.html)]

<span data-ttu-id="e6592-751">이 컨트롤에 대해 지정 된 클래스의 기본값은 "aspNetDisabled"입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-751">The default value for the class that specified for this control is "aspNetDisabled".</span></span> <span data-ttu-id="e6592-752">그러나 *WebControl* 클래스의 정적 *Disabledcssclass* 정적 속성을 설정 하 여이 기본값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-752">However, you can change this default value by setting the static *DisabledCssClass* static property of the *WebControl* class.</span></span> <span data-ttu-id="e6592-753">컨트롤 개발자의 경우 *SupportsDisabledAttribute* 속성을 사용 하 여 특정 컨트롤에 사용할 동작을 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-753">For control developers, the behavior to use for a specific control can also be defined using the *SupportsDisabledAttribute* property.</span></span>

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a><span data-ttu-id="e6592-754">숨겨진 필드 주위의 div 요소 숨기기</span><span class="sxs-lookup"><span data-stu-id="e6592-754">Hiding div Elements Around Hidden Fields</span></span>

<span data-ttu-id="e6592-755">ASP.NET 2.0 이상 버전은 XHTML 표준을 준수 하기 위해 시스템 관련 숨겨진 필드 (예: 뷰 상태 정보를 저장 하는 데 사용 되는 *숨겨진* 요소)를 *div* 요소 내에 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-755">ASP.NET 2.0 and later versions render system-specific hidden fields (such as the *hidden* element used to store view state information) inside *div* element in order to comply with the XHTML standard.</span></span> <span data-ttu-id="e6592-756">그러나 CSS 규칙이 페이지의 *div* 요소에 영향을 주는 경우이로 인해 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-756">However, this can cause a problem when a CSS rule affects *div* elements on a page.</span></span> <span data-ttu-id="e6592-757">예를 들어 페이지에 숨겨진 *div* 요소 주위에 1 픽셀 줄이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-757">For example, it can result in a one-pixel line appearing in the page around hidden *div* elements.</span></span> <span data-ttu-id="e6592-758">ASP.NET 4에서 ASP.NET에 의해 생성 된 숨겨진 필드를 둘러싸는 *div* 요소는 다음 예제와 같이 CSS 클래스 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-758">In ASP.NET 4, *div* elements that enclose the hidden fields generated by ASP.NET add a CSS class reference as in the following example:</span></span>

[!code-html[Main](overview/samples/sample74.html)]

<span data-ttu-id="e6592-759">그런 다음, 다음 예제와 같이 ASP.NET에 의해 생성 되는 *숨겨진* 요소에만 적용 되는 CSS 클래스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-759">You can then define a CSS class that applies only to the *hidden* elements that are generated by ASP.NET, as in the following example:</span></span>

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a><span data-ttu-id="e6592-760">템플릿 기반 컨트롤에 대 한 외부 테이블 렌더링</span><span class="sxs-lookup"><span data-stu-id="e6592-760">Rendering an Outer Table for Templated Controls</span></span>

<span data-ttu-id="e6592-761">기본적으로 템플릿을 지 원하는 다음 ASP.NET 웹 서버 컨트롤은 인라인 스타일을 적용 하는 데 사용 되는 외부 테이블에 자동으로 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-761">By default, the following ASP.NET Web server controls that support templates are automatically wrapped in an outer table that is used to apply inline styles:</span></span>

- <span data-ttu-id="e6592-762">*FormView*</span><span class="sxs-lookup"><span data-stu-id="e6592-762">*FormView*</span></span>
- <span data-ttu-id="e6592-763">*로그인*</span><span class="sxs-lookup"><span data-stu-id="e6592-763">*Login*</span></span>
- <span data-ttu-id="e6592-764">*PasswordRecovery*</span><span class="sxs-lookup"><span data-stu-id="e6592-764">*PasswordRecovery*</span></span>
- <span data-ttu-id="e6592-765">*ChangePassword*</span><span class="sxs-lookup"><span data-stu-id="e6592-765">*ChangePassword*</span></span>
- <span data-ttu-id="e6592-766">*마법사*</span><span class="sxs-lookup"><span data-stu-id="e6592-766">*Wizard*</span></span>
- <span data-ttu-id="e6592-767">*CreateUserWizard*</span><span class="sxs-lookup"><span data-stu-id="e6592-767">*CreateUserWizard*</span></span>

<span data-ttu-id="e6592-768">태그에서 외부 테이블을 제거할 수 있도록 하는 *RenderOuterTable* 라는 새 속성이 이러한 컨트롤에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-768">A new property named *RenderOuterTable* has been added to these controls that allows the outer table to be removed from the markup.</span></span> <span data-ttu-id="e6592-769">예를 들어 *FormView* 컨트롤의 다음 예를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-769">For example, consider the following example of a *FormView* control:</span></span>

[!code-aspx[Main](overview/samples/sample76.aspx)]

<span data-ttu-id="e6592-770">이 태그는 HTML 테이블을 포함 하는 페이지에 다음 출력을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-770">This markup renders the following output to the page, which includes an HTML table:</span></span>

[!code-html[Main](overview/samples/sample77.html)]

<span data-ttu-id="e6592-771">테이블이 렌더링 되지 않도록 하려면 다음 예제와 같이 *FormView* 컨트롤의 *RenderOuterTable* 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-771">To prevent the table from being rendered, you can set the *FormView* control's *RenderOuterTable* property, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample78.aspx)]

<span data-ttu-id="e6592-772">이전 예제에서는 *테이블*, *tr*및 *td* 요소 없이 다음 출력을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-772">The previous example renders the following output, without the *table*, *tr*, and *td* elements:</span></span>

> <span data-ttu-id="e6592-773">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="e6592-773">Content</span></span>

<span data-ttu-id="e6592-774">이러한 향상 된 기능을 통해 컨트롤에서 예기치 않은 태그가 렌더링 되지 않으므로 CSS를 사용 하 여 컨트롤 내용의 스타일을 보다 쉽게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-774">This enhancement can make it easier to style the content of the control with CSS, because no unexpected tags are rendered by the control.</span></span>

> [!NOTE]
> <span data-ttu-id="e6592-775">참고 이렇게 변경 하면 자동 서식 옵션으로 생성 된 스타일 특성을 호스트할 수 있는 *테이블* 요소가 더 이상 없기 때문에 Visual Studio 2010 디자이너에서 자동 서식 함수를 지원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-775">Note This change disables support for the auto-format function in the Visual Studio 2010 designer, because there is no longer a *table* element that can host style attributes that are generated by the auto-format option.</span></span>

<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a><span data-ttu-id="e6592-776">ListView 컨트롤의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="e6592-776">ListView Control Enhancements</span></span>

<span data-ttu-id="e6592-777">*ListView* 컨트롤은 ASP.NET 4에서 더 쉽게 사용할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-777">The *ListView* control has been made easier to use in ASP.NET 4.</span></span> <span data-ttu-id="e6592-778">이전 버전의 컨트롤에서는 알려진 ID의 서버 컨트롤을 포함 하는 레이아웃 템플릿을 지정 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-778">The earlier version of the control required that you specify a layout template that contained a server control with a known ID.</span></span> <span data-ttu-id="e6592-779">다음 태그는 ASP.NET 3.5에서 *ListView* 컨트롤을 사용 하는 방법의 일반적인 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-779">The following markup shows a typical example of how to use the *ListView* control in ASP.NET 3.5.</span></span>

[!code-aspx[Main](overview/samples/sample79.aspx)]

<span data-ttu-id="e6592-780">ASP.NET 4에서는 *ListView* 컨트롤에 레이아웃 템플릿이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-780">In ASP.NET 4, the *ListView* control does not require a layout template.</span></span> <span data-ttu-id="e6592-781">이전 예제에 표시 된 태그를 다음 태그로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-781">The markup shown in the previous example can be replaced with the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a><span data-ttu-id="e6592-782">CheckBoxList 및 RadioButtonList 제어 기능 향상</span><span class="sxs-lookup"><span data-stu-id="e6592-782">CheckBoxList and RadioButtonList Control Enhancements</span></span>

<span data-ttu-id="e6592-783">ASP.NET 3.5에서는 다음 두 가지 설정을 사용 하 여 *CheckBoxList* 및 *RadioButtonList* 에 대 한 레이아웃을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-783">In ASP.NET 3.5, you can specify layout for the *CheckBoxList* and *RadioButtonList* using the following two settings:</span></span>

- <span data-ttu-id="e6592-784">*Flow*.</span><span class="sxs-lookup"><span data-stu-id="e6592-784">*Flow*.</span></span> <span data-ttu-id="e6592-785">컨트롤은 해당 콘텐츠를 포함 하는 *범위* 요소를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-785">The control renders *span* elements to contain its content.</span></span>
- <span data-ttu-id="e6592-786">*테이블*.</span><span class="sxs-lookup"><span data-stu-id="e6592-786">*Table*.</span></span> <span data-ttu-id="e6592-787">컨트롤은 해당 콘텐츠를 포함 하는 *table* 요소를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-787">The control renders a *table* element to contain its content.</span></span>

<span data-ttu-id="e6592-788">다음 예제에서는 이러한 각 컨트롤에 대 한 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-788">The following example shows markup for each of these controls.</span></span>

[!code-aspx[Main](overview/samples/sample81.aspx)]

<span data-ttu-id="e6592-789">기본적으로 컨트롤은 다음과 유사한 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-789">By default, the controls render HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample82.html)]

<span data-ttu-id="e6592-790">이러한 컨트롤은 항목 목록을 포함 하므로 의미상 올바른 HTML을 렌더링 하기 위해*li*(html 목록) 요소를 사용 하 여 콘텐츠를 렌더링 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-790">Because these controls contain lists of items, to render semantically correct HTML, they should render their contents using HTML list (*li*) elements.</span></span> <span data-ttu-id="e6592-791">이렇게 하면 보조 기술을 사용 하 여 웹 페이지를 읽는 사용자가 더 쉽게 작업할 수 있으며 CSS를 사용 하 여 컨트롤의 스타일을 보다 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-791">This makes it easier for users who read Web pages using assistive technology, and makes the controls easier to style using CSS.</span></span>

<span data-ttu-id="e6592-792">ASP.NET 4에서 *CheckBoxList* 및 *RadioButtonList* 컨트롤은 *RepeatLayout* 속성에 대해 다음과 같은 새 값을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-792">In ASP.NET 4, the *CheckBoxList* and *RadioButtonList* controls support the following new values for the *RepeatLayout* property:</span></span>

- <span data-ttu-id="e6592-793">*OrderedList* – 콘텐츠가 *ol* 요소 내에서 *li* 요소로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-793">*OrderedList* – The content is rendered as *li* elements within an *ol* element.</span></span>
- <span data-ttu-id="e6592-794">*UnorderedList* – 콘텐츠가 *ul* 요소 내에서 *li* 요소로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-794">*UnorderedList* – The content is rendered as *li* elements within a *ul* element.</span></span>

<span data-ttu-id="e6592-795">다음 예제에서는 이러한 새 값을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-795">The following example shows how to use these new values.</span></span>

[!code-aspx[Main](overview/samples/sample83.aspx)]

<span data-ttu-id="e6592-796">위의 태그는 다음 HTML을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-796">The preceding markup generates the following HTML:</span></span>

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> <span data-ttu-id="e6592-797">참고 *RepeatLayout* 를 *OrderedList* 또는 *UnorderedList*로 설정 하는 경우 *RepeatDirection* 속성을 더 이상 사용할 수 없으며, 속성이 태그 또는 코드 내에 설정 된 경우 런타임에 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-797">Note If you set *RepeatLayout* to *OrderedList* or *UnorderedList*, the *RepeatDirection* property can no longer be used and will throw an exception at run time if the property has been set within your markup or code.</span></span> <span data-ttu-id="e6592-798">이러한 컨트롤의 시각적 레이아웃은 CSS를 사용 하 여 정의 되기 때문에 속성에는 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-798">The property would have no value because the visual layout of these controls is defined using CSS instead.</span></span>

<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a><span data-ttu-id="e6592-799">메뉴 컨트롤 개선</span><span class="sxs-lookup"><span data-stu-id="e6592-799">Menu Control Improvements</span></span>

<span data-ttu-id="e6592-800">ASP.NET 4 이전에는 *Menu* 컨트롤이 일련의 HTML 테이블을 렌더링 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-800">Before ASP.NET 4, the *Menu* control rendered a series of HTML tables.</span></span> <span data-ttu-id="e6592-801">이렇게 하면 인라인 속성 설정 외에 CSS 스타일을 적용 하기가 더 어려워집니다. 또한 액세스 가능성 표준과 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-801">This made it more difficult to apply CSS styles outside of setting inline properties and was also not compliant with accessibility standards.</span></span>

<span data-ttu-id="e6592-802">ASP.NET 4에서 컨트롤은 이제 순서가 지정 되지 않은 목록 및 목록 요소로 구성 된 의미 태그를 사용 하 여 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-802">In ASP.NET 4, the control now renders HTML using semantic markup that consists of an unordered list and list elements.</span></span> <span data-ttu-id="e6592-803">다음 예제에서는 *Menu* 컨트롤에 대 한 ASP.NET 페이지의 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-803">The following example shows markup in an ASP.NET page for the *Menu* control.</span></span>

[!code-aspx[Main](overview/samples/sample85.aspx)]

<span data-ttu-id="e6592-804">페이지가 렌더링 되 면 컨트롤은 다음 HTML을 생성 합니다 (명확성을 위해 *onclick* 코드는 생략 됨).</span><span class="sxs-lookup"><span data-stu-id="e6592-804">When the page renders, the control produces the following HTML (the *onclick* code has been omitted for clarity):</span></span>

[!code-html[Main](overview/samples/sample86.html)]

<span data-ttu-id="e6592-805">렌더링 기능 향상 외에도, 포커스 관리를 사용 하 여 메뉴의 키보드 탐색 기능이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-805">In addition to rendering improvements, keyboard navigation of the menu has been improved using focus management.</span></span> <span data-ttu-id="e6592-806">*메뉴* 컨트롤이 포커스를 가져오는 경우 화살표 키를 사용 하 여 요소를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-806">When the *Menu* control gets focus, you can use the arrow keys to navigate elements.</span></span> <span data-ttu-id="e6592-807">또한 *메뉴* 컨트롤은 내게 필요한 옵션을 향상 시키기 위해 액세스 가능한 리치 인터넷 응용 프로그램 (ARIA) 역할 및 특성을 ([에](http://www.w3.org/TR/wai-aria-practices/#menu "메뉴 ARIA 지침")연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-807">The *Menu* control also now attaches accessible rich internet applications (ARIA) roles and attributes follo[wing the](http://www.w3.org/TR/wai-aria-practices/#menu "Menu ARIA guidelines")for improved accessibility.</span></span>

<span data-ttu-id="e6592-808">메뉴 컨트롤에 대 한 스타일은 렌더링 된 HTML 요소를 포함 하는 대신 페이지 맨 위에 있는 스타일 블록에서 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-808">Styles for the menu control are rendered in a style block at the top of the page, rather than in line with the rendered HTML elements.</span></span> <span data-ttu-id="e6592-809">컨트롤의 스타일을 완벽 하 게 제어 하려면 새 *IncludeStyleBlock* 속성을 *false*로 설정 하면 됩니다 .이 경우 스타일 블록은 내보내지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-809">If you want to take full control over the styling for the control, you can set the new *IncludeStyleBlock* property to *false*, in which case the style block is not emitted.</span></span> <span data-ttu-id="e6592-810">이 속성을 사용 하는 한 가지 방법은 Visual Studio 디자이너의 자동 서식 기능을 사용 하 여 메뉴의 모양을 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-810">One way to use this property is to use the auto-format feature in the Visual Studio designer to set the appearance of the menu.</span></span> <span data-ttu-id="e6592-811">그런 다음 페이지를 실행 하 고 페이지 소스를 연 다음 렌더링 된 스타일 블록을 외부 CSS 파일에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-811">You can then run the page, open the page source, and then copy the rendered style block to an external CSS file.</span></span> <span data-ttu-id="e6592-812">Visual Studio에서 스타일을 실행 취소 하 고 *IncludeStyleBlock* 을 *false*로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-812">In Visual Studio, undo the styling and set *IncludeStyleBlock* to *false*.</span></span> <span data-ttu-id="e6592-813">그 결과 메뉴 모양이 외부 스타일 시트의 스타일을 사용 하 여 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-813">The result is that the menu appearance is defined using styles in an external style sheet.</span></span>

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a><span data-ttu-id="e6592-814">Wizard 및 CreateUserWizard 컨트롤</span><span class="sxs-lookup"><span data-stu-id="e6592-814">Wizard and CreateUserWizard Controls</span></span>

<span data-ttu-id="e6592-815">ASP.NET *마법사* 및 *CreateUserWizard* 컨트롤은 렌더링 되는 HTML을 정의 하는 데 사용할 수 있는 템플릿을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-815">The ASP.NET *Wizard* and *CreateUserWizard* controls support templates that let you define the HTML that they render.</span></span> <span data-ttu-id="e6592-816">(*CreateUserWizard* 는 *마법사*에서 파생 됩니다.) 다음 예제에서는 완전히 템플릿 기반 *CreateUserWizard* 컨트롤에 대 한 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-816">(*CreateUserWizard* derives from *Wizard*.) The following example shows the markup for a fully templated *CreateUserWizard* control:</span></span>

[!code-aspx[Main](overview/samples/sample87.aspx)]

<span data-ttu-id="e6592-817">컨트롤은 다음과 유사한 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-817">The control renders HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample88.html)]

<span data-ttu-id="e6592-818">ASP.NET 3.5 s p 1에서 템플릿 콘텐츠를 변경할 수 있지만 *마법사* 컨트롤의 출력에 대 한 제한 된 제어를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-818">In ASP.NET 3.5 SP1, although you can change the template contents, you still have limited control over the output of the *Wizard* control.</span></span> <span data-ttu-id="e6592-819">ASP.NET 4에서는 *이 layouttemplate* 템플릿을 만들고, 예약 된 이름을 사용 하 여 *자리 표시자* 컨트롤을 삽입 하 여 *마법사 컨트롤이* 렌더링 되는 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-819">In ASP.NET 4, you can create a *LayoutTemplate* template and insert *PlaceHolder* controls (using reserved names) to specify how you want the *Wizard control* to render.</span></span> <span data-ttu-id="e6592-820">다음 예제에서는이를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-820">The following example shows this:</span></span>

[!code-aspx[Main](overview/samples/sample89.aspx)]

<span data-ttu-id="e6592-821">이 예에는 *이 layouttemplate* 요소에 다음과 같은 명명 된 자리 표시 자가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-821">The example contains the following named placeholders in the *LayoutTemplate* element:</span></span>

- <span data-ttu-id="e6592-822">*Headerplaceholder* – 런타임에 *HeaderTemplate* 요소의 콘텐츠로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-822">*headerPlaceholder* – At run time, this is replaced by the contents of the *HeaderTemplate* element.</span></span>
- <span data-ttu-id="e6592-823">나란히 표시 되는 *자리 표시자* – 런타임에는이를 외부 항목 *템플릿* 요소의 콘텐츠로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-823">*sideBarPlaceholder* – At run time, this is replaced by the contents of the *SideBarTemplate* element.</span></span>
- <span data-ttu-id="e6592-824">*wizardstststststststststststststststststststststststststststststat*</span><span class="sxs-lookup"><span data-stu-id="e6592-824">*wizardStepPlaceHolder* – At run time, this is replaced by the contents of the *WizardStepTemplate* element.</span></span>
- <span data-ttu-id="e6592-825">*Navigationplaceholder* – 런타임에 사용자가 정의한 탐색 템플릿으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-825">*navigationPlaceholder* – At run time, this is replaced by any navigation templates that you have defined.</span></span>

<span data-ttu-id="e6592-826">자리 표시자를 사용 하는 예제의 태그는 템플릿에 실제로 정의 된 내용이 없는 다음 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-826">The markup in the example that uses placeholders renders the following HTML (without the content actually defined in the templates):</span></span>

[!code-html[Main](overview/samples/sample90.html)]

<span data-ttu-id="e6592-827">현재 사용자 정의 되지 않은 HTML만 *범위* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-827">The only HTML that is now not user-defined is a *span* element.</span></span> <span data-ttu-id="e6592-828">이후 릴리스에서는 *span* 요소도 렌더링 되지 않을 것으로 예상 합니다. 이제 *마법사* 컨트롤에 의해 생성 되는 거의 모든 콘텐츠를 완전히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-828">(We anticipate that in future releases, even the *span* element will not be rendered.) This now gives you full control over virtually all the content that is generated by the *Wizard* control.</span></span>

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a><span data-ttu-id="e6592-829">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e6592-829">ASP.NET MVC</span></span>

<span data-ttu-id="e6592-830">ASP.NET MVC는 3 월 2009에 ASP.NET 3.5 s p 1의 추가 기능 프레임 워크로 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-830">ASP.NET MVC was introduced as an add-on framework to ASP.NET 3.5 SP1 in March 2009.</span></span> <span data-ttu-id="e6592-831">Visual Studio 2010에는 새로운 기능과 기능을 포함 하는 ASP.NET MVC 2가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-831">Visual Studio 2010 includes ASP.NET MVC 2, which includes new features and capabilities.</span></span>

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a><span data-ttu-id="e6592-832">영역 지원</span><span class="sxs-lookup"><span data-stu-id="e6592-832">Areas Support</span></span>

<span data-ttu-id="e6592-833">영역을 사용 하면 컨트롤러 및 뷰를 다른 섹션과 상대적으로 격리 된 많은 응용 프로그램의 섹션으로 그룹화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-833">Areas let you group controllers and views into sections of a large application in relative isolation from other sections.</span></span> <span data-ttu-id="e6592-834">각 영역은 주 응용 프로그램에서 참조할 수 있는 별도의 ASP.NET MVC 프로젝트로 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-834">Each area can be implemented as a separate ASP.NET MVC project that can then be referenced by the main application.</span></span> <span data-ttu-id="e6592-835">이렇게 하면 규모가 많은 응용 프로그램을 빌드하는 경우 복잡성을 관리 하 고, 여러 팀이 단일 응용 프로그램에서 함께 작업할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-835">This helps manage complexity when you build a large application and makes it easier for multiple teams to work together on a single application.</span></span>

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a><span data-ttu-id="e6592-836">데이터 주석 특성 유효성 검사 지원</span><span class="sxs-lookup"><span data-stu-id="e6592-836">Data-Annotation Attribute Validation Support</span></span>

<span data-ttu-id="e6592-837">*Dataannotations* 특성을 사용 하면 메타 데이터 특성을 사용 하 여 유효성 검사 논리를 모델에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-837">*DataAnnotations* attributes let you attach validation logic to a model by using metadata attributes.</span></span> <span data-ttu-id="e6592-838">*Dataannotations* 특성은 ASP.NET Dynamic Data ASP.NET 3.5 s p 1에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-838">*DataAnnotations* attributes were introduced in ASP.NET Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="e6592-839">이러한 특성은 기본 모델 바인더에 통합 되어 사용자 입력의 유효성을 검사 하는 메타 데이터 기반 수단을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-839">These attributes have been integrated into the default model binder and provide a metadata-driven means to validate user input.</span></span>

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a><span data-ttu-id="e6592-840">템플릿 기반 도우미</span><span class="sxs-lookup"><span data-stu-id="e6592-840">Templated Helpers</span></span>

<span data-ttu-id="e6592-841">템플릿 기반 도우미를 사용 하면 편집 및 표시 템플릿을 데이터 형식과 자동으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-841">Templated helpers let you automatically associate edit and display templates with data types.</span></span> <span data-ttu-id="e6592-842">예를 들어 템플릿 도우미를 사용 하 여 날짜 선택 UI 요소가 *시스템의 DateTime* 값에 대해 자동으로 렌더링 되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-842">For example, you can use a template helper to specify that a date-picker UI element is automatically rendered for a *System.DateTime* value.</span></span> <span data-ttu-id="e6592-843">이는 ASP.NET Dynamic Data의 필드 템플릿과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-843">This is similar to field templates in ASP.NET Dynamic Data.</span></span>

<span data-ttu-id="e6592-844">도우미에 대 한 *html* . *a* p a. a p a. i a. a p a.</span><span class="sxs-lookup"><span data-stu-id="e6592-844">The *Html.EditorFor* and *Html.DisplayFor* helper methods have built-in support for rendering standard data types as well as complex objects with multiple properties.</span></span> <span data-ttu-id="e6592-845">또한 *DisplayName* 및 *ScaffoldColumn* 와 같은 데이터 주석 특성을 *ViewModel* 개체에 적용할 수 있도록 하 여 렌더링을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-845">They also customize rendering by letting you apply data-annotation attributes like *DisplayName* and *ScaffoldColumn* to the *ViewModel* object.</span></span>

<span data-ttu-id="e6592-846">UI 도우미의 출력을 추가로 사용자 지정 하 고 생성 되는 내용을 완전히 제어 하려는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-846">Often you want to customize the output from UI helpers even further and have complete control over what is generated.</span></span> <span data-ttu-id="e6592-847">도우미에 대 한 *html* . *p* a p. i p v의 경우에는 렌더링 된 출력을 재정의 하 고 제어할 수 있는 외부 템플릿을 정의할 수 있는 템플릿 메커니즘을 사용 하 여이를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-847">The *Html.EditorFor* and *Html.DisplayFor* helper methods support this using a templating mechanism that lets you define external templates that can override and control the output rendered.</span></span> <span data-ttu-id="e6592-848">템플릿은 클래스에 대해 개별적으로 렌더링 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-848">The templates can be rendered individually for a class.</span></span>

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a><span data-ttu-id="e6592-849">Dynamic Data</span><span class="sxs-lookup"><span data-stu-id="e6592-849">Dynamic Data</span></span>

<span data-ttu-id="e6592-850">Dynamic Data는 2008의 .NET Framework 3.5 SP1 릴리스에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-850">Dynamic Data was introduced in the .NET Framework 3.5 SP1 release in mid-2008.</span></span> <span data-ttu-id="e6592-851">이 기능은 다음을 포함 하 여 데이터 기반 응용 프로그램을 만들기 위한 다양 한 향상 된 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-851">This feature provides many enhancements for creating data-driven applications, including the following:</span></span>

- <span data-ttu-id="e6592-852">데이터 기반 웹 사이트를 신속 하 게 빌드하기 위한 RAD 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-852">A RAD experience for quickly building a data-driven Web site.</span></span>
- <span data-ttu-id="e6592-853">데이터 모델에 정의 된 제약 조건을 기반으로 하는 자동 유효성 검사입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-853">Automatic validation that is based on constraints defined in the data model.</span></span>
- <span data-ttu-id="e6592-854">Dynamic Data 프로젝트의 일부인 필드 템플릿을 사용 하 여 *GridView* 및 *DetailsView* 컨트롤의 필드에 대해 생성 되는 태그를 쉽게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-854">The ability to easily change the markup that is generated for fields in the *GridView* and *DetailsView* controls by using field templates that are part of your Dynamic Data project.</span></span>

> [!NOTE]
> <span data-ttu-id="e6592-855">참고 자세한 내용은 MSDN Library의 [Dynamic Data 설명서](https://msdn.microsoft.com/library/cc488545.aspx) 를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e6592-855">Note For more information, see the [Dynamic Data documentation](https://msdn.microsoft.com/library/cc488545.aspx) in the MSDN Library.</span></span>

<span data-ttu-id="e6592-856">ASP.NET 4의 경우 개발자가 데이터 기반 웹 사이트를 신속 하 게 빌드할 수 있는 더 많은 기능을 제공 하도록 Dynamic Data 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-856">For ASP.NET 4, Dynamic Data has been enhanced to give developers even more power for quickly building data-driven Web sites.</span></span>

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a><span data-ttu-id="e6592-857">기존 프로젝트에 대 한 Dynamic Data 사용</span><span class="sxs-lookup"><span data-stu-id="e6592-857">Enabling Dynamic Data for Existing Projects</span></span>

<span data-ttu-id="e6592-858">Dynamic Data .NET Framework 3.5 s p 1에서 제공 되는 기능은 다음과 같은 새로운 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-858">Dynamic Data features that shipped in the .NET Framework 3.5 SP1 brought new features such as the following:</span></span>

- <span data-ttu-id="e6592-859">필드 템플릿 – 데이터 바인딩된 컨트롤에 대 한 데이터 형식 기반 템플릿을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-859">Field templates – These provide data-type-based templates for data-bound controls.</span></span> <span data-ttu-id="e6592-860">필드 템플릿은 각 필드에 대 한 템플릿 필드를 사용 하는 것 보다 간단 하 게 데이터 컨트롤의 모양을 사용자 지정 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-860">Field templates provide a simpler way to customize the look of data controls than using template fields for each field.</span></span>
- <span data-ttu-id="e6592-861">유효성 검사 – Dynamic Data를 사용 하면 데이터 클래스에서 특성을 사용 하 여 필수 필드, 범위 검사, 형식 검사, 정규식을 사용한 패턴 일치 및 사용자 지정 유효성 검사와 같은 일반적인 시나리오에 대 한 유효성 검사를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-861">Validation – Dynamic Data lets you use attributes on data classes to specify validation for common scenarios like required fields, range checking, type checking, pattern matching using regular expressions, and custom validation.</span></span> <span data-ttu-id="e6592-862">유효성 검사는 데이터 컨트롤에 의해 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-862">Validation is enforced by the data controls.</span></span>

<span data-ttu-id="e6592-863">그러나 이러한 기능에는 다음과 같은 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-863">However, these features had the following requirements:</span></span>

- <span data-ttu-id="e6592-864">데이터 액세스 계층은 Entity Framework 또는 LINQ to SQL를 기반으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-864">The data-access layer had to be based on Entity Framework or LINQ to SQL.</span></span>
- <span data-ttu-id="e6592-865">이러한 기능에 대해 지원 되는 데이터 원본 컨트롤은 *EntityDataSource* 또는 *LinqDataSource* 컨트롤 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-865">The only data source controls supported for these features were the *EntityDataSource* or *LinqDataSource* controls.</span></span>
- <span data-ttu-id="e6592-866">이 기능을 사용 하려면 기능을 지 원하는 데 필요한 모든 파일을 포함 하기 위해 Dynamic Data 또는 Dynamic Data 엔터티 템플릿을 사용 하 여 만든 웹 프로젝트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-866">The features required a Web project that had been created using the Dynamic Data or Dynamic Data Entities templates in order to have all the files that were required to support the feature.</span></span>

<span data-ttu-id="e6592-867">ASP.NET 4에서 Dynamic Data 지원의 주요 목표는 모든 ASP.NET 응용 프로그램에 대해 Dynamic Data의 새로운 기능을 사용 하도록 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-867">A major goal of Dynamic Data support in ASP.NET 4 is to enable the new functionality of Dynamic Data for any ASP.NET application.</span></span> <span data-ttu-id="e6592-868">다음 예제에서는 기존 페이지의 Dynamic Data 기능을 활용할 수 있는 컨트롤에 대 한 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-868">The following example shows markup for controls that can take advantage of Dynamic Data functionality in an existing page.</span></span>

[!code-aspx[Main](overview/samples/sample91.aspx)]

<span data-ttu-id="e6592-869">페이지의 코드에서 다음 코드를 추가 해야 이러한 컨트롤에 대 한 Dynamic Data 지원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-869">In the code for the page, the following code must be added in order to enable Dynamic Data support for these controls:</span></span>

[!code-csharp[Main](overview/samples/sample92.cs)]

<span data-ttu-id="e6592-870">*GridView* 컨트롤이 편집 모드에 있으면 Dynamic Data는 입력 한 데이터가 적절 한 형식 인지 자동으로 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-870">When the *GridView* control is in edit mode, Dynamic Data automatically validates that the data entered is in the proper format.</span></span> <span data-ttu-id="e6592-871">그렇지 않으면 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-871">If it is not, an error message is displayed.</span></span>

<span data-ttu-id="e6592-872">이 기능은 삽입 모드에 대 한 기본값을 지정할 수 있는 등의 다른 이점도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-872">This functionality also provides other benefits, such as being able to specify default values for insert mode.</span></span> <span data-ttu-id="e6592-873">Dynamic Data 하지 않고 필드의 기본값을 구현 하려면 이벤트에 연결 하 고 컨트롤을 찾아 ( *FindControl*사용) 해당 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-873">Without Dynamic Data, to implement a default value for a field, you must attach to an event, locate the control (using *FindControl*), and set its value.</span></span> <span data-ttu-id="e6592-874">ASP.NET 4에서 *EnableDynamicData* 호출은 다음 예제와 같이 개체의 모든 필드에 대 한 기본값을 전달할 수 있는 두 번째 매개 변수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-874">In ASP.NET 4, the *EnableDynamicData* call supports a second parameter that lets you pass default values for any field on the object, as shown in this example:</span></span>

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a><span data-ttu-id="e6592-875">선언적 DynamicDataManager 컨트롤 구문</span><span class="sxs-lookup"><span data-stu-id="e6592-875">Declarative DynamicDataManager Control Syntax</span></span>

<span data-ttu-id="e6592-876">*DynamicDataManager* 컨트롤은 코드 뿐 아니라 ASP.NET의 대부분 컨트롤과 마찬가지로 선언적으로 구성할 수 있도록 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-876">The *DynamicDataManager* control has been enhanced so that you can configure it declaratively, as with most controls in ASP.NET, instead of only in code.</span></span> <span data-ttu-id="e6592-877">*DynamicDataManager* 컨트롤에 대 한 태그는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-877">The markup for the *DynamicDataManager* control looks like the following example:</span></span>

[!code-aspx[Main](overview/samples/sample94.aspx)]

<span data-ttu-id="e6592-878">이 태그를 사용 하면 *DynamicDataManager* 컨트롤의 *DataControls* 섹션에서 참조 되는 GridView1 컨트롤에 대 한 Dynamic Data 동작을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-878">This markup enables Dynamic Data behavior for the GridView1 control that is referenced in the *DataControls* section of the *DynamicDataManager* control.</span></span>

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a><span data-ttu-id="e6592-879">엔터티 템플릿</span><span class="sxs-lookup"><span data-stu-id="e6592-879">Entity Templates</span></span>

<span data-ttu-id="e6592-880">엔터티 템플릿은 사용자 지정 페이지를 만들지 않고도 데이터의 레이아웃을 사용자 지정할 수 있는 새로운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-880">Entity templates offer a new way to customize the layout of data without requiring you to create a custom page.</span></span> <span data-ttu-id="e6592-881">페이지 템플릿은 이전 버전의 Dynamic Data에서 페이지 템플릿에서 사용 되는 *DetailsView* 컨트롤 대신 *FormView* 컨트롤을 사용 하 고, 엔터티 템플릿을 렌더링 하는 *dynamicentity* 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-881">Page templates use the *FormView* control (instead of the *DetailsView* control, as used in page templates in earlier versions of Dynamic Data) and the *DynamicEntity* control to render Entity templates.</span></span> <span data-ttu-id="e6592-882">이렇게 하면 Dynamic Data에 의해 렌더링 되는 태그를 더 효과적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-882">This gives you more control over the markup that is rendered by Dynamic Data.</span></span>

<span data-ttu-id="e6592-883">다음 목록에서는 엔터티 템플릿이 포함 된 새 프로젝트 디렉터리 레이아웃을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-883">The following list shows the new project directory layout that contains entity templates:</span></span>

[!code-console[Main](overview/samples/sample95.cmd)]

<span data-ttu-id="e6592-884">`EntityTemplate` 디렉터리에는 데이터 모델 개체를 표시 하는 방법에 대 한 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-884">The `EntityTemplate` directory contains templates for how to display data model objects.</span></span> <span data-ttu-id="e6592-885">기본적으로 개체는 ASP.NET 3.5 s p 1의 Dynamic Data에서 사용 하는 *DetailsView* 컨트롤에 의해 생성 된 태그와 같이 보이는 태그를 제공 하는 `Default.ascx` 템플릿을 사용 하 여 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-885">By default, objects are rendered by using the `Default.ascx` template, which provides markup that looks just like the markup created by the *DetailsView* control used by Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="e6592-886">다음 예제에서는 `Default.ascx` 컨트롤에 대 한 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-886">The following example shows the markup for the `Default.ascx` control:</span></span>

[!code-aspx[Main](overview/samples/sample96.aspx)]

<span data-ttu-id="e6592-887">기본 템플릿을 편집 하 여 전체 사이트의 모양과 느낌을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-887">The default templates can be edited to change the look and feel for the entire site.</span></span> <span data-ttu-id="e6592-888">표시, 편집 및 삽입 작업에 대 한 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-888">There are templates for display, edit, and insert operations.</span></span> <span data-ttu-id="e6592-889">데이터 개체의 이름을 기준으로 새 템플릿을 추가 하 여 하나의 개체 형식에 대 한 모양과 느낌을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-889">New templates can be added based on the name of the data object in order to change the look and feel of just one type of object.</span></span> <span data-ttu-id="e6592-890">예를 들어 다음 템플릿을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-890">For example, you can add the following template:</span></span>

[!code-console[Main](overview/samples/sample97.cmd)]

<span data-ttu-id="e6592-891">템플릿에는 다음 태그가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-891">The template might contain the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample98.aspx)]

<span data-ttu-id="e6592-892">새 *dynamicentity* 컨트롤을 사용 하 여 새 엔터티 템플릿이 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-892">The new entity templates are displayed on a page by using the new *DynamicEntity* control.</span></span> <span data-ttu-id="e6592-893">런타임에이 컨트롤이 엔터티 템플릿의 콘텐츠로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-893">At run time, this control is replaced with the contents of the entity template.</span></span> <span data-ttu-id="e6592-894">다음 태그는 엔터티 템플릿을 사용 하는 `Detail.aspx` 페이지 템플릿의 *FormView* 컨트롤을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-894">The following markup shows the *FormView* control in the `Detail.aspx` page template that uses the entity template.</span></span> <span data-ttu-id="e6592-895">태그에서 *Dynamicentity* 요소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-895">Notice the *DynamicEntity* element in the markup.</span></span>

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a><span data-ttu-id="e6592-896">Url 및 전자 메일 주소에 대 한 새 필드 템플릿</span><span class="sxs-lookup"><span data-stu-id="e6592-896">New Field Templates for URLs and Email Addresses</span></span>

<span data-ttu-id="e6592-897">ASP.NET 4에서는 두 개의 새로운 기본 제공 필드 템플릿 `EmailAddress.ascx` 및 `Url.ascx`를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-897">ASP.NET 4 introduces two new built-in field templates, `EmailAddress.ascx` and `Url.ascx`.</span></span> <span data-ttu-id="e6592-898">이러한 템플릿은 *EmailAddress* 로 표시 된 필드나 *DataType* 특성을 가진 *Url* 에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-898">These templates are used for fields that are marked as *EmailAddress* or *Url* with the *DataType* attribute.</span></span> <span data-ttu-id="e6592-899">*EmailAddress* 개체의 경우에는 *mailto:* 프로토콜을 사용 하 여 만든 하이퍼링크로 필드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-899">For *EmailAddress* objects, the field is displayed as a hyperlink that is created by using the *mailto:* protocol.</span></span> <span data-ttu-id="e6592-900">사용자가 링크를 클릭 하면 사용자의 전자 메일 클라이언트를 열고 기본 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-900">When users click the link, it opens the user's email client and creates a skeleton message.</span></span> <span data-ttu-id="e6592-901">*Url* 로 입력 된 개체는 일반 하이퍼링크로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-901">Objects typed as *Url* are displayed as ordinary hyperlinks.</span></span>

<span data-ttu-id="e6592-902">다음 예에서는 필드를 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-902">The following example shows how fields would be marked.</span></span>

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a><span data-ttu-id="e6592-903">DynamicHyperLink 컨트롤을 사용 하 여 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="e6592-903">Creating Links with the DynamicHyperLink Control</span></span>

<span data-ttu-id="e6592-904">Dynamic Data는 .NET Framework 3.5 s p 1에 추가 된 새 라우팅 기능을 사용 하 여 최종 사용자가 웹 사이트에 액세스할 때 표시 하는 Url을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-904">Dynamic Data uses the new routing feature that was added in the .NET Framework 3.5 SP1 to control the URLs that end users see when they access the Web site.</span></span> <span data-ttu-id="e6592-905">새 *DynamicHyperLink* 컨트롤을 사용 하면 Dynamic Data 사이트의 페이지에 대 한 링크를 쉽게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-905">The new *DynamicHyperLink* control makes it easy to build links to pages in a Dynamic Data site.</span></span> <span data-ttu-id="e6592-906">다음 예제에서는 *DynamicHyperLink* 컨트롤을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-906">The following example shows how to use the *DynamicHyperLink* control:</span></span>

[!code-aspx[Main](overview/samples/sample101.aspx)]

<span data-ttu-id="e6592-907">이 태그는 `Global.asax` 파일에 정의 된 경로를 기반으로 `Products` 테이블에 대 한 목록 페이지를 가리키는 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-907">This markup creates a link that points to the List page for the `Products` table based on routes that are defined in the `Global.asax` file.</span></span> <span data-ttu-id="e6592-908">컨트롤은 Dynamic Data 페이지의 기반이 되는 기본 테이블 이름을 자동으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-908">The control automatically uses the default table name that the Dynamic Data page is based on.</span></span>

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a><span data-ttu-id="e6592-909">데이터 모델의 상속에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="e6592-909">Support for Inheritance in the Data Model</span></span>

<span data-ttu-id="e6592-910">Entity Framework와 LINQ to SQL는 모두 해당 데이터 모델에서 상속을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-910">Both the Entity Framework and LINQ to SQL support inheritance in their data models.</span></span> <span data-ttu-id="e6592-911">이에 대 한 예는 `InsurancePolicy` 테이블이 있는 데이터베이스 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-911">An example of this might be a database that has an `InsurancePolicy` table.</span></span> <span data-ttu-id="e6592-912">`InsurancePolicy`와 동일한 필드가 있는 `CarPolicy` 및 `HousePolicy` 테이블을 포함 하 고 필드를 더 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-912">It might also contain `CarPolicy` and `HousePolicy` tables that have the same fields as `InsurancePolicy` and then add more fields.</span></span> <span data-ttu-id="e6592-913">Dynamic Data는 데이터 모델의 상속 된 개체를 이해 하 고 상속 된 테이블에 대 한 스 캐 폴딩을 지원 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-913">Dynamic Data has been modified to understand inherited objects in the data model and to support scaffolding for the inherited tables.</span></span>

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a><span data-ttu-id="e6592-914">다 대 다 관계에 대 한 지원 (Entity Framework에만 해당)</span><span class="sxs-lookup"><span data-stu-id="e6592-914">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>

<span data-ttu-id="e6592-915">Entity Framework는 *엔터티* 개체의 컬렉션으로 관계를 노출 하 여 구현 되는 테이블 간의 다 대 다 관계에 대 한 다양 한 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-915">The Entity Framework has rich support for many-to-many relationships between tables, which is implemented by exposing the relationship as a collection on an *Entity* object.</span></span> <span data-ttu-id="e6592-916">다 대 다 관계에 관련 된 데이터를 표시 하 고 편집할 수 있도록 새 `ManyToMany.ascx` 및 `ManyToMany_Edit.ascx` 필드 템플릿이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-916">New `ManyToMany.ascx` and `ManyToMany_Edit.ascx` field templates have been added to provide support for displaying and editing data that is involved in many-to-many relationships.</span></span>

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a><span data-ttu-id="e6592-917">표시 및 지원 열거를 제어 하기 위한 새 특성</span><span class="sxs-lookup"><span data-stu-id="e6592-917">New Attributes to Control Display and Support Enumerations</span></span>

<span data-ttu-id="e6592-918">*Displayattribute* 를 추가 하 여 필드가 표시 되는 방법을 보다 세밀 하 게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-918">The *DisplayAttribute* has been added to give you additional control over how fields are displayed.</span></span> <span data-ttu-id="e6592-919">이전 버전의 Dynamic Data *DisplayName* 특성을 사용 하 여 필드의 캡션으로 사용 되는 이름을 변경할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-919">The *DisplayName* attribute in earlier versions of Dynamic Data allowed you to change the name that is used as a caption for a field.</span></span> <span data-ttu-id="e6592-920">새 *Displayattribute* 클래스를 사용 하면 필드가 표시 되는 순서 및 필드가 필터로 사용 되는지 여부와 같은 필드 표시에 대 한 추가 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-920">The new *DisplayAttribute* class lets you specify more options for displaying a field, such as the order in which a field is displayed and whether a field will be used as a filter.</span></span> <span data-ttu-id="e6592-921">또한 특성은 *GridView* 컨트롤의 레이블에 사용 되는 이름, *DetailsView* 컨트롤에서 사용 되는 이름, 필드에 대 한 도움말 텍스트 및 필드에 사용 되는 워터 마크 (필드가 텍스트 입력을 받아들이는 경우)에 사용 되는 이름을 독립적으로 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-921">The attribute also provides independent control of the name used for the labels in a *GridView* control, the name used in a *DetailsView* control, the help text for the field, and the watermark used for the field (if the field accepts text input).</span></span>

<span data-ttu-id="e6592-922">*EnumDataTypeAttribute* 클래스가 추가 되어 필드를 열거형에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-922">The *EnumDataTypeAttribute* class has been added to let you map fields to enumerations.</span></span> <span data-ttu-id="e6592-923">필드에이 특성을 적용 하는 경우 열거형 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-923">When you apply this attribute to a field, you specify an enumeration type.</span></span> <span data-ttu-id="e6592-924">Dynamic Data는 새 `Enumeration.ascx` 필드 템플릿을 사용 하 여 열거형 값을 표시 하 고 편집 하는 UI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-924">Dynamic Data uses the new `Enumeration.ascx` field template to create UI for displaying and editing enumeration values.</span></span> <span data-ttu-id="e6592-925">템플릿은 데이터베이스의 값을 열거형의 이름에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-925">The template maps the values from the database to the names in the enumeration.</span></span>

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a><span data-ttu-id="e6592-926">향상 된 필터 지원</span><span class="sxs-lookup"><span data-stu-id="e6592-926">Enhanced Support for Filters</span></span>

<span data-ttu-id="e6592-927">Dynamic Data 1.0은 부울 열과 외래 키 열에 대 한 기본 제공 필터와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-927">Dynamic Data 1.0 shipped with built-in filters for Boolean columns and foreign-key columns.</span></span> <span data-ttu-id="e6592-928">필터를 사용 하 여 표시 되었는지 아니면 표시 되는 순서를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-928">The filters did not allow you to specify whether they were displayed or in what order they were displayed.</span></span> <span data-ttu-id="e6592-929">새 *Displayattribute* 특성은 열이 필터로 표시 되는지 여부를 제어 하 고 표시 되는 순서를 제어 하 여 이러한 문제를 모두 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-929">The new *DisplayAttribute* attribute addresses both of these issues by giving you control over whether a column is displayed as a filter and in what order it will be displayed.</span></span>

<span data-ttu-id="e6592-930">추가 기능 향상으로 인해 Web Forms의[새로운 기능을 사용 하도록](#0.2__QueryExtender "_QueryExtender") 필터링 지원이 다시 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-930">An additional enhancement is that filtering support has been re[written to use the new](#0.2__QueryExtender "_QueryExtender") feature of Web Forms.</span></span> <span data-ttu-id="e6592-931">이렇게 하면 필터를 사용할 데이터 소스 컨트롤에 대 한 지식이 없어도 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-931">This lets you create filters without requiring knowledge of the data source control that the filters will be used with.</span></span> <span data-ttu-id="e6592-932">이러한 확장과 함께 필터도 템플릿 컨트롤로 확장 되어 새 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-932">Along with these extensions, filters have also been turned into template controls, which allows you to add new ones.</span></span> <span data-ttu-id="e6592-933">마지막으로 언급 된 *Displayattribute* 클래스를 사용 하 여 기본 필터를 재정의할 수 있습니다. *UIHint* 는 열에 대 한 기본 필드 템플릿이 재정의 되도록 허용 하는 것과 동일한 방식으로 기본 필터를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-933">Finally, the *DisplayAttribute* class mentioned earlier allows the default filter to be overridden, in the same way that *UIHint* allows the default field template for a column to be overridden.</span></span>

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a><span data-ttu-id="e6592-934">Visual Studio 2010 웹 개발 개선 사항</span><span class="sxs-lookup"><span data-stu-id="e6592-934">Visual Studio 2010 Web Development Improvements</span></span>

<span data-ttu-id="e6592-935">Visual Studio 2010의 웹 개발은 CSS 호환성이 향상 되었으며 HTML 및 ASP.NET 마크업 코드 조각 및 새로운 동적 IntelliSense JavaScript를 통해 생산성을 향상 시켰습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-935">Web development in Visual Studio 2010 has been enhanced for greater CSS compatibility, increased productivity through HTML and ASP.NET markup snippets and new dynamic IntelliSense JavaScript.</span></span>

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a><span data-ttu-id="e6592-936">향상 된 CSS 호환성</span><span class="sxs-lookup"><span data-stu-id="e6592-936">Improved CSS Compatibility</span></span>

<span data-ttu-id="e6592-937">Visual Studio 2010의 Visual Web Developer designer가 CSS 2.1 표준 준수를 개선 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-937">The Visual Web Developer designer in Visual Studio 2010 has been updated to improve CSS 2.1 standards compliance.</span></span> <span data-ttu-id="e6592-938">디자이너는 HTML 소스의 무결성을 더 잘 유지 하 고 이전 버전의 Visual Studio 보다 더 강력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-938">The designer better preserves integrity of the HTML source and is more robust than in previous versions of Visual Studio.</span></span> <span data-ttu-id="e6592-939">내부적으로 아키텍처를 개선 하 여 렌더링, 레이아웃 및 서비스 가능성을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-939">Under the hood, architectural improvements have also been made that will better enable future enhancements in rendering, layout, and serviceability.</span></span>

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a><span data-ttu-id="e6592-940">HTML 및 JavaScript 코드 조각</span><span class="sxs-lookup"><span data-stu-id="e6592-940">HTML and JavaScript Snippets</span></span>

<span data-ttu-id="e6592-941">HTML 편집기에서 IntelliSense는 태그 이름을 자동으로 완성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-941">In the HTML editor, IntelliSense auto-completes tag names.</span></span> <span data-ttu-id="e6592-942">IntelliSense 코드 조각 기능은 전체 태그 등을 자동으로 완성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-942">The IntelliSense Snippets feature auto-completes entire tags and more.</span></span> <span data-ttu-id="e6592-943">Visual Studio 2010에서 IntelliSense 코드 조각은 이전 버전의 Visual Studio에서 C# 지원 되는 및 Visual Basic와 함께 JavaScript에 대해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-943">In Visual Studio 2010, IntelliSense snippets are supported for JavaScript, alongside C# and Visual Basic, which were supported in earlier versions of Visual Studio.</span></span>

<span data-ttu-id="e6592-944">Visual Studio 2010에는 필수 특성 (예: runat = "server") 및 태그와 관련 된 공통 특성 (예: *ID*, *DataSourceID*, *ControlToValidate*및 *텍스트*)을 비롯 하 여 일반적인 ASP.NET 및 HTML 태그를 자동으로 완성 하는 데 도움이 되는 200 개 이상의 코드 조각이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-944">Visual Studio 2010 includes over 200 snippets that help you auto-complete common ASP.NET and HTML tags, including required attributes (such as runat="server") and common attributes specific to a tag (such as *ID*, *DataSourceID*, *ControlToValidate*, and *Text*).</span></span>

<span data-ttu-id="e6592-945">추가 코드 조각을 다운로드 하거나 사용자 또는 팀에서 일반 작업에 사용 하는 태그 블록을 캡슐화 하는 사용자 고유의 코드 조각을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-945">You can download additional snippets, or you can write your own snippets that encapsulate the blocks of markup that you or your team use for common tasks.</span></span>

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a><span data-ttu-id="e6592-946">JavaScript IntelliSense의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="e6592-946">JavaScript IntelliSense Enhancements</span></span>

<span data-ttu-id="e6592-947">Visual 2010에서 JavaScript IntelliSense는 훨씬 더 풍부한 편집 환경을 제공 하도록 다시 디자인 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-947">In Visual 2010, JavaScript IntelliSense has been redesigned to provide an even richer editing experience.</span></span> <span data-ttu-id="e6592-948">IntelliSense는 이제 *Registernamespace* 와 같은 메서드 및 다른 JavaScript 프레임 워크에서 사용 하는 유사한 기법에 의해 동적으로 생성 된 개체를 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-948">IntelliSense now recognizes objects that have been dynamically generated by methods such as *registerNamespace* and by similar techniques used by other JavaScript frameworks.</span></span> <span data-ttu-id="e6592-949">스크립트의 많은 라이브러리를 분석 하 고 처리 지연이 거의 없거나 전혀 없는 IntelliSense를 표시 하는 성능이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-949">Performance has been improved to analyze large libraries of script and to display IntelliSense with little or no processing delay.</span></span> <span data-ttu-id="e6592-950">거의 모든 타사 라이브러리를 지원 하 고 다양 한 코딩 스타일을 지원 하기 위해 호환성이 크게 늘어났습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-950">Compatibility has been dramatically increased to support nearly all third-party libraries and to support diverse coding styles.</span></span> <span data-ttu-id="e6592-951">이제 사용자가 입력 하면 문서 주석이 구문 분석 되 고 IntelliSense에서 즉시 활용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-951">Documentation comments are now parsed as you type and are immediately leveraged by IntelliSense.</span></span>

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a><span data-ttu-id="e6592-952">Visual Studio 2010을 사용 하 여 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e6592-952">Web Application Deployment with Visual Studio 2010</span></span>

<span data-ttu-id="e6592-953">ASP.NET 개발자가 웹 응용 프로그램을 배포 하는 경우 다음과 같은 문제가 발생 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-953">When ASP.NET developers deploy a Web application, they often find that they encounter issues such as the following:</span></span>

- <span data-ttu-id="e6592-954">공유 호스팅 사이트에 배포 하는 데는 FTP와 같은 기술이 필요 하며이는 속도가 느릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-954">Deploying to a shared hosting site requires technologies such as FTP, which can be slow.</span></span> <span data-ttu-id="e6592-955">또한 SQL 스크립트를 실행 하 여 데이터베이스를 구성 하는 등의 작업을 수동으로 수행 해야 하며 가상 디렉터리 폴더를 응용 프로그램으로 구성 하는 등의 IIS 설정을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-955">In addition, you must manually perform tasks such as running SQL scripts to configure a database and you must change IIS settings, such as configuring a virtual directory folder as an application.</span></span>
- <span data-ttu-id="e6592-956">엔터프라이즈 환경에서 웹 응용 프로그램 파일을 배포 하는 것 외에도 관리자는 종종 ASP.NET 구성 파일 및 IIS 설정을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-956">In an enterprise environment, in addition to deploying the Web application files, administrators frequently must modify ASP.NET configuration files and IIS settings.</span></span> <span data-ttu-id="e6592-957">데이터베이스 관리자는 일련의 SQL 스크립트를 실행 하 여 응용 프로그램 데이터베이스를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-957">Database administrators must run a series of SQL scripts to get the application database running.</span></span> <span data-ttu-id="e6592-958">이러한 설치는 많은 노력이 필요 하며, 작업을 완료 하는 데 몇 시간 정도 걸리며, 신중 하 게 문서화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-958">Such installations are labor intensive, often take hours to complete, and must be carefully documented.</span></span>

<span data-ttu-id="e6592-959">Visual Studio 2010에는 이러한 문제를 해결 하 고 웹 응용 프로그램을 원활 하 게 배포할 수 있는 기술이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-959">Visual Studio 2010 includes technologies that address these issues and that let you seamlessly deploy Web applications.</span></span> <span data-ttu-id="e6592-960">이러한 기술 중 하나는 IIS 웹 배포 도구 (Msdeploy.exe)입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-960">One of these technologies is the IIS Web Deployment Tool (MsDeploy.exe).</span></span>

<span data-ttu-id="e6592-961">Visual Studio 2010의 웹 배포 기능에는 다음과 같은 주요 영역이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-961">Web deployment features in Visual Studio 2010 include the following major areas:</span></span>

- <span data-ttu-id="e6592-962">웹 패키징</span><span class="sxs-lookup"><span data-stu-id="e6592-962">Web packaging</span></span>
- <span data-ttu-id="e6592-963">Web.config 변환</span><span class="sxs-lookup"><span data-stu-id="e6592-963">Web.config transformation</span></span>
- <span data-ttu-id="e6592-964">데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="e6592-964">Database deployment</span></span>
- <span data-ttu-id="e6592-965">한 번 클릭으로 웹 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="e6592-965">One-click publish for Web applications</span></span>

<span data-ttu-id="e6592-966">다음 섹션에서는 이러한 기능에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-966">The following sections provide details about these features.</span></span>

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a><span data-ttu-id="e6592-967">웹 패키징</span><span class="sxs-lookup"><span data-stu-id="e6592-967">Web Packaging</span></span>

<span data-ttu-id="e6592-968">Visual Studio 2010는 Msdeploy.exe 도구를 사용 하 여 응용 프로그램에 대 한 압축 (.zip) 파일을 만듭니다 .이 파일을 *웹 패키지*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-968">Visual Studio 2010 uses the MSDeploy tool to create a compressed (.zip) file for your application, which is referred to as a *Web package*.</span></span> <span data-ttu-id="e6592-969">패키지 파일에는 응용 프로그램에 대 한 메타 데이터와 다음 콘텐츠가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-969">The package file contains metadata about your application plus the following content:</span></span>

- <span data-ttu-id="e6592-970">응용 프로그램 풀 설정, 오류 페이지 설정 등을 포함 하는 IIS 설정</span><span class="sxs-lookup"><span data-stu-id="e6592-970">IIS settings, which includes application pool settings, error page settings, and so on.</span></span>
- <span data-ttu-id="e6592-971">웹 페이지, 사용자 정의 컨트롤, 정적 콘텐츠 (이미지 및 HTML 파일) 등을 포함 하는 실제 웹 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="e6592-971">The actual Web content, which includes Web pages, user controls, static content (images and HTML files), and so on.</span></span>
- <span data-ttu-id="e6592-972">데이터베이스 스키마 및 데이터를 SQL Server 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-972">SQL Server database schemas and data.</span></span>
- <span data-ttu-id="e6592-973">보안 인증서, GAC에 설치 하는 구성 요소, 레지스트리 설정 등에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-973">Security certificates, components to install in the GAC, registry settings, and so on.</span></span>

<span data-ttu-id="e6592-974">웹 패키지를 모든 서버에 복사한 다음 IIS 관리자를 사용 하 여 수동으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-974">A Web package can be copied to any server and then installed manually by using IIS Manager.</span></span> <span data-ttu-id="e6592-975">또는 자동 배포의 경우 명령줄 명령을 사용 하거나 배포 Api를 사용 하 여 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-975">Alternatively, for automated deployment, the package can be installed by using command-line commands or by using deployment APIs.</span></span>

<span data-ttu-id="e6592-976">Visual Studio 2010은 웹 패키지를 만들기 위한 기본 제공 MSBuild 작업 및 대상을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-976">Visual Studio 2010 provides built in MSBuild tasks and targets to create Web packages.</span></span> <span data-ttu-id="e6592-977">자세한 내용은 MSDN 웹 사이트에서 [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) 를 참조 하 고 인 vishal Joshi의 블로그에서 [웹 패키지를 만들어야 하는 10 개](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) 이상의 이유를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-977">For more information, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) on the MSDN Web site and [10 + 20 reasons why you should create a Web Package](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a><span data-ttu-id="e6592-978">Web.config 변환</span><span class="sxs-lookup"><span data-stu-id="e6592-978">Web.config Transformation</span></span>

<span data-ttu-id="e6592-979">웹 응용 프로그램 배포의 경우 Visual Studio 2010에는 `Web.config` 파일을 개발 설정에서 프로덕션 설정으로 변환할 수 있는 기능인 [XML 문서 변환 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-979">For Web application deployment, Visual Studio 2010 introduces [XML Document Transform (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), which is a feature that lets you transform a `Web.config` file from development settings to production settings.</span></span> <span data-ttu-id="e6592-980">변환 설정은 `web.debug.config`, `web.release.config`등의 변환 파일에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-980">Transformation settings are specified in transform files named `web.debug.config`, `web.release.config`, and so on.</span></span> <span data-ttu-id="e6592-981">이러한 파일의 이름은 MSBuild 구성과 일치 합니다. 변환 파일에는 배포 된 `Web.config` 파일에 수행 해야 하는 변경 내용만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-981">(The names of these files match MSBuild configurations.) A transform file includes just the changes that you need to make to a deployed `Web.config` file.</span></span> <span data-ttu-id="e6592-982">간단한 구문을 사용 하 여 변경 내용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-982">You specify the changes by using simple syntax.</span></span>

<span data-ttu-id="e6592-983">다음 예제에서는 릴리스 구성의 배포에 대해 생성 될 수 있는 `web.release.config` 파일의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-983">The following example shows a portion of a `web.release.config` file that might be produced for deployment of your release configuration.</span></span> <span data-ttu-id="e6592-984">예제의 Replace 키워드는 배포 하는 동안 `Web.config` 파일의 *connectionString* 노드가 예제에 나열 된 값으로 대체 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-984">The Replace keyword in the example specifies that during deployment the *connectionString* node in the `Web.config` file will be replaced with the values that are listed in the example.</span></span>

[!code-xml[Main](overview/samples/sample102.xml)]

<span data-ttu-id="e6592-985">자세한 내용은 MSDN <a id="0.2_a"></a> 웹 사이트 및[웹 배포](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) 의 웹 [응용 프로그램 프로젝트 배포를 위한 Web.config 변환 구문](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) (인 vishal Joshi의 블로그에서 web.config 변환)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-985">For more information, see [Web.config Transformation Syntax for Web Application Project Deployment](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) on the MSDN <a id="0.2_a"></a> Web site and[Web Deployment: Web.Config Transformation](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a><span data-ttu-id="e6592-986">데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="e6592-986">Database Deployment</span></span>

<span data-ttu-id="e6592-987">Visual Studio 2010 배포 패키지에 SQL Server 데이터베이스에 대 한 종속성이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-987">A Visual Studio 2010 deployment package can include dependencies on SQL Server databases.</span></span> <span data-ttu-id="e6592-988">패키지 정의의 일부로 원본 데이터베이스에 대 한 연결 문자열을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-988">As part of the package definition, you provide the connection string for your source database.</span></span> <span data-ttu-id="e6592-989">웹 패키지를 만들 때 Visual Studio 2010는 데이터베이스 스키마에 대 한 SQL 스크립트를 만든 다음 필요에 따라 데이터를 패키지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-989">When you create the Web package, Visual Studio 2010 creates SQL scripts for the database schema and optionally for the data, and then adds these to the package.</span></span> <span data-ttu-id="e6592-990">또한 사용자 지정 SQL 스크립트를 제공 하 고 서버에서 실행 해야 하는 순서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-990">You can also provide custom SQL scripts and specify the sequence in which they should run on the server.</span></span> <span data-ttu-id="e6592-991">배포 시 대상 서버에 적절 한 연결 문자열을 제공 합니다. 그러면 배포 프로세스에서이 연결 문자열을 사용 하 여 데이터베이스 스키마를 만들고 데이터를 추가 하는 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-991">At deployment time, you provide a connection string that is appropriate for the target server; the deployment process then uses this connection string to run the scripts that create the database schema and add the data.</span></span>

<span data-ttu-id="e6592-992">또한 한 번 클릭 게시를 사용 하 여 응용 프로그램이 원격 공유 호스팅 사이트에 게시 될 때 데이터베이스를 직접 게시 하도록 배포를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-992">In addition, by using one-click publish, you can configure deployment to publish your database directly when the application is published to a remote shared hosting site.</span></span> <span data-ttu-id="e6592-993">자세한 내용은 MSDN 웹 사이트에서 [웹 응용 프로그램 프로젝트를 사용 하 여 데이터베이스 배포](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) 및 인 vishal Joshi의 블로그에서 [VS 2010를 사용 하 여 데이터베이스 배포](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-993">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) on the MSDN Web site and [Database Deployment with VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a><span data-ttu-id="e6592-994">한 번 클릭으로 웹 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="e6592-994">One-Click Publish for Web Applications</span></span>

<span data-ttu-id="e6592-995">Visual Studio 2010에서는 IIS 원격 관리 서비스를 사용 하 여 원격 서버에 웹 응용 프로그램을 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-995">Visual Studio 2010 also lets you use the IIS remote management service to publish a Web application to a remote server.</span></span> <span data-ttu-id="e6592-996">호스팅 계정 또는 테스트 서버나 준비 서버에 대 한 게시 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-996">You can create a publish profile for your hosting account or for testing servers or staging servers.</span></span> <span data-ttu-id="e6592-997">각 프로필은 적절 한 자격 증명을 안전 하 게 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-997">Each profile can save appropriate credentials securely.</span></span> <span data-ttu-id="e6592-998">그런 다음 한 번 클릭으로 웹 게시 도구 모음을 클릭 하 여 대상 서버에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-998">You can then deploy to any of the target servers with one click by using the Web one-click publish toolbar.</span></span> <span data-ttu-id="e6592-999">Visual Studio 2010에서는 MSBuild 명령줄을 사용 하 여 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-999">With Visual Studio 2010, you can also publish by using the MSBuild command line.</span></span> <span data-ttu-id="e6592-1000">이렇게 하면 연속 통합 모델에 게시를 포함 하도록 팀 빌드 환경을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1000">This lets you configure your team build environment to include publishing in a continuous-integration model.</span></span>

<span data-ttu-id="e6592-1001">자세한 내용은 MSDN 웹 사이트 및 웹에서 [한 번 클릭 게시 및 웹 배포를 사용 하 여 웹 응용 프로그램 프로젝트 배포](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) -인 vishal Joshi의 블로그에서 [VS 2010를 사용 하 여 게시를 클릭](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-1001">For more information, see [How to: Deploy a Web Application Project Using One-Click Publish and Web Deploy](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) on the MSDN Web site and [Web 1-Click Publish with VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) on Vishal Joshi's blog.</span></span> <span data-ttu-id="e6592-1002">Visual Studio 2010의 웹 응용 프로그램 배포에 대 한 비디오 프레젠테이션을 보려면 인 vishal Joshi의 블로그에서 [VS 2010 For Web Developer](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) preview를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-1002">To view video presentations about Web application deployment in Visual Studio 2010, see [VS 2010 for Web Developer Previews](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a><span data-ttu-id="e6592-1003">리소스</span><span class="sxs-lookup"><span data-stu-id="e6592-1003">Resources</span></span>

<span data-ttu-id="e6592-1004">다음 웹 사이트는 ASP.NET 4 및 Visual Studio 2010에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1004">The following Web sites provide additional information about ASP.NET 4 and Visual Studio 2010.</span></span>

- <span data-ttu-id="e6592-1005">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) -MSDN 웹 사이트에 있는 ASP.NET 4의 공식 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1005">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — The official documentation for ASP.NET 4 on the MSDN Web site.</span></span>
- <span data-ttu-id="e6592-1006">[https://www.asp.net/](https://www.asp.net/) -ASP.NET 팀 자체의 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1006">[https://www.asp.net/](https://www.asp.net/) — The ASP.NET team's own Web site.</span></span>
- <span data-ttu-id="e6592-1007">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) 및 [ASP.NET Dynamic Data 콘텐츠 맵](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) -ASP.NET 팀 사이트의 온라인 리소스와 ASP.NET Dynamic Data 공식 설명서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e6592-1007">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) and [ASP.NET Dynamic Data Content Map](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) — Online resources on the ASP.NET team site and in the official documentation for ASP.NET Dynamic Data.</span></span>
- <span data-ttu-id="e6592-1008">[https://www.asp.net/ajax/](../../ajax/index.md) -ASP.NET Ajax 개발을 위한 주 웹 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1008">[https://www.asp.net/ajax/](../../ajax/index.md) — The main Web resource for ASP.NET Ajax development.</span></span>
- <span data-ttu-id="e6592-1009">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) -visual Studio 2010의 기능에 대 한 정보를 포함 하는 Visual Web Developer 팀 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1009">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — The Visual Web Developer Team blog, which includes information about features in Visual Studio 2010.</span></span>
- <span data-ttu-id="e6592-1010">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -ASP.NET의 미리 보기 릴리스에 대 한 주 웹 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1010">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — The main Web resource for preview releases of ASP.NET.</span></span>

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a><span data-ttu-id="e6592-1011">고지 사항</span><span class="sxs-lookup"><span data-stu-id="e6592-1011">Disclaimer</span></span>

<span data-ttu-id="e6592-1012">본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1012">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="e6592-1013">이 문서에 포함된 정보는 게시 날짜 당시 논의된 문제에 대한 Microsoft Corporation의 현재 관점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1013">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="e6592-1014">Microsoft는 변화하는 시장 상황에 대응해야 하므로 Microsoft의 약속으로 해석되지 않아야 하며, Microsoft는 게시 날짜 이후 제시된 정보의 정확성을 보증하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1014">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="e6592-1015">이 백서는 정보를 제공할 목적으로만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1015">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="e6592-1016">MICROSOFT는 이 문서에 포함된 정보와 관련하여 명시적이든 암시적이든 어떠한 보증도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1016">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="e6592-1017">해당 저작권법을 준수하는 것은 사용자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1017">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="e6592-1018">저작권에서의 권리와는 별도로 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나 검색 시스템에 저장 또는 도입되거나 전송될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1018">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="e6592-1019">Microsoft는 이 설명서 본안에 관련된 특허권, 상표권, 저작권, 또는 기타 지적 재산권 등을 보유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1019">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="e6592-1020">서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 설명서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권 또는 기타 지적 재산권 등에 대한 어떠한 사용권도 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1020">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="e6592-1021">별도로 언급 하지 않는 한, 용례에 사용 된 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트는 실제 데이터가 아닙니다. 어떠한 실제 회사, 조직, 제품, 도메인 이름, 전자 메일에도 연결 되지 않습니다. 주소, 로고, 사람, 장소 또는 이벤트를 작성 하거나 유추 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1021">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="e6592-1022">© 2009 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="e6592-1022">© 2009 Microsoft Corporation.</span></span> <span data-ttu-id="e6592-1023">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="e6592-1023">All rights reserved.</span></span>

<span data-ttu-id="e6592-1024">Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1024">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="e6592-1025">여기에 인용된 실제 회사와 제품 이름은 해당 소유자의 상표일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6592-1025">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
