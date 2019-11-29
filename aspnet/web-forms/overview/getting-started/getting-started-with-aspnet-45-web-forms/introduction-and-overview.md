---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.7 Web Forms 및 Visual Studio 2017 시작 | Microsoft Docs
author: Erikre
description: 이 단계별 자습서 시리즈는 ASP.NET 4.7 및를 사용 하 여 ASP.NET Web Forms 응용 프로그램 빌드에 대 한 기본 사항을 알려 줍니다 Microsoft Visual Studio
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615460"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a><span data-ttu-id="e153b-103">ASP.NET 4.5 Web Forms 및 Visual Studio 2017 시작</span><span class="sxs-lookup"><span data-stu-id="e153b-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2017</span></span>

<span data-ttu-id="e153b-104">[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="e153b-104">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="e153b-105">이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio 2017를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-105">This tutorial series shows you how to build an ASP.NET Web Forms application with ASP.NET 4.5 and Microsoft Visual Studio 2017.</span></span> 

## <a name="introduction"></a><span data-ttu-id="e153b-106">소개</span><span class="sxs-lookup"><span data-stu-id="e153b-106">Introduction</span></span>

<span data-ttu-id="e153b-107">이 자습서 시리즈에서는 Visual Studio 2017 및 ASP.NET 4.5을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-107">This tutorial series guides you through creating an ASP.NET Web Forms application using Visual Studio 2017 and ASP.NET 4.5.</span></span> <span data-ttu-id="e153b-108">Storefront 라는 응용 프로그램을 만듭니다 .이 응용 프로그램은 **온라인에서 항목** 을 판매 하는 간단한 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-108">You'll create an application named **Wingtip Toys** - a simplified storefront web site selling items online.</span></span> <span data-ttu-id="e153b-109">시리즈 중에는 새 ASP.NET 4.5 기능이 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-109">During the series, new ASP.NET 4.5 features are highlighted.</span></span>

### <a name="target-audience"></a><span data-ttu-id="e153b-110">대상 사용자</span><span class="sxs-lookup"><span data-stu-id="e153b-110">Target audience</span></span>

<span data-ttu-id="e153b-111">ASP.NET Web Forms를 처음 접하는 개발자는이 자습서 시리즈의 대상 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-111">Developers new to ASP.NET Web Forms are the target audience for this tutorial series.</span></span>

<span data-ttu-id="e153b-112">다음 영역에 대 한 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-112">You should have some knowledge in the following areas:</span></span>

- <span data-ttu-id="e153b-113">OOP (개체 지향 프로그래밍) 및 언어</span><span class="sxs-lookup"><span data-stu-id="e153b-113">Object-oriented programming (OOP) and languages</span></span>
- <span data-ttu-id="e153b-114">웹 개발 (HTML, CSS, JavaScript)</span><span class="sxs-lookup"><span data-stu-id="e153b-114">Web development (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="e153b-115">관계형 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e153b-115">Relational databases</span></span>
- <span data-ttu-id="e153b-116">N 계층 아키텍처</span><span class="sxs-lookup"><span data-stu-id="e153b-116">N-tier architecture</span></span>

<span data-ttu-id="e153b-117">이러한 영역을 검토 하려면 다음 내용을 연구 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e153b-117">To review these areas, consider studying the following content:</span></span>

- [<span data-ttu-id="e153b-118">Visual C# 시작</span><span class="sxs-lookup"><span data-stu-id="e153b-118">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="e153b-119">[웹 개발](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="e153b-119">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="e153b-120">관계형 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e153b-120">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="e153b-121">다중 계층 아키텍처</span><span class="sxs-lookup"><span data-stu-id="e153b-121">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="e153b-122">응용 프로그램 기능</span><span class="sxs-lookup"><span data-stu-id="e153b-122">Application features</span></span>

<span data-ttu-id="e153b-123">이 시리즈에서 제공 되는 ASP.NET Web Form 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-123">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="e153b-124">웹 응용 프로그램 프로젝트 (웹 사이트 프로젝트가 아님)</span><span class="sxs-lookup"><span data-stu-id="e153b-124">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="e153b-125">Web Forms</span><span class="sxs-lookup"><span data-stu-id="e153b-125">Web Forms</span></span>
- <span data-ttu-id="e153b-126">마스터 페이지, 구성</span><span class="sxs-lookup"><span data-stu-id="e153b-126">Master Pages, Configuration</span></span>
- <span data-ttu-id="e153b-127">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="e153b-127">Bootstrap</span></span>
- <span data-ttu-id="e153b-128">Entity Framework Code First, LocalDB</span><span class="sxs-lookup"><span data-stu-id="e153b-128">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="e153b-129">요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e153b-129">Request Validation</span></span>
- <span data-ttu-id="e153b-130">강력한 형식의 데이터 컨트롤</span><span class="sxs-lookup"><span data-stu-id="e153b-130">Strongly-typed Data Controls</span></span>
- <span data-ttu-id="e153b-131">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="e153b-131">Model Binding</span></span>
- <span data-ttu-id="e153b-132">데이터 주석</span><span class="sxs-lookup"><span data-stu-id="e153b-132">Data Annotations</span></span>
- <span data-ttu-id="e153b-133">값 공급자</span><span class="sxs-lookup"><span data-stu-id="e153b-133">Value Providers</span></span>
- <span data-ttu-id="e153b-134">SSL 및 OAuth</span><span class="sxs-lookup"><span data-stu-id="e153b-134">SSL and OAuth</span></span>
- <span data-ttu-id="e153b-135">ASP.NET Identity, 구성 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="e153b-135">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="e153b-136">조심 스럽게 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e153b-136">Unobtrusive Validation</span></span>
- <span data-ttu-id="e153b-137">라우팅</span><span class="sxs-lookup"><span data-stu-id="e153b-137">Routing</span></span>
- <span data-ttu-id="e153b-138">ASP.NET 오류 처리</span><span class="sxs-lookup"><span data-stu-id="e153b-138">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="e153b-139">응용 프로그램 시나리오 및 작업</span><span class="sxs-lookup"><span data-stu-id="e153b-139">Application scenarios and tasks</span></span>

<span data-ttu-id="e153b-140">자습서 시리즈 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-140">Tutorial series tasks include:</span></span>

- <span data-ttu-id="e153b-141">새 프로젝트 만들기, 검토 및 실행</span><span class="sxs-lookup"><span data-stu-id="e153b-141">Creating, reviewing, and running a new project</span></span>
- <span data-ttu-id="e153b-142">데이터베이스 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="e153b-142">Creating a database structure</span></span>
- <span data-ttu-id="e153b-143">데이터베이스 초기화 및 시드</span><span class="sxs-lookup"><span data-stu-id="e153b-143">Initializing and seeding a database</span></span>
- <span data-ttu-id="e153b-144">스타일, 그래픽 및 마스터 페이지를 사용 하 여 UI 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="e153b-144">Customizing the UI with styles, graphics, and a master page</span></span>
- <span data-ttu-id="e153b-145">페이지 및 탐색 추가</span><span class="sxs-lookup"><span data-stu-id="e153b-145">Adding pages and navigation</span></span>
- <span data-ttu-id="e153b-146">메뉴 세부 정보 및 제품 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="e153b-146">Displaying menu details and product data</span></span>
- <span data-ttu-id="e153b-147">쇼핑 카트 만들기</span><span class="sxs-lookup"><span data-stu-id="e153b-147">Creating a shopping cart</span></span>
- <span data-ttu-id="e153b-148">SSL 및 OAuth 지원 추가</span><span class="sxs-lookup"><span data-stu-id="e153b-148">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="e153b-149">지불 방법 추가</span><span class="sxs-lookup"><span data-stu-id="e153b-149">Adding a payment method</span></span>
- <span data-ttu-id="e153b-150">응용 프로그램에 관리자 역할 및 사용자 포함</span><span class="sxs-lookup"><span data-stu-id="e153b-150">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="e153b-151">특정 페이지 및 폴더에 대 한 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="e153b-151">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="e153b-152">웹 응용 프로그램에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="e153b-152">Uploading a file to the web application</span></span>
- <span data-ttu-id="e153b-153">입력 유효성 검사 구현</span><span class="sxs-lookup"><span data-stu-id="e153b-153">Implementing input validation</span></span>
- <span data-ttu-id="e153b-154">웹 응용 프로그램에 대 한 경로 등록</span><span class="sxs-lookup"><span data-stu-id="e153b-154">Registering routes for the web application</span></span>
- <span data-ttu-id="e153b-155">오류 처리 및 오류 로깅 구현</span><span class="sxs-lookup"><span data-stu-id="e153b-155">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="e153b-156">개요</span><span class="sxs-lookup"><span data-stu-id="e153b-156">Overview</span></span>

<span data-ttu-id="e153b-157">이 자습서 시리즈는 프로그래밍 개념에 익숙한 사용자를 대상으로 하지만 ASP.NET Web Forms를 처음 사용 하는 사용자를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-157">This tutorial series is intended for someone familiar with programming concepts, but new to ASP.NET Web Forms.</span></span> <span data-ttu-id="e153b-158">ASP.NET Web Forms에 대해 잘 알고 있는 경우에도이 시리즈는 새로운 ASP.NET 4.5 기능에 대해 배우는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-158">If you're already familiar with ASP.NET Web Forms, this series can still help you learn about new ASP.NET 4.5 features.</span></span> <span data-ttu-id="e153b-159">프로그래밍 개념 및 ASP.NET Web Forms에 익숙하지 않은 독자의 경우 ASP.NET 웹 사이트의 [시작](../../../index.md) 섹션에서 제공 하는 추가 Web Forms 자습서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e153b-159">For readers unfamiliar with programming concepts and ASP.NET Web Forms, see the additional Web Forms tutorials provided in the [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="e153b-160">이 자습서 시리즈에 제공 된 ASP.NET 4.5에는 다음과 같은 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-160">The ASP.NET 4.5 provided in this tutorial series includes the following features:</span></span>

- <span data-ttu-id="e153b-161">많은 ASP.NET 프레임 워크 (Web Forms, MVC 및 Web API) [에 대 한 지원을](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) 제공 하는 프로젝트를 만드는 간단한 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-161">A simple UI for creating projects that offers [support for many ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="e153b-162">[부트스트랩](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), 레이아웃, 테마 및 응답성이 뛰어난 디자인 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-162">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout, theming, and responsive design framework.</span></span>
- <span data-ttu-id="e153b-163">[ASP.NET Identity](../../../../identity/index.md)모든 ASP.NET 프레임 워크에서 동일 하 게 작동 하며 IIS 이외의 웹 호스팅 소프트웨어와 작동 하는 새로운 ASP.NET 멤버 자격 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-163">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- [<span data-ttu-id="e153b-164">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="e153b-164">Entity Framework 6</span></span>](https://msdn.microsoft.com/data/ef.aspx)

  <span data-ttu-id="e153b-165">Entity Framework 업데이트를 사용 하 여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-165">An update to the Entity Framework enabling you to:</span></span>
  - <span data-ttu-id="e153b-166">데이터를 강력한 형식의 개체로 검색 및 조작</span><span class="sxs-lookup"><span data-stu-id="e153b-166">Retrieve and manipulate data as strongly-typed objects</span></span>
  - <span data-ttu-id="e153b-167">비동기적으로 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="e153b-167">Access data asynchronously</span></span>
  - <span data-ttu-id="e153b-168">일시적인 연결 오류 처리</span><span class="sxs-lookup"><span data-stu-id="e153b-168">Handle transient connection faults</span></span>
  - <span data-ttu-id="e153b-169">로그 SQL 문</span><span class="sxs-lookup"><span data-stu-id="e153b-169">Log SQL statements</span></span>

<span data-ttu-id="e153b-170">전체 ASP.NET 4.5 기능 목록은 [ASP.NET 및 Web Tools Visual Studio 2013 릴리스 정보](../../../../visual-studio/overview/2013/release-notes.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e153b-170">For a complete ASP.NET 4.5 feature list, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="e153b-171">정문 장난감 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e153b-171">The Wingtip Toys sample application</span></span>

<span data-ttu-id="e153b-172">다음 스크린샷은이 자습서 시리즈에서 만든 ASP.NET Web Forms 응용 프로그램에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-172">The following screenshots are from the ASP.NET Web Forms application that you create in this tutorial series.</span></span> <span data-ttu-id="e153b-173">Visual Studio에서 응용 프로그램을 실행 하면 다음 웹 홈 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-173">When you run the application in Visual Studio, the following web Home page appears.</span></span>

![정문 장난감-기본 페이지](introduction-and-overview/_static/image1.png)

<span data-ttu-id="e153b-175">새 사용자로 등록 하거나 기존 사용자로 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-175">You can register as a new user, or sign in as an existing user.</span></span> <span data-ttu-id="e153b-176">상단 탐색에는 데이터베이스에서 제품 범주와 해당 제품에 대 한 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-176">The top navigation has links to product categories and their products from the database.</span></span>

<span data-ttu-id="e153b-177">**제품**을 선택 하면 사용 가능한 모든 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-177">If you select **Products**, all available products are displayed.</span></span> 

![정문 장난감-제품](introduction-and-overview/_static/image2.png)

<span data-ttu-id="e153b-179">특정 제품을 선택 하는 경우 제품 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-179">If you select a specific product, product details are displayed.</span></span>

![정문 장난감-제품 세부 정보](introduction-and-overview/_static/image3.png)

<span data-ttu-id="e153b-181">사용자는 Web Forms 템플릿 기본 기능을 사용 하 여 등록 하 고 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-181">As a user, you can register and sign in with Web Forms template default functionality.</span></span> <span data-ttu-id="e153b-182">이 자습서에서는 기존 Gmail 계정을 사용 하 여 로그인 하는 방법에 대해서도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-182">This tutorial also explains how to sign in using an existing Gmail account.</span></span> <span data-ttu-id="e153b-183">또한 관리자 권한으로 로그인 하 여 데이터베이스에서 제품을 추가 하 고 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-183">Additionally, you can sign in as the administrator to add and remove products from the database.</span></span>

![동 장난감-로그인](introduction-and-overview/_static/image4.png)

<span data-ttu-id="e153b-185">사용자로 로그인 한 후에는 쇼핑 카트에 제품을 추가 하 고 PayPal으로 체크 아웃할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-185">Once you've signed in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="e153b-186">샘플 응용 프로그램은 PayPal의 개발자 샌드박스에서 사용할 수 있도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-186">The sample application is designed to work in PayPal's developer sandbox.</span></span> <span data-ttu-id="e153b-187">실제 money 트랜잭션은 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-187">No actual money transaction takes place.</span></span>

![정문 장난감-쇼핑 카트](introduction-and-overview/_static/image5.png)

<span data-ttu-id="e153b-189">PayPal은 계정, 주문 및 지불 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-189">PayPal confirms your account, order, and payment information.</span></span>

![동 장난감-PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="e153b-191">PayPal에서 반환 된 후 주문을 검토 하 고 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-191">After returning from PayPal, you can review and complete your order.</span></span>

![동 장난감 주문 검토](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="e153b-193">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e153b-193">Prerequisites</span></span>

<span data-ttu-id="e153b-194">시작 하기 전에 다음 소프트웨어가 컴퓨터에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-194">Before you start, make sure the following software is installed on your computer:</span></span>

- <span data-ttu-id="e153b-195">[Microsoft Visual Studio 2017 또는 Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e153b-195">[Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span></span>

<span data-ttu-id="e153b-196">.NET Framework 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-196">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="e153b-197">이 자습서 시리즈에서는 Microsoft Visual Studio Community 2017를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-197">This tutorial series uses Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="e153b-198">또는 Microsoft Visual Studio 2017를 사용 하 여이 자습서 시리즈를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-198">You can use either that or Microsoft Visual Studio 2017 to complete this tutorial series.</span></span>

<span data-ttu-id="e153b-199">Visual Studio에 대 한 다음 사항에 유의 하세요.</span><span class="sxs-lookup"><span data-stu-id="e153b-199">Note the following about Visual Studio:</span></span>

* <span data-ttu-id="e153b-200">Microsoft Visual Studio 2017 및 Microsoft Visual Studio Community 2017은이 자습서 시리즈 전체에서 *Visual Studio* 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-200">Microsoft Visual Studio 2017 and Microsoft Visual Studio Community 2017 are referred to as *Visual Studio* throughout this tutorial series.</span></span>

* <span data-ttu-id="e153b-201">Visual Studio 2017는 이미 설치 된 이전 버전 옆에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-201">Visual Studio 2017 is installed next to any older versions already installed.</span></span> <span data-ttu-id="e153b-202">이전 버전에서 만든 사이트는 Visual Studio 2017에서 열 수 있으며 이전 버전에서 계속 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-202">Sites created in earlier versions can be opened in Visual Studio 2017 and continue to open in previous versions.</span></span>

* <span data-ttu-id="e153b-203">처음 Visual Studio를 시작할 때 *웹 개발* 설정을 선택 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-203">The first time you started Visual Studio, it is assumed you selected the *Web Development* settings.</span></span> <span data-ttu-id="e153b-204">자세한 내용은 [방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e153b-204">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

<span data-ttu-id="e153b-205">필수 구성 요소를 설치한 후이 자습서 시리즈에 제공 된 웹 프로젝트를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-205">After installing the prerequisites, you're ready to begin creating the Web project presented in this tutorial series.</span></span>

## <a name="download-the-sample-application"></a><span data-ttu-id="e153b-206">샘플 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="e153b-206">Download the sample application</span></span>

 <span data-ttu-id="e153b-207">언제 든 지 MSDN Samples 사이트에서 완성 된 샘플 응용 프로그램을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-207">You can download the completed sample application at anytime from the MSDN Samples site:</span></span>

<span data-ttu-id="e153b-208">[ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작-동 장난감](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="e153b-208">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

 <span data-ttu-id="e153b-209">이 다운로드에는 다음과 같은 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-209">This download has the following items:</span></span>

- <span data-ttu-id="e153b-210">*WingtipToys* 폴더에 있는 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-210">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="e153b-211">*WingtipToys* 폴더의 *WingtipToys* 폴더에서 샘플 응용 프로그램을 만드는 데 사용 되는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-211">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

<span data-ttu-id="e153b-212">다운로드는 *.zip* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-212">The download is a *.zip* file.</span></span> <span data-ttu-id="e153b-213">이 자습서 시리즈에서 만든 완료 된 프로젝트를 보려면 .zip 파일에서 *C#* 폴더를 찾아서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-213">To see the completed project that this tutorial series creates, find and select the *C#* folder in the .zip file.</span></span> <span data-ttu-id="e153b-214">Visual Studio C# 프로젝트 작업에 사용 하는 폴더에 폴더를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-214">Save the C# folder to the folder you use to work with Visual Studio projects.</span></span> <span data-ttu-id="e153b-215">기본적으로 Visual Studio 2017 projects 폴더는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-215">By default, the Visual Studio 2017 projects folder is:</span></span>

<span data-ttu-id="e153b-216"><strong>C:\Users&#92;</strong>  <strong><em>&lt;username&gt;</em></strong> <strong>\source\repos</strong></span><span class="sxs-lookup"><span data-stu-id="e153b-216"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong></span></span>

<span data-ttu-id="e153b-217">***C#*** 폴더 이름을 ***WingtipToys***로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-217">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="e153b-218">프로젝트 폴더에 이름이 *WingtipToys* 인 폴더가 이미 있는 경우 *C#* 폴더 이름을 *WingtipToys*로 바꾸기 전에 기존 폴더의 이름을 임시로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-218">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>

<span data-ttu-id="e153b-219">완료 된 프로젝트를 실행 하려면 *WingtipToys* 폴더를 열고 *WingtipToys* 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-219">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="e153b-220">Visual Studio 2017에서 프로젝트가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-220">Visual Studio 2017 opens the project.</span></span> <span data-ttu-id="e153b-221">다음으로 **솔루션 탐색기** 에서 default.aspx 파일을 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 보기**를 *선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="e153b-221">Next, right-click the *Default.aspx* file in **Solution Explorer** and select **View In Browser**.</span></span>

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a><span data-ttu-id="e153b-222">ASP.NET Web Forms 퀴즈를 사용 하 여 콘텐츠 검토</span><span class="sxs-lookup"><span data-stu-id="e153b-222">Take a ASP.NET Web Forms quiz to review content</span></span>

<span data-ttu-id="e153b-223">자습서 시리즈를 완료 한 후 퀴즈를 수행 하 여 지식을 테스트 하 고 주요 개념을 보강 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-223">After completing the tutorial series, take a quiz to test your knowledge and reinforce key concepts.</span></span> <span data-ttu-id="e153b-224">각 질문은 설명 및 추가 지침에 대 한 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-224">Each question provides an explanation and links to additional guidance.</span></span>

* [<span data-ttu-id="e153b-225">ASP.NET Web Forms 퀴즈</span><span class="sxs-lookup"><span data-stu-id="e153b-225">ASP.NET Web Forms Quiz</span></span>](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a><span data-ttu-id="e153b-226">자습서 지원 및 주석</span><span class="sxs-lookup"><span data-stu-id="e153b-226">Tutorial support and comments</span></span>

<span data-ttu-id="e153b-227">질문과 의견은 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013-정문 장난감](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 샘플 페이지에 포함 된 Q 및 섹션을 사용 하세요.</span><span class="sxs-lookup"><span data-stu-id="e153b-227">For questions and comments, use the Q and A section included on the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span>

<span data-ttu-id="e153b-228">이 자습서 시리즈에 대 한 설명은 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-228">Comments on this tutorial series are welcome.</span></span> <span data-ttu-id="e153b-229">이 자습서 시리즈를 업데이트 한 후에는 향상 된 기능에 대 한 수정 또는 제안을 고려 하 여 모든 노력이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-229">When this tutorial series is updated, every effort is made to consider corrections or suggestions for improvements.</span></span>

<span data-ttu-id="e153b-230">오류가 발생 하는 경우 문제를 해결 하는 방법에 대 한 설명이 없는 해당 오류 메시지가 혼란 스 러 울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-230">If an error occurs, the corresponding error messages could be confusing, with no good explanation on how to fix it.</span></span> <span data-ttu-id="e153b-231">도움말은 [ASP.NET 포럼](https://forums.asp.net/)을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-231">For help, you can check the [ASP.NET forums](https://forums.asp.net/).</span></span> <span data-ttu-id="e153b-232">또 다른 좋은 소스는 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013-정문 장난감](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 샘플 페이지의 Q 및 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="e153b-232">Another good source is the Q and A section in the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="e153b-233">다음</span><span class="sxs-lookup"><span data-stu-id="e153b-233">Next</span></span>](create-the-project.md)
