---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server 데이터베이스 업데이트 배포-11/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78423977"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a><span data-ttu-id="b0f97-103">Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server 데이터베이스 업데이트 배포-11/12</span><span class="sxs-lookup"><span data-stu-id="b0f97-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a SQL Server Database Update - 11 of 12</span></span>

<span data-ttu-id="b0f97-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="b0f97-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="b0f97-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="b0f97-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="b0f97-106">이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="b0f97-107">웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="b0f97-108">시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b0f97-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="b0f97-109">Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여주고, Windows Azure 웹 사이트에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 웹 배포 ASP.NET](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b0f97-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="b0f97-110">개요</span><span class="sxs-lookup"><span data-stu-id="b0f97-110">Overview</span></span>

<span data-ttu-id="b0f97-111">이 자습서에서는 전체 SQL Server 데이터베이스에 데이터베이스 업데이트를 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-111">This tutorial shows you how to deploy a database update to a full SQL Server database.</span></span> <span data-ttu-id="b0f97-112">Code First 마이그레이션는 데이터베이스 업데이트 작업을 모두 수행 하기 때문에이 프로세스는 [데이터베이스 업데이트 배포](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) 자습서에서 SQL Server Compact 했던 프로세스와 거의 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-112">Because Code First Migrations does all the work of updating the database, the process is almost identical to what you did for SQL Server Compact in the [Deploying a Database Update](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) tutorial.</span></span>

<span data-ttu-id="b0f97-113">미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="b0f97-114">테이블에 새 열 추가</span><span class="sxs-lookup"><span data-stu-id="b0f97-114">Adding a New Column to a Table</span></span>

<span data-ttu-id="b0f97-115">자습서의이 섹션에서는 데이터베이스를 변경 하 고 해당 코드를 변경한 다음 테스트 및 프로덕션 환경에 배포 하기 위해 Visual Studio에서 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-115">In this section of the tutorial you'll make a database change and corresponding code changes, then test them in Visual Studio in preparation for deploying them to the test and production environments.</span></span> <span data-ttu-id="b0f97-116">변경 내용에는 `OfficeHours` 열을 `Instructor` 엔터티에 추가 하 고 **강사** 웹 페이지에 새 정보를 표시 하는 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-116">The change involves adding an `OfficeHours` column to the `Instructor` entity and displaying the new information in the **Instructors** web page.</span></span>

<span data-ttu-id="b0f97-117">ContosoUniversity 프로젝트에서 *Instructor.cs* 를 열고 `HireDate`와 `Courses` 속성 사이에 다음 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-117">In the ContosoUniversity.DAL project, open *Instructor.cs* and add the following property between the `HireDate` and `Courses` properties:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

<span data-ttu-id="b0f97-118">테스트 데이터를 사용 하 여 새 열을 시드 하도록 이니셜라이저 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-118">Update the initializer class so that it seeds the new column with test data.</span></span> <span data-ttu-id="b0f97-119">*Migrations\ configuration.cs* 를 열고 `var instructors = new List<Instructor>` 시작 하는 코드 블록을 새 열을 포함 하는 다음 코드 블록으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes the new column:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

<span data-ttu-id="b0f97-120">ContosoUniversity 프로젝트에서 *강사 .aspx* 를 열고 첫 번째 `GridView` 컨트롤에서 닫는 `</Columns>` 태그 바로 앞에 office 시간에 대 한 새 템플릿 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-120">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field for office hours just before the closing `</Columns>` tag in the first `GridView` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

<span data-ttu-id="b0f97-121">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-121">Build the solution.</span></span>

<span data-ttu-id="b0f97-122">**패키지 관리자 콘솔** 창을 열고 **기본 프로젝트로**ContosoUniversity를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-122">Open the **Package Manager Console** window, and select ContosoUniversity.DAL as the **Default project**.</span></span>

<span data-ttu-id="b0f97-123">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-123">Enter the following commands:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

<span data-ttu-id="b0f97-124">응용 프로그램을 실행 하 고 **강사** 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-124">Run the application and select the **Instructors** page.</span></span> <span data-ttu-id="b0f97-125">Entity Framework는 데이터베이스를 다시 만들고 테스트 데이터를 사용 하 여 시드 하므로 페이지를 로드 하는 데 평소 보다 약간 더 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-125">The page takes a little longer than usual to load, because the Entity Framework re-creates the database and seeds it with test data.</span></span>

<span data-ttu-id="b0f97-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b0f97-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="b0f97-127">테스트 환경에 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="b0f97-127">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="b0f97-128">Code First 마이그레이션를 사용 하는 경우 데이터베이스 변경 내용을 SQL Server에 배포 하는 방법은 SQL Server Compact와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-128">When you use Code First Migrations, the method for deploying a database change to SQL Server is the same as for SQL Server Compact.</span></span> <span data-ttu-id="b0f97-129">그러나 SQL Server Compact에서 SQL Server로 마이그레이션하도록 설정 되어 있으므로 테스트 게시 프로필을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-129">However, you have to change the Test publish profile because it is still set up to migrate from SQL Server Compact to SQL Server.</span></span>

<span data-ttu-id="b0f97-130">첫 번째 단계는 이전 자습서에서 만든 연결 문자열 변환을 제거 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-130">The first step is to remove the connection string transformations that you created in the previous tutorial.</span></span> <span data-ttu-id="b0f97-131">SQL Server로 마이그레이션하기 위해 **SQL 패키지 및 게시** 탭을 구성 하기 전과 같이 게시 프로필에 연결 문자열 변환을 지정 하므로 더 이상 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-131">These are no longer needed because you'll specify connection string transformations in the publish profile, as you did before you configured the **Package/Publish SQL** tab for migration to SQL Server.</span></span>

<span data-ttu-id="b0f97-132">*Web.config* 파일을 열고 `connectionStrings` 요소를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-132">Open the *Web.Test.config* file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="b0f97-133">*Web.config 파일에서* 유일 하 게 남은 변환은 `appSettings` 요소의 `Environment` 값에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-133">The only remaining transformation in the *Web.Test.config* file is for the `Environment` value in the `appSettings` element.</span></span>

<span data-ttu-id="b0f97-134">이제 게시 프로필을 업데이트 하 고 테스트 환경에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-134">Now you can update the publish profile and publish to the test environment.</span></span>

<span data-ttu-id="b0f97-135">**웹 게시** 마법사를 열고 **프로필** 탭으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-135">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="b0f97-136">**테스트** 게시 프로필을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-136">Select the **Test** publish profile.</span></span>

<span data-ttu-id="b0f97-137">**설정** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-137">Select the **Settings** tab.</span></span>

<span data-ttu-id="b0f97-138">**새 데이터베이스 게시 개선 기능 사용을**클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-138">Click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="b0f97-139">**Schoolcontext.cs**에 대 한 연결 문자열 상자에 이전 자습서의 web.config 변환 파일에서 사용한 것과 동일한 값을 *입력 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b0f97-139">In the connection string box for **SchoolContext**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

<span data-ttu-id="b0f97-140">**Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-140">Select **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="b0f97-141">사용자의 Visual Studio 버전에서 확인란에 **Code First 마이그레이션 적용**이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-141">(In your version of Visual Studio, the check box might be labeled **Apply Code First Migrations**.)</span></span>

<span data-ttu-id="b0f97-142">**Defaultconnection**에 대 한 연결 문자열 상자에 이전 자습서의 web.config 변환 파일에서 사용한 것과 동일한 값을 *입력 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b0f97-142">In the connection string box for **DefaultConnection**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

<span data-ttu-id="b0f97-143">**업데이트 데이터베이스** 를 지운 채로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-143">Leave **Update database** cleared.</span></span>

<span data-ttu-id="b0f97-144">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-144">Click **Publish**.</span></span>

<span data-ttu-id="b0f97-145">Visual Studio는 테스트 환경에 코드 변경 내용을 배포 하 고 브라우저를 Contoso 대학 홈 페이지로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-145">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="b0f97-146">강사 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-146">Select the Instructors page.</span></span>

<span data-ttu-id="b0f97-147">응용 프로그램은이 페이지를 실행할 때 데이터베이스에 액세스를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-147">When the application runs this page, it tries to access the database.</span></span> <span data-ttu-id="b0f97-148">Code First 마이그레이션 데이터베이스가 최신 인지 확인 하 고 최신 마이그레이션이 아직 적용 되지 않은 것을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-148">Code First Migrations checks if the database is current, and finds that the latest migration has not been applied yet.</span></span> <span data-ttu-id="b0f97-149">Code First 마이그레이션 최신 마이그레이션을 적용 하 고 `Seed` 메서드를 실행 한 다음 페이지가 정상적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-149">Code First Migrations applies the latest migration, runs the `Seed` method, and then the page runs normally.</span></span> <span data-ttu-id="b0f97-150">시드 된 데이터와 함께 새 Office 시간 열이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-150">You see the new Office Hours column with the seeded data.</span></span>

<span data-ttu-id="b0f97-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b0f97-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="b0f97-152">프로덕션 환경에 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="b0f97-152">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="b0f97-153">프로덕션 환경에 대 한 게시 프로필도 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-153">You have to change the publish profile for the production environment also.</span></span> <span data-ttu-id="b0f97-154">이 경우 기존 프로필을 제거 하 고 publishsettings 파일을 가져와 새 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-154">In this case you'll remove the existing profile and create a new one by importing an updated .publishsettings file.</span></span> <span data-ttu-id="b0f97-155">업데이트 된 파일에는 Cytanium의 SQL Server 데이터베이스에 대 한 연결 문자열이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-155">The updated file will include the connection string for the SQL Server database at Cytanium.</span></span>

<span data-ttu-id="b0f97-156">테스트 환경에 배포할 때 볼 수 있듯이, *web.config* 변환 파일에 연결 문자열 변환이 더 이상 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-156">As you saw when you deployed to the test environment, you no longer need connection string transforms in the *Web.Production.config* transformation file.</span></span> <span data-ttu-id="b0f97-157">해당 파일을 열고 `connectionStrings` 요소를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-157">Open that file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="b0f97-158">나머지 변환은 `appSettings` 요소의 `Environment` 값 및 Elmah 오류 보고서에 대 한 액세스를 제한 하는 `location` 요소에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-158">The remaining transformations are for the `Environment` value in the `appSettings` element and the `location` element that restricts access to Elmah error reports.</span></span>

<span data-ttu-id="b0f97-159">프로덕션 환경에 대 한 새 게시 프로필을 만들기 전에 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서의 이전 단계와 동일한 방식으로 업데이트 된 publishsettings 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-159">Before you create a new publish profile for production, download an updated .publishsettings file the same way you did earlier in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="b0f97-160">Cytanium 컨트롤 패널에서 **웹 사이트**를 클릭 한 다음 **contosouniversity.com** 웹 사이트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-160">(In the Cytanium control panel, click **Web Sites**, and then click the **contosouniversity.com** website.</span></span> <span data-ttu-id="b0f97-161">**웹 게시** 탭을 선택 하 고 **이 웹 사이트에 대 한 게시 프로필 다운로드**를 클릭 합니다. 이 작업을 수행 하는 이유는 publishsettings 파일에서 데이터베이스 연결 문자열을 선택 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-161">Select the **Web Publishing** tab, and then click **Download Publishing Profile for this web site**.) The reason you are doing this is to pick up the database connection string in the .publishsettings file.</span></span> <span data-ttu-id="b0f97-162">연결 문자열은 파일을 처음 다운로드할 때 사용할 수 없습니다. 아직 SQL Server Compact를 사용 하 고 있으므로 아직 Cytanium에서 SQL Server 데이터베이스를 만들지 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-162">The connection string wasn't available the first time you downloaded the file, because you were still using SQL Server Compact and hadn't created the SQL Server database at Cytanium yet.</span></span>

<span data-ttu-id="b0f97-163">이제 게시 프로필을 업데이트 하 고 프로덕션 환경에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-163">Now you can update the publish profile and publish to the production environment.</span></span>

<span data-ttu-id="b0f97-164">**웹 게시** 마법사를 열고 **프로필** 탭으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-164">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="b0f97-165">**프로필 관리**를 클릭 한 다음 프로덕션 프로필을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-165">Click **Manage Profiles**, and then delete the Production profile.</span></span>

<span data-ttu-id="b0f97-166">이 변경 내용을 저장 하려면 **웹 게시** 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-166">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="b0f97-167">**웹 게시** 마법사를 다시 열고 **가져오기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-167">Open the **Publish Web** wizard again, and then click **Import**.</span></span>

<span data-ttu-id="b0f97-168">임시 URL을 사용 하는 경우 **연결** 탭에서 **대상 url** 을 적절 한 값으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-168">On the **Connection** tab, change **Destination URL** to the appropriate value if you are using a temporary URL.</span></span>

<span data-ttu-id="b0f97-169">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-169">Click **Next**.</span></span>

<span data-ttu-id="b0f97-170">**설정** 탭에서 **새 데이터베이스 게시 개선 기능 사용**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-170">On the **Settings** tab, click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="b0f97-171">**Schoolcontext.cs**에 대 한 연결 문자열 드롭다운 목록에서 Cytanium 연결 문자열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-171">In the connection string drop-down list for **SchoolContext**, select the Cytanium connection string.</span></span>

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

<span data-ttu-id="b0f97-173">**Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행)** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-173">Select **Execute Code First migrations (runs on application start)**.</span></span>

<span data-ttu-id="b0f97-174">**Defaultconnection**에 대 한 연결 문자열 드롭다운 목록에서 Cytanium 연결 문자열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-174">In the connection string drop-down list for **DefaultConnection**, select the Cytanium connection string.</span></span>

<span data-ttu-id="b0f97-175">**프로필** 탭을 선택 하 고, 프로필 **관리**를 클릭 하 고, 프로필 이름을 "contosouniversity.com-웹 배포"에서 "Production"로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-175">Select the **Profile** tab, click **Manage Profiles**, and rename the profile from "contosouniversity.com - Web Deploy" to "Production".</span></span>

<span data-ttu-id="b0f97-176">게시 프로필을 닫아 변경 내용을 저장 한 다음 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-176">Close the publish profile to save the change, then open it again.</span></span>

<span data-ttu-id="b0f97-177">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-177">Click **Publish**.</span></span> <span data-ttu-id="b0f97-178">실제 프로덕션 웹 사이트의 경우에는 *응용 프로그램\_오프 라인* 으로 복사 하 고 게시 하기 전에 프로젝트 폴더에 넣은 다음 배포가 완료 되 면 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-178">(For a real production website, you would copy *app\_offline.htm* to production and put it in your project folder before publishing, then remove it when deployment is complete.)</span></span>

<span data-ttu-id="b0f97-179">Visual Studio는 테스트 환경에 코드 변경 내용을 배포 하 고 브라우저를 Contoso 대학 홈 페이지로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-179">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="b0f97-180">강사 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-180">Select the Instructors page.</span></span>

<span data-ttu-id="b0f97-181">Code First 마이그레이션는 테스트 환경에서와 동일한 방식으로 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-181">Code First Migrations updates the database the same way it did in the Test environment.</span></span> <span data-ttu-id="b0f97-182">시드 된 데이터와 함께 새 Office 시간 열이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-182">You see the new Office Hours column with the seeded data.</span></span>

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

<span data-ttu-id="b0f97-184">이제 SQL Server 데이터베이스를 사용 하 여 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트를 성공적으로 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-184">You have now successfully deployed an application update that included a database change, using a SQL Server database.</span></span>

## <a name="more-information"></a><span data-ttu-id="b0f97-185">추가 정보</span><span class="sxs-lookup"><span data-stu-id="b0f97-185">More Information</span></span>

<span data-ttu-id="b0f97-186">이는 ASP.NET 웹 응용 프로그램을 타사 호스팅 공급자에 배포 하는 방법에 대 한 자습서 시리즈를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-186">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="b0f97-187">이러한 자습서에서 설명 하는 항목에 대 한 자세한 내용은 MSDN 웹 사이트에서 [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) 을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b0f97-187">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) on the MSDN web site.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="b0f97-188">감사의 말</span><span class="sxs-lookup"><span data-stu-id="b0f97-188">Acknowledgements</span></span>

<span data-ttu-id="b0f97-189">이 자습서 시리즈의 내용에 대해 상당한 기여를 수행한 다음 사용자에 게 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f97-189">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="b0f97-190">Alberto Poblacion, MVP &amp; MCT, 스페인</span><span class="sxs-lookup"><span data-stu-id="b0f97-190">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.support.microsoft.com/profile/Alberto)
- <span data-ttu-id="b0f97-191">Jarod Ferguson, Data Platform Development MVP, 미국</span><span class="sxs-lookup"><span data-stu-id="b0f97-191">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="b0f97-192">Microsoft의 거칠게 Mittal</span><span class="sxs-lookup"><span data-stu-id="b0f97-192">Harsh Mittal, Microsoft</span></span>
- [<span data-ttu-id="b0f97-193">Kristina Olson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="b0f97-193">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="b0f97-194">Mike Pope, Microsoft</span><span class="sxs-lookup"><span data-stu-id="b0f97-194">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="b0f97-195">Mohit Srivastava, Microsoft</span><span class="sxs-lookup"><span data-stu-id="b0f97-195">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="b0f97-196">Raffaele Rialdi, 이탈리아</span><span class="sxs-lookup"><span data-stu-id="b0f97-196">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="b0f97-197">Rick Anderson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="b0f97-197">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="b0f97-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="b0f97-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="b0f97-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="b0f97-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="b0f97-200">[Scott 헌터, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="b0f97-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="b0f97-201">Srđan Božović, 세르비아</span><span class="sxs-lookup"><span data-stu-id="b0f97-201">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="b0f97-202">[인 vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="b0f97-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b0f97-203">[이전](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [다음](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="b0f97-203">[Previous](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[Next](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span></span>
