---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server로 마이그레이션 (12/10) Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: c5281a42596d95e725b32e652c75785abe0fd64e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462839"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a><span data-ttu-id="18b5b-103">Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server로 마이그레이션 (12/10)</span><span class="sxs-lookup"><span data-stu-id="18b5b-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Migrating to SQL Server - 10 of 12</span></span>

<span data-ttu-id="18b5b-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="18b5b-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="18b5b-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="18b5b-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="18b5b-106">이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="18b5b-107">웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="18b5b-108">시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="18b5b-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="18b5b-109">Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="18b5b-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="18b5b-110">개요</span><span class="sxs-lookup"><span data-stu-id="18b5b-110">Overview</span></span>

<span data-ttu-id="18b5b-111">이 자습서에서는 SQL Server Compact에서 SQL Server로 마이그레이션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-111">This tutorial shows you how to migrate from SQL Server Compact to SQL Server.</span></span> <span data-ttu-id="18b5b-112">이 작업을 수행 하는 한 가지 이유는 저장 프로시저, 트리거, 뷰, 복제 등 SQL Server Compact 지원 하지 않는 SQL Server 기능을 활용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-112">One reason you might want to do that is to take advantage of SQL Server features that SQL Server Compact does not support, such as stored procedures, triggers, views, or replication.</span></span> <span data-ttu-id="18b5b-113">SQL Server Compact와 SQL Server 간의 차이점에 대 한 자세한 내용은 [SQL Server Compact 배포](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) 자습서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="18b5b-113">For more information about the differences between SQL Server Compact and SQL Server, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

### <a name="sql-server-express-versus-full-sql-server-for-development"></a><span data-ttu-id="18b5b-114">개발을 위한 전체 SQL Server SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="18b5b-114">SQL Server Express versus full SQL Server for Development</span></span>

<span data-ttu-id="18b5b-115">SQL Server로 업그레이드 하기로 결정 한 후에는 개발 및 테스트 환경에서 SQL Server 또는 SQL Server Express를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-115">Once you've decided to upgrade to SQL Server, you might want to use SQL Server or SQL Server Express in your development and test environments.</span></span> <span data-ttu-id="18b5b-116">도구 지원과 데이터베이스 엔진 기능의 차이점 외에도 공급자 구현에 SQL Server Compact와 다른 SQL Server 버전 간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-116">In addition to the differences in tool support and in database engine features, there are differences in provider implementations between SQL Server Compact and other versions of SQL Server.</span></span> <span data-ttu-id="18b5b-117">이러한 차이로 인해 동일한 코드가 다른 결과를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-117">These differences can cause the same code to generate different results.</span></span> <span data-ttu-id="18b5b-118">따라서 SQL Server Compact를 개발 데이터베이스로 유지 하기로 결정 한 경우 프로덕션에 배포 하기 전에 테스트 환경에서 SQL Server 또는 SQL Server Express에서 사이트를 철저히 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-118">Therefore, if you decide to keep SQL Server Compact as your development database, you should thoroughly test your site in SQL Server or SQL Server Express in a test environment before each deployment to production.</span></span>

<span data-ttu-id="18b5b-119">SQL Server Compact와 달리 SQL Server Express은 기본적으로 동일한 데이터베이스 엔진 이며 전체 SQL Server 동일한 .NET 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-119">Unlike SQL Server Compact, SQL Server Express is essentially the same database engine and uses the same .NET provider as full SQL Server.</span></span> <span data-ttu-id="18b5b-120">SQL Server Express를 사용 하 여 테스트 하는 경우 SQL Server와 동일한 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-120">When you test with SQL Server Express, you can be confident of getting the same results as you will with SQL Server.</span></span> <span data-ttu-id="18b5b-121">SQL Server Express와 함께 사용할 수 있는 대부분의 동일한 데이터베이스 도구를 사용 하 여 SQL Server ( [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)하는 주목할 만한 예외)를 사용할 수 있으며, 저장 프로시저, 뷰, 트리거 및 복제와 같은 SQL Server의 다른 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-121">You can use most of the same database tools with SQL Server Express that you can use with SQL Server (a notable exception being [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)), and it supports other features of SQL Server like stored procedures, views, triggers, and replication.</span></span> <span data-ttu-id="18b5b-122">그러나 일반적으로 프로덕션 웹 사이트에서는 전체 SQL Server를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-122">(You typically have to use full SQL Server in a production website, however.</span></span> <span data-ttu-id="18b5b-123">SQL Server Express은 공유 호스팅 환경에서 실행할 수 있지만이를 위해 설계 되지 않았으므로 많은 호스팅 공급자가이를 지원 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="18b5b-123">SQL Server Express can run in a shared hosting environment, but it was not designed for that, and many hosting providers do not support it.)</span></span>

<span data-ttu-id="18b5b-124">Visual Studio 2012을 사용 하는 경우 일반적으로 Visual Studio에서 기본적으로 설치 되는 것 이기 때문에 개발 환경에 대 한 SQL Server Express LocalDB를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-124">If you are using Visual Studio 2012, you typically choose SQL Server Express LocalDB for your development environment because that is what is installed by default with Visual Studio.</span></span> <span data-ttu-id="18b5b-125">그러나 LocalDB는 IIS에서 작동 하지 않으므로 테스트 환경에 SQL Server 또는 SQL Server Express를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-125">However, LocalDB does not work in IIS, so for your test environment you have to use either SQL Server or SQL Server Express.</span></span>

### <a name="combining-databases-versus-keeping-them-separate"></a><span data-ttu-id="18b5b-126">데이터베이스 조합 및 분리</span><span class="sxs-lookup"><span data-stu-id="18b5b-126">Combining Databases versus Keeping Them Separate</span></span>

<span data-ttu-id="18b5b-127">Contoso 대학 응용 프로그램에는 두 개의 SQL Server Compact 데이터베이스, 즉 멤버 자격 데이터베이스 (*aspnet .sdf*)와 응용 프로그램 데이터베이스 (*School*)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-127">The Contoso University application has two SQL Server Compact databases: the membership database (*aspnet.sdf*) and the application database (*School.sdf*).</span></span> <span data-ttu-id="18b5b-128">마이그레이션할 때 이러한 데이터베이스를 두 개의 개별 데이터베이스나 단일 데이터베이스로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-128">When you migrate, you can migrate these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="18b5b-129">응용 프로그램 데이터베이스와 멤버 자격 데이터베이스 간의 데이터베이스 조인을 용이 하 게 하기 위해 결합 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-129">You might want to combine them in order to facilitate database joins between your application database and your membership database.</span></span> <span data-ttu-id="18b5b-130">호스팅 계획을 결합 하는 이유가 제공 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-130">Your hosting plan might also provide a reason to combine them.</span></span> <span data-ttu-id="18b5b-131">예를 들어 호스팅 공급자는 여러 데이터베이스에 대해 더 많은 요금을 청구 하거나 둘 이상의 데이터베이스를 허용 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-131">For example, the hosting provider might charge more for multiple databases or might not even allow more than one database.</span></span> <span data-ttu-id="18b5b-132">단일 SQL Server 데이터베이스만 허용 하는이 자습서에 사용 되는 Cytanium Lite 호스팅 계정을 사용 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-132">That's the case with the Cytanium Lite hosting account that's used for this tutorial, which allows only a single SQL Server database.</span></span>

<span data-ttu-id="18b5b-133">이 자습서에서는 다음과 같은 방법으로 두 개의 데이터베이스를 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-133">In this tutorial, you'll migrate your two databases this way:</span></span>

- <span data-ttu-id="18b5b-134">개발 환경에서 두 개의 LocalDB 데이터베이스로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-134">Migrate to two LocalDB databases in the development environment.</span></span>
- <span data-ttu-id="18b5b-135">테스트 환경에서 두 개의 SQL Server Express 데이터베이스로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-135">Migrate to two SQL Server Express databases in the test environment.</span></span>
- <span data-ttu-id="18b5b-136">프로덕션 환경에서 결합 된 전체 SQL Server 데이터베이스 하나로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-136">Migrate to one combined full SQL Server database in the production environment.</span></span>

<span data-ttu-id="18b5b-137">미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-137">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="installing-sql-server-express"></a><span data-ttu-id="18b5b-138">SQL Server Express 설치</span><span class="sxs-lookup"><span data-stu-id="18b5b-138">Installing SQL Server Express</span></span>

<span data-ttu-id="18b5b-139">SQL Server Express는 기본적으로 Visual Studio 2010와 함께 자동으로 설치 되지만, 기본적으로 Visual Studio 2012과 함께 설치 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-139">SQL Server Express is automatically installed by default with Visual Studio 2010, but by default it is not installed with Visual Studio 2012.</span></span> <span data-ttu-id="18b5b-140">SQL Server 2012 Express를 설치 하려면 다음 링크를 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="18b5b-140">To install SQL Server 2012 Express, click the following link</span></span>

- [<span data-ttu-id="18b5b-141">SQL Server Express 2012</span><span class="sxs-lookup"><span data-stu-id="18b5b-141">SQL Server Express 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=29062)

<span data-ttu-id="18b5b-142">*한국어/x64/sqlexpr\_x64\_enu* 또는 *enu/X86/sqlexpr\_x86\_enu*를 선택 하 고 설치 마법사에서 기본 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-142">Choose *ENU/x64/SQLEXPR\_x64\_ENU.exe* or *ENU/x86/SQLEXPR\_x86\_ENU.exe*, and in the installation wizard accept the default settings.</span></span> <span data-ttu-id="18b5b-143">설치 옵션에 대 한 자세한 내용은 설치 [마법사에서 SQL Server 2012 설치 (설치 프로그램)](https://msdn.microsoft.com/library/ms143219.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="18b5b-143">For more information about installation options, see [Install SQL Server 2012 from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="18b5b-144">테스트 환경에 대 한 SQL Server Express 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="18b5b-144">Creating SQL Server Express Databases for the Test Environment</span></span>

<span data-ttu-id="18b5b-145">다음 단계는 ASP.NET 멤버 자격과 School 데이터베이스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-145">The next step is to create the ASP.NET membership and School databases.</span></span>

<span data-ttu-id="18b5b-146">**보기** 메뉴에서 **서버 탐색기** (Visual Web Developer에서**데이터베이스 탐색기** )를 선택 하 고 **데이터 연결** 을 마우스 오른쪽 단추로 클릭 한 다음 **새 SQL Server 데이터베이스 만들기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-146">From the **View** menu select **Server Explorer** (**Database Explorer** in Visual Web Developer), and then right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

<span data-ttu-id="18b5b-148">**새 SQL Server 데이터베이스 만들기** 대화 상자에서 **서버 이름** 상자에 ".\SQLExpress"를 입력 하 고 **새 데이터베이스 이름** 상자에 "aspnet-Test"를 입력 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-148">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-Test" in the **New database name** box, then click **OK**.</span></span>

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

<span data-ttu-id="18b5b-150">동일한 절차에 따라 "School-Test" 라는 새 SQL Server Express School 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-150">Follow the same procedure to create a new SQL Server Express School database named "School-Test".</span></span>

<span data-ttu-id="18b5b-151">나중에 개발 환경에 대 한 각 데이터베이스의 추가 인스턴스를 만들고 두 데이터베이스 집합을 구분할 수 있어야 하므로 이러한 데이터베이스 이름에 "Test"를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-151">(You're appending "Test" to these database names because later you'll create an additional instance of each database for the development environment, and you need to be able to differentiate the two sets of databases.)</span></span>

<span data-ttu-id="18b5b-152">이제 **서버 탐색기** 에 두 개의 새 데이터베이스가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-152">**Server Explorer** now shows the two new databases.</span></span>

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a><span data-ttu-id="18b5b-154">새 데이터베이스에 대 한 Grant 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="18b5b-154">Creating a Grant Script for the New Databases</span></span>

<span data-ttu-id="18b5b-155">응용 프로그램이 개발 컴퓨터의 IIS에서 실행 되는 경우 응용 프로그램은 기본 응용 프로그램 풀의 자격 증명을 사용 하 여 데이터베이스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-155">When the application runs in IIS on your development computer, the application accesses the database by using the default application pool's credentials.</span></span> <span data-ttu-id="18b5b-156">그러나 기본적으로 응용 프로그램 풀 id에는 데이터베이스를 열 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-156">However, by default, the application pool identity does not have permission to open the databases.</span></span> <span data-ttu-id="18b5b-157">따라서 해당 사용 권한을 부여 하는 스크립트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-157">So you have to run a script to grant that permission.</span></span> <span data-ttu-id="18b5b-158">이 섹션에서는 응용 프로그램이 IIS에서 실행 될 때 데이터베이스를 열 수 있도록 나중에 실행할 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-158">In this section you create the script that you'll run later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="18b5b-159">[프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에서 만든 솔루션의 *솔루션의 솔루션 폴더에서* *Grant .sql*이라는 새 SQL 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-159">In the solution's *SolutionFiles* folder that you created in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial, create a new SQL file named *Grant.sql*.</span></span> <span data-ttu-id="18b5b-160">다음 SQL 명령을 파일에 복사 하 고 파일을 저장 한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-160">Copy the following SQL commands into the file, and then save and close the file:</span></span>

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> <span data-ttu-id="18b5b-161">이 스크립트는이 자습서에 지정 된 대로 SQL Server 2008 및 Windows 7의 IIS 설정에서 작동 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-161">This script is designed to work with SQL Server 2008 and with the IIS settings in Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="18b5b-162">다른 버전의 SQL Server 또는 Windows를 사용 하는 경우 또는 컴퓨터에 IIS를 다르게 설정 하는 경우이 스크립트를 변경 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-162">If you're using a different version of SQL Server or of Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="18b5b-163">SQL Server 스크립트에 대 한 자세한 내용은 [SQL Server 온라인 설명서](https://go.microsoft.com/fwlink/?LinkId=132511)을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="18b5b-163">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="18b5b-164">**보안 정보** 이 스크립트는 런타임에 데이터베이스에 액세스 하는 사용자에 게 db\_소유자 권한을 제공 합니다 .이 권한은 프로덕션 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-164">**Security Note** This script gives db\_owner permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="18b5b-165">일부 시나리오에서는 배포에 대 한 전체 데이터베이스 스키마 업데이트 권한만 있는 사용자를 지정 하 고 데이터를 읽고 쓸 수 있는 권한만 있는 다른 사용자를 런타임에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-165">In some scenarios you might want to specify a user that has full database schema update permissions only for deployment, and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="18b5b-166">자세한 내용은 [IIS에 테스트 환경으로 배포 하](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) **는 Code First 마이그레이션에 대 한 자동 Web.config 변경 내용 검토** 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="18b5b-166">For more information, see **Reviewing the Automatic Web.config Changes for Code First Migrations** in [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md).</span></span>

## <a name="configuring-database-deployment-for-the-test-environment"></a><span data-ttu-id="18b5b-167">테스트 환경에 대 한 데이터베이스 배포 구성</span><span class="sxs-lookup"><span data-stu-id="18b5b-167">Configuring Database Deployment for the Test Environment</span></span>

<span data-ttu-id="18b5b-168">다음에는 각 데이터베이스에 대해 다음 작업을 수행할 수 있도록 Visual Studio를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-168">Next, you'll configure Visual Studio so that it will do the following tasks for each database:</span></span>

- <span data-ttu-id="18b5b-169">대상 데이터베이스의 원본 데이터베이스 구조 (테이블, 열, 제약 조건 등)를 만드는 SQL 스크립트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-169">Generate a SQL script that creates the source database's structure (tables, columns, constraints, etc.) in the destination database.</span></span>
- <span data-ttu-id="18b5b-170">원본 데이터베이스의 데이터를 대상 데이터베이스의 테이블에 삽입 하는 SQL 스크립트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-170">Generate a SQL script that inserts the source database's data into the tables in the destination database.</span></span>
- <span data-ttu-id="18b5b-171">생성 된 스크립트와 사용자가 만든 Grant 스크립트를 대상 데이터베이스에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-171">Run the generated scripts, and the Grant script that you created, in the destination database.</span></span>

<span data-ttu-id="18b5b-172">**프로젝트 속성** 창을 열고 **SQL 패키지 및 게시** 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-172">Open the **Project Properties** window and select the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="18b5b-173">**구성** 드롭다운 목록에서 **활성 (릴리스)** 또는 **릴리스** 가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-173">Make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="18b5b-174">**이 페이지 사용**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-174">Click **Enable this Page**.</span></span>

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

<span data-ttu-id="18b5b-176">**SQL 패키지 및 게시** 탭은 레거시 배포 방법을 지정 하므로 일반적으로 비활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-176">The **Package/Publish SQL** tab is normally disabled because it specifies a legacy deployment method.</span></span> <span data-ttu-id="18b5b-177">대부분의 시나리오의 경우 **웹 게시** 마법사에서 데이터베이스 배포를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-177">For most scenarios, you should configure database deployment in the **Publish Web** wizard.</span></span> <span data-ttu-id="18b5b-178">SQL Server Compact에서 SQL Server 또는 SQL Server Express으로 마이그레이션하는 것은이 방법을 선택 하는 것이 좋은 특수 한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-178">Migrating from SQL Server Compact to SQL Server or SQL Server Express is a special case for which this method is a good choice.</span></span>

<span data-ttu-id="18b5b-179">**Web.config에서 가져오기를**클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-179">Click **Import from Web.config**.</span></span>

![Selecting_Import_from_Web.config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

<span data-ttu-id="18b5b-181">Visual Studio는 web.config 파일에서 연결 문자열을 찾고, 멤버 자격 데이터베이스와 School 데이터베이스에 대해 하나를 찾고, **데이터베이스 항목** 테이블의 각 연결 문자열에 해당 하는 행을 *추가 합니다.*</span><span class="sxs-lookup"><span data-stu-id="18b5b-181">Visual Studio looks for connection strings in the *Web.config* file, finds one for the membership database and one for the School database, and adds a row corresponding to each connection string in the **Database Entries** table.</span></span> <span data-ttu-id="18b5b-182">기존 SQL Server Compact 데이터베이스에 대 한 연결 문자열을 찾은 후 다음 단계는 이러한 데이터베이스를 배포할 방법 및 위치를 구성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-182">The connection strings it finds are for the existing SQL Server Compact databases, and your next step will be to configure how and where to deploy these databases.</span></span>

<span data-ttu-id="18b5b-183">데이터베이스 항목 **세부 정보** 섹션 **의 데이터베이스 항목 테이블 아래** 에 데이터베이스 배포 설정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-183">You enter database deployment settings in the **Database Entry Details** section below the **Database Entries** table.</span></span> <span data-ttu-id="18b5b-184">**데이터베이스 항목 세부 정보** 섹션에 표시 된 설정은 다음 그림에 표시 된 것 처럼 **데이터베이스 항목** 테이블의 어떤 행이 선택 되었는지와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-184">The settings shown in the **Database Entry Details** section pertain to whichever row in the **Database Entries** table is selected, as shown in the following illustration.</span></span>

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="18b5b-186">멤버 자격 데이터베이스에 대 한 배포 설정 구성</span><span class="sxs-lookup"><span data-stu-id="18b5b-186">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="18b5b-187">멤버 자격 데이터베이스에 적용 되는 설정을 구성 하기 위해 **데이터베이스 항목** 테이블에서 **Defaultconnection-Deployment** 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-187">Select the **DefaultConnection-Deployment** row in the **Database Entries** table in order to configure settings that apply to the membership database.</span></span>

<span data-ttu-id="18b5b-188">**대상 데이터베이스에 대 한 연결 문자열**에 새 SQL Server Express 멤버 자격 데이터베이스를 가리키는 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-188">In **Connection string for destination database**, enter a connection string that points to the new SQL Server Express membership database.</span></span> <span data-ttu-id="18b5b-189">**서버 탐색기**에서 필요한 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-189">You can get the connection string you need from **Server Explorer**.</span></span> <span data-ttu-id="18b5b-190">**서버 탐색기**에서 **데이터 연결** 을 확장 하 고 **AspnetTest** 데이터베이스를 선택한 다음 **속성** 창에서 **연결 문자열** 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-190">In **Server Explorer**, expand **Data Connections** and select the **aspnetTest** database, then from the **Properties** window copy the **Connection String** value.</span></span>

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

<span data-ttu-id="18b5b-192">동일한 연결 문자열이 다음과 같이 재현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-192">The same connection string is reproduced here:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

<span data-ttu-id="18b5b-193">**SQL 패키지 및 게시** 탭에서 **대상 데이터베이스에 대 한 연결 문자열** 에이 연결 문자열을 복사 하 여 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-193">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="18b5b-194">**기존 데이터베이스에서 데이터 및/또는 스키마 끌어오기** 가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-194">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span> <span data-ttu-id="18b5b-195">이로 인해 SQL 스크립트가 자동으로 생성 되 고 대상 데이터베이스에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-195">This is what causes SQL scripts to be automatically generated and run in the destination database.</span></span>

<span data-ttu-id="18b5b-196">**원본 데이터베이스 값에 대 한 연결 문자열** 을 *web.config 파일에서* 추출 하 고 개발 SQL Server Compact 데이터베이스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-196">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="18b5b-197">이는 대상 데이터베이스에서 나중에 실행 될 스크립트를 생성 하는 데 사용 되는 원본 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-197">This is the source database that will be used to generate the scripts that will run later in the destination database.</span></span> <span data-ttu-id="18b5b-198">프로덕션 버전의 데이터베이스를 배포 하려는 경우 "aspnet-Dev"을 "aspnet-Prod"로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-198">Since you want to deploy the production version of the database, change "aspnet-Dev.sdf" to "aspnet-Prod.sdf".</span></span>

<span data-ttu-id="18b5b-199">데이터베이스 구조 뿐만 아니라 데이터 (사용자 계정 및 역할)를 복사 하려는 경우에 **만 스키마** 에서 스키마 **및 데이터로** **데이터베이스 스크립팅 옵션** 을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-199">Change **Database scripting options** from **Schema Only** to **Schema and data**, since you want to copy your data (user accounts and roles) as well as the database structure.</span></span>

<span data-ttu-id="18b5b-200">이전에 만든 grant 스크립트를 실행 하도록 배포를 구성 하려면 **데이터베이스 스크립트** 섹션에 해당 스크립트를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-200">To configure deployment to run the grant scripts that you created earlier, you have to add them to the **Database Scripts** section.</span></span> <span data-ttu-id="18b5b-201">**스크립트 추가**를 클릭 하 고 **SQL 스크립트 추가** 대화 상자에서 grant 스크립트를 저장 한 폴더로 이동 합니다 .이 폴더는 솔루션 파일이 들어 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-201">Click **Add Script**, and in the **Add SQL Scripts** dialog box, navigate to the folder where you stored the grant script (this is the folder that contains your solution file).</span></span> <span data-ttu-id="18b5b-202">*Grant .sql*이라는 파일을 선택 하 고 **열기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-202">Select the file named *Grant.sql*, and click **Open**.</span></span>

<span data-ttu-id="18b5b-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="18b5b-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span></span>

<span data-ttu-id="18b5b-204">**데이터베이스 항목** 에서 **defaultconnection 배포** 행의 설정은 이제 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-204">The settings for the **DefaultConnection-Deployment** row in **Database Entries** now look like the following illustration:</span></span>

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="18b5b-206">School 데이터베이스에 대 한 배포 설정 구성</span><span class="sxs-lookup"><span data-stu-id="18b5b-206">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="18b5b-207">그런 다음 School 데이터베이스에 대 한 배포 설정을 구성 하기 위해 **데이터베이스 항목** 테이블에서 **schoolcontext.cs** 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-207">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure deployment settings for the School database.</span></span>

<span data-ttu-id="18b5b-208">이전에 사용한 것과 동일한 방법을 사용 하 여 새 SQL Server Express 데이터베이스에 대 한 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-208">You can use the same method you used earlier to get the connection string for the new SQL Server Express database.</span></span> <span data-ttu-id="18b5b-209">**SQL 패키지 및 게시** 탭에서 **대상 데이터베이스에 대 한 연결 문자열** 에이 연결 문자열을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-209">Copy this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

<span data-ttu-id="18b5b-210">**기존 데이터베이스에서 데이터 및/또는 스키마 끌어오기** 가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-210">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span>

<span data-ttu-id="18b5b-211">**원본 데이터베이스 값에 대 한 연결 문자열** 을 *web.config 파일에서* 추출 하 고 개발 SQL Server Compact 데이터베이스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-211">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="18b5b-212">"School-Dev"을 "School-Prod"로 변경 하 여 데이터베이스의 프로덕션 버전을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-212">Change "School-Dev.sdf" to "School-Prod.sdf" to deploy the production version of the database.</span></span> <span data-ttu-id="18b5b-213">응용 프로그램\_Data 폴더에 School-Prod 파일을 만들지 않았기 때문에이 파일을 테스트 환경에서 나중에 ContosoUniversity 프로젝트 폴더의 App\_Data 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-213">(You never created a School-Prod.sdf file in the App\_Data folder, so you'll copy that file from the test environment to the App\_Data folder in the ContosoUniversity project folder later.)</span></span>

<span data-ttu-id="18b5b-214">**스키마 및 데이터**에 대 한 **데이터베이스 스크립팅 옵션** 을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-214">Change **Database scripting options** to **Schema and data**.</span></span>

<span data-ttu-id="18b5b-215">또한 스크립트를 실행 하 여이 데이터베이스에 대 한 읽기 및 쓰기 권한을 응용 프로그램 풀 id에 부여 하는 것 이므로 *grant .sql* 스크립트 파일을 멤버 자격 데이터베이스에 대해 수행한 그대로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-215">You also want to run the script to grant read and write permission for this database to the application pool identity, so add the *Grant.sql* script file as you did for the membership database.</span></span>

<span data-ttu-id="18b5b-216">완료 되 면 **데이터베이스 항목** 에서 **schoolcontext.cs-Deployment** 행의 설정은 다음 그림과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-216">When you're done, the settings for the **SchoolContext-Deployment** row in **Database Entries** look like the following illustration:</span></span>

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

<span data-ttu-id="18b5b-218">**SQL 패키지 및 게시** 탭에 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-218">Save the changes to the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="18b5b-219">*C:\inetpub\wwwroot\ContosoUniversity\App\_Data* 폴더에서 ContosoUniversity 프로젝트의 *App\_data* 폴더로 *School-Prod* 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-219">Copy the *School-Prod.sdf* file from the *c:\inetpub\wwwroot\ContosoUniversity\App\_Data* folder to the *App\_Data* folder in the ContosoUniversity project.</span></span>

### <a name="specifying-transacted-mode-for-the-grant-script"></a><span data-ttu-id="18b5b-220">Grant 스크립트의 트랜잭션 모드 지정</span><span class="sxs-lookup"><span data-stu-id="18b5b-220">Specifying Transacted Mode for the Grant Script</span></span>

<span data-ttu-id="18b5b-221">배포 프로세스에서는 데이터베이스 스키마 및 데이터를 배포 하는 스크립트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-221">The deployment process generates scripts that deploy the database schema and data.</span></span> <span data-ttu-id="18b5b-222">기본적으로 이러한 스크립트는 트랜잭션에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-222">By default, these scripts run in a transaction.</span></span> <span data-ttu-id="18b5b-223">그러나 기본적으로 사용자 지정 스크립트 (예: grant 스크립트)는 트랜잭션에서 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-223">However, custom scripts (like the grant scripts) by default do not run in a transaction.</span></span> <span data-ttu-id="18b5b-224">배포 프로세스에서 트랜잭션 모드를 혼합 하는 경우 배포 중에 스크립트를 실행할 때 시간 초과 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-224">If the deployment process mixes transaction modes, you might get a timeout error when the scripts run during deployment.</span></span> <span data-ttu-id="18b5b-225">이 섹션에서는 트랜잭션에서 실행 되도록 사용자 지정 스크립트를 구성 하기 위해 프로젝트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-225">In this section, you edit the project file in order to configure the custom scripts to run in a transaction.</span></span>

<span data-ttu-id="18b5b-226">**솔루션 탐색기**에서 **ContosoUniversity** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **프로젝트 언로드**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-226">In **Solution Explorer**, right-click the **ContosoUniversity** project and select **Unload Project**.</span></span>

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

<span data-ttu-id="18b5b-228">그런 다음 프로젝트를 다시 마우스 오른쪽 단추로 클릭 하 고 **ContosoUniversity 편집**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-228">Then right-click the project again and select **Edit ContosoUniversity.csproj**.</span></span>

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

<span data-ttu-id="18b5b-230">Visual Studio 편집기에는 프로젝트 파일의 XML 콘텐츠가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-230">The Visual Studio editor shows you the XML content of the project file.</span></span> <span data-ttu-id="18b5b-231">몇 가지 `PropertyGroup` 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-231">Notice that there are several `PropertyGroup` elements.</span></span> <span data-ttu-id="18b5b-232">이미지에서 `PropertyGroup` 요소의 콘텐츠가 생략 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-232">(In the image, the contents of the `PropertyGroup` elements have been omitted.)</span></span>

![프로젝트 파일 편집기 창](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

<span data-ttu-id="18b5b-234">`Condition` 특성이 없는 첫 번째 항목은 빌드 구성과 상관 없이 적용 되는 설정에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-234">The first one, which has no `Condition` attribute, is for settings that apply regardless of build configuration.</span></span> <span data-ttu-id="18b5b-235">하나의 `PropertyGroup` 요소는 디버그 빌드 `Condition` 구성에만 적용 되 고, 하나는 릴리스 빌드 구성에만 적용 되며, 하나는 테스트 빌드 구성에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-235">One `PropertyGroup` element applies only to the Debug build configuration (note the `Condition` attribute), one applies only to the Release build configuration, and one applies only to the Test build configuration.</span></span> <span data-ttu-id="18b5b-236">릴리스 빌드 구성에 대 한 `PropertyGroup` 요소 내에서 **SQL 패키지 및 게시** 탭에서 입력 한 설정이 포함 된 `PublishDatabaseSettings` 요소가 표시 됩니다. 지정한 각 grant 스크립트에 해당 하는 `Object` 요소가 있습니다. "Grant .sql"의 두 인스턴스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-236">Within the `PropertyGroup` element for the Release build configuration, you'll see a `PublishDatabaseSettings` element that contains the settings you entered on the **Package/Publish SQL** tab. There is an `Object` element that corresponds to each of the grant scripts you specified (notice the two instances of "Grant.sql").</span></span> <span data-ttu-id="18b5b-237">기본적으로 각 grant 스크립트에 대 한 `Source` 요소의 `Transacted` 특성은 `False`됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-237">By default, the `Transacted` attribute of the `Source` element for each grant script is `False`.</span></span>

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

<span data-ttu-id="18b5b-239">`Source` 요소의 `Transacted` 특성 값을 `True`로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-239">Change the value of the `Transacted` attribute of the `Source` element to `True`.</span></span>

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

<span data-ttu-id="18b5b-241">프로젝트 파일을 저장 하 고 닫은 다음 **솔루션 탐색기** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **프로젝트 다시 로드**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-241">Save and close the project file, and then right-click the project in **Solution Explorer** and select **Reload Project**.</span></span>

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a><span data-ttu-id="18b5b-243">연결 문자열에 대 한 Web.config 변환 설정</span><span class="sxs-lookup"><span data-stu-id="18b5b-243">Setting up Web.Config Transformations for the Connection Strings</span></span>

<span data-ttu-id="18b5b-244">**Sql 패키지 및 게시** 탭에 입력 한 새 SQL Express 데이터베이스의 연결 문자열은 배포 중에 대상 데이터베이스를 업데이트 하는 경우에만 웹 배포에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-244">The connection strings for the new SQL Express databases that you entered on the **Package/Publish SQL** tab are used by Web Deploy only for updating the destination database during deployment.</span></span> <span data-ttu-id="18b5b-245">*배포 된 web.config 파일* 의 연결 문자열이 새 SQL Server Express 데이터베이스를 가리키도록 *web.config* 변환을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-245">You still have to set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file point to the new SQL Server Express databases.</span></span> <span data-ttu-id="18b5b-246">**SQL 패키지 및 게시** 탭을 사용 하는 경우 게시 프로필에서 연결 문자열을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-246">(When you use the **Package/Publish SQL** tab, you can't configure connection strings in the publish profile.)</span></span>

<span data-ttu-id="18b5b-247">*Web.config* 를 열고 다음 예제에서 `connectionStrings` 요소를 `connectionStrings` 요소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-247">Open *Web.Test.config* and replace the `connectionStrings` element with the `connectionStrings` element in the following example.</span></span> <span data-ttu-id="18b5b-248">(컨텍스트를 제공 하기 위해 여기에 표시 된 주변 코드가 아닌 connectionStrings 요소만 복사 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="18b5b-248">(Make sure you only copy the connectionStrings element, not the surrounding code that is shown here to provide context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

<span data-ttu-id="18b5b-249">이 코드는 배포 된 *web.config* 파일에서 각 `add` 요소의 `connectionString` 및 `providerName` 특성을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-249">This code causes the `connectionString` and `providerName` attributes of each `add` element to be replaced in the deployed *Web.config* file.</span></span> <span data-ttu-id="18b5b-250">이러한 연결 문자열은 **SQL 패키지 및 게시** 탭에 입력 한 문자열과 동일 하지 않습니다. Entity Framework 및 Universal Providers에 필요 하기 때문에 "MultipleActiveResultSets = True" 설정이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-250">These connection strings are not identical to the ones you entered in the **Package/Publish SQL** tab. The setting "MultipleActiveResultSets=True" has been added to them because it's required for the Entity Framework and the Universal Providers.</span></span>

## <a name="installing-sql-server-compact"></a><span data-ttu-id="18b5b-251">SQL Server Compact 설치</span><span class="sxs-lookup"><span data-stu-id="18b5b-251">Installing SQL Server Compact</span></span>

<span data-ttu-id="18b5b-252">SqlServerCompact NuGet 패키지는 Contoso 대학 응용 프로그램에 대 한 SQL Server Compact 데이터베이스 엔진 어셈블리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-252">The SqlServerCompact NuGet package provides the SQL Server Compact database engine assemblies for the Contoso University application.</span></span> <span data-ttu-id="18b5b-253">그러나 이제는 응용 프로그램이 아니지만 SQL Server 데이터베이스에서 실행할 스크립트를 만들기 위해 SQL Server Compact 데이터베이스를 읽을 수 있어야 하는 웹 배포.</span><span class="sxs-lookup"><span data-stu-id="18b5b-253">But now it is not the application but Web Deploy that must be able to read the SQL Server Compact databases, in order to create scripts to run in the SQL Server databases.</span></span> <span data-ttu-id="18b5b-254">웹 배포 SQL Server Compact 데이터베이스를 읽도록 설정 하려면 [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)링크를 사용 하 여 개발 컴퓨터에 SQL Server Compact을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-254">To enable Web Deploy to read SQL Server Compact databases, install SQL Server Compact on the development computer by using the following link: [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6).</span></span>

## <a name="deploying-to-the-test-environment"></a><span data-ttu-id="18b5b-255">테스트 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="18b5b-255">Deploying to the Test Environment</span></span>

<span data-ttu-id="18b5b-256">테스트 환경에 게시 하려면 게시 프로필 데이터베이스 설정 대신 데이터베이스 게시에 대 한 **SQL 패키지 및 게시** 탭을 사용 하도록 구성 된 게시 프로필을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-256">In order to publish to the Test environment, you have to create a publish profile that is configured to use the **Package/Publish SQL** tab for database publishing instead of the publish profile database settings.</span></span>

<span data-ttu-id="18b5b-257">먼저 기존 테스트 프로필을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-257">First, delete the existing Test profile.</span></span>

<span data-ttu-id="18b5b-258">**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-258">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="18b5b-259">**프로필** 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-259">Select the **Profile** tab.</span></span>

<span data-ttu-id="18b5b-260">**프로필 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-260">Click **Manage Profiles**.</span></span>

<span data-ttu-id="18b5b-261">**테스트**를 선택 하 고 **제거**를 클릭 한 다음 **닫기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-261">Select **Test**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="18b5b-262">이 변경 내용을 저장 하려면 **웹 게시** 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-262">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="18b5b-263">그런 다음 새 테스트 프로필을 만들어 프로젝트를 게시 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-263">Next, create a new Test profile and use it to publish the project.</span></span>

<span data-ttu-id="18b5b-264">**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-264">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="18b5b-265">**프로필** 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-265">Select the **Profile** tab.</span></span>

<span data-ttu-id="18b5b-266">드롭다운 목록에서 **&lt;새로 만들기 ...&gt;** 를 선택 하 고 프로필 이름으로 "Test"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-266">Select **&lt;New...&gt;** from the drop-down list, and enter "Test" as the profile name.</span></span>

<span data-ttu-id="18b5b-267">**서비스 URL** 상자에 *localhost*를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-267">In the **Service URL** box, enter *localhost*.</span></span>

<span data-ttu-id="18b5b-268">**사이트/응용 프로그램** 상자에서 *기본 웹 사이트/ContosoUniversity*를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-268">In the **Site/application** box, enter *Default Web Site/ContosoUniversity*.</span></span>

<span data-ttu-id="18b5b-269">**대상 URL** 상자에 `http://localhost/ContosoUniversity/`을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-269">In the **Destination URL** box, enter `http://localhost/ContosoUniversity/`.</span></span>

<span data-ttu-id="18b5b-270">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-270">Click **Next**.</span></span>

<span data-ttu-id="18b5b-271">**설정** 탭에서는 **SQL 패키지 및 게시** 탭이 구성 되었다는 경고를 표시 하 고 새 데이터베이스 게시 기능 사용을 클릭 하 여 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-271">The **Settings** tab warns you that the **Package/Publish SQL** tab has been configured, and it gives you an opportunity to override them by clicking enable the new database publishing improvements.</span></span> <span data-ttu-id="18b5b-272">이 배포의 경우 **SQL 패키지 및 게시** 탭 설정을 재정의 하지 말고 **다음**을 클릭 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-272">For this deployment you don't want to override the **Package/Publish SQL** tab settings, so just click **Next**.</span></span>

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

<span data-ttu-id="18b5b-274">**미리 보기** 탭의 메시지는 **게시할 데이터베이스가 선택**되지 않았음을 나타냅니다. 하지만이는 게시 프로필에서 데이터베이스 게시가 구성 되지 않았음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-274">A message on the **Preview** tab indicates that **No databases are selected to publish**, but this only means that database publishing is not configured in the publish profile.</span></span>

<span data-ttu-id="18b5b-275">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-275">Click **Publish**.</span></span>

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

<span data-ttu-id="18b5b-277">Visual Studio에서 응용 프로그램을 배포 하 고 테스트 환경에서 사이트의 홈 페이지로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-277">Visual Studio deploys the application and opens the browser to the home page of the site in the test environment.</span></span> <span data-ttu-id="18b5b-278">강사 페이지를 실행 하 여 앞에서 살펴본 것과 동일한 데이터가 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-278">Run the Instructors page to see that it displays the same data that you saw earlier.</span></span> <span data-ttu-id="18b5b-279">**학생 추가** 페이지를 실행 하 고, 새 학생을 추가한 다음, **학생** 페이지에서 새 학생을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-279">Run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="18b5b-280">이렇게 하면 데이터베이스를 업데이트할 수 있는지 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-280">This verifies that the you can update the database.</span></span> <span data-ttu-id="18b5b-281">멤버 자격 데이터베이스를 배포 하 고 해당 데이터베이스에 액세스할 수 있는지 확인 하려면 **크레딧 업데이트** 페이지를 선택 합니다 (로그인 해야 함).</span><span class="sxs-lookup"><span data-stu-id="18b5b-281">Select the **Update Credits** page (you'll need to log in) to verify that the membership database was deployed and you have access to it.</span></span>

## <a name="creating-a-sql-server-database-for-the-production-environment"></a><span data-ttu-id="18b5b-282">프로덕션 환경에 대 한 SQL Server 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="18b5b-282">Creating a SQL Server Database for the Production Environment</span></span>

<span data-ttu-id="18b5b-283">이제 테스트 환경에 배포 했으므로 프로덕션에 배포를 설정할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-283">Now that you've deployed to the test environment, you're ready to set up deployment to production.</span></span> <span data-ttu-id="18b5b-284">배포할 데이터베이스를 만들어 테스트 환경에서 수행한 것 처럼 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-284">You begin as you did for the test environment, by creating a database to deploy to.</span></span> <span data-ttu-id="18b5b-285">개요에서 Cytanium Lite 호스팅 요금제는 단일 SQL Server 데이터베이스만 허용 하므로 두 개의 데이터베이스를 하나만 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-285">As you recall from the Overview, the Cytanium Lite hosting plan only allows a single SQL Server database, so you will set up only one database, not two.</span></span> <span data-ttu-id="18b5b-286">멤버 자격과 School SQL Server Compact 데이터베이스의 모든 테이블 및 데이터는 프로덕션 환경에서 하나의 SQL Server 데이터베이스에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-286">All of the tables and data from the membership and School SQL Server Compact databases will be deployed into one SQL Server database in production.</span></span>

<span data-ttu-id="18b5b-287">[http://panel.cytanium.com](http://panel.cytanium.com)에서 Cytanium 컨트롤 패널로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-287">Go to the Cytanium control panel at [http://panel.cytanium.com](http://panel.cytanium.com).</span></span> <span data-ttu-id="18b5b-288">**데이터베이스** 위에 마우스를 놓고 **SQL Server 2008**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-288">Hold the mouse over **Databases** and then click **SQL Server 2008**.</span></span>

<span data-ttu-id="18b5b-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="18b5b-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span></span>

<span data-ttu-id="18b5b-290">**SQL Server 2008** 페이지에서 **데이터베이스 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-290">In the **SQL Server 2008** page, click **Create Database**.</span></span>

<span data-ttu-id="18b5b-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="18b5b-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span></span>

<span data-ttu-id="18b5b-292">데이터베이스 이름을 "School"으로 선택 하 고 **저장**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-292">Name the database "School" and click **Save**.</span></span> <span data-ttu-id="18b5b-293">페이지에 "contosouSchool" 접두사가 자동으로 추가 되므로 유효 이름이 ""이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-293">(The page automatically adds the prefix "contosou", so the effective name will be "contosouSchool".)</span></span>

<span data-ttu-id="18b5b-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="18b5b-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span></span>

<span data-ttu-id="18b5b-295">동일한 페이지에서 **사용자 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-295">On the same page, click **Create User**.</span></span> <span data-ttu-id="18b5b-296">Cytanium 서버에서 Windows 통합 보안을 사용 하 고 응용 프로그램 풀 id를 사용 하 여 데이터베이스를 열도록 허용 하는 대신 데이터베이스를 열 수 있는 권한이 있는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-296">On Cytanium's servers, rather than using integrated Windows security and letting the application pool identity open your database, you'll create a user that has authority to open your database.</span></span> <span data-ttu-id="18b5b-297">프로덕션 *web.config* 파일에 있는 연결 문자열에 사용자의 자격 증명을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-297">You'll add the user's credentials to the connection strings that go in the production *Web.config* file.</span></span> <span data-ttu-id="18b5b-298">이 단계에서는 이러한 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-298">In this step you create those credentials.</span></span>

<span data-ttu-id="18b5b-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="18b5b-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span></span>

<span data-ttu-id="18b5b-300">**SQL 사용자 속성** 페이지에서 필수 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-300">Fill in the required fields in the **SQL User Properties** page:</span></span>

- <span data-ttu-id="18b5b-301">이름으로 "다음으로"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-301">Enter "ContosoUniversityUser" as the name.</span></span>
- <span data-ttu-id="18b5b-302">암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-302">Enter a password.</span></span>
- <span data-ttu-id="18b5b-303">기본 데이터베이스로 **contosouSchool** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-303">Select **contosouSchool** as the default database.</span></span>
- <span data-ttu-id="18b5b-304">**ContosouSchool** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-304">Select the **contosouSchool** check box.</span></span>

<span data-ttu-id="18b5b-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="18b5b-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span></span>

## <a name="configuring-database-deployment-for-the-production-environment"></a><span data-ttu-id="18b5b-306">프로덕션 환경에 대 한 데이터베이스 배포 구성</span><span class="sxs-lookup"><span data-stu-id="18b5b-306">Configuring Database Deployment for the Production Environment</span></span>

<span data-ttu-id="18b5b-307">이제 테스트 환경에 대해 이전에 수행한 것 처럼 **SQL 패키지 및 게시** 탭에서 데이터베이스 배포 설정을 설정할 준비가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-307">Now you're ready to set up database deployment settings in the **Package/Publish SQL** tab, as you did earlier for the test environment.</span></span>

<span data-ttu-id="18b5b-308">**프로젝트 속성** 창을 열고 **SQL 패키지 및 게시** 탭을 선택한 후 **구성** 드롭다운 목록에서 **활성 (릴리스)** 또는 **릴리스** 가 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-308">Open the **Project Properties** window, select the **Package/Publish SQL** tab, and make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="18b5b-309">각 데이터베이스에 대 한 배포 설정을 구성 하는 경우, 프로덕션 및 테스트 환경에서 수행 하는 작업 간의 주요 차이점은 연결 문자열을 구성 하는 방법에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-309">When you configure deployment settings for each database, the key difference between what you do for production and test environments is in how you configure connection strings.</span></span> <span data-ttu-id="18b5b-310">테스트 환경에서 다른 대상 데이터베이스 연결 문자열을 입력 했지만 프로덕션 환경의 경우 대상 연결 문자열은 두 데이터베이스에 대해 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-310">For the test environment you entered different destination database connection strings, but for the production environment the destination connection string will be the same for both databases.</span></span> <span data-ttu-id="18b5b-311">이는 프로덕션 환경의 한 데이터베이스에 두 데이터베이스를 배포 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-311">This is because you are deploying both databases to one database in production.</span></span>

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="18b5b-312">멤버 자격 데이터베이스에 대 한 배포 설정 구성</span><span class="sxs-lookup"><span data-stu-id="18b5b-312">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="18b5b-313">멤버 자격 데이터베이스에 적용 되는 설정을 구성 하려면 **데이터베이스 항목** 테이블에서 **Defaultconnection-Deployment** 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-313">To configure settings that apply to the membership database, select the **DefaultConnection-Deployment** row in the **Database Entries** table.</span></span>

<span data-ttu-id="18b5b-314">**대상 데이터베이스에 대 한 연결 문자열**에서 방금 만든 새 프로덕션 SQL Server 데이터베이스를 가리키는 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-314">In **Connection string for destination database**, enter a connection string that points to the new production SQL Server database that you just created.</span></span> <span data-ttu-id="18b5b-315">환영 전자 메일에서 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-315">You can get the connection string from your welcome email.</span></span> <span data-ttu-id="18b5b-316">전자 메일의 관련 부분에는 다음과 같은 샘플 연결 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-316">The relevant part of the email contains the following sample connection string:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

<span data-ttu-id="18b5b-317">세 개의 변수를 바꾼 후 필요한 연결 문자열은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-317">After you replace the three variables, the connection string you need looks like this example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

<span data-ttu-id="18b5b-318">**SQL 패키지 및 게시** 탭에서 **대상 데이터베이스에 대 한 연결 문자열** 에이 연결 문자열을 복사 하 여 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-318">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="18b5b-319">**기존 데이터베이스에서 데이터 및/또는 스키마 끌어오기** 를 선택 하 고 **데이터베이스 스크립팅 옵션** 은 여전히 **스키마와 데이터**인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-319">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="18b5b-320">**데이터베이스 스크립트** 상자에서 Grant. sql 스크립트 옆에 있는 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-320">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="18b5b-322">School 데이터베이스에 대 한 배포 설정 구성</span><span class="sxs-lookup"><span data-stu-id="18b5b-322">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="18b5b-323">그런 다음, School 데이터베이스 설정을 구성 하기 위해 **데이터베이스 항목** 테이블에서 **schoolcontext.cs** 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-323">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure the School database settings.</span></span>

<span data-ttu-id="18b5b-324">멤버 자격 데이터베이스의 해당 필드에 복사한 **대상 데이터베이스의 연결 문자열** 에 동일한 연결 문자열을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-324">Copy the same connection string into **Connection string for destination database** that you copied into that field for the membership database.</span></span>

<span data-ttu-id="18b5b-325">**기존 데이터베이스에서 데이터 및/또는 스키마 끌어오기** 를 선택 하 고 **데이터베이스 스크립팅 옵션** 은 여전히 **스키마와 데이터**인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-325">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="18b5b-326">**데이터베이스 스크립트** 상자에서 Grant. sql 스크립트 옆에 있는 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-326">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

<span data-ttu-id="18b5b-327">**SQL 패키지 및 게시** 탭에 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-327">Save the changes to the **Package/Publish SQL** tab.</span></span>

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a><span data-ttu-id="18b5b-328">프로덕션 데이터베이스에 대 한 연결 문자열에 대 한 Web.config 변환 설정</span><span class="sxs-lookup"><span data-stu-id="18b5b-328">Setting Up Web.Config Transforms for the Connection Strings to Production Databases</span></span>

<span data-ttu-id="18b5b-329">다음으로 *, 배포 된 web.config 파일* 의 연결 문자열이 새 프로덕션 데이터베이스를 가리키도록 *web.config* 변환을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-329">Next, you'll set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file to point to the new production database.</span></span> <span data-ttu-id="18b5b-330">`MultipleResultSets` 옵션을 추가 하는 경우를 제외 하 고는 **SQL 패키지 및 게시** 탭에 입력 한 연결 문자열이 응용 프로그램에서 사용 해야 하는 것과 웹 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-330">The connection string that you entered on the **Package/Publish SQL** tab for Web Deploy to use is the same as the one the application needs to use, except for the addition of the `MultipleResultSets` option.</span></span>

<span data-ttu-id="18b5b-331">*Web.config* 를 열고 `connectionStrings` 요소를 다음 예제와 같은 `connectionStrings` 요소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-331">Open *Web.Production.config* and replace the `connectionStrings` element with a `connectionStrings` element that looks like the following example.</span></span> <span data-ttu-id="18b5b-332">컨텍스트를 표시 하기 위해 제공 된 주변 태그가 아닌 `connectionStrings` 요소만 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-332">(Only copy the `connectionStrings` element, not the surrounding tags that are provided to show the context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

<span data-ttu-id="18b5b-333">경우에 따라 *web.config 파일에서* 연결 문자열을 항상 암호화 하도록 알려 주는 조언이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-333">You sometimes see advice that tells you to always encrypt connection strings in the *Web.config* file.</span></span> <span data-ttu-id="18b5b-334">이는 회사의 네트워크에 있는 서버에 배포 하는 경우에 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-334">This might be appropriate if you were deploying to servers on your own company's network.</span></span> <span data-ttu-id="18b5b-335">그러나 공유 호스팅 환경에 배포 하는 경우 호스팅 공급자의 보안 사례를 신뢰 하 고, 연결 문자열을 암호화 하는 것은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-335">When you are deploying to a shared hosting environment, though, you're trusting the security practices of the hosting provider, and it's not necessary or practical to encrypt the connection strings.</span></span>

## <a name="deploying-to-the-production-environment"></a><span data-ttu-id="18b5b-336">프로덕션 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="18b5b-336">Deploying to the Production Environment</span></span>

<span data-ttu-id="18b5b-337">이제 프로덕션 환경에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-337">Now you're ready to deploy to production.</span></span> <span data-ttu-id="18b5b-338">웹 배포는 프로젝트의 *App\_데이터* 폴더에 있는 SQL Server Compact 데이터베이스를 읽고 프로덕션 SQL Server 데이터베이스에 있는 모든 테이블 및 데이터를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-338">Web Deploy will read the SQL Server Compact databases in your project's *App\_Data* folder and re-create all of their tables and data in the production SQL Server database.</span></span> <span data-ttu-id="18b5b-339">**웹 패키지 및 게시** 탭 설정을 사용 하 여 게시 하려면 프로덕션을 위한 새 게시 프로필을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-339">In order to publish by using the **Package/Publish Web** tab settings, you have to create a new publish profile for production.</span></span>

<span data-ttu-id="18b5b-340">먼저 이전에 테스트 프로필을 수행한 것 처럼 기존 프로덕션 프로필을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-340">First, delete the existing Production profile as you did the Test profile earlier.</span></span>

<span data-ttu-id="18b5b-341">**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-341">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="18b5b-342">**프로필** 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-342">Select the **Profile** tab.</span></span>

<span data-ttu-id="18b5b-343">**프로필 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-343">Click **Manage Profiles**.</span></span>

<span data-ttu-id="18b5b-344">**프로덕션**을 선택 하 고 **제거**를 클릭 한 다음 **닫기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-344">Select **Production**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="18b5b-345">이 변경 내용을 저장 하려면 **웹 게시** 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-345">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="18b5b-346">그런 다음 새 프로덕션 프로필을 만들고이를 사용 하 여 프로젝트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-346">Next, create a new Production profile and use it to publish the project.</span></span>

<span data-ttu-id="18b5b-347">**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-347">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="18b5b-348">**프로필** 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-348">Select the **Profile** tab.</span></span>

<span data-ttu-id="18b5b-349">**가져오기**를 클릭 하 고 앞에서 다운로드 한 publishsettings 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-349">Click **Import**, and select the .publishsettings file that you downloaded earlier.</span></span>

<span data-ttu-id="18b5b-350">**연결** 탭에서 **대상 url** 을 올바른 임시 url로 변경 합니다 .이 예제에서는 http://contosouniversity.com.vserver01.cytanium.com합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-350">On the **Connection** tab, change the **Destination URL** to the correct temporary URL, which in this example is http://contosouniversity.com.vserver01.cytanium.com.</span></span>

<span data-ttu-id="18b5b-351">프로필의 이름을 Production로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-351">Rename the profile to Production.</span></span> <span data-ttu-id="18b5b-352">( **프로필** 탭을 선택 하 고 **프로필 관리** 를 클릭 하 여 해당 작업을 수행 합니다.)</span><span class="sxs-lookup"><span data-stu-id="18b5b-352">(Select the **Profile** tab and click **Manage Profiles** to do that).</span></span>

<span data-ttu-id="18b5b-353">**웹 게시** 마법사를 닫고 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-353">Close the **Publish Web** wizard to save your changes.</span></span>

<span data-ttu-id="18b5b-354">프로덕션에서 데이터베이스를 업데이트 하는 실제 응용 프로그램에서는 게시 하기 전에 다음과 같은 두 가지 추가 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-354">In a real application in which the database was being updated in production, you would do two additional steps now before you publish:</span></span>

1. <span data-ttu-id="18b5b-355">[프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에 표시 된 대로 *앱\_오프 라인*으로 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-355">Upload *app\_offline.htm*, as shown in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span>
2. <span data-ttu-id="18b5b-356">Cytanium 제어판의 **파일 관리자** 기능을 사용 하 여 프로덕션 사이트에서 ContosoUniversity 프로젝트의 *App\_Data* 폴더로 *aspnet-Prod* 및 *School-Prod* 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-356">Use the **File Manager** feature of the Cytanium control panel to copy the *aspnet-Prod.sdf* and *School-Prod.sdf* files from the production site to the *App\_Data* folder of the ContosoUniversity project.</span></span> <span data-ttu-id="18b5b-357">이렇게 하면 새 SQL Server 데이터베이스에 배포 하는 데이터에 프로덕션 웹 사이트에서 수행 하는 최신 업데이트가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-357">This ensures that the data you're deploying to the new SQL Server database includes the latest updates made by your production website.</span></span>

<span data-ttu-id="18b5b-358">웹에서 **게시** 도구 모음을 클릭 한 다음 **프로덕션** 프로필을 선택 했는지 확인 하 고 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-358">In the **Web One Click Publish** toolbar, make sure that the **Production** profile is selected, and then click **Publish**.</span></span>

<span data-ttu-id="18b5b-359">게시 하기 전에 <em>오프 라인으로\_앱</em> 을 업로드 한 경우 Cytanium 제어판의 <strong>파일 관리자</strong> 유틸리티를 사용 하 여 <em>오프 라인에서 앱\_</em> 를 삭제 해야 합니다. 테스트 하기 전에 htm.</span><span class="sxs-lookup"><span data-stu-id="18b5b-359">If you uploaded <em>app\_offline.htm</em> before publishing, you have to use the <strong>File Manager</strong> utility in the Cytanium control panel to delete <em>app\_offline.</em>htm before you test.</span></span> <span data-ttu-id="18b5b-360">또한 <em>앱\_데이터</em> 폴더에서 <em>.sdf</em> 파일을 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-360">You can also at the same time delete the <em>.sdf</em> files from the <em>App\_Data</em> folder.</span></span>

<span data-ttu-id="18b5b-361">이제 브라우저를 열고 공용 사이트의 URL로 이동 하 여 테스트 환경에 배포한 후와 동일한 방식으로 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-361">You can now open a browser and go to the URL of your public site to test the application the same way you did after deploying to the test environment.</span></span>

## <a name="switching-to-sql-server-express-localdb-in-development"></a><span data-ttu-id="18b5b-362">개발 중인 LocalDB SQL Server Express로 전환</span><span class="sxs-lookup"><span data-stu-id="18b5b-362">Switching to SQL Server Express LocalDB in Development</span></span>

<span data-ttu-id="18b5b-363">개요에 설명 된 대로 일반적으로 테스트 및 프로덕션 환경에서 사용 하는 것과 동일한 데이터베이스 엔진을 개발에 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-363">As was explained in the Overview, it's generally best to use the same database engine in development that you use in test and production.</span></span> <span data-ttu-id="18b5b-364">개발에 SQL Server Express를 사용 하는 이점은 데이터베이스가 개발, 테스트 및 프로덕션 환경에서 동일 하 게 작동 한다는 것을 명심 해야 합니다. 이 섹션에서는 Visual Studio에서 응용 프로그램을 실행할 때 SQL Server Express LocalDB를 사용 하도록 ContosoUniversity 프로젝트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-364">(Remember that the advantage to using SQL Server Express in development is that the database will work the same in your development, test, and production environments.) In this section you'll set up the ContosoUniversity project to use SQL Server Express LocalDB when you run the application from Visual Studio.</span></span>

<span data-ttu-id="18b5b-365">이 마이그레이션을 수행 하는 가장 간단한 방법은 Code First 하 고 멤버 자격 시스템에서 새로운 개발 데이터베이스를 모두 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-365">The simplest way to perform this migration is to let Code First and the membership system create both new development databases for you.</span></span> <span data-ttu-id="18b5b-366">이 방법을 사용 하려면 다음 세 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-366">Using this method to migrate requires three steps:</span></span>

1. <span data-ttu-id="18b5b-367">새 SQL Express LocalDB 데이터베이스를 지정 하도록 연결 문자열을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-367">Change the connection strings to specify new SQL Express LocalDB databases.</span></span>
2. <span data-ttu-id="18b5b-368">웹 사이트 관리 도구를 실행 하 여 관리자 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-368">Run the Web Site Administration Tool to create an administrator user.</span></span> <span data-ttu-id="18b5b-369">그러면 멤버 자격 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-369">This creates the membership database.</span></span>
3. <span data-ttu-id="18b5b-370">Code First 마이그레이션 update-database 명령을 사용 하 여 응용 프로그램 데이터베이스를 만들고 초기값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-370">Use the Code First Migrations update-database command to create and seed the application database.</span></span>

### <a name="updating-connection-strings-in-the-webconfig-file"></a><span data-ttu-id="18b5b-371">Web.config 파일에서 연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="18b5b-371">Updating Connection Strings in the Web.config file</span></span>

<span data-ttu-id="18b5b-372">*Web.config* 파일을 열고 `connectionStrings` 요소를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-372">Open the *Web.config* file and replace the `connectionStrings` element with the following code:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a><span data-ttu-id="18b5b-373">멤버 자격 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="18b5b-373">Creating the Membership Database</span></span>

<span data-ttu-id="18b5b-374">**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 선택한 다음 **프로젝트** 메뉴에서 **ASP.NET 구성** 을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-374">In **Solution Explorer**, select the ContosoUniversity project, and then click **ASP.NET Configuration** in the **Project** menu.</span></span>

<span data-ttu-id="18b5b-375">보안 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-375">Select the Security tab.</span></span>

<span data-ttu-id="18b5b-376">**역할 만들기 또는 관리**를 클릭 한 다음 **관리자** 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-376">Click **Create or Manage Roles**, and then create an **Administrator** role.</span></span>

<span data-ttu-id="18b5b-377">보안 탭으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-377">Return to the Security tab.</span></span>

<span data-ttu-id="18b5b-378">**사용자 만들기**를 클릭 한 다음 **관리자** 확인란을 선택 하 고 admin 이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-378">Click **Create user**, and then select the **Administrator** check box and create a user named admin.</span></span>

<span data-ttu-id="18b5b-379">**웹 사이트 관리 도구**를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-379">Close the **Web Site Administration Tool**.</span></span>

### <a name="creating-the-school-database"></a><span data-ttu-id="18b5b-380">School 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="18b5b-380">Creating the School Database</span></span>

<span data-ttu-id="18b5b-381">패키지 관리자 콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-381">Open the Package Manager Console window.</span></span>

<span data-ttu-id="18b5b-382">**기본 프로젝트** 드롭다운 목록에서 ContosoUniversity 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-382">In the **Default project** drop-down list, select the ContosoUniversity.DAL project.</span></span>

<span data-ttu-id="18b5b-383">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-383">Enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

<span data-ttu-id="18b5b-384">Code First 마이그레이션는 데이터베이스를 만드는 초기 마이그레이션을 적용 한 다음 AddBirthDate 마이그레이션을 적용 한 후 초기값 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-384">Code First Migrations applies the Initial migration that creates the database and then applies the AddBirthDate migration, then it runs the Seed method.</span></span>

<span data-ttu-id="18b5b-385">Ctrl 키를 눌러 사이트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-385">Run the site by pressing Control-F5.</span></span> <span data-ttu-id="18b5b-386">테스트 및 프로덕션 환경에서 수행한 것 처럼 **학생 추가** 페이지를 실행 하 고 새 학생을 추가한 다음 **학생** 페이지에서 새 학생을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-386">As you did for the test and production environments, run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="18b5b-387">이렇게 하면 School 데이터베이스가 만들어지고 초기화 되었으며 여기에 대 한 읽기 및 쓰기 권한이 있는지 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-387">This verifies that the School database was created and initialized and that you have read and write access to it.</span></span>

<span data-ttu-id="18b5b-388">**크레딧 업데이트** 페이지를 선택 하 고 로그인 하 여 멤버 자격 데이터베이스가 배포 되어 있고 액세스 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-388">Select the **Update Credits** page and log in to verify that the membership database was deployed and that you have access to it.</span></span> <span data-ttu-id="18b5b-389">사용자 계정을 마이그레이션하지 않은 경우 관리자 계정을 만든 다음, **크레딧 업데이트** 페이지를 선택 하 여 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-389">If you did not migrate your user accounts, create an administrator account and then select the **Update Credits** page to verify that it works.</span></span>

## <a name="cleaning-up-sql-server-compact-files"></a><span data-ttu-id="18b5b-390">SQL Server Compact 파일 정리</span><span class="sxs-lookup"><span data-stu-id="18b5b-390">Cleaning Up SQL Server Compact Files</span></span>

<span data-ttu-id="18b5b-391">SQL Server Compact를 지원 하기 위해 포함 된 파일 및 NuGet 패키지는 더 이상 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-391">You no longer need files and NuGet packages that were included to support SQL Server Compact.</span></span> <span data-ttu-id="18b5b-392">원하는 경우 (이 단계는 필요 하지 않음) 불필요 한 파일 및 참조를 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-392">If you want (this step is not required), you can clean up unneeded files and references.</span></span>

<span data-ttu-id="18b5b-393">**솔루션 탐색기**에서 *응용 프로그램\_Data* 폴더의 *.sdf* 파일과 *bin* 폴더의 *amd64* 및 *x86* 폴더를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-393">In **Solution Explorer**, delete the *.sdf* files from the *App\_Data* folder and the *amd64* and *x86* folders from the *bin* folder.</span></span>

<span data-ttu-id="18b5b-394">**솔루션 탐색기**에서 솔루션 (프로젝트 중 하나가 아님)을 마우스 오른쪽 단추로 클릭 한 다음 **솔루션에 대 한 NuGet 패키지 관리**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-394">In **Solution Explorer**, right-click the solution (not one of the projects), and then click **Manage NuGet Packages for Solution**.</span></span>

<span data-ttu-id="18b5b-395">**NuGet 패키지 관리** 대화 상자의 왼쪽 창에서 **설치 된 패키지**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-395">In the left pane of the **Manage NuGet Packages** dialog box, select **Installed packages**.</span></span>

<span data-ttu-id="18b5b-396">**SqlServerCompact** 패키지를 선택 하 고 **관리**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-396">Select the **EntityFramework.SqlServerCompact** package and click **Manage**.</span></span>

<span data-ttu-id="18b5b-397">**프로젝트 선택** 대화 상자에서 두 프로젝트를 모두 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-397">In the **Select Projects** dialog box, both projects are selected.</span></span> <span data-ttu-id="18b5b-398">두 프로젝트 모두에서 패키지를 제거 하려면 두 확인란의 선택을 취소 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-398">To uninstall the package in both projects, clear both check boxes, then click **OK**.</span></span>

<span data-ttu-id="18b5b-399">종속 패키지를 제거할지 묻는 대화 상자에서 아니요를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-399">In the dialog box that asks if you want to uninstall the dependent packages also, click No.</span></span> <span data-ttu-id="18b5b-400">다음 중 하나는 유지 해야 하는 Entity Framework 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-400">One of these is the Entity Framework package that you have to keep.</span></span>

<span data-ttu-id="18b5b-401">동일한 절차에 따라 **SqlServerCompact** 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-401">Follow the same procedure to uninstall the **SqlServerCompact** package.</span></span> <span data-ttu-id="18b5b-402">**SqlServerCompact** 패키지는 **SqlServerCompact** 패키지에 종속 되므로이 순서로 패키지를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-402">(The packages must be uninstalled in this order because the **EntityFramework.SqlServerCompact** package depends on the **SqlServerCompact** package.)</span></span>

<span data-ttu-id="18b5b-403">이제 SQL Server Express 및 전체 SQL Server 성공적으로 마이그레이션 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-403">You have now successfully migrated to SQL Server Express and full SQL Server.</span></span> <span data-ttu-id="18b5b-404">다음 자습서에서는 다른 데이터베이스를 변경 하 고 테스트 및 프로덕션 데이터베이스에서 SQL Server Express 및 전체 SQL Server를 사용 하는 경우 데이터베이스 변경 내용을 배포 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="18b5b-404">In the next tutorial you'll make another database change, and you'll see how to deploy database changes when your test and production databases use SQL Server Express and full SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="18b5b-405">[이전](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="18b5b-405">[Previous](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span></span>
