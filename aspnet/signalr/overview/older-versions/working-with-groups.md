---
uid: signalr/overview/older-versions/working-with-groups
title: SignalR 1.x에서 그룹 작업 | Microsoft Docs
author: bradygaster
description: 이 항목에서는 허브 API를 사용 하 여 그룹 멤버 자격 정보를 유지 하는 방법에 대해 설명 합니다.
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 5f50dc162d6cdcfbf2261e6a751f5f99078d5c54
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467897"
---
# <a name="working-with-groups-in-signalr-1x"></a><span data-ttu-id="e5582-103">SignalR 1.x에서 그룹 사용</span><span class="sxs-lookup"><span data-stu-id="e5582-103">Working with Groups in SignalR 1.x</span></span>

<span data-ttu-id="e5582-104">[Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e5582-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="e5582-105">이 항목에서는 그룹에 사용자를 추가 하 고 그룹 멤버 자격 정보를 유지 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-105">This topic describes how to add users to groups and persist group membership information.</span></span>

## <a name="overview"></a><span data-ttu-id="e5582-106">개요</span><span class="sxs-lookup"><span data-stu-id="e5582-106">Overview</span></span>

<span data-ttu-id="e5582-107">SignalR의 그룹은 연결 된 클라이언트의 지정 된 하위 집합에 메시지를 브로드캐스팅하는 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-107">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="e5582-108">그룹에는 원하는 수의 클라이언트가 있을 수 있으며, 클라이언트는 원하는 수의 그룹의 구성원이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-108">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="e5582-109">그룹을 명시적으로 만들 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-109">You don't have to explicitly create groups.</span></span> <span data-ttu-id="e5582-110">실제로 그룹에 대 한 호출에서 처음으로 그룹 이름을 지정할 때 그룹이 자동으로 생성 되며,이 그룹의 멤버 자격에서 마지막 연결을 제거 하면 그룹이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-110">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="e5582-111">그룹 사용에 대 한 소개는 허브 API-서버 가이드의 [허브 클래스에서 그룹 멤버 자격을 관리 하는 방법](index.md) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e5582-111">For an introduction to using groups, see [How to manage group membership from the Hub class](index.md) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="e5582-112">그룹 구성원 목록이 나 그룹 목록을 가져오기 위한 API는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-112">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="e5582-113">SignalR는 pub/sub 모델을 기반으로 클라이언트 및 그룹에 메시지를 보내고 서버는 그룹 또는 그룹 멤버 자격 목록을 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-113">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="e5582-114">이를 통해 웹 팜에 노드를 추가할 때마다 SignalR가 유지 관리 하는 모든 상태를 새 노드에 전파 해야 하므로 확장성을 최대화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-114">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="e5582-115">`Groups.Add` 메서드를 사용 하 여 그룹에 사용자를 추가 하는 경우 사용자는 현재 연결 기간 동안 해당 그룹으로 전달 된 메시지를 받지만 해당 그룹의 사용자 멤버 자격은 현재 연결을 넘어 지속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-115">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="e5582-116">그룹 및 그룹 멤버 자격에 대 한 정보를 영구적으로 유지 하려면 해당 데이터를 데이터베이스 또는 Azure table storage와 같은 리포지토리에 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-116">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="e5582-117">그런 다음 사용자가 응용 프로그램에 연결할 때마다 사용자가 속한 그룹을 저장소에서 검색 하 고 해당 사용자를 해당 그룹에 수동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-117">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="e5582-118">일시적으로 중단 한 후 다시 연결 하는 경우 사용자는 이전에 할당 된 그룹을 자동으로 다시 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-118">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="e5582-119">자동으로 다시 가입 하기는 다시 연결 하는 경우에만 적용 되며 새 연결을 설정할 때만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-119">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="e5582-120">디지털 서명 된 토큰은 이전에 할당 된 그룹 목록을 포함 하는 클라이언트로부터 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-120">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="e5582-121">사용자가 요청 된 그룹에 속해 있는지 확인 하려면 기본 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-121">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="e5582-122">이 항목에는 다음 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-122">This topic includes the following sections:</span></span>

- [<span data-ttu-id="e5582-123">사용자 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="e5582-123">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="e5582-124">그룹의 멤버 호출</span><span class="sxs-lookup"><span data-stu-id="e5582-124">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="e5582-125">데이터베이스에 그룹 구성원 자격 저장</span><span class="sxs-lookup"><span data-stu-id="e5582-125">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="e5582-126">Azure 테이블 저장소에 그룹 구성원 자격 저장</span><span class="sxs-lookup"><span data-stu-id="e5582-126">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="e5582-127">다시 연결할 때 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="e5582-127">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="e5582-128">사용자 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="e5582-128">Adding and removing users</span></span>

<span data-ttu-id="e5582-129">그룹에서 사용자를 추가 하거나 제거 하려면 [add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 또는 [remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 메서드를 호출 하 고 사용자의 연결 id와 그룹 이름을 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-129">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="e5582-130">연결이 종료 되 면 그룹에서 사용자를 수동으로 제거할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-130">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="e5582-131">다음 예제에서는 허브 메서드에서 사용 되는 `Groups.Add` 및 `Groups.Remove` 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-131">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="e5582-132">`Groups.Add` 및 `Groups.Remove` 메서드는 비동기적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-132">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="e5582-133">그룹에 클라이언트를 추가 하 고 해당 그룹을 사용 하 여 클라이언트에 즉시 메시지를 전송 하려는 경우에는 Groups 메서드가 먼저 완료 되었는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-133">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="e5582-134">다음 코드 예제에서는 .NET 4.5에서 작동 하는 코드를 사용 하 고 .NET 4에서 작동 하는 코드를 사용 하 여 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-134">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4.</span></span>

#### <a name="asynchronous-net-45-example"></a><span data-ttu-id="e5582-135">비동기 .NET 4.5 예제</span><span class="sxs-lookup"><span data-stu-id="e5582-135">Asynchronous .NET 4.5 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a><span data-ttu-id="e5582-136">비동기 .NET 4 예</span><span class="sxs-lookup"><span data-stu-id="e5582-136">Asynchronous .NET 4 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

<span data-ttu-id="e5582-137">일반적으로는 제거 하려는 연결 id를 더 이상 사용할 수 없기 때문에 `Groups.Remove` 메서드를 호출할 때 `await`을 포함 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-137">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="e5582-138">이 경우 요청 시간이 초과 된 후에 `TaskCanceledException`이 throw 됩니다. 응용 프로그램에서 그룹으로 메시지를 보내기 전에 그룹에서 사용자가 제거 되었는지 확인 해야 하는 경우 그룹 앞에 `await`을 추가한 다음 throw 될 수 있는 `TaskCanceledException` 예외를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-138">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before Groups.Remove, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="e5582-139">그룹의 멤버 호출</span><span class="sxs-lookup"><span data-stu-id="e5582-139">Calling members of a group</span></span>

<span data-ttu-id="e5582-140">다음 예에 표시 된 것 처럼 그룹의 모든 멤버나 지정 된 멤버만 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-140">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="e5582-141">지정 된 그룹의 **모든** 연결 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-141">**All** connected clients in a specified group.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- <span data-ttu-id="e5582-142">지정 된 그룹에서 연결 ID로 식별 된 **지정 된 클라이언트를 제외한**모든 연결 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-142">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span> 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- <span data-ttu-id="e5582-143">**호출 클라이언트를 제외한**지정 된 그룹에 있는 모든 연결 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-143">All connected clients in a specified group **except the calling client**.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="e5582-144">데이터베이스에 그룹 구성원 자격 저장</span><span class="sxs-lookup"><span data-stu-id="e5582-144">Storing group membership in a database</span></span>

<span data-ttu-id="e5582-145">다음 예에서는 데이터베이스에서 그룹 및 사용자 정보를 보존 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-145">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="e5582-146">모든 데이터 액세스 기술을 사용할 수 있습니다. 그러나 다음 예에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-146">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="e5582-147">이러한 엔터티 모델은 데이터베이스 테이블 및 필드에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-147">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="e5582-148">데이터 구조는 응용 프로그램의 요구 사항에 따라 크게 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-148">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="e5582-149">이 예제에는 사용자가 스포츠 또는 가든과 같은 다양 한 주제에 대 한 대화를 조인할 수 있도록 하는 `ConversationRoom` 라는 클래스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-149">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="e5582-150">또한이 예제에는 연결에 대 한 클래스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-150">This example also includes a class for the connections.</span></span> <span data-ttu-id="e5582-151">연결 클래스는 그룹 멤버 자격을 추적 하는 데 반드시 필요한 것은 아니지만, 종종 추적 사용자를 위한 강력한 솔루션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-151">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<span data-ttu-id="e5582-152">그런 다음 허브에서 데이터베이스의 그룹 및 사용자 정보를 검색 하 고 사용자를 적절 한 그룹에 수동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-152">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="e5582-153">예제에는 사용자 연결을 추적 하는 코드가 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-153">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="e5582-154">이 예에서는 메시지를 그룹의 구성원에 게 즉시 보내지 않기 때문에 `Groups.Add` 전에는 `await` 키워드가 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-154">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="e5582-155">새 멤버를 추가한 직후에 그룹의 모든 멤버에 게 메시지를 보내려면 비동기 작업이 완료 되었는지 확인 하기 위해 `await` 키워드를 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-155">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="e5582-156">Azure 테이블 저장소에 그룹 구성원 자격 저장</span><span class="sxs-lookup"><span data-stu-id="e5582-156">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="e5582-157">Azure table storage를 사용 하 여 그룹 및 사용자 정보를 저장 하는 것은 데이터베이스를 사용 하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-157">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="e5582-158">다음 예에서는 사용자 이름 및 그룹 이름을 저장 하는 테이블 엔터티를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-158">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<span data-ttu-id="e5582-159">허브에서 사용자가 연결할 때 할당 된 그룹을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-159">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="e5582-160">다시 연결할 때 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="e5582-160">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="e5582-161">기본적으로 SignalR는 연결 시간이 초과 되기 전에 연결이 삭제 되 고 다시 설정 되는 경우와 같이 일시적인 중단 으로부터 다시 연결할 때 사용자를 적절 한 그룹에 자동으로 다시 할당 합니다. 사용자의 그룹 정보는 다시 연결할 때 토큰으로 전달 되 고 해당 토큰은 서버에서 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-161">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="e5582-162">다시 가입 하기 사용자를 그룹에 연결 하는 확인 프로세스에 대 한 자세한 내용은 다시 연결할 [때 다시 가입 하기 그룹](index.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e5582-162">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](index.md).</span></span>

<span data-ttu-id="e5582-163">일반적으로 다시 연결 시 자동으로 다시 가입 하기 그룹의 기본 동작을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-163">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="e5582-164">SignalR 그룹은 중요 한 데이터에 대 한 액세스를 제한 하는 보안 메커니즘으로 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-164">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="e5582-165">그러나 다시 연결할 때 응용 프로그램에서 사용자의 그룹 멤버 자격을 두 번 확인 해야 하는 경우에는 기본 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-165">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="e5582-166">사용자가 연결할 때 뿐만 아니라 각 다시 연결에 대해 사용자의 그룹 멤버 자격을 검색 해야 하기 때문에 기본 동작을 변경 하면 데이터베이스에 부담을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-166">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="e5582-167">다시 연결 시 그룹 구성원 자격을 확인 해야 하는 경우 아래와 같이 할당 된 그룹 목록을 반환 하는 새 허브 파이프라인 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-167">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

<span data-ttu-id="e5582-168">그런 다음 아래 강조 표시 된 대로 해당 모듈을 허브 파이프라인에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5582-168">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
