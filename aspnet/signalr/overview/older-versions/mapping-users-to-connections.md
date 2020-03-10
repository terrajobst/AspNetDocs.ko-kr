---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: SignalR 사용자를 SignalR 1. x의 연결에 매핑 | Microsoft Docs
author: bradygaster
description: 이 항목에서는 사용자와 해당 연결에 대 한 정보를 유지 하는 방법을 보여 줍니다.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 9d948495e9b8821fcb465611b6926603c3756a19
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449999"
---
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a><span data-ttu-id="a5a9d-103">SignalR 1.x에서 SignalR 사용자를 연결에 매핑</span><span class="sxs-lookup"><span data-stu-id="a5a9d-103">Mapping SignalR Users to Connections in SignalR 1.x</span></span>

<span data-ttu-id="a5a9d-104">[Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a5a9d-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="a5a9d-105">이 항목에서는 사용자와 해당 연결에 대 한 정보를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-105">This topic shows how to retain information about users and their connections.</span></span>

## <a name="introduction"></a><span data-ttu-id="a5a9d-106">소개</span><span class="sxs-lookup"><span data-stu-id="a5a9d-106">Introduction</span></span>

<span data-ttu-id="a5a9d-107">허브에 연결 하는 각 클라이언트는 고유한 연결 id를 전달 합니다. 허브 컨텍스트의 `Context.ConnectionId` 속성에서이 값을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-107">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="a5a9d-108">응용 프로그램에서 사용자를 연결 id에 매핑하고 해당 매핑을 유지 해야 하는 경우 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-108">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- <span data-ttu-id="a5a9d-109">사전 같은 [메모리 내 저장소](#inmemory)</span><span class="sxs-lookup"><span data-stu-id="a5a9d-109">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="a5a9d-110">각 사용자에 대 한 SignalR 그룹</span><span class="sxs-lookup"><span data-stu-id="a5a9d-110">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="a5a9d-111">데이터베이스 테이블 또는 Azure table storage와 같은 [영구 외부 저장소](#database)</span><span class="sxs-lookup"><span data-stu-id="a5a9d-111">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="a5a9d-112">이러한 각 구현은이 항목에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-112">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="a5a9d-113">`Hub` 클래스의 `OnConnected`, `OnDisconnected`및 `OnReconnected` 메서드를 사용 하 여 사용자 연결 상태를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-113">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="a5a9d-114">응용 프로그램에 대 한 가장 좋은 방법은 다음에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-114">The best approach for your application depends on:</span></span>

- <span data-ttu-id="a5a9d-115">응용 프로그램을 호스팅하는 웹 서버의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-115">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="a5a9d-116">현재 연결 된 사용자의 목록을 가져와야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-116">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="a5a9d-117">응용 프로그램 또는 서버를 다시 시작할 때 그룹 및 사용자 정보를 유지 해야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-117">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="a5a9d-118">외부 서버 호출의 대기 시간이 문제 인지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-118">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="a5a9d-119">다음 표에서는 이러한 고려 사항에 대해 작동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-119">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="a5a9d-120">둘 이상의 서버</span><span class="sxs-lookup"><span data-stu-id="a5a9d-120">More than one server</span></span> | <span data-ttu-id="a5a9d-121">현재 연결 된 사용자 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="a5a9d-121">Get list of currently connected users</span></span> | <span data-ttu-id="a5a9d-122">다시 시작한 후 정보 유지</span><span class="sxs-lookup"><span data-stu-id="a5a9d-122">Persist information after restarts</span></span> | <span data-ttu-id="a5a9d-123">최적의 성능</span><span class="sxs-lookup"><span data-stu-id="a5a9d-123">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="a5a9d-124">메모리 내</span><span class="sxs-lookup"><span data-stu-id="a5a9d-124">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="a5a9d-125">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="a5a9d-125">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="a5a9d-126">영구, 외부</span><span class="sxs-lookup"><span data-stu-id="a5a9d-126">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="a5a9d-127">메모리 내 저장소</span><span class="sxs-lookup"><span data-stu-id="a5a9d-127">In-memory storage</span></span>

<span data-ttu-id="a5a9d-128">다음 예에서는 메모리에 저장 된 사전에 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-128">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="a5a9d-129">사전은 `HashSet`를 사용 하 여 연결 id를 저장 합니다. 사용자는 언제 든 지 SignalR 응용 프로그램에 대 한 연결을 둘 이상 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-129">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="a5a9d-130">예를 들어 여러 장치 또는 둘 이상의 브라우저 탭을 통해 연결 된 사용자에 게는 둘 이상의 연결 id가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-130">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="a5a9d-131">응용 프로그램이 종료 되 면 모든 정보가 손실 되지만 사용자가 연결을 다시 설정 하면 다시 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-131">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="a5a9d-132">각 서버에 별도의 연결 컬렉션이 있기 때문에 환경에 둘 이상의 웹 서버가 포함 된 경우에는 메모리 내 저장소가 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-132">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="a5a9d-133">첫 번째 예제에서는 연결에 대 한 사용자 매핑을 관리 하는 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-133">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="a5a9d-134">HashSet의 키는 사용자의 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-134">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="a5a9d-135">다음 예제에서는 허브에서 연결 매핑 클래스를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-135">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="a5a9d-136">클래스의 인스턴스는 `_connections`변수 이름에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-136">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="a5a9d-137">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="a5a9d-137">Single-user groups</span></span>

<span data-ttu-id="a5a9d-138">각 사용자에 대 한 그룹을 만든 다음 해당 사용자 에게만 도달 하려는 경우 해당 그룹에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-138">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="a5a9d-139">각 그룹의 이름은 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-139">The name of each group is the name of the user.</span></span> <span data-ttu-id="a5a9d-140">사용자가 두 개 이상의 연결을 사용 하는 경우 각 연결 id는 사용자 그룹에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-140">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="a5a9d-141">사용자가 연결을 끊을 때 그룹에서 사용자를 수동으로 제거 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-141">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="a5a9d-142">이 작업은 SignalR 프레임 워크에서 자동으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-142">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="a5a9d-143">다음 예제에서는 단일 사용자 그룹을 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-143">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="a5a9d-144">영구, 외부 저장소</span><span class="sxs-lookup"><span data-stu-id="a5a9d-144">Permanent, external storage</span></span>

<span data-ttu-id="a5a9d-145">이 항목에서는 데이터베이스 또는 Azure table storage를 사용 하 여 연결 정보를 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-145">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="a5a9d-146">이 방법은 각 웹 서버가 동일한 데이터 저장소와 상호 작용할 수 있기 때문에 여러 웹 서버를 사용 하는 경우 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-146">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="a5a9d-147">웹 서버의 작동이 중지 되거나 응용 프로그램이 다시 시작 되 면 `OnDisconnected` 메서드가 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-147">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="a5a9d-148">따라서 데이터 리포지토리에 더 이상 유효 하지 않은 연결 id 레코드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-148">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="a5a9d-149">이러한 분리 된 레코드를 정리 하려면 응용 프로그램과 관련 된 시간 범위 밖에 서 만들어진 모든 연결을 무효화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-149">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="a5a9d-150">이 섹션의 예에는 연결을 만들 때 추적 하는 값이 포함 되어 있지만이를 백그라운드 프로세스로 수행 하려는 경우에는 오래 된 레코드를 정리 하는 방법은 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-150">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="a5a9d-151">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="a5a9d-151">Database</span></span>

<span data-ttu-id="a5a9d-152">다음 예에서는 데이터베이스에서 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-152">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="a5a9d-153">모든 데이터 액세스 기술을 사용할 수 있습니다. 그러나 다음 예에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="a5a9d-154">이러한 엔터티 모델은 데이터베이스 테이블 및 필드에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="a5a9d-155">데이터 구조는 응용 프로그램의 요구 사항에 따라 크게 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-155">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="a5a9d-156">첫 번째 예제에서는 많은 연결 엔터티와 연결 될 수 있는 사용자 엔터티를 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-156">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="a5a9d-157">그런 다음 허브에서 아래와 같은 코드를 사용 하 여 각 연결의 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-157">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a><span data-ttu-id="a5a9d-158">Azure 테이블 스토리지</span><span class="sxs-lookup"><span data-stu-id="a5a9d-158">Azure table storage</span></span>

<span data-ttu-id="a5a9d-159">다음 Azure table storage 예는 데이터베이스 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-159">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="a5a9d-160">Azure Table Storage 서비스를 시작 하는 데 필요한 일부 정보는 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-160">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="a5a9d-161">자세한 내용은 [.net에서 테이블 저장소를 사용 하는 방법을](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-161">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="a5a9d-162">다음 예에서는 연결 정보를 저장 하기 위한 테이블 엔터티를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-162">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="a5a9d-163">사용자 이름으로 데이터를 분할 하 고 각 엔터티를 연결 id로 식별 하므로 사용자는 언제 든 지 여러 연결을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-163">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<span data-ttu-id="a5a9d-164">허브에서 각 사용자의 연결 상태를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9d-164">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
