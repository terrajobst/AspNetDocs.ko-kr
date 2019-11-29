---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 업데이트 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636826"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a><span data-ttu-id="176a1-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="176a1-103">ASP.NET Web Deployment using Visual Studio: Deploying a Database Update</span></span>

<span data-ttu-id="176a1-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="176a1-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="176a1-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="176a1-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="176a1-106">이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="176a1-107">계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="176a1-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="176a1-108">개요</span><span class="sxs-lookup"><span data-stu-id="176a1-108">Overview</span></span>

<span data-ttu-id="176a1-109">이 자습서에서는 데이터베이스를 변경 하 고 관련 코드를 변경 하 고, Visual Studio에서 변경 내용을 테스트 하 고, 테스트, 스테이징 및 프로덕션 환경에 업데이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-109">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to the test, staging, and production environments.</span></span>

<span data-ttu-id="176a1-110">이 자습서에서는 먼저 Code First 마이그레이션로 관리 되는 데이터베이스를 업데이트 한 다음 나중에 dbDacFx 공급자를 사용 하 여 데이터베이스를 업데이트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-110">The tutorial first shows how to update a database that is managed by Code First Migrations, and then later it shows how to update a database by using the dbDacFx provider.</span></span>

<span data-ttu-id="176a1-111">미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](troubleshooting.md)를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-111">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a><span data-ttu-id="176a1-112">Code First 마이그레이션를 사용 하 여 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="176a1-112">Deploy a database update by using Code First Migrations</span></span>

<span data-ttu-id="176a1-113">이 섹션에서는 `Student` 및 `Instructor` 엔터티에 대 한 `Person` 기본 클래스에 생년월일 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-113">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="176a1-114">그런 다음 새 열을 표시 하도록 강사 데이터를 표시 하는 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-114">Then you update the page that displays instructor data so that it displays the new column.</span></span> <span data-ttu-id="176a1-115">마지막으로 테스트, 스테이징 및 프로덕션에 대 한 변경 내용을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-115">Finally, you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-application-database"></a><span data-ttu-id="176a1-116">응용 프로그램 데이터베이스의 테이블에 열 추가</span><span class="sxs-lookup"><span data-stu-id="176a1-116">Add a column to a table in the application database</span></span>

1. <span data-ttu-id="176a1-117">*ContosoUniversity* 프로젝트에서 *Person.cs* 를 열고 `Person` 클래스의 끝에 다음 속성을 추가 합니다. 다음에 닫는 중괄호가 두 개 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-117">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    <span data-ttu-id="176a1-118">그런 다음 새 열에 대 한 값을 제공 하도록 `Seed` 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-118">Next, update the `Seed` method so that it provides a value for the new column.</span></span> <span data-ttu-id="176a1-119">*Migrations\ configuration.cs* 를 열고 `var instructors = new List<Instructor>` 시작 하는 코드 블록을 출생 날짜 정보를 포함 하는 다음 코드 블록으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. <span data-ttu-id="176a1-120">솔루션을 빌드한 다음 **패키지 관리자 콘솔** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-120">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="176a1-121">ContosoUniversity가 여전히 **기본 프로젝트로**선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-121">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>
3. <span data-ttu-id="176a1-122">**패키지 관리자 콘솔** 창에서 **기본 프로젝트로** **ContosoUniversity** 를 선택 하 고 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-122">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    <span data-ttu-id="176a1-123">이 명령이 완료 되 면 Visual Studio는 새 `DbMigration` 클래스를 정의 하는 클래스 파일을 열고 `Up` 메서드에서 새 열을 만드는 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-123">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span> <span data-ttu-id="176a1-124">`Up` 메서드는 변경을 구현할 때 열을 만들고, `Down` 메서드는 변경을 롤백할 때 열을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-124">The `Up` method creates the column when you are implementing the change, and the `Down` method deletes the column when you are rolling back the change.</span></span>

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. <span data-ttu-id="176a1-126">솔루션을 빌드한 후 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다 (ContosoUniversity 프로젝트를 계속 선택 해야 합니다).</span><span class="sxs-lookup"><span data-stu-id="176a1-126">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    <span data-ttu-id="176a1-127">Entity Framework `Up` 메서드를 실행 한 다음 `Seed` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-127">The Entity Framework runs the `Up` method and then runs the `Seed` method.</span></span>

### <a name="display-the-new-column-in-the-instructors-page"></a><span data-ttu-id="176a1-128">강사 페이지에 새 열을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-128">Display the new column in the Instructors page</span></span>

1. <span data-ttu-id="176a1-129">ContosoUniversity 프로젝트에서 *강사 .aspx* 를 열고 생년월일을 표시할 새 템플릿 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-129">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="176a1-130">채용 날짜 및 사무실 할당에 대 한 항목 사이에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-130">Add it between the ones for hire date and office assignment:</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    <span data-ttu-id="176a1-131">코드 들여쓰기가 동기화 되지 않으면 CTRL + K를 누르고 CTRL + D를 눌러 자동으로 파일의 서식을 다시 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-131">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>
2. <span data-ttu-id="176a1-132">응용 프로그램을 실행 하 고 **강사** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-132">Run the application and click the **Instructors** link.</span></span>

    <span data-ttu-id="176a1-133">페이지가 로드 되 면 새 생년월일 필드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-133">When the page loads, you see that it has the new birth date field.</span></span>

    ![생일을 사용 하는 강사 페이지](deploying-a-database-update/_static/image2.png)
3. <span data-ttu-id="176a1-135">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-135">Close the browser.</span></span>

### <a name="deploy-the-database-update"></a><span data-ttu-id="176a1-136">데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="176a1-136">Deploy the database update</span></span>

1. <span data-ttu-id="176a1-137">**솔루션 탐색기** 에서 ContosoUniversity 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-137">In **Solution Explorer** select the ContosoUniversity project.</span></span>
2. <span data-ttu-id="176a1-138">웹에서 **게시** 도구 모음을 클릭 하 고 **테스트** 게시 프로필을 클릭 한 다음 **웹 게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-138">In the **Web One Click Publish** toolbar, click the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="176a1-139">(도구 모음을 사용할 수 없는 경우 **솔루션 탐색기**에서 ContosoUniversity 프로젝트를 선택 합니다.)</span><span class="sxs-lookup"><span data-stu-id="176a1-139">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

    <span data-ttu-id="176a1-140">Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 홈 페이지에 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-140">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
3. <span data-ttu-id="176a1-141">**강사** 페이지를 실행 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-141">Run the **Instructors** page to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="176a1-142">응용 프로그램에서이 페이지의 데이터베이스에 액세스 하려고 하면 Code First는 데이터베이스 스키마를 업데이트 하 고 `Seed` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-142">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="176a1-143">페이지가 표시 되 면 예상 **생년월일** 열에 날짜가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-143">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>
4. <span data-ttu-id="176a1-144">웹에서 **게시** 도구 모음을 클릭 한 다음 **스테이징** 게시 프로필을 클릭 하 고 **웹 게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-144">In the **Web One Click Publish** toolbar, click the **Staging** publish profile, and then click **Publish Web**.</span></span>
5. <span data-ttu-id="176a1-145">스테이징에서 **강사** 페이지를 실행 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-145">Run the **Instructors** page in staging to verify that the update was successfully deployed.</span></span>
6. <span data-ttu-id="176a1-146">웹에서 **게시** 도구 모음을 클릭 한 다음 **프로덕션** 게시 프로필을 클릭 하 고 **웹 게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-146">In the **Web One Click Publish** toolbar, click the **Production** publish profile, and then click **Publish Web**.</span></span>
7. <span data-ttu-id="176a1-147">프로덕션에서 **강사** 페이지를 실행 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-147">Run the **Instructors** page in production to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="176a1-148">데이터베이스 변경을 포함 하는 실제 프로덕션 응용 프로그램 업데이트의 경우 일반적으로 이전 자습서에서 살펴본 것 처럼 응용 프로그램을 *\_오프 라인*으로 사용 하 여 배포 하는 동안 응용 프로그램을 오프 라인으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-148">For a real production application update that includes a database change you would also typically take the application offline during deployment by using *app\_offline.htm*, as you saw in the previous tutorial.</span></span>

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a><span data-ttu-id="176a1-149">DbDacFx 공급자를 사용 하 여 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="176a1-149">Deploy a database update by using the dbDacFx provider</span></span>

<span data-ttu-id="176a1-150">이 섹션에서는 멤버 자격 데이터베이스의 *사용자* 테이블에 *comments* 열을 추가 하 고 각 사용자에 대 한 설명을 표시 하 고 편집할 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-150">In this section, you add a *Comments* column to the *User* table in the membership database and create a page that lets you display and edit comments for each user.</span></span> <span data-ttu-id="176a1-151">그런 다음 테스트, 스테이징 및 프로덕션에 대 한 변경 내용을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-151">Then you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-membership-database"></a><span data-ttu-id="176a1-152">멤버 자격 데이터베이스의 테이블에 열 추가</span><span class="sxs-lookup"><span data-stu-id="176a1-152">Add a column to a table in the membership database</span></span>

1. <span data-ttu-id="176a1-153">Visual Studio에서 **SQL Server 개체 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-153">In Visual Studio, open **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="176a1-154">**(Localdb) \v11.0**, **데이터베이스**, **aspnet-ContosoUniversity** ( **ContosoUniversity-Prod**)를 차례로 확장 한 다음 **테이블**을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-154">Expand **(localdb)\v11.0**, expand **Databases**, expand **aspnet-ContosoUniversity** (not **aspnet-ContosoUniversity-Prod**) and then expand **Tables**.</span></span>

    <span data-ttu-id="176a1-155">**SQL Server** 노드 아래에 **(localdb) \v11.0** 이 표시 되지 않으면 **SQL Server** 노드를 마우스 오른쪽 단추로 클릭 하 고 **SQL Server 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-155">If you don't see **(localdb)\v11.0** under the **SQL Server** node, right-click the **SQL Server** node and click **Add SQL Server**.</span></span> <span data-ttu-id="176a1-156">**서버에 연결** 대화 상자에서 **서버 이름**으로 *(localdb) \v11.0* 을 입력 한 다음 **연결**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-156">In the **Connect to Server** dialog box enter *(localdb)\v11.0* as the **Server name**, and then click **Connect**.</span></span>

    <span data-ttu-id="176a1-157">**ContosoUniversity**가 표시 되지 않으면 프로젝트를 실행 하 고 *관리자* 자격 증명 (암호는 *devpwd*)을 사용 하 여 로그인 한 다음 **SQL Server 개체 탐색기** 창을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-157">If you don't see **aspnet-ContosoUniversity**, run the project and log in using the *admin* credentials (password is *devpwd*), and then refresh the **SQL Server Object Explorer** window.</span></span>
3. <span data-ttu-id="176a1-158">**사용자** 테이블을 마우스 오른쪽 단추로 클릭 한 다음 **뷰 디자이너**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-158">Right-click the **Users** table, and then click **View Designer**.</span></span>

    ![SSOX 뷰 디자이너](deploying-a-database-update/_static/image3.png)
4. <span data-ttu-id="176a1-160">디자이너에서 *주석* 열을 추가 하 고 *nvarchar (128)* 및 nullable로 설정 하 고 **업데이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-160">In the designer, add a *Comments* column and make it *nvarchar(128)* and nullable, and then click **Update**.</span></span>

    ![설명 열 추가](deploying-a-database-update/_static/image4.png)
5. <span data-ttu-id="176a1-162">데이터베이스 업데이트 **미리 보기** 상자에서 **데이터베이스 업데이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-162">In the **Preview Database Updates** box, click **Update Database**.</span></span>

    ![데이터베이스 업데이트 미리 보기](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a><span data-ttu-id="176a1-164">새 열을 표시 하 고 편집할 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-164">Create a page to display and edit the new column</span></span>

1. <span data-ttu-id="176a1-165">**솔루션 탐색기**에서 ContosoUniversity 프로젝트의 **계정** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 항목**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-165">In **Solution Explorer**, right-click the **Account** folder in the ContosoUniversity project, click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="176a1-166">**마스터 페이지를 사용 하 여 새 Web Form** 을 만들고 이름을 *login.aspx*로 이름을로 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-166">Create a new **Web Form Using Master Page** and name it *UserInfo.aspx*.</span></span> <span data-ttu-id="176a1-167">기본 site.master 파일을 마스터 페이지로 적용 *합니다.*</span><span class="sxs-lookup"><span data-stu-id="176a1-167">Accept the default *Site.Master* file as the master page.</span></span>
3. <span data-ttu-id="176a1-168">다음 태그를 `MainContent` `Content` 요소 (3 개의 `Content` 요소 중 마지막 요소)에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-168">Copy the following markup into the `MainContent` `Content` element (the last of the 3 `Content` elements):</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. <span data-ttu-id="176a1-169">*UserInfo* 페이지를 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 보기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-169">Right-click the *UserInfo.aspx* page and click **View in Browser**.</span></span>
5. <span data-ttu-id="176a1-170">*관리자* 사용자 자격 증명을 사용 하 여 로그인 하 고 (암호는 *devpwd*) 사용자에 게 일부 의견을 추가 하 여 페이지가 제대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-170">Log in with your *admin* user credentials (password is *devpwd*) and add some comments to a user to verify that the page works correctly.</span></span>

    ![UserInfo 페이지](deploying-a-database-update/_static/image6.png)
6. <span data-ttu-id="176a1-172">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-172">Close the browser.</span></span>

## <a name="deploy-the-database-update"></a><span data-ttu-id="176a1-173">데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="176a1-173">Deploy the database update</span></span>

<span data-ttu-id="176a1-174">DbDacFx 공급자를 사용 하 여 배포 하려면 게시 프로필에서 **데이터베이스 업데이트** 옵션을 선택 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-174">To deploy by using the dbDacFx provider, you just need to select the **Update database** option in the publish profile.</span></span> <span data-ttu-id="176a1-175">그러나이 옵션을 사용 하는 경우 초기 배포의 경우 몇 가지 추가 SQL 스크립트를 실행할 수도 있습니다. 이러한 스크립트는 여전히 프로필에 포함 되어 있으므로 다시 실행 하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-175">However, for the initial deployment when you used this option you also configured some additional SQL scripts to run: those are still in the profile and you'll have to prevent them from running again.</span></span>

1. <span data-ttu-id="176a1-176">ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 하 여 **웹 게시** 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-176">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="176a1-177">**테스트** 프로필을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-177">Select the **Test** profile.</span></span>
3. <span data-ttu-id="176a1-178">**설정** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-178">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="176a1-179">**Defaultconnection**에서 **데이터베이스 업데이트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-179">Under **DefaultConnection**, select **Update database**.</span></span>
5. <span data-ttu-id="176a1-180">초기 배포에 대해 실행 하도록 구성한 추가 스크립트를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-180">Disable the additional scripts that you configured to run for the initial deployment:</span></span>

    1. <span data-ttu-id="176a1-181">**데이터베이스 업데이트 구성**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-181">Click **Configure database updates**.</span></span>
    2. <span data-ttu-id="176a1-182">**데이터베이스 업데이트 구성** 대화 상자에서 *Grant .sql* and *aspnet-data-dev*옆에 있는 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-182">In the **Configure Database Updates** dialog box, clear the check boxes next to *Grant.sql* and *aspnet-data-dev.sql*.</span></span>
    3. <span data-ttu-id="176a1-183">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-183">Click **Close**.</span></span>
6. <span data-ttu-id="176a1-184">**미리 보기** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-184">Click the **Preview** tab.</span></span>
7. <span data-ttu-id="176a1-185">데이터베이스 **에서** **defaultconnection**의 오른쪽에 있는 **데이터베이스 미리 보기** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-185">Under **Databases** and to the right of **DefaultConnection**, click the **Preview database** link.</span></span>

    ![데이터베이스 미리 보기](deploying-a-database-update/_static/image7.png)

    <span data-ttu-id="176a1-187">미리 보기 창에는 데이터베이스 스키마가 원본 데이터베이스의 스키마와 일치 하도록 대상 데이터베이스에서 실행 될 스크립트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-187">The preview window shows the script that will be run in the destination database to make that database schema match the schema of the source database.</span></span> <span data-ttu-id="176a1-188">스크립트에는 새 열을 추가 하는 ALTER TABLE 명령이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-188">The script includes an ALTER TABLE command that adds the new column.</span></span>
8. <span data-ttu-id="176a1-189">**데이터베이스 미리 보기** 대화 상자를 닫은 다음 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-189">Close the **Database Preview** dialog box, and then click **Publish**.</span></span>

    <span data-ttu-id="176a1-190">Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 홈 페이지에 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-190">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
9. <span data-ttu-id="176a1-191">정보 페이지 (홈 페이지 URL에 *계정/개인 정보 .aspx* 추가)를 실행 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-191">Run the UserInfo page (add *Account/UserInfo.aspx* to the home page URL) to verify that the update was successfully deployed.</span></span> <span data-ttu-id="176a1-192">*관리자* 및 *devpwd*를 입력 하 여 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-192">You'll have to log in by entering *admin* and *devpwd*.</span></span>

    <span data-ttu-id="176a1-193">테이블의 데이터는 기본적으로 배포 되지 않으며 데이터 배포 스크립트를 실행 하도록 구성 하지 않았기 때문에 개발에서 추가한 주석이 검색 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-193">Data in tables is not deployed by default, and you didn't configure a data deployment script to run, so you won't find the comment that you added in development.</span></span> <span data-ttu-id="176a1-194">이제 준비에 새 설명을 추가 하 여 변경 내용이 데이터베이스에 배포 되 고 페이지가 제대로 작동 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-194">You can add a new comment now in staging to verify that the change was deployed to the database and the page works correctly.</span></span>
10. <span data-ttu-id="176a1-195">동일한 절차에 따라 스테이징 및 프로덕션에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-195">Follow the same procedure to deploy to staging and production.</span></span>

    <span data-ttu-id="176a1-196">추가 스크립트를 사용 하지 않도록 설정 하는 것을 잊지 마세요.</span><span class="sxs-lookup"><span data-stu-id="176a1-196">Don't forget to disable the extra scripts.</span></span> <span data-ttu-id="176a1-197">테스트 프로필에 비해 유일한 차이점은 준비 및 프로덕션 프로필은 *aspnet-prod-data*만 실행 하도록 구성 되었기 때문에 한 개의 스크립트만 사용 하지 않도록 설정 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-197">The only difference compared to the Test profile is that you will disable only one script in the Staging and Production profiles because they were configured to run only *aspnet-prod-data.sql*.</span></span>

    <span data-ttu-id="176a1-198">스테이징 및 프로덕션에 대 한 자격 증명은 admin 및 prodpwd입니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-198">The credentials for staging and production are admin and prodpwd.</span></span>

    <span data-ttu-id="176a1-199">데이터베이스 변경을 포함 하는 실제 프로덕션 응용 프로그램 업데이트의 경우 [이전 자습서](deploying-a-code-update.md)에서 살펴본 것 처럼 나중에 게시 하 고 삭제 하기 전에 *오프 라인으로 앱\_* 업로드 하 여 배포 중에 응용 프로그램을 오프 라인으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-199">For a real production application update that includes a database change you would also typically take the application offline during deployment by uploading *app\_offline.htm* before publishing and deleting it afterward, as you saw in [the previous tutorial](deploying-a-code-update.md).</span></span>

## <a name="summary"></a><span data-ttu-id="176a1-200">요약</span><span class="sxs-lookup"><span data-stu-id="176a1-200">Summary</span></span>

<span data-ttu-id="176a1-201">이제 Code First 마이그레이션 및 dbDacFx 공급자를 사용 하 여 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-201">You've now deployed an application update that included a database change using both Code First Migrations and the dbDacFx provider.</span></span>

![생일을 사용 하는 강사 페이지](deploying-a-database-update/_static/image8.png)

![UserInfo 페이지](deploying-a-database-update/_static/image9.png)

<span data-ttu-id="176a1-204">다음 자습서는 명령줄을 사용 하 여 배포를 실행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="176a1-204">The next tutorial shows you how to execute deployments by using the command line.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="176a1-205">[이전](deploying-a-code-update.md)
> [다음](command-line-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="176a1-205">[Previous](deploying-a-code-update.md)
[Next](command-line-deployment.md)</span></span>
