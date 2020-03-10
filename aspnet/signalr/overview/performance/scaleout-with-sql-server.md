---
uid: signalr/overview/performance/scaleout-with-sql-server
title: SQL Server SignalR 확장 | Microsoft Docs
author: bradygaster
description: 이전 버전의에 대 한 자세한 내용은이 항목에서 사용 된 소프트웨어 버전 Visual Studio 2013 .NET 4.5 SignalR 버전 2 이전 버전의 항목을 참조 하세요.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467741"
---
# <a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="3e67d-103">SQL Server로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="3e67d-103">SignalR Scaleout with SQL Server</span></span>

<span data-ttu-id="3e67d-104">사람, [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="3e67d-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="3e67d-105">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="3e67d-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="3e67d-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3e67d-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="3e67d-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="3e67d-107">.NET 4.5</span></span>
> - <span data-ttu-id="3e67d-108">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="3e67d-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="3e67d-109">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="3e67d-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="3e67d-110">이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3e67d-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="3e67d-111">질문 및 설명</span><span class="sxs-lookup"><span data-stu-id="3e67d-111">Questions and comments</span></span>
>
> <span data-ttu-id="3e67d-112">이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="3e67d-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="3e67d-113">자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="3e67d-114">이 자습서에서는 SQL Server를 사용 하 여 별도의 두 IIS 인스턴스에 배포 된 SignalR 응용 프로그램을 통해 메시지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="3e67d-115">단일 테스트 컴퓨터에서이 자습서를 실행할 수도 있지만, 전체 결과를 얻으려면 SignalR 응용 프로그램을 둘 이상의 서버에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="3e67d-116">또한 서버 중 하나 또는 별도의 전용 서버에 SQL Server를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="3e67d-117">또 다른 옵션은 Azure에서 Vm을 사용 하 여 자습서를 실행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="3e67d-118">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="3e67d-118">Prerequisites</span></span>

<span data-ttu-id="3e67d-119">2005 이상 Microsoft SQL Server 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="3e67d-120">후면판은 SQL Server의 데스크톱 및 서버 버전을 모두 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="3e67d-121">SQL Server Compact Edition 또는 Azure SQL Database를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="3e67d-122">응용 프로그램이 Azure에서 호스트 되는 경우에는 Service Bus 후면판을 고려 하세요.)</span><span class="sxs-lookup"><span data-stu-id="3e67d-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="3e67d-123">개요</span><span class="sxs-lookup"><span data-stu-id="3e67d-123">Overview</span></span>

<span data-ttu-id="3e67d-124">자세한 자습서를 시작 하기 전에 수행할 작업에 대 한 간략 한 개요를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3e67d-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="3e67d-125">비어 있는 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-125">Create a new empty database.</span></span> <span data-ttu-id="3e67d-126">후면판이이 데이터베이스에 필요한 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="3e67d-127">응용 프로그램에 다음 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-127">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="3e67d-128">SignalR</span><span class="sxs-lookup"><span data-stu-id="3e67d-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="3e67d-129">SignalR.</span><span class="sxs-lookup"><span data-stu-id="3e67d-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="3e67d-130">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="3e67d-131">Startup.cs에 다음 코드를 추가 하 여 후면판을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-131">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="3e67d-132">이 코드는 [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) 및 [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)에 대 한 기본값을 사용 하 여 후면판을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="3e67d-133">이러한 값을 변경 하는 방법에 대 한 자세한 내용은 [SignalR Performance: 확장 메트릭](signalr-performance.md#scaleout_metrics)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3e67d-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

## <a name="configure-the-database"></a><span data-ttu-id="3e67d-134">데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="3e67d-134">Configure the Database</span></span>

<span data-ttu-id="3e67d-135">응용 프로그램에서 데이터베이스에 액세스 하는 데 Windows 인증을 사용할지 또는 SQL Server 인증을 사용할지 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="3e67d-136">에 관계 없이 데이터베이스 사용자에 게 로그인 하 고, 스키마를 만들고, 테이블을 만들 수 있는 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="3e67d-137">후면판에서 사용할 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="3e67d-138">데이터베이스 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-138">You can give the database any name.</span></span> <span data-ttu-id="3e67d-139">데이터베이스에 테이블을 만들 필요가 없습니다. 후면판에서 필요한 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="3e67d-140">Service Broker 사용</span><span class="sxs-lookup"><span data-stu-id="3e67d-140">Enable Service Broker</span></span>

<span data-ttu-id="3e67d-141">후면판 데이터베이스에 대해 Service Broker를 사용 하도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="3e67d-142">Service Broker은 SQL Server의 메시징 및 큐에 대 한 기본 지원을 제공 하므로 후면판에서 업데이트를 보다 효율적으로 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="3e67d-143">그러나 후면판은 Service Broker 없이도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="3e67d-144">Service Broker 사용 하도록 설정 되어 있는지 여부를 확인 하려면를 사용 **하 여** **\_Broker\_사용** 열을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="3e67d-145">Service Broker를 사용 하도록 설정 하려면 다음 SQL 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="3e67d-146">이 쿼리가 교착 상태로 표시 되는 경우 DB에 연결 된 응용 프로그램이 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="3e67d-147">추적을 사용 하도록 설정한 경우 추적에 Service Broker 사용 되는지 여부도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="3e67d-148">SignalR 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="3e67d-148">Create a SignalR Application</span></span>

<span data-ttu-id="3e67d-149">다음 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="3e67d-150">SignalR 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="3e67d-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="3e67d-151">SignalR 2.0 및 MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="3e67d-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="3e67d-152">다음으로 SQL Server와의 확장을 지원 하도록 채팅 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="3e67d-153">먼저 SignalR NuGet 패키지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="3e67d-154">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-154">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="3e67d-155">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="3e67d-156">그런 다음 Startup.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="3e67d-157">**Configure** 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="3e67d-158">응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="3e67d-158">Deploy and Run the Application</span></span>

<span data-ttu-id="3e67d-159">Windows Server 인스턴스를 준비 하 여 SignalR 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="3e67d-160">IIS 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-160">Add the IIS role.</span></span> <span data-ttu-id="3e67d-161">WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="3e67d-162">관리 서비스 ("관리 도구" 아래에 나열 됨)도 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="3e67d-163">**웹 배포 3.0을 설치 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3e67d-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="3e67d-164">IIS 관리자를 실행 하는 경우 Microsoft 웹 플랫폼을 설치 하 라는 메시지가 표시 되거나 [설치 관리자를 다운로드할](https://go.microsoft.com/fwlink/?LinkId=255386)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="3e67d-165">플랫폼 설치 관리자에서 웹 배포을 검색 하 고 웹 배포 3.0를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="3e67d-166">웹 관리 서비스가 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="3e67d-167">그렇지 않은 경우 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-167">If not, start the service.</span></span> <span data-ttu-id="3e67d-168">Windows 서비스 목록에 웹 관리 서비스가 표시 되지 않으면 IIS 역할을 추가할 때 관리 서비스를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="3e67d-169">마지막으로 TCP에 대해 8172 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="3e67d-170">웹 배포 도구에서 사용 하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="3e67d-171">이제 개발 컴퓨터의 Visual Studio 프로젝트를 서버에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="3e67d-172">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="3e67d-173">웹 배포에 대 한 자세한 설명서는 [Visual Studio 및 ASP.NET 용 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3e67d-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="3e67d-174">두 개의 서버에 응용 프로그램을 배포 하는 경우 별도의 브라우저 창에서 각 인스턴스를 열 수 있으며 각 인스턴스는 서로 SignalR 메시지를 수신 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="3e67d-175">물론 프로덕션 환경에서는 두 서버가 부하 분산 장치 뒤에 앉아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="3e67d-176">응용 프로그램을 실행 한 후 SignalR에서 데이터베이스에 자동으로 생성 된 테이블을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="3e67d-177">SignalR는 테이블을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-177">SignalR manages the tables.</span></span> <span data-ttu-id="3e67d-178">응용 프로그램이 배포 되는 동안에는 행을 삭제 하거나 테이블을 수정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e67d-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
