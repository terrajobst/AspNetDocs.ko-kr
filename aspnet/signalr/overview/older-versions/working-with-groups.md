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
# <a name="working-with-groups-in-signalr-1x"></a>SignalR 1.x에서 그룹 사용

[Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 항목에서는 그룹에 사용자를 추가 하 고 그룹 멤버 자격 정보를 유지 하는 방법에 대해 설명 합니다.

## <a name="overview"></a>개요

SignalR의 그룹은 연결 된 클라이언트의 지정 된 하위 집합에 메시지를 브로드캐스팅하는 메서드를 제공 합니다. 그룹에는 원하는 수의 클라이언트가 있을 수 있으며, 클라이언트는 원하는 수의 그룹의 구성원이 될 수 있습니다. 그룹을 명시적으로 만들 필요는 없습니다. 실제로 그룹에 대 한 호출에서 처음으로 그룹 이름을 지정할 때 그룹이 자동으로 생성 되며,이 그룹의 멤버 자격에서 마지막 연결을 제거 하면 그룹이 삭제 됩니다. 그룹 사용에 대 한 소개는 허브 API-서버 가이드의 [허브 클래스에서 그룹 멤버 자격을 관리 하는 방법](index.md) 을 참조 하세요.

그룹 구성원 목록이 나 그룹 목록을 가져오기 위한 API는 없습니다. SignalR는 pub/sub 모델을 기반으로 클라이언트 및 그룹에 메시지를 보내고 서버는 그룹 또는 그룹 멤버 자격 목록을 유지 하지 않습니다. 이를 통해 웹 팜에 노드를 추가할 때마다 SignalR가 유지 관리 하는 모든 상태를 새 노드에 전파 해야 하므로 확장성을 최대화할 수 있습니다.

`Groups.Add` 메서드를 사용 하 여 그룹에 사용자를 추가 하는 경우 사용자는 현재 연결 기간 동안 해당 그룹으로 전달 된 메시지를 받지만 해당 그룹의 사용자 멤버 자격은 현재 연결을 넘어 지속 되지 않습니다. 그룹 및 그룹 멤버 자격에 대 한 정보를 영구적으로 유지 하려면 해당 데이터를 데이터베이스 또는 Azure table storage와 같은 리포지토리에 저장 해야 합니다. 그런 다음 사용자가 응용 프로그램에 연결할 때마다 사용자가 속한 그룹을 저장소에서 검색 하 고 해당 사용자를 해당 그룹에 수동으로 추가 합니다.

일시적으로 중단 한 후 다시 연결 하는 경우 사용자는 이전에 할당 된 그룹을 자동으로 다시 조인 합니다. 자동으로 다시 가입 하기는 다시 연결 하는 경우에만 적용 되며 새 연결을 설정할 때만 적용 됩니다. 디지털 서명 된 토큰은 이전에 할당 된 그룹 목록을 포함 하는 클라이언트로부터 전달 됩니다. 사용자가 요청 된 그룹에 속해 있는지 확인 하려면 기본 동작을 재정의할 수 있습니다.

이 항목에는 다음 섹션이 포함되어 있습니다.

- [사용자 추가 및 제거](#add)
- [그룹의 멤버 호출](#call)
- [데이터베이스에 그룹 구성원 자격 저장](#storedatabase)
- [Azure 테이블 저장소에 그룹 구성원 자격 저장](#storeazuretable)
- [다시 연결할 때 그룹 구성원 자격 확인](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>사용자 추가 및 제거

그룹에서 사용자를 추가 하거나 제거 하려면 [add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 또는 [remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 메서드를 호출 하 고 사용자의 연결 id와 그룹 이름을 매개 변수로 전달 합니다. 연결이 종료 되 면 그룹에서 사용자를 수동으로 제거할 필요가 없습니다.

다음 예제에서는 허브 메서드에서 사용 되는 `Groups.Add` 및 `Groups.Remove` 메서드를 보여 줍니다.

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

`Groups.Add` 및 `Groups.Remove` 메서드는 비동기적으로 실행 됩니다.

그룹에 클라이언트를 추가 하 고 해당 그룹을 사용 하 여 클라이언트에 즉시 메시지를 전송 하려는 경우에는 Groups 메서드가 먼저 완료 되었는지 확인 해야 합니다. 다음 코드 예제에서는 .NET 4.5에서 작동 하는 코드를 사용 하 고 .NET 4에서 작동 하는 코드를 사용 하 여 작업을 수행 하는 방법을 보여 줍니다.

#### <a name="asynchronous-net-45-example"></a>비동기 .NET 4.5 예제

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a>비동기 .NET 4 예

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

일반적으로는 제거 하려는 연결 id를 더 이상 사용할 수 없기 때문에 `Groups.Remove` 메서드를 호출할 때 `await`을 포함 하면 안 됩니다. 이 경우 요청 시간이 초과 된 후에 `TaskCanceledException`이 throw 됩니다. 응용 프로그램에서 그룹으로 메시지를 보내기 전에 그룹에서 사용자가 제거 되었는지 확인 해야 하는 경우 그룹 앞에 `await`을 추가한 다음 throw 될 수 있는 `TaskCanceledException` 예외를 제거할 수 있습니다.

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>그룹의 멤버 호출

다음 예에 표시 된 것 처럼 그룹의 모든 멤버나 지정 된 멤버만 메시지를 보낼 수 있습니다.

- 지정 된 그룹의 **모든** 연결 된 클라이언트입니다. 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- 지정 된 그룹에서 연결 ID로 식별 된 **지정 된 클라이언트를 제외한**모든 연결 된 클라이언트입니다. 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- **호출 클라이언트를 제외한**지정 된 그룹에 있는 모든 연결 된 클라이언트입니다. 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>데이터베이스에 그룹 구성원 자격 저장

다음 예에서는 데이터베이스에서 그룹 및 사용자 정보를 보존 하는 방법을 보여 줍니다. 모든 데이터 액세스 기술을 사용할 수 있습니다. 그러나 다음 예에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다. 이러한 엔터티 모델은 데이터베이스 테이블 및 필드에 해당 합니다. 데이터 구조는 응용 프로그램의 요구 사항에 따라 크게 다를 수 있습니다. 이 예제에는 사용자가 스포츠 또는 가든과 같은 다양 한 주제에 대 한 대화를 조인할 수 있도록 하는 `ConversationRoom` 라는 클래스가 포함 되어 있습니다. 또한이 예제에는 연결에 대 한 클래스가 포함 되어 있습니다. 연결 클래스는 그룹 멤버 자격을 추적 하는 데 반드시 필요한 것은 아니지만, 종종 추적 사용자를 위한 강력한 솔루션의 일부입니다.

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

그런 다음 허브에서 데이터베이스의 그룹 및 사용자 정보를 검색 하 고 사용자를 적절 한 그룹에 수동으로 추가할 수 있습니다. 예제에는 사용자 연결을 추적 하는 코드가 포함 되어 있지 않습니다. 이 예에서는 메시지를 그룹의 구성원에 게 즉시 보내지 않기 때문에 `Groups.Add` 전에는 `await` 키워드가 적용 되지 않습니다. 새 멤버를 추가한 직후에 그룹의 모든 멤버에 게 메시지를 보내려면 비동기 작업이 완료 되었는지 확인 하기 위해 `await` 키워드를 적용 해야 합니다.

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>Azure 테이블 저장소에 그룹 구성원 자격 저장

Azure table storage를 사용 하 여 그룹 및 사용자 정보를 저장 하는 것은 데이터베이스를 사용 하는 것과 비슷합니다. 다음 예에서는 사용자 이름 및 그룹 이름을 저장 하는 테이블 엔터티를 보여 줍니다.

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

허브에서 사용자가 연결할 때 할당 된 그룹을 검색 합니다.

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>다시 연결할 때 그룹 구성원 자격 확인

기본적으로 SignalR는 연결 시간이 초과 되기 전에 연결이 삭제 되 고 다시 설정 되는 경우와 같이 일시적인 중단 으로부터 다시 연결할 때 사용자를 적절 한 그룹에 자동으로 다시 할당 합니다. 사용자의 그룹 정보는 다시 연결할 때 토큰으로 전달 되 고 해당 토큰은 서버에서 확인 됩니다. 다시 가입 하기 사용자를 그룹에 연결 하는 확인 프로세스에 대 한 자세한 내용은 다시 연결할 [때 다시 가입 하기 그룹](index.md)을 참조 하세요.

일반적으로 다시 연결 시 자동으로 다시 가입 하기 그룹의 기본 동작을 사용 해야 합니다. SignalR 그룹은 중요 한 데이터에 대 한 액세스를 제한 하는 보안 메커니즘으로 사용 되지 않습니다. 그러나 다시 연결할 때 응용 프로그램에서 사용자의 그룹 멤버 자격을 두 번 확인 해야 하는 경우에는 기본 동작을 재정의할 수 있습니다. 사용자가 연결할 때 뿐만 아니라 각 다시 연결에 대해 사용자의 그룹 멤버 자격을 검색 해야 하기 때문에 기본 동작을 변경 하면 데이터베이스에 부담을 추가할 수 있습니다.

다시 연결 시 그룹 구성원 자격을 확인 해야 하는 경우 아래와 같이 할당 된 그룹 목록을 반환 하는 새 허브 파이프라인 모듈을 만듭니다.

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

그런 다음 아래 강조 표시 된 대로 해당 모듈을 허브 파이프라인에 추가 합니다.

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
