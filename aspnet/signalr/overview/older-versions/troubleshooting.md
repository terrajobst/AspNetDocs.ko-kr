---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR 문제 해결 (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: 이 문서에서는 SignalR 응용 프로그램 개발과 관련 된 일반적인 문제를 설명 합니다.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468101"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>SignalR 문제 해결(SignalR 1.x)

[Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 SignalR 관련 된 일반적인 문제 해결에 대해 설명 합니다.

이 문서에는 다음과 같은 섹션이 포함 되어 있습니다.

- [클라이언트와 서버 간에 메서드를 자동으로 호출 하지 못합니다.](#connection)
- [기타 연결 문제](#other)
- [컴파일 및 서버 쪽 오류](#server)
- [Visual Studio 문제](#vs)
- [인터넷 정보 서비스 문제](#iis)
- [Azure 문제](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>클라이언트와 서버 간에 메서드를 자동으로 호출 하지 못합니다.

이 섹션에서는 클라이언트와 서버 간의 메서드 호출이 의미 있는 오류 메시지 없이 실패할 수 있는 원인을 설명 합니다. SignalR 응용 프로그램에서 서버는 클라이언트가 구현 하는 메서드에 대 한 정보를 포함 하지 않습니다. 서버에서 클라이언트 메서드를 호출 하면 메서드 이름 및 매개 변수 데이터가 클라이언트에 전송 되 고 메서드가 지정 된 형식으로 존재 하는 경우에만 메서드가 실행 됩니다. 클라이언트에서 일치 하는 메서드가 없는 경우 아무 일도 발생 하지 않으며 서버에서 오류 메시지가 발생 하지 않습니다.

호출 되지 않는 클라이언트 메서드를 추가로 조사 하기 위해 허브에서 시작 메서드를 호출 하기 전에 로깅을 설정 하 여 서버에서 들어오는 호출을 확인할 수 있습니다. JavaScript 응용 프로그램에서 로깅을 사용 하도록 설정 하려면 [클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법 (javascript 클라이언트 버전)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)을 참조 하세요. .NET 클라이언트 응용 프로그램에서 로깅을 사용 하도록 설정 하려면 [클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법 (.Net 클라이언트 버전)](../guide-to-the-api/hubs-api-guide-net-client.md#logging)을 참조 하세요.

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>철자가 잘못 된 메서드, 잘못 된 메서드 서명 또는 잘못 된 허브 이름

호출 된 메서드의 이름 또는 시그니처가 클라이언트의 적절 한 메서드와 정확 하 게 일치 하지 않으면 호출이 실패 합니다. 서버에 의해 호출 된 메서드 이름이 클라이언트의 메서드 이름과 일치 하는지 확인 합니다. 또한 SignalR는 JavaScript에서와 같이 카멜식 대/소문자를 사용 하는 메서드를 사용 하 여 허브 프록시를 만들기 때문에 서버에서 `SendMessage` 호출 된 메서드를 클라이언트 프록시에서 `sendMessage` 이라고 합니다. 서버 쪽 코드에서 `HubName` 특성을 사용 하는 경우 사용 된 이름이 클라이언트에서 허브를 만드는 데 사용 된 이름과 일치 하는지 확인 합니다. `HubName` 특성을 사용 하지 않는 경우 JavaScript 클라이언트의 허브 이름이 ChatHub 대신 chatHub와 같은 카멜식 대/소문자를 사용 하는지 확인 합니다.

### <a name="duplicate-method-name-on-client"></a>클라이언트에서 중복 된 메서드 이름

클라이언트에서 대/소문자만 다른 중복 메서드가 없는지 확인 합니다. 클라이언트 응용 프로그램에 `sendMessage`이라는 메서드가 있는 경우에는 `SendMessage` 메서드도 없다는 것을 확인 합니다.

### <a name="missing-json-parser-on-the-client"></a>클라이언트에 JSON 파서가 없습니다.

SignalR에는 서버와 클라이언트 간의 호출을 serialize 하기 위해 JSON 파서가 있어야 합니다. 클라이언트에 기본 제공 JSON 파서 (예: Internet Explorer 7)가 없는 경우 응용 프로그램에 하나를 포함 해야 합니다. JSON 파서는 [여기](http://nuget.org/packages/json2)에서 다운로드할 수 있습니다.

### <a name="mixing-hub-and-persistentconnection-syntax"></a>Hub 및 PersistentConnection 구문 혼합

SignalR는 허브와 PersistentConnections의 두 가지 통신 모델을 사용 합니다. 이러한 두 통신 모델을 호출 하는 구문은 클라이언트 코드에서 다릅니다. 서버 코드에 허브를 추가한 경우 모든 클라이언트 코드에서 적절 한 허브 구문을 사용 하는지 확인 합니다.

**JavaScript 클라이언트에 PersistentConnection를 만드는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**Javascript 클라이언트에서 허브 프록시를 만드는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**C#PersistentConnection에 경로를 매핑하는 서버 코드**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**C#여러 응용 프로그램이 있는 경우 허브 또는 여러 허브에 경로를 매핑하는 서버 코드**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>구독을 추가 하기 전에 연결을 시작 했습니다.

서버에서 호출할 수 있는 메서드가 프록시에 추가 되기 전에 허브의 연결이 시작 되 면 메시지가 수신 되지 않습니다. 다음 JavaScript 코드는 허브를 제대로 시작 하지 않습니다.

**허브 메시지를 수신 하지 못하게 하는 잘못 된 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

대신 Start를 호출 하기 전에 메서드 구독을 추가 합니다.

**허브에 구독을 올바르게 추가 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>허브 프록시에 메서드 이름이 없습니다.

서버에 정의 된 메서드가 클라이언트에서 구독 되는지 확인 합니다. 서버에서 메서드를 정의 하는 경우에도 여전히 클라이언트 프록시에 추가 해야 합니다. 메서드는 다음과 같은 방법으로 클라이언트 프록시에 추가할 수 있습니다. 메서드는 허브가 아닌 허브의 `client` 멤버에 추가 됩니다.

**허브 프록시에 메서드를 추가 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>허브 또는 허브 메서드가 Public으로 선언 되지 않았습니다.

클라이언트에서 볼 수 있도록 허브 구현 및 메서드를 `public`으로 선언 해야 합니다.

### <a name="accessing-hub-from-a-different-application"></a>다른 응용 프로그램에서 허브 액세스

SignalR 허브는 SignalR 클라이언트를 구현 하는 응용 프로그램을 통해서만 액세스할 수 있습니다. SignalR는 다른 통신 라이브러리 (예: SOAP 또는 WCF 웹 서비스)와 상호 운용할 수 없습니다. 대상 플랫폼에 사용할 수 있는 SignalR 클라이언트가 없는 경우 서버 끝점에 직접 액세스할 수 없습니다.

### <a name="manually-serializing-data"></a>수동으로 데이터 직렬화

SignalR는 자동으로 JSON을 사용 하 여 메서드 매개 변수를 직렬화 합니다 .이 작업은 직접 수행할 필요가 없습니다.

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>원격 허브 메서드가 OnDisconnected 함수의 클라이언트에서 실행 되지 않음

이 동작은 의도된 것입니다. `OnDisconnected`를 호출 하면 허브는 추가 허브 메서드 호출을 허용 하지 않는 `Disconnected` 상태를 이미 입력 한 것입니다.

**C#OnDisconnected 이벤트에서 코드를 올바르게 실행 하는 서버 코드**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>연결 제한에 도달 함

Windows 7과 같은 클라이언트 운영 체제에서 전체 버전의 IIS를 사용 하는 경우 10 개의 연결 제한이 적용 됩니다. 클라이언트 OS를 사용 하는 경우이 제한을 방지 하기 위해 IIS Express를 대신 사용 합니다.

### <a name="cross-domain-connection-not-set-up-properly"></a>도메인 간 연결이 제대로 설정 되지 않았습니다.

도메인 간 연결 (SignalR URL이 호스팅 페이지와 동일한 도메인에 있지 않은 연결)이 올바르게 설정 되지 않은 경우 오류 메시지 없이 연결이 실패할 수 있습니다. 도메인 간 통신을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [도메인 간 연결을 설정](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)하는 방법을 참조 하세요.

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>NTLM을 사용 하는 연결 (Active Directory)이 .NET 클라이언트에서 작동 하지 않음

연결이 제대로 구성 되지 않은 경우 도메인 보안을 사용 하는 .NET 클라이언트 응용 프로그램의 연결이 실패할 수 있습니다. 도메인 환경에서 SignalR를 사용 하려면 다음과 같이 필수 연결 속성을 설정 합니다.

**C#연결 자격 증명을 구현 하는 클라이언트 코드**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>기타 연결 문제

이 섹션에서는 연결 중에 발생 하는 특정 증상 또는 오류 메시지에 대 한 원인과 해결 방법을 설명 합니다.

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>"데이터를 전송 하려면 먼저 Start를 호출 해야 합니다." 오류

이 오류는 코드에서 연결을 시작 하기 전에 SignalR 개체를 참조 하는 경우에 일반적으로 나타납니다. 서버에 정의 된 메서드를 호출 하는 처리기 및 이와 같은 wireup는 연결이 완료 된 후에 추가 되어야 합니다. `Start`에 대 한 호출은 비동기 이므로 호출 후의 코드가 완료 되기 전에 실행 될 수 있습니다. 연결을 완전히 시작한 후 처리기를 추가 하는 가장 좋은 방법은 시작 메서드에 매개 변수로 전달 되는 콜백 함수에 추가 하는 것입니다.

**SignalR 개체를 참조 하는 이벤트 처리기를 올바르게 추가 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

SignalR 개체가 여전히 참조 되는 동안 연결이 중지 되는 경우에도이 오류가 표시 됩니다.

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>"301을 영구적으로 이동" 또는 "302" 일시적으로 이동 "오류

이 오류는 프로젝트가 자동으로 생성 된 프록시를 방해 하는 SignalR 라는 폴더를 포함 하는 경우에 나타날 수 있습니다. 이 오류를 방지 하려면 응용 프로그램에서 `SignalR` 라는 폴더를 사용 하지 않거나 자동 프록시 생성을 해제 합니다. 자세한 내용은 [생성 된 프록시 및 수행 하는 작업](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) 을 참조 하세요.

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>.NET 또는 Silverlight 클라이언트에서 "403 사용할 수 없음" 오류 발생

도메인 간 통신이 제대로 사용 하도록 설정 되지 않은 도메인 간 환경에서이 오류가 발생할 수 있습니다. 도메인 간 통신을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [도메인 간 연결을 설정](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)하는 방법을 참조 하세요. Silverlight 클라이언트에서 도메인 간 연결을 설정 하려면 [silverlight 클라이언트에서 도메인 간](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)연결을 참조 하세요.

### <a name="404-not-found-error"></a>"404를 찾을 수 없음" 오류

이 문제에 대 한 여러 원인이 있습니다. 다음을 모두 확인 합니다.

- **허브 프록시 주소 참조의 형식이 잘못 되었습니다.** 이 오류는 생성 된 허브 프록시 주소에 대 한 참조의 형식이 잘못 된 경우에 일반적으로 나타납니다. 허브 주소에 대 한 참조가 올바르게 설정 되었는지 확인 합니다. 자세한 내용은 [동적으로 생성 된 프록시를 참조 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) 참조 하세요.
- **허브 경로를 추가 하기 전에 응용 프로그램에 경로를 추가 합니다.** 응용 프로그램에서 다른 경로를 사용 하는 경우 추가 된 첫 번째 경로가 `MapHubs`에 대 한 호출 인지 확인 합니다.

### <a name="500-internal-server-error"></a>"500 내부 서버 오류"

이는 매우 일반적인 오류 이며 다양 한 원인이 있을 수 있습니다. 오류의 세부 정보는 서버의 이벤트 로그에 표시 되거나 서버 디버깅을 통해 찾을 수 있습니다. 서버에서 자세한 오류를 설정 하 여 자세한 오류 정보를 얻을 수 있습니다. 자세한 내용은 [허브 클래스에서 오류를 처리 하는 방법](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)을 참조 하세요.

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"TypeError: &lt;hubType&gt;이 (가) 정의 되어 있지 않습니다." 오류

`MapHubs`에 대 한 호출이 제대로 수행 되지 않으면이 오류가 발생 합니다. 자세한 내용은 [SignalR 경로를 등록 하 고 SignalR 옵션을 구성 하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#route) 참조 하세요.

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException가 사용자 코드에서 처리 되지 않았습니다.

메서드에 보내는 매개 변수에 직렬화 할 수 없는 형식 (예: 파일 핸들 또는 데이터베이스 연결)이 포함 되어 있지 않은지 확인 합니다. 클라이언트에 보내지 않으려는 서버 쪽 개체의 멤버를 사용 해야 하는 경우 (보안 또는 serialization의 이유로) `JSONIgnore` 특성을 사용 합니다.

### <a name="protocol-error-unknown-transport-error"></a>"프로토콜 오류: 알 수 없는 전송" 오류

이 오류는 클라이언트가 SignalR에서 사용 하는 전송을 지원 하지 않는 경우에 발생할 수 있습니다. SignalR와 함께 사용할 수 있는 브라우저에 대 한 자세한 내용은 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports) 를 참조 하세요.

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"JavaScript 허브 프록시 생성을 사용할 수 없습니다."

`signalr/hubs`에서 동적으로 생성 된 프록시에 대 한 참조를 포함 하는 동시에 `DisableJavaScriptProxies` 설정 된 경우이 오류가 발생 합니다. 프록시를 수동으로 만드는 방법에 대 한 자세한 내용은 [생성 된 프록시와 사용자의 역할](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)을 참조 하세요.

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"연결 ID의 형식이 잘못 되었습니다." 또는 "활성 SignalR 연결 중에 사용자 id가 변경 될 수 없습니다." 오류

이 오류는 인증을 사용 하는 경우 연결을 중지 하기 전에 클라이언트를 로그 아웃할 때 나타날 수 있습니다. 이 솔루션은 클라이언트를 로그 아웃 하기 전에 SignalR 연결을 중지 하는 것입니다.

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"Catch 되지 않은 오류: SignalR: jQuery를 찾을 수 없습니다. JQuery가 SignalR 파일 앞에서 참조 되는지 확인 하세요. "오류

SignalR JavaScript 클라이언트를 실행 하려면 jQuery를 실행 해야 합니다. JQuery에 대 한 참조가 올바른지, 사용 된 경로가 올바른지, jQuery에 대 한 참조가 SignalR에 대 한 참조 보다 이전 인지 확인 합니다.

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>"Catch 되지 않은 TypeError: 속성 '&lt;속성&gt;' 정의 되지 않음" 오류를 읽을 수 없습니다.

이 오류는 jQuery를 갖지 않거나 허브 프록시가 제대로 참조 되지 않았기 때문에 발생 합니다. JQuery 및 허브 프록시에 대 한 참조가 올바른지, 사용 된 경로가 올바른지, jQuery에 대 한 참조가 허브 프록시에 대 한 참조 보다 이전 인지 확인 합니다. 허브 프록시에 대 한 기본 참조는 다음과 같습니다.

**허브 프록시를 올바르게 참조 하는 HTML 클라이언트 쪽 코드**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"RuntimeBinderException이 사용자 코드에서 처리 되지 않았습니다." 오류

이 오류는 `Hub.On`의 잘못 된 오버 로드를 사용 하는 경우 발생할 수 있습니다. 메서드에 반환 값이 있는 경우 반환 형식을 제네릭 형식 매개 변수로 지정 해야 합니다.

**프록시를 생성 하지 않고 클라이언트에 정의 된 메서드**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>연결 ID가 일치 하지 않거나 페이지 로드 간의 연결 끊김

이 동작은 의도된 것입니다. 허브 개체는 페이지 개체에서 호스트 되므로 페이지가 새로 고쳐질 때 허브가 제거 됩니다. 다중 페이지 응용 프로그램은 페이지 로드 간에 일관 되도록 사용자와 연결 Id 간의 연결을 유지 해야 합니다. 연결 Id는 `ConcurrentDictionary` 개체 또는 데이터베이스의 서버에 저장할 수 있습니다.

### <a name="value-cannot-be-null-error"></a>"값이 null 일 수 없습니다." 오류

선택적 매개 변수가 있는 서버 쪽 메서드는 현재 지원 되지 않습니다. 선택적 매개 변수를 생략 하면 메서드가 실패 합니다. 자세한 내용은 [선택적 매개 변수](https://github.com/SignalR/SignalR/issues/324)를 참조 하세요.

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"Firefox에서 Firebug의 &lt;서버에 대 한 연결을 설정할 수 없습니다&gt;" 오류

이 오류 메시지는 WebSocket 전송에 대 한 협상이 실패 하 고 다른 전송이 대신 사용 되는 경우 Firebug에서 볼 수 있습니다. 이 동작은 의도된 것입니다.

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>".NET 클라이언트 응용 프로그램에서" 유효성 검사 절차에 따르면 원격 인증서가 유효 하지 않습니다. "오류가 발생 합니다.

서버에 사용자 지정 클라이언트 인증서가 필요한 경우 요청이 만들어지기 전에 x509certificate를 연결에 추가할 수 있습니다. `Connection.AddClientCertificate`를 사용 하 여 연결에 인증서를 추가 합니다.

### <a name="connection-drops-after-authentication-times-out"></a>인증 시간이 초과 된 후 연결이 삭제 됩니다.

이 동작은 의도된 것입니다. 연결이 활성화 되어 있는 동안에는 인증 자격 증명을 수정할 수 없습니다. 자격 증명을 새로 고치려면 연결을 중지 했다가 다시 시작 해야 합니다.

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>JQuery Mobile을 사용 하면 OnConnected가 두 번 호출 됩니다.

jQuery Mobile의 `initializePage` 함수는 각 페이지의 스크립트를 강제로 다시 실행 하 여 두 번째 연결을 만듭니다. 이 문제에 대 한 해결 방법은 다음과 같습니다.

- JavaScript 파일 앞에 jQuery Mobile에 대 한 참조를 포함 합니다.
- `$.mobile.autoInitializePage = false`을 설정 하 여 `initializePage` 함수를 사용 하지 않도록 설정 합니다.
- 연결을 시작 하기 전에 페이지 초기화가 완료 될 때까지 기다립니다.

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>서버에서 보낸 이벤트를 사용 하 여 Silverlight 응용 프로그램에서 메시지가 지연 됨

Silverlight에서 서버에서 보낸 이벤트를 사용할 때 메시지가 지연 됩니다. 대신 긴 폴링을 강제로 사용 하려면 연결을 시작할 때 다음을 사용 합니다.

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>영구 프레임 프로토콜을 사용 하는 "사용 권한이 거부 되었습니다."

이 문제는 [여기](https://github.com/SignalR/SignalR/issues/1963)에서 설명 하는 알려진 문제입니다. 이 증상은 최신 JQuery 라이브러리를 사용 하 여 볼 수 있습니다. 해결 방법은 응용 프로그램을 JQuery 1.8.2으로 다운 그레이드 하는 것입니다.

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>컴파일 및 서버 쪽 오류

 다음 섹션에는 컴파일러 및 서버 쪽 런타임 오류에 대 한 가능한 해결 방법이 포함 되어 있습니다. 

### <a name="reference-to-hub-instance-is-null"></a>허브 인스턴스에 대 한 참조가 null입니다.

허브 인스턴스는 각 연결에 대해 만들어지므로 코드에서 직접 허브 인스턴스를 만들 수 없습니다. 허브 자체 외부에서 허브의 메서드를 호출 하려면 허브 컨텍스트에 대 한 참조를 얻는 방법에 대해 [허브 클래스 외부에서 클라이언트 메서드를 호출 하 고 그룹을 관리 하는 방법](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) 을 참조 하세요.

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext. 세션이 null입니다.

이 동작은 의도된 것입니다. SignalR는 세션 상태를 사용 하도록 설정 하면 이중 메시징을 중단 하므로 ASP.NET 세션 상태를 지원 하지 않습니다.

### <a name="no-suitable-method-to-override"></a>재정의할 적절 한 메서드가 없습니다.

이전 문서 또는 블로그의 코드를 사용 하는 경우이 오류가 표시 될 수 있습니다. 변경 되었거나 더 이상 사용 되지 않는 메서드 (예: `OnConnectedAsync`)의 이름을 참조 하 고 있지 않은지 확인 합니다.

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>HostContextExtensions. WebSocketServerUrl가 null입니다.

이 동작은 의도된 것입니다. 이 멤버는 더 이상 사용 되지 않으므로 사용 하면 안 됩니다.

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"이름이 ' signalr ' 인 경로가 경로 컬렉션에 이미 있습니다." 오류

응용 프로그램에서 `MapHubs`를 두 번 호출 하는 경우이 오류가 표시 됩니다. 일부 예제 응용 프로그램은 전역 응용 프로그램 파일에서 직접 `MapHubs`를 호출 합니다. 다른 클래스는 래퍼 클래스에서 호출을 수행 합니다. 응용 프로그램에서 두 가지 모두를 수행 하지 않는지 확인 합니다.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Visual Studio 문제

이 단원에서는 Visual Studio에서 발생 하는 문제에 대해 설명 합니다.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>스크립트 문서 노드가 솔루션 탐색기에 표시 되지 않습니다.

일부 자습서에서는 디버그 하는 동안 솔루션 탐색기의 "스크립트 문서" 노드로 안내 합니다. 이 노드는 JavaScript 디버거에서 생성 되며 Internet Explorer에서 브라우저 클라이언트를 디버그 하는 동안에만 표시 됩니다. Chrome 또는 Firefox를 사용 하는 경우에는 노드가 표시 되지 않습니다. 다른 클라이언트 디버거가 실행 중인 경우 (예: Silverlight 디버거) JavaScript 디버거도 실행 되지 않습니다.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR가 Visual Studio 2008 이전 버전에서 작동 하지 않음

이 동작은 의도된 것입니다. SignalR에 .NET Framework 4 이상이 필요 합니다. 이렇게 하려면 Visual Studio 2010 이상에서 SignalR 응용 프로그램을 개발 해야 합니다.

<a id="iis"></a>

## <a name="iis-issues"></a>IIS 문제

이 섹션에는 인터넷 정보 서비스 관련 된 문제가 있습니다.

### <a name="web-site-crashes-after-maphubs-call"></a>MapHubs 호출 후 웹 사이트 충돌

최신 버전의 SignalR에서이 문제가 해결 되었습니다. NuGet을 사용 하 여 설치를 업데이트 하 여 최신 릴리스 버전의 SignalR를 사용 하 고 있는지 확인 합니다.

<a id="azure"></a>

## <a name="azure-issues"></a>Azure 문제

이 섹션에는 Microsoft Azure 관련 된 문제가 있습니다.

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>항목 이름을 변경한 후에 Azure 후면판을 통해 메시지를 받지 않음

Azure 후면판에서 사용 하는 토픽은 사용자가 구성할 수 없습니다.
