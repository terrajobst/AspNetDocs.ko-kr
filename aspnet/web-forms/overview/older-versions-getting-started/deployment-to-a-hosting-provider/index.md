---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/index
title: ASP.NET 4-Visual Studio를 사용 하 여 SQL Server Compact 웹 배포 | Microsoft Docs
author: rick-anderson
description: 이 자습서 시리즈는 인터넷을 통해 사용할 수 있는 SQL Server Compact를 사용 하는 ASP.NET 웹 응용 프로그램을 타사 h ...로 배포 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/29/2011
ms.assetid: 6798c7e4-f08e-4802-9fa5-443f67d5df62
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider
msc.type: chapter
ms.openlocfilehash: bb9a47eeb4197348e85bb469b68c0055e7c696a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514697"
---
# <a name="aspnet-4---web-deployment-with-sql-server-compact-using-visual-studio"></a><span data-ttu-id="a2606-103">ASP.NET 4 - Visual Studio를 사용하여 SQL Server Compact로 웹 배포</span><span class="sxs-lookup"><span data-stu-id="a2606-103">ASP.NET 4 - Web Deployment with SQL Server Compact using Visual Studio</span></span>

> <span data-ttu-id="a2606-104">이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 SQL Server Compact 사용 하 여 인터넷을 통해 사용할 수 있는 웹 응용 프로그램을 타사 호스팅 공급자에 게 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2606-104">This tutorial series shows how to make an ASP.NET web application that uses SQL Server Compact available over the internet by deploying it to a third-party hosting provider.</span></span> <span data-ttu-id="a2606-105">Visual Studio 2012 RC 또는 Visual Studio 2010가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2606-105">Requires Visual Studio 2012 RC or Visual Studio 2010.</span></span> <span data-ttu-id="a2606-106">배포 기능에 대 한 최신 정보 또는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법에 대 한 자세한 내용은 [Visual Studio를 사용 하 여 웹 배포 ASP.NET](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a2606-106">For more up-to-date information about deployment features, or for information about how to deploy SQL Server editions other than SQL Server Compact, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

- [<span data-ttu-id="a2606-107">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - 소개</span><span class="sxs-lookup"><span data-stu-id="a2606-107">Visual Studio Web Deployment with SQL Server Compact - Introduction</span></span>](deployment-to-a-hosting-provider-introduction-1-of-12.md)
- [<span data-ttu-id="a2606-108">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - SQL Server Compact 데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="a2606-108">Visual Studio Web Deployment with SQL Server Compact- Deploying SQL Server Compact Databases</span></span>](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
- [<span data-ttu-id="a2606-109">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - Web.Config 파일 변환</span><span class="sxs-lookup"><span data-stu-id="a2606-109">Visual Studio Web Deployment with SQL Server Compact - Web.Config File Transformations</span></span>](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
- [<span data-ttu-id="a2606-110">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - 프로젝트 속성 구성</span><span class="sxs-lookup"><span data-stu-id="a2606-110">Visual Studio Web Deployment with SQL Server Compact - Configuring Project Properties</span></span>](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
- [<span data-ttu-id="a2606-111">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - IIS에 테스트 환경으로 배포</span><span class="sxs-lookup"><span data-stu-id="a2606-111">Visual Studio Web Deployment with SQL Server Compact - Deploying to IIS as a Test Environment</span></span>](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
- [<span data-ttu-id="a2606-112">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - 폴더 권한 설정</span><span class="sxs-lookup"><span data-stu-id="a2606-112">Visual Studio Web Deployment with SQL Server Compact - Setting Folder Permissions</span></span>](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
- [<span data-ttu-id="a2606-113">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - 프로덕션 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="a2606-113">Visual Studio Web Deployment with SQL Server Compact - Deploying to the Production Environment</span></span>](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
- [<span data-ttu-id="a2606-114">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - 코드 전용 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="a2606-114">Visual Studio Web Deployment with SQL Server Compact - Deploying a Code-Only Update</span></span>](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
- [<span data-ttu-id="a2606-115">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="a2606-115">Visual Studio Web Deployment with SQL Server Compact - Deploying a Database Update</span></span>](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
- [<span data-ttu-id="a2606-116">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - SQL Server로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="a2606-116">Visual Studio Web Deployment with SQL Server Compact - Migrating to SQL Server</span></span>](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
- [<span data-ttu-id="a2606-117">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - SQL Server Database 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="a2606-117">Visual Studio Web Deployment with SQL Server Compact - Deploying a SQL Server Database Update</span></span>](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
- [<span data-ttu-id="a2606-118">SQL Server Compact를 사용하여 Visual Studio 웹 배포 - 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a2606-118">Visual Studio Web Deployment with SQL Server Compact - Troubleshooting</span></span>](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)
