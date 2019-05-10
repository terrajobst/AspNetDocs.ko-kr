---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/index
title: Visual Studio 2008 및 이전 버전의 웹 사이트 프로젝트 배포 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 응용 프로그램은 일반적으로 설계, 생성 및 로컬 개발 환경에서 테스트 및 프로덕션 환경 o에 배포 해야 하는 중...
ms.author: riande
ms.date: 05/16/2012
ms.assetid: 6f72bde8-f2f1-4e4a-94e5-494c3c153c14
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects
msc.type: chapter
ms.openlocfilehash: 43c2397ef4ccc5eacb2ff4c5d04f62b9c8c481b7
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65134419"
---
# <a name="deploying-web-site-projects-in-visual-studio-2008-and-earlier"></a><span data-ttu-id="b9edd-103">Visual Studio 2008 이하에서 웹 사이트 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="b9edd-103">Deploying Web Site Projects in Visual Studio 2008 and earlier</span></span>

> <span data-ttu-id="b9edd-104">ASP.NET 웹 응용 프로그램은 일반적으로 디자인, 생성 및 테스트 로컬 개발 환경 및 릴리스에 대 한 준비가 되 면 프로덕션 환경에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9edd-104">ASP.NET web applications are typically designed, created, and tested in a local development environment and need to be deployed to a production environment once it is ready for release.</span></span> <span data-ttu-id="b9edd-105">이 자습서 시리즈 배포 프로세스를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b9edd-105">This tutorial series details the deployment process.</span></span>

- [<span data-ttu-id="b9edd-106">ASP.NET 호스팅 옵션(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-106">ASP.NET Hosting Options (C#)</span></span>](asp-net-hosting-options-cs.md)
- [<span data-ttu-id="b9edd-107">배포할 파일 확인(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-107">Determining What Files Need to Be Deployed (C#)</span></span>](determining-what-files-need-to-be-deployed-cs.md)
- [<span data-ttu-id="b9edd-108">FTP 클라이언트를 사용하여 사이트 배포(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-108">Deploying Your Site Using an FTP Client (C#)</span></span>](deploying-your-site-using-an-ftp-client-cs.md)
- [<span data-ttu-id="b9edd-109">Visual Studio를 사용하여 사이트 배포(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-109">Deploying Your Site Using Visual Studio (C#)</span></span>](deploying-your-site-using-visual-studio-cs.md)
- [<span data-ttu-id="b9edd-110">개발 환경과 프로덕션 환경의 일반적인 구성 차이(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-110">Common Configuration Differences Between Development and Production (C#)</span></span>](common-configuration-differences-between-development-and-production-cs.md)
- [<span data-ttu-id="b9edd-111">IIS와 ASP.NET 개발 서버의 결정적 차이(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-111">Core Differences Between IIS and the ASP.NET Development Server (C#)</span></span>](core-differences-between-iis-and-the-asp-net-development-server-cs.md)
- [<span data-ttu-id="b9edd-112">데이터베이스 배포(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-112">Deploying a Database (C#)</span></span>](deploying-a-database-cs.md)
- [<span data-ttu-id="b9edd-113">프로덕션 데이터베이스를 사용하도록 프로덕션 웹 애플리케이션 구성(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-113">Configuring the Production Web Application to Use the Production Database (C#)</span></span>](configuring-the-production-web-application-to-use-the-production-database-cs.md)
- [<span data-ttu-id="b9edd-114">애플리케이션 서비스를 사용하는 웹 사이트 구성(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-114">Configuring a Website that Uses Application Services (C#)</span></span>](configuring-a-website-that-uses-application-services-cs.md)
- [<span data-ttu-id="b9edd-115">데이터베이스 개발 및 배포 전략(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-115">Strategies for Database Development and Deployment (C#)</span></span>](strategies-for-database-development-and-deployment-cs.md)
- [<span data-ttu-id="b9edd-116">사용자 지정 오류 페이지 표시(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-116">Displaying a Custom Error Page (C#)</span></span>](displaying-a-custom-error-page-cs.md)
- [<span data-ttu-id="b9edd-117">처리되지 않은 예외 처리(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-117">Processing Unhandled Exceptions (C#)</span></span>](processing-unhandled-exceptions-cs.md)
- [<span data-ttu-id="b9edd-118">ASP.NET 상태 모니터링을 사용하여 오류 세부 정보 로깅(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-118">Logging Error Details with ASP.NET Health Monitoring (C#)</span></span>](logging-error-details-with-asp-net-health-monitoring-cs.md)
- [<span data-ttu-id="b9edd-119">ELMAH를 사용하여 오류 세부 정보 로깅(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-119">Logging Error Details with ELMAH (C#)</span></span>](logging-error-details-with-elmah-cs.md)
- [<span data-ttu-id="b9edd-120">웹 사이트 미리 컴파일(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-120">Precompiling Your Website (C#)</span></span>](precompiling-your-website-cs.md)
- [<span data-ttu-id="b9edd-121">프로덕션 웹 사이트의 사용자 및 역할(C#)</span><span class="sxs-lookup"><span data-stu-id="b9edd-121">Users and Roles On Production Website (C#)</span></span>](users-and-roles-on-the-production-website-cs.md)
- [<span data-ttu-id="b9edd-122">ASP.NET 호스팅 옵션(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-122">ASP.NET Hosting Options (VB)</span></span>](asp-net-hosting-options-vb.md)
- [<span data-ttu-id="b9edd-123">배포할 파일 확인(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-123">Determining What Files Need to Be Deployed (VB)</span></span>](determining-what-files-need-to-be-deployed-vb.md)
- [<span data-ttu-id="b9edd-124">FTP 클라이언트를 사용하여 사이트 배포(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-124">Deploying Your Site Using an FTP Client (VB)</span></span>](deploying-your-site-using-an-ftp-client-vb.md)
- [<span data-ttu-id="b9edd-125">Visual Studio를 사용하여 사이트 배포(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-125">Deploying Your Site Using Visual Studio (VB)</span></span>](deploying-your-site-using-visual-studio-vb.md)
- [<span data-ttu-id="b9edd-126">개발 환경과 프로덕션 환경의 일반적인 구성 차이(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-126">Common Configuration Differences Between Development and Production (VB)</span></span>](common-configuration-differences-between-development-and-production-vb.md)
- [<span data-ttu-id="b9edd-127">IIS와 ASP.NET 개발 서버의 결정적 차이(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-127">Core Differences Between IIS and the ASP.NET Development Server (VB)</span></span>](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
- [<span data-ttu-id="b9edd-128">데이터베이스 배포(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-128">Deploying a Database (VB)</span></span>](deploying-a-database-vb.md)
- [<span data-ttu-id="b9edd-129">프로덕션 데이터베이스를 사용하도록 프로덕션 웹 애플리케이션 구성(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-129">Configuring the Production Web Application to Use the Production Database (VB)</span></span>](configuring-the-production-web-application-to-use-the-production-database-vb.md)
- [<span data-ttu-id="b9edd-130">애플리케이션 서비스를 사용하는 웹 사이트 구성(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-130">Configuring a Website that Uses Application Services (VB)</span></span>](configuring-a-website-that-uses-application-services-vb.md)
- [<span data-ttu-id="b9edd-131">데이터베이스 개발 및 배포 전략(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-131">Strategies for Database Development and Deployment (VB)</span></span>](strategies-for-database-development-and-deployment-vb.md)
- [<span data-ttu-id="b9edd-132">사용자 지정 오류 페이지 표시(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-132">Displaying a Custom Error Page (VB)</span></span>](displaying-a-custom-error-page-vb.md)
- [<span data-ttu-id="b9edd-133">처리되지 않은 예외 처리(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-133">Processing Unhandled Exceptions (VB)</span></span>](processing-unhandled-exceptions-vb.md)
- [<span data-ttu-id="b9edd-134">ASP.NET 상태 모니터링을 사용하여 오류 세부 정보 로깅(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-134">Logging Error Details with ASP.NET Health Monitoring (VB)</span></span>](logging-error-details-with-asp-net-health-monitoring-vb.md)
- [<span data-ttu-id="b9edd-135">ELMAH를 사용하여 오류 세부 정보 로깅(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-135">Logging Error Details with ELMAH (VB)</span></span>](logging-error-details-with-elmah-vb.md)
- [<span data-ttu-id="b9edd-136">웹 사이트 미리 컴파일(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-136">Precompiling Your Website (VB)</span></span>](precompiling-your-website-vb.md)
- [<span data-ttu-id="b9edd-137">프로덕션 웹 사이트의 사용자 및 역할(VB)</span><span class="sxs-lookup"><span data-stu-id="b9edd-137">Users and Roles On Production Website (VB)</span></span>](users-and-roles-on-the-production-website-vb.md)
