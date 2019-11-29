---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 데이터베이스 업데이트 배포-9/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582001"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a><span data-ttu-id="9ac79-103">Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 데이터베이스 업데이트 배포-9/12</span><span class="sxs-lookup"><span data-stu-id="9ac79-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Database Update - 9 of 12</span></span>

<span data-ttu-id="9ac79-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9ac79-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="9ac79-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="9ac79-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="9ac79-106">이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="9ac79-107">웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="9ac79-108">시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9ac79-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="9ac79-109">Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="9ac79-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="9ac79-110">개요</span><span class="sxs-lookup"><span data-stu-id="9ac79-110">Overview</span></span>

<span data-ttu-id="9ac79-111">이 자습서에서는 데이터베이스를 변경 하 고 관련 코드를 변경 하 고, Visual Studio에서 변경 내용을 테스트 하 고, 테스트 환경과 프로덕션 환경 모두에 업데이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-111">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to both the test and production environments.</span></span>

<span data-ttu-id="9ac79-112">미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="9ac79-113">테이블에 새 열 추가</span><span class="sxs-lookup"><span data-stu-id="9ac79-113">Adding a New Column to a Table</span></span>

<span data-ttu-id="9ac79-114">이 섹션에서는 `Student` 및 `Instructor` 엔터티에 대 한 `Person` 기본 클래스에 생년월일 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-114">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="9ac79-115">그런 다음 새 열을 표시 하도록 강사 데이터를 표시 하는 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-115">Then you update the page that displays instructor data so that it displays the new column.</span></span>

<span data-ttu-id="9ac79-116">*ContosoUniversity* 프로젝트에서 *Person.cs* 를 열고 `Person` 클래스의 끝에 다음 속성을 추가 합니다. 다음에 닫는 중괄호가 두 개 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-116">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

<span data-ttu-id="9ac79-117">그런 다음 새 열에 대 한 값을 제공 하도록 초기값 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-117">Next, update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="9ac79-118">*Migrations\ configuration.cs* 를 열고 `var instructors = new List<Instructor>` 시작 하는 코드 블록을 출생 날짜 정보를 포함 하는 다음 코드 블록으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-118">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

<span data-ttu-id="9ac79-119">ContosoUniversity 프로젝트에서 *강사 .aspx* 를 열고 생년월일을 표시할 새 템플릿 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-119">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="9ac79-120">채용 날짜 및 사무실 할당에 대 한 항목 사이에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-120">Add it between the ones for hire date and office assignment:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

<span data-ttu-id="9ac79-121">코드 들여쓰기가 동기화 되지 않으면 CTRL + K를 누르고 CTRL + D를 눌러 자동으로 파일의 서식을 다시 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-121">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>

<span data-ttu-id="9ac79-122">솔루션을 빌드한 다음 **패키지 관리자 콘솔** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-122">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="9ac79-123">ContosoUniversity가 여전히 **기본 프로젝트로**선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-123">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>

<span data-ttu-id="9ac79-124">**패키지 관리자 콘솔** 창에서 **기본 프로젝트로** **ContosoUniversity** 를 선택 하 고 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-124">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

<span data-ttu-id="9ac79-125">이 명령이 완료 되 면 Visual Studio는 새 `DbMigration` 클래스를 정의 하는 클래스 파일을 열고 `Up` 메서드에서 새 열을 만드는 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-125">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span>

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

<span data-ttu-id="9ac79-127">솔루션을 빌드한 후 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다 (ContosoUniversity 프로젝트를 계속 선택 해야 합니다).</span><span class="sxs-lookup"><span data-stu-id="9ac79-127">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

<span data-ttu-id="9ac79-128">명령이 완료 되 면 응용 프로그램을 실행 하 고 강사 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-128">When the command finishes, run the application and select the Instructors page.</span></span> <span data-ttu-id="9ac79-129">페이지가 로드 되 면 새 생년월일 필드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-129">When the page loads, you see that it has the new birth date field.</span></span>

<span data-ttu-id="9ac79-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="9ac79-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="9ac79-131">테스트 환경에 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="9ac79-131">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="9ac79-132">**솔루션 탐색기** 에서 ContosoUniversity 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-132">In **Solution Explorer** select the ContosoUniversity project.</span></span>

<span data-ttu-id="9ac79-133">웹에서 **게시** 도구 모음을 클릭 한 다음 **테스트** 게시 프로필을 선택 하 고 **웹 게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-133">In the **Web One Click Publish** toolbar, select the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="9ac79-134">(도구 모음을 사용할 수 없는 경우 **솔루션 탐색기**에서 ContosoUniversity 프로젝트를 선택 합니다.)</span><span class="sxs-lookup"><span data-stu-id="9ac79-134">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

<span data-ttu-id="9ac79-135">Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 홈 페이지에 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-135">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span> <span data-ttu-id="9ac79-136">강사 페이지를 실행 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-136">Run the Instructors page to verify that the update was successfully deployed.</span></span> <span data-ttu-id="9ac79-137">응용 프로그램에서이 페이지의 데이터베이스에 액세스 하려고 하면 Code First는 데이터베이스 스키마를 업데이트 하 고 `Seed` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-137">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="9ac79-138">페이지가 표시 되 면 예상 **생년월일** 열에 날짜가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-138">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>

<span data-ttu-id="9ac79-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="9ac79-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="9ac79-140">프로덕션 환경에 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="9ac79-140">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="9ac79-141">이제 프로덕션 환경에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-141">You can now deploy to production.</span></span> <span data-ttu-id="9ac79-142">유일한 차이점은 사용자가 사이트에 액세스 하 여 변경 내용을 배포 하는 동안 데이터베이스를 업데이트 하는 것을 방지 하기 위해 *\_오프 라인 .htm 앱* 을 사용 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-142">The only difference is that you'll use *app\_offline.htm* to prevent users from accessing the site and thus updating the database while you're deploying changes.</span></span> <span data-ttu-id="9ac79-143">프로덕션 배포의 경우 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-143">For production deployment perform the following steps:</span></span>

- <span data-ttu-id="9ac79-144">*앱\_오프 라인 .htm* 파일을 프로덕션 사이트에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-144">Upload the *app\_offline.htm* file to the production site.</span></span>
- <span data-ttu-id="9ac79-145">Visual Studio의 **웹에서 게시** 도구 모음을 클릭 한 후 **웹 게시**를 클릭 하 여 프로덕션 프로필을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-145">In Visual Studio, choose the Production profile in the **Web One Click Publish** toolbar and click **Publish Web**.</span></span>
- <span data-ttu-id="9ac79-146">프로덕션 사이트에서 *앱\_오프 라인 .htm* 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-146">Delete the *app\_offline.htm* file from the production site.</span></span>

> [!NOTE]
> <span data-ttu-id="9ac79-147">프로덕션 환경에서 응용 프로그램을 사용 하는 동안에는 백업 계획을 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-147">While your application is in use in the production environment you should be implementing a backup plan.</span></span> <span data-ttu-id="9ac79-148">즉, 프로덕션 사이트에서 안전한 저장소 위치에 *School-Prod* 및 *aspnet-Prod* 파일을 주기적으로 복사 해야 하며, 이러한 백업에 대 한 여러 세대를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-148">That is, you should be periodically copying the *School-Prod.sdf* and *aspnet-Prod.sdf* files from the production site to a secure storage location, and you should be keeping several generations of such backups.</span></span> <span data-ttu-id="9ac79-149">데이터베이스를 업데이트 하는 경우 변경 직전에 백업 복사본을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-149">When you update the database, you should make a backup copy from immediately before the change.</span></span> <span data-ttu-id="9ac79-150">그런 다음, 실수를 하 고 프로덕션 환경에 배포한 후에도이를 검색 하지 않으면 데이터베이스가 손상 되기 전의 상태로 복구 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-150">Then, if you make a mistake and don't discover it until after you have deployed it to production, you will still be able to recover the database to the state it was in before it became corrupted.</span></span>

<span data-ttu-id="9ac79-151">Visual Studio가 브라우저에서 홈 페이지 URL을 열면 *앱\_오프 라인 .htm* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-151">When Visual Studio opens the home page URL in the browser, the *app\_offline.htm* page is displayed.</span></span> <span data-ttu-id="9ac79-152">*응용 프로그램\_오프 라인 .htm* 파일을 삭제 한 후 홈 페이지로 이동 하 여 업데이트가 성공적으로 배포 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-152">After you delete the *app\_offline.htm* file, you can browse to your home page again to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="9ac79-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="9ac79-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span></span>

<span data-ttu-id="9ac79-154">이제 테스트와 프로덕션 모두에 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-154">You've now deployed an application update that included a database change to both test and production.</span></span> <span data-ttu-id="9ac79-155">다음 자습서에서는 데이터베이스를 SQL Server Compact에서 SQL Server Express 및 SQL Server로 마이그레이션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ac79-155">The next tutorial shows you how to migrate your database from SQL Server Compact to SQL Server Express and SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9ac79-156">[이전](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [다음](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="9ac79-156">[Previous](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
[Next](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span></span>
