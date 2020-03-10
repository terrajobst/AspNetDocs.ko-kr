---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: 이를 위한 NerdDinner 자습서 소개 | Microsoft Docs
author: shanselman
description: 새 프레임 워크를 학습 하는 가장 좋은 방법은이를 사용 하 여 항목을 빌드하는 것입니다. 이 자습서에서는 ASP.NE를 사용 하 여 작고 완전 한 응용 프로그램을 빌드하는 방법을 안내 합니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468935"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="bc255-104">NerdDinner 자습서 소개</span><span class="sxs-lookup"><span data-stu-id="bc255-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="bc255-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="bc255-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="bc255-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="bc255-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="bc255-107">새 프레임 워크를 학습 하는 가장 좋은 방법은이를 사용 하 여 항목을 빌드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="bc255-108">이 자습서에서는 ASP.NET MVC 1을 사용 하 여 작고 완전 한 응용 프로그램을 빌드하는 방법을 안내 하 고 그 뒤에 핵심 개념 중 일부를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="bc255-109">ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-tutorial"></a><span data-ttu-id="bc255-110">NerdDinner 자습서</span><span class="sxs-lookup"><span data-stu-id="bc255-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="bc255-111">새 프레임 워크를 학습 하는 가장 좋은 방법은이를 사용 하 여 항목을 빌드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="bc255-112">이 자습서에서는 ASP.NET MVC를 사용 하 여 작고 완전 한 응용 프로그램을 빌드하는 방법을 안내 하 고 그 뒤에 나오는 핵심 개념 중 일부를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="bc255-113">빌드 하려는 응용 프로그램을 "가 중 Ddinner" 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="bc255-114">Dinners Ddinner는 사람들이 온라인으로 온라인으로 찾고 구성할 수 있는 쉬운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="bc255-115">Dinners Ddinner를 사용 하면 등록 된 사용자가을 만들고 편집 하 고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="bc255-116">응용 프로그램에서 일관성 있는 유효성 검사 및 비즈니스 규칙 집합을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="bc255-117">방문자는 AJAX 기반 지도를 사용 하 여 근처에 보관 될 예정 dinners를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="bc255-118">저녁을 클릭 하면 세부 정보 페이지로 이동 하 여 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="bc255-119">저녁에 참석 하는 데 관심이 있는 경우 사이트에 로그인 하거나 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="bc255-120">그런 다음 AJAX 기반 RSVP 링크를 클릭 하 여 이벤트에 참석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="bc255-121">하는 경우의 NerdDinner 구현</span><span class="sxs-lookup"><span data-stu-id="bc255-121">Implementing NerdDinner</span></span>

<span data-ttu-id="bc255-122">Visual Studio 내에서 파일-&gt;새 프로젝트 명령을 사용 하 여 새 ASP.NET MVC 프로젝트를 만들기 위해 microsoft에서 고객의 NerdDinner 응용 프로그램을 시작할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="bc255-123">그런 다음 기능 및 기능을 증분 방식으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="bc255-124">다룰 방법:</span><span class="sxs-lookup"><span data-stu-id="bc255-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="bc255-125">새 ASP.NET MVC 프로젝트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="bc255-126">데이터베이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="bc255-127">비즈니스 규칙 유효성 검사를 사용 하 여 모델을 작성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="bc255-128">컨트롤러 및 뷰를 사용 하 여 목록/세부 정보 UI를 구현 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="bc255-129">CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원을 제공 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="bc255-130">ViewData를 사용 하 고 ViewModel 클래스를 구현 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="bc255-131">마스터 페이지 및 부분를 사용 하 여 UI를 다시 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="bc255-132">효율적인 데이터 페이징을 구현 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="bc255-133">인증 및 권한 부여를 사용 하 여 응용 프로그램을 보호 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="bc255-134">AJAX를 사용 하 여 동적 업데이트를 제공 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="bc255-135">AJAX를 사용 하 여 매핑 시나리오를 구현 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="bc255-136">자동화 된 단위 테스트를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc255-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="bc255-137">이 챕터에서 연습 하는 각 단계를 완료 하 여 처음부터 개별 사용자의 고유한 복사본을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="bc255-138">또는 [GitHub의 Nerddinner에서](https://github.com/AspNetMVPSamples/NerdDinner)전체 버전의 소스 코드를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="bc255-139">또한 자습서를 오프 라인으로 읽으려고 하는 경우 필요에 따라 [이 자습서의 무료 PDF 버전을 다운로드할](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="bc255-140">Visual Studio 2008 또는 무료 Visual Web Developer 2008 Express를 사용 하 여 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="bc255-141">데이터베이스에 SQL Server 또는 무료 SQL Server Express를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="bc255-142">[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 의 V2를 사용 하 여 ASP.NET MVC, Visual Web Developer 2008 Express 및 SQL Server Express (모두 무료로)를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="bc255-143">이제 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-143">Now let's get started....</span></span>

<span data-ttu-id="bc255-144">이제 되셨나요?의 부분을 살펴보았습니다. 이제 코드를 작성 하 고 몇 가지 코드를 작성 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="bc255-145">먼저 Visual Studio 내에서 파일&gt;새 프로젝트를 사용 하 여 공동으로 사용 하는 Ddinner 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc255-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bc255-146">다음</span><span class="sxs-lookup"><span data-stu-id="bc255-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
