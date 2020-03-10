---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: SignalR 확장 with SQL Server (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431129"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a><span data-ttu-id="b8fc5-102">SQL Server로 SignalR 규모 확장(SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="b8fc5-102">SignalR Scaleout with SQL Server (SignalR 1.x)</span></span>

<span data-ttu-id="b8fc5-103">사람, [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="b8fc5-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="b8fc5-104">이 자습서에서는 SQL Server를 사용 하 여 별도의 두 IIS 인스턴스에 배포 된 SignalR 응용 프로그램을 통해 메시지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-104">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="b8fc5-105">단일 테스트 컴퓨터에서이 자습서를 실행할 수도 있지만, 전체 결과를 얻으려면 SignalR 응용 프로그램을 둘 이상의 서버에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-105">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="b8fc5-106">또한 서버 중 하나 또는 별도의 전용 서버에 SQL Server를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-106">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="b8fc5-107">또 다른 옵션은 Azure에서 Vm을 사용 하 여 자습서를 실행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-107">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="b8fc5-108">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="b8fc5-108">Prerequisites</span></span>

<span data-ttu-id="b8fc5-109">2005 이상 Microsoft SQL Server 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-109">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="b8fc5-110">후면판은 SQL Server의 데스크톱 및 서버 버전을 모두 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-110">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="b8fc5-111">SQL Server Compact Edition 또는 Azure SQL Database를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-111">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="b8fc5-112">응용 프로그램이 Azure에서 호스트 되는 경우에는 Service Bus 후면판을 고려 하세요.)</span><span class="sxs-lookup"><span data-stu-id="b8fc5-112">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="b8fc5-113">개요</span><span class="sxs-lookup"><span data-stu-id="b8fc5-113">Overview</span></span>

<span data-ttu-id="b8fc5-114">자세한 자습서를 시작 하기 전에 수행할 작업에 대 한 간략 한 개요를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-114">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="b8fc5-115">비어 있는 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-115">Create a new empty database.</span></span> <span data-ttu-id="b8fc5-116">후면판이이 데이터베이스에 필요한 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-116">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="b8fc5-117">응용 프로그램에 다음 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-117">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="b8fc5-118">SignalR</span><span class="sxs-lookup"><span data-stu-id="b8fc5-118">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="b8fc5-119">SignalR.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-119">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="b8fc5-120">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-120">Create a SignalR application.</span></span>
4. <span data-ttu-id="b8fc5-121">Global.asax에 다음 코드를 추가 하 여 후면판을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-121">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a><span data-ttu-id="b8fc5-122">데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="b8fc5-122">Configure the Database</span></span>

<span data-ttu-id="b8fc5-123">응용 프로그램에서 데이터베이스에 액세스 하는 데 Windows 인증을 사용할지 또는 SQL Server 인증을 사용할지 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-123">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="b8fc5-124">에 관계 없이 데이터베이스 사용자에 게 로그인 하 고, 스키마를 만들고, 테이블을 만들 수 있는 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-124">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="b8fc5-125">후면판에서 사용할 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-125">Create a new database for the backplane to use.</span></span> <span data-ttu-id="b8fc5-126">데이터베이스 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-126">You can give the database any name.</span></span> <span data-ttu-id="b8fc5-127">데이터베이스에 테이블을 만들 필요가 없습니다. 후면판에서 필요한 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-127">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="b8fc5-128">Service Broker 사용</span><span class="sxs-lookup"><span data-stu-id="b8fc5-128">Enable Service Broker</span></span>

<span data-ttu-id="b8fc5-129">후면판 데이터베이스에 대해 Service Broker를 사용 하도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-129">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="b8fc5-130">Service Broker은 SQL Server의 메시징 및 큐에 대 한 기본 지원을 제공 하므로 후면판에서 업데이트를 보다 효율적으로 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-130">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="b8fc5-131">그러나 후면판은 Service Broker 없이도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-131">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="b8fc5-132">Service Broker 사용 하도록 설정 되어 있는지 여부를 확인 하려면를 사용 **하 여** **\_Broker\_사용** 열을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-132">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="b8fc5-133">Service Broker를 사용 하도록 설정 하려면 다음 SQL 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-133">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="b8fc5-134">이 쿼리가 교착 상태로 표시 되는 경우 DB에 연결 된 응용 프로그램이 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-134">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="b8fc5-135">추적을 사용 하도록 설정한 경우 추적에 Service Broker 사용 되는지 여부도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-135">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="b8fc5-136">SignalR 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b8fc5-136">Create a SignalR Application</span></span>

<span data-ttu-id="b8fc5-137">다음 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-137">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="b8fc5-138">SignalR 시작 하기</span><span class="sxs-lookup"><span data-stu-id="b8fc5-138">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="b8fc5-139">SignalR 및 MVC 4 시작</span><span class="sxs-lookup"><span data-stu-id="b8fc5-139">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="b8fc5-140">다음으로 SQL Server와의 확장을 지원 하도록 채팅 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-140">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="b8fc5-141">먼저 SignalR NuGet 패키지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-141">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="b8fc5-142">Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-142">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="b8fc5-143">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-143">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="b8fc5-144">그런 다음, Global.asax 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-144">Next, open the Global.asax file.</span></span> <span data-ttu-id="b8fc5-145">**응용 프로그램\_Start** 메서드에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-145">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="b8fc5-146">응용 프로그램 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="b8fc5-146">Deploy and Run the Application</span></span>

<span data-ttu-id="b8fc5-147">Windows Server 인스턴스를 준비 하 여 SignalR 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-147">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="b8fc5-148">IIS 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-148">Add the IIS role.</span></span> <span data-ttu-id="b8fc5-149">WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-149">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="b8fc5-150">관리 서비스 ("관리 도구" 아래에 나열 됨)도 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-150">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="b8fc5-151">**웹 배포 3.0을 설치 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b8fc5-151">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="b8fc5-152">IIS 관리자를 실행 하는 경우 Microsoft 웹 플랫폼을 설치 하 라는 메시지가 표시 되거나 [설치 관리자를 다운로드할](https://go.microsoft.com/fwlink/?LinkId=255386)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-152">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="b8fc5-153">플랫폼 설치 관리자에서 웹 배포을 검색 하 고 웹 배포 3.0를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-153">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="b8fc5-154">웹 관리 서비스가 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-154">Check that the Web Management Service is running.</span></span> <span data-ttu-id="b8fc5-155">그렇지 않은 경우 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-155">If not, start the service.</span></span> <span data-ttu-id="b8fc5-156">Windows 서비스 목록에 웹 관리 서비스가 표시 되지 않으면 IIS 역할을 추가할 때 관리 서비스를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-156">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="b8fc5-157">마지막으로 TCP에 대해 8172 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-157">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="b8fc5-158">웹 배포 도구에서 사용 하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-158">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="b8fc5-159">이제 개발 컴퓨터의 Visual Studio 프로젝트를 서버에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-159">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="b8fc5-160">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-160">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="b8fc5-161">웹 배포에 대 한 자세한 설명서는 [Visual Studio 및 ASP.NET 용 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-161">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="b8fc5-162">두 개의 서버에 응용 프로그램을 배포 하는 경우 별도의 브라우저 창에서 각 인스턴스를 열 수 있으며 각 인스턴스는 서로 SignalR 메시지를 수신 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-162">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="b8fc5-163">물론 프로덕션 환경에서는 두 서버가 부하 분산 장치 뒤에 앉아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-163">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="b8fc5-164">응용 프로그램을 실행 한 후 SignalR에서 데이터베이스에 자동으로 생성 된 테이블을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-164">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="b8fc5-165">SignalR는 테이블을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-165">SignalR manages the tables.</span></span> <span data-ttu-id="b8fc5-166">응용 프로그램이 배포 되는 동안에는 행을 삭제 하거나 테이블을 수정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8fc5-166">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
