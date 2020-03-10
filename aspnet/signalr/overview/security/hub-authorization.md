---
uid: signalr/overview/security/hub-authorization
title: SignalR Hub에 대 한 인증 및 권한 부여 | Microsoft Docs
author: bradygaster
description: 이 항목에서는 허브 메서드에 액세스할 수 있는 사용자 또는 역할을 제한 하는 방법에 대해 설명 합니다. 이 항목에서 사용 되는 소프트웨어 버전 Visual Studio 2013 .NET 4.5 SignalR ve ...
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 5006af5e623da6958a6d59949c6f2cf776c77fc3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467513"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a>SignalR 허브에 대한 인증 및 권한 부여

[Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 항목에서는 허브 메서드에 액세스할 수 있는 사용자 또는 역할을 제한 하는 방법에 대해 설명 합니다.
>
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 버전 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
>
> 이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.
>
> ## <a name="questions-and-comments"></a>질문 및 설명
>
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.

## <a name="overview"></a>개요

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

- [권한 부여 특성](#authorizeattribute)
- [모든 허브에 대 한 인증 필요](#requireauth)
- [사용자 지정 된 권한 부여](#custom)
- [클라이언트에 인증 정보 전달](#passauth)
- [.NET 클라이언트에 대 한 인증 옵션](#authoptions)

    - [폼 인증을 사용 하는 쿠키](#cookie)
    - [Windows 인증](#windows)
    - [연결 헤더](#header)
    - [MSSQLSERVER에 대한 프로토콜 속성](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>권한 부여 특성

SignalR는 허브 또는 메서드에 대 한 액세스 권한이 있는 사용자 또는 역할을 지정 하는 [권한 부여](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 특성을 제공 합니다. 이 특성은 `Microsoft.AspNet.SignalR` 네임 스페이스에 있습니다. 허브 또는 허브의 특정 메서드에 `Authorize` 특성을 적용 합니다. `Authorize` 특성을 허브 클래스에 적용 하면 지정 된 권한 부여 요구 사항이 허브의 모든 메서드에 적용 됩니다. 이 항목에서는 적용할 수 있는 다양 한 유형의 권한 부여 요구 사항에 대 한 예를 제공 합니다. `Authorize` 특성이 없으면 연결 된 클라이언트가 허브의 모든 공용 메서드에 액세스할 수 있습니다.

웹 응용 프로그램에서 "Admin" 이라는 역할을 정의한 경우 해당 역할의 사용자만 다음 코드를 사용 하 여 허브에 액세스할 수 있도록 지정할 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

또는 아래와 같이 허브에 모든 사용자가 사용할 수 있는 하나의 메서드와 인증 된 사용자만 사용할 수 있는 두 번째 메서드를 포함 하도록 지정할 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

다음 예에서는 다양 한 권한 부여 시나리오를 처리 합니다.

- `[Authorize]` – 인증 된 사용자만
- `[Authorize(Roles = "Admin,Manager")]` – 지정 된 역할의 인증 된 사용자만
- `[Authorize(Users = "user1,user2")]` – 지정 된 사용자 이름의 인증 된 사용자만
- `[Authorize(RequireOutgoing=false)]` – 인증 된 사용자만 허브를 호출할 수 있지만, 서버에서 클라이언트로의 호출은 특정 사용자만 메시지를 보낼 수 있지만 다른 모든 사용자는 메시지를 받을 수 있는 경우와 같은 권한 부여로 제한 되지 않습니다. RequireOutgoing 속성은 허브 내의 개별 메서드가 아니라 전체 허브에만 적용할 수 있습니다. RequireOutgoing가 false로 설정 되지 않은 경우 권한 부여 요구 사항을 충족 하는 사용자만 서버에서 호출 됩니다.

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>모든 허브에 대 한 인증 필요

응용 프로그램을 시작할 때 [Requireauthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) 메서드를 호출 하 여 응용 프로그램의 모든 허브 및 허브 메서드에 대 한 인증을 요구할 수 있습니다. 여러 허브가 있고 모든 허브에 대 한 인증 요구 사항을 적용 하려는 경우이 방법을 사용할 수 있습니다. 이 방법을 사용 하면 역할, 사용자 또는 나가는 권한 부여에 대 한 요구 사항을 지정할 수 없습니다. 허브 메서드에 대 한 액세스는 인증 된 사용자로만 제한 되도록 지정할 수 있습니다. 그러나 허브 또는 메서드에 권한 부여 특성을 적용 하 여 추가 요구 사항을 지정할 수 있습니다. 특성에 지정 하는 모든 요구 사항은 인증의 기본 요구 사항에 추가 됩니다.

다음 예에서는 모든 허브 메서드를 인증 된 사용자로 제한 하는 시작 파일을 보여 줍니다.

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

SignalR 요청이 처리 된 후에 `RequireAuthentication()` 메서드를 호출 하면 SignalR에서 `InvalidOperationException` 예외를 throw 합니다. SignalR는 파이프라인이 호출 된 후에 모듈을 HubPipeline에 추가할 수 없기 때문에이 예외를 throw 합니다. 앞의 예제에서는 첫 번째 요청을 처리 하기 전에 한 번 실행 되는 `Configuration` 메서드에서 `RequireAuthentication` 메서드를 호출 하는 방법을 보여 줍니다.

<a id="custom"></a>

## <a name="customized-authorization"></a>사용자 지정 된 권한 부여

권한 부여가 결정 되는 방법을 사용자 지정 해야 하는 경우 `AuthorizeAttribute`에서 파생 되는 클래스를 만들고 [userauthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) 메서드를 재정의할 수 있습니다. 각 요청에 대해 SignalR는이 메서드를 호출 하 여 사용자에 게 요청을 완료할 수 있는 권한이 있는지 여부를 확인 합니다. 재정의 된 메서드에서 권한 부여 시나리오에 필요한 논리를 제공 합니다. 다음 예제에서는 클레임 기반 id를 통해 권한 부여를 적용 하는 방법을 보여 줍니다.

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>클라이언트에 인증 정보 전달

클라이언트에서 실행 되는 코드에서 인증 정보를 사용 해야 할 수도 있습니다. 클라이언트에서 메서드를 호출할 때 필요한 정보를 전달 합니다. 예를 들어 채팅 응용 프로그램 메서드는 아래와 같이 메시지를 게시 하는 사람의 사용자 이름을 매개 변수로 전달할 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

또는 아래와 같이 인증 정보를 표시 하 고 해당 개체를 매개 변수로 전달 하는 개체를 만들 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

악의적인 사용자가 해당 클라이언트의 요청을 모방 하는 데 사용할 수 있으므로 한 클라이언트의 연결 id를 다른 클라이언트에 전달 하면 안 됩니다.

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>.NET 클라이언트에 대 한 인증 옵션

인증 된 사용자로 제한 되는 허브와 상호 작용 하는 콘솔 앱과 같은 .NET 클라이언트가 있는 경우 쿠키, 연결 헤더 또는 인증서에서 인증 자격 증명을 전달할 수 있습니다. 이 섹션의 예에서는 사용자를 인증 하는 다른 방법을 사용 하는 방법을 보여 줍니다. 완전 한 기능을 갖춘 SignalR 앱은 아닙니다. SignalR를 사용 하는 .NET 클라이언트에 대 한 자세한 내용은 [허브 API 가이드-.Net 클라이언트](../guide-to-the-api/hubs-api-guide-net-client.md)를 참조 하세요.

<a id="cookie"></a>

### <a name="cookie"></a>쿠키

.NET 클라이언트가 ASP.NET Forms 인증을 사용 하는 허브와 상호 작용 하는 경우 연결에서 인증 쿠키를 수동으로 설정 해야 합니다. [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) 개체의 `CookieContainer` 속성에 쿠키를 추가 합니다. 다음 예제에서는 웹 페이지에서 인증 쿠키를 검색 하 고 해당 쿠키를 연결에 추가 하는 콘솔 앱을 보여 줍니다.

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

콘솔 앱은 다음 코드 숨김이 포함 된 빈 페이지를 참조할 수 있는 <strong>www.contoso.com/RemoteLogin</strong> 에 자격 증명을 게시 합니다.

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Windows 인증

Windows 인증을 사용 하는 경우 [defaultcredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) 속성을 사용 하 여 현재 사용자의 자격 증명을 전달할 수 있습니다. 연결에 대 한 자격 증명을 DefaultCredentials의 값으로 설정 합니다.

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>연결 헤더

응용 프로그램에서 쿠키를 사용 하지 않는 경우 연결 헤더에 사용자 정보를 전달할 수 있습니다. 예를 들어 연결 헤더에 토큰을 전달할 수 있습니다.

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

그런 다음 허브에서 사용자의 토큰을 확인 합니다.

<a id="certificate"></a>

### <a name="certificate"></a>인증서

클라이언트 인증서를 전달 하 여 사용자를 확인할 수 있습니다. 연결을 만들 때 인증서를 추가 합니다. 다음 예제에서는 연결에 클라이언트 인증서를 추가 하는 방법만 보여 줍니다. 전체 콘솔 앱은 표시 되지 않습니다. 이 클래스는 인증서를 만드는 여러 가지 방법을 제공 하는 [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) 클래스를 사용 합니다.

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
