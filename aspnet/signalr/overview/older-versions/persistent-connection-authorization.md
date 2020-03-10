---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: SignalR 영구 연결에 대 한 인증 및 권한 부여 (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: 이 항목에서는 영구 연결에 대 한 권한 부여를 적용 하는 방법에 대해 설명 합니다. 보안을 SignalR 응용 프로그램에 통합 하는 방법에 대 한 일반적인 정보는,...
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9ccc59e3ea502daf12ce82382ab30ca73ca0f9b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431189"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>SignalR 영구 연결에 대한 인증 및 권한 부여(SignalR 1.x)

[Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 항목에서는 영구 연결에 대 한 권한 부여를 적용 하는 방법에 대해 설명 합니다. 보안을 SignalR 응용 프로그램에 통합 하는 방법에 대 한 일반적인 내용은 [보안 소개](index.md)를 참조 하세요.

## <a name="enforce-authorization"></a>권한 부여 적용

[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) 를 사용할 때 권한 부여 규칙을 적용 하려면 `AuthorizeRequest` 메서드를 재정의 해야 합니다. 영구 연결에는 `Authorize` 특성을 사용할 수 없습니다. `AuthorizeRequest` 메서드는 요청 된 작업을 수행할 수 있는 권한이 사용자에 게 있는지 확인 하기 위해 모든 요청 이전에 SignalR 프레임 워크에서 호출 됩니다. `AuthorizeRequest` 메서드가 클라이언트에서 호출 되지 않습니다. 대신 응용 프로그램의 표준 인증 메커니즘을 통해 사용자를 인증 합니다.

아래 예제에서는 요청을 인증 된 사용자로 제한 하는 방법을 보여 줍니다.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

AuthorizeRequest 메서드에서 사용자 지정 된 권한 부여 논리를 추가할 수 있습니다. 예를 들어 사용자가 특정 역할에 속하는지 여부를 확인 합니다.
