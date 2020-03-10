---
uid: web-api/overview/security/individual-accounts-in-web-api
title: ASP.NET Web API 2.2에서 개별 계정 및 로컬 로그인을 사용 하 여 Web API 보안 유지 Microsoft Docs
author: MikeWasson
description: 이 항목에서는 OAuth2를 사용 하 여 웹 API를 보호 하 여 멤버 자격 데이터베이스에 대해 인증 하는 방법을 보여 줍니다. Visual Studio 201 자습서에서 사용 되는 소프트웨어 버전 ...
ms.author: riande
ms.date: 10/15/2014
ms.assetid: 92c84846-f0ea-4b5e-94b6-5004874eb060
msc.legacyurl: /web-api/overview/security/individual-accounts-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7492c4aa4c2a0a8aeed64c3462bda8fc51f35a6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447179"
---
# <a name="secure-a-web-api-with-individual-accounts-and-local-login-in-aspnet-web-api-22"></a>ASP.NET Web API 2.2에서 개별 계정 및 로컬 로그인을 사용 하 여 Web API 보안 유지

[Mike Wasson](https://github.com/MikeWasson)

[샘플 앱 다운로드](https://github.com/MikeWasson/LocalAccountsApp)

> 이 항목에서는 OAuth2를 사용 하 여 웹 API를 보호 하 여 멤버 자격 데이터베이스에 대해 인증 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013 업데이트 3](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - [웹 API 2.2](../releases/whats-new-in-aspnet-web-api-22.md)
> - [ASP.NET Identity 2.1](../../../identity/index.md)

Visual Studio 2013 웹 API 프로젝트 템플릿은 인증을 위한 세 가지 옵션을 제공 합니다.

- **개별 계정.** 앱은 멤버 자격 데이터베이스를 사용 합니다.
- **조직 계정.** 사용자는 Azure Active Directory, Office 365 또는 온-프레미스 Active Directory 자격 증명을 사용 하 여 로그인 합니다.
- **Windows 인증.** 이 옵션은 인트라넷 응용 프로그램용 이며 Windows 인증 IIS 모듈을 사용 합니다.

이러한 옵션에 대 한 자세한 내용은 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#auth)를 참조 하세요.

개별 계정은 사용자가 로그인 할 수 있는 두 가지 방법을 제공 합니다.

- **로컬 로그인**. 사용자가 사이트에 등록 하 고 사용자 이름과 암호를 입력 합니다. 앱은 멤버 자격 데이터베이스에 암호 해시를 저장 합니다. 사용자가 로그인 하면 ASP.NET Identity 시스템에서 암호를 확인 합니다.
- **소셜 로그인**. 사용자가 Facebook, Microsoft 또는 Google과 같은 외부 서비스를 사용 하 여 로그인 합니다. 앱은 여전히 멤버 자격 데이터베이스에서 사용자에 대 한 항목을 만들지만 자격 증명을 저장 하지는 않습니다. 사용자가 외부 서비스에 로그인 하 여 인증 합니다.

이 문서에서는 로컬 로그인 시나리오를 살펴봅니다. 웹 API는 로컬 로그인과 소셜 로그인 모두에 대해 OAuth2를 사용 하 여 요청을 인증 합니다. 그러나 로컬 및 소셜 로그인에 대 한 자격 증명 흐름은 다릅니다.

이 문서에서는 사용자가 로그인 하 여 웹 API에 인증 된 AJAX 호출을 보낼 수 있는 간단한 앱을 설명 합니다. 샘플 코드는 [여기](https://github.com/MikeWasson/LocalAccountsApp)에서 다운로드할 수 있습니다. 추가 정보는 Visual Studio에서 샘플을 처음부터 만드는 방법을 설명 합니다.

[![](individual-accounts-in-web-api/_static/image2.png)](individual-accounts-in-web-api/_static/image1.png)

샘플 앱은 데이터 바인딩 및 jQuery에 대해 녹아웃을 사용 하 여 AJAX 요청을 보냅니다. AJAX 호출에 초점을 맞춘 후이 문서에 대 한 사용자의 녹아웃을 알 필요가 없습니다.

이 과정을 통해 다음과 같이 설명할 수 있습니다.

- 응용 프로그램이 클라이언트 쪽에서 수행 하는 작업입니다.
- 서버에서 무슨 일이 발생 합니다.
- 중간의 HTTP 트래픽입니다.

먼저 일부 OAuth2 용어를 정의 해야 합니다.

- *리소스*. 보호할 수 있는 데이터의 일부입니다.
- *리소스 서버*. 리소스를 호스트 하는 서버입니다.
- *리소스 소유자*입니다. 리소스에 대 한 액세스 권한을 부여할 수 있는 엔터티입니다. (일반적으로 사용자입니다.)
- *클라이언트*: 리소스에 액세스 하려는 앱입니다. 이 문서에서 클라이언트는 웹 브라우저입니다.
- *액세스 토큰*입니다. 리소스에 대 한 액세스 권한을 부여 하는 토큰입니다.
- *전달자 토큰*입니다. 사용자가 토큰을 사용할 수 있는 속성을 가진 특정 형식의 액세스 토큰입니다. 즉, 클라이언트는 전달자 토큰을 사용 하는 암호화 키 또는 기타 비밀이 필요 하지 않습니다. 이러한 이유로 전달자 토큰은 HTTPS를 통해서만 사용 해야 하며, 짧은 만료 시간을 사용 해야 합니다.
- *권한 부여 서버*. 액세스 토큰을 제공 하는 서버입니다.

응용 프로그램은 권한 부여 서버 및 리소스 서버 역할을 할 수 있습니다. Web API 프로젝트 템플릿은이 패턴을 따릅니다.

## <a name="local-login-credential-flow"></a>로컬 로그인 자격 증명 흐름

로컬 로그인의 경우 Web API는 OAuth2에 정의 된 [리소스 소유자 암호 흐름](http://oauthlib.readthedocs.org/en/latest/oauth2/grants/password.html) 을 사용 합니다.

1. 사용자가 클라이언트에 이름과 암호를 입력 합니다.
2. 클라이언트는 권한 부여 서버에 이러한 자격 증명을 보냅니다.
3. 권한 부여 서버는 자격 증명을 인증 하 고 액세스 토큰을 반환 합니다.
4. 보호 된 리소스에 액세스 하기 위해 클라이언트는 HTTP 요청의 인증 헤더에 액세스 토큰을 포함 합니다.

![](individual-accounts-in-web-api/_static/image3.png)

웹 API 프로젝트 템플릿에서 **개별 계정을** 선택 하면 프로젝트에 사용자 자격 증명의 유효성을 검사 하 고 토큰을 발급 하는 권한 부여 서버가 포함 됩니다. 다음 다이어그램에서는 Web API 구성 요소를 기준으로 동일한 자격 증명 흐름을 보여 줍니다.

![](individual-accounts-in-web-api/_static/image4.png)

이 시나리오에서 Web API 컨트롤러는 리소스 서버 역할을 합니다. 인증 필터는 액세스 토큰의 유효성을 검사 하 고 **[권한 부여]** 특성은 리소스를 보호 하는 데 사용 됩니다. 컨트롤러나 작업에 **[권한 부여]** 특성이 있는 경우 해당 컨트롤러 또는 작업에 대 한 모든 요청을 인증 해야 합니다. 그렇지 않으면 권한 부여가 거부 되 고 Web API는 401 (권한 없음) 오류를 반환 합니다.

권한 부여 서버와 인증 필터는 모두 OAuth2의 세부 정보를 처리 하는 [OWIN 미들웨어](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 구성 요소를 호출 합니다. 디자인은이 자습서의 뒷부분에서 자세히 설명 합니다.

## <a name="sending-an-unauthorized-request"></a>권한 없는 요청 보내기

시작 하려면 앱을 실행 하 고 **API 호출** 단추를 클릭 합니다. 요청이 완료 되 면 **결과** 상자에 오류 메시지가 표시 됩니다. 요청이 액세스 토큰을 포함 하지 않기 때문에 요청이 권한 없는 것입니다.

[![](individual-accounts-in-web-api/_static/image6.png)](individual-accounts-in-web-api/_static/image5.png)

**Api 호출** 단추는 웹 API 컨트롤러 작업을 호출 하는 ~/api/values에 AJAX 요청을 보냅니다. 다음은 AJAX 요청을 보내는 JavaScript 코드의 섹션입니다. 샘플 앱에서 모든 JavaScript 앱 코드는 Scripts\app.js 파일에 있습니다.

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample1.js)]

사용자가 로그인 할 때까지 전달자 토큰이 없으며, 따라서 요청에 권한 부여 헤더가 없습니다. 이로 인해 요청에서 401 오류가 반환 됩니다.

다음은 HTTP 요청입니다. ( [Fiddler](http://www.telerik.com/fiddler) 를 사용 하 여 HTTP 트래픽을 캡처 했습니다.)

[!code-console[Main](individual-accounts-in-web-api/samples/sample2.cmd)]

HTTP 응답:

[!code-console[Main](individual-accounts-in-web-api/samples/sample3.cmd?highlight=1,4)]

응답에는 챌린지가 설정 된 Www 인증 헤더가 포함 되어 있습니다. 서버에 전달자 토큰이 필요 함을 나타냅니다.

## <a name="register-a-user"></a>사용자 등록

앱의 **등록** 섹션에서 전자 메일 및 암호를 입력 하 고 **등록** 단추를 클릭 합니다.

이 샘플에 유효한 전자 메일 주소를 사용할 필요는 없지만 실제 앱은 주소를 확인 합니다. ( [로그인, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 ASP.NET MVC 5 웹 앱 만들기를](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)참조 하세요.) 암호에 대해 대문자, 소문자, 숫자 및 영숫자가 아닌 문자를 포함 하는 "Password1!"와 같은 항목을 사용 합니다. 앱을 간단 하 게 유지 하기 위해 클라이언트 쪽 유효성 검사를 수행 하 여 암호 형식에 문제가 있는 경우 400 (잘못 된 요청) 오류가 발생 합니다.

[![](individual-accounts-in-web-api/_static/image8.png)](individual-accounts-in-web-api/_static/image7.png)

**등록** 단추를 클릭 하면 POST 요청을 ~/api/Account/Register/.로 보냅니다. 요청 본문은 이름과 암호를 포함 하는 JSON 개체입니다. 요청을 보내는 JavaScript 코드는 다음과 같습니다.

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample4.js)]

HTTP 요청:

[!code-console[Main](individual-accounts-in-web-api/samples/sample5.cmd?highlight=5,10)]

HTTP 응답:

[!code-console[Main](individual-accounts-in-web-api/samples/sample6.cmd)]

이 요청은 `AccountController` 클래스에 의해 처리 됩니다. 내부적으로 `AccountController`는 ASP.NET Identity를 사용 하 여 멤버 자격 데이터베이스를 관리 합니다.

Visual Studio에서 로컬로 응용 프로그램을 실행 하는 경우 사용자 계정은 LocalDB의 AspNetUsers 테이블에 저장 됩니다. Visual Studio에서 테이블을 보려면 **보기** 메뉴를 클릭 하 **서버 탐색기**, **데이터 연결**을 차례로 확장 합니다.

![](individual-accounts-in-web-api/_static/image9.png)

## <a name="get-an-access-token"></a>액세스 토큰 가져오기

지금까지 OAuth를 수행 하지 않았지만, 이제 액세스 토큰을 요청할 때 작동 중인 OAuth 권한 부여 서버가 표시 됩니다. 샘플 앱의 **로그인** 영역에서 전자 메일 및 암호를 입력 하 고 **로그인**을 클릭 합니다.

[![](individual-accounts-in-web-api/_static/image11.png)](individual-accounts-in-web-api/_static/image10.png)

**로그인** 단추는 토큰 끝점에 요청을 보냅니다. 요청 본문에는 다음과 같은 폼 url로 인코딩된 데이터가 포함 되어 있습니다.

- grant\_유형: "password"
- 사용자 이름: 사용자의 전자 메일을 &lt;&gt;
- 암호: 암호 &lt;&gt;

AJAX 요청을 보내는 JavaScript 코드는 다음과 같습니다.

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample7.js?highlight=14)]

요청이 성공 하면 권한 부여 서버는 응답 본문에 액세스 토큰을 반환 합니다. 세션 저장소에 토큰을 저장 하 여 나중에 API로 요청을 보낼 때 사용 합니다. 일부 인증 형태 (예: 쿠키 기반 인증)와 달리 브라우저는 후속 요청에 액세스 토큰을 자동으로 포함 하지 않습니다. 응용 프로그램은 명시적으로이 작업을 수행 해야 합니다. 이것은 [Csrf 취약성](preventing-cross-site-request-forgery-csrf-attacks.md)을 제한 하기 때문입니다.

HTTP 요청:

[!code-console[Main](individual-accounts-in-web-api/samples/sample8.cmd?highlight=5,10)]

요청에 사용자 자격 증명이 포함 되어 있는 것을 볼 수 있습니다. 전송 계층 보안을 제공 하려면 HTTPS를 사용 *해야* 합니다.

HTTP 응답:

[!code-console[Main](individual-accounts-in-web-api/samples/sample9.cmd?highlight=8)]

가독성을 위해 JSON을 들여쓴 후 매우 긴 액세스 토큰을 자릅니다.

`access_token`, `token_type`및 `expires_in` 속성은 OAuth2 사양으로 정의 됩니다. 다른 속성 (`userName`, `.issued`및 `.expires`)은 참고용 으로만 사용 됩니다. `TokenEndpoint` 메서드에서/Providers/ApplicationOAuthProvider.cs 파일에 추가 속성을 추가 하는 코드를 찾을 수 있습니다.

## <a name="send-an-authenticated-request"></a>인증 된 요청 보내기

이제 전달자 토큰이 있으므로 API에 대 한 인증 된 요청을 수행할 수 있습니다. 요청에서 권한 부여 헤더를 설정 하 여이 작업을 수행 합니다. **API 호출** 단추를 다시 클릭 하 여이를 확인 합니다.

[![](individual-accounts-in-web-api/_static/image13.png)](individual-accounts-in-web-api/_static/image12.png)

HTTP 요청:

[!code-console[Main](individual-accounts-in-web-api/samples/sample10.cmd?highlight=5)]

HTTP 응답:

[!code-console[Main](individual-accounts-in-web-api/samples/sample11.cmd)]

## <a name="log-out"></a>로그아웃

브라우저는 자격 증명이 나 액세스 토큰을 캐시 하지 않으므로 세션 저장소에서 토큰을 제거 하 여 토큰을 "잊어버린" 경우에만 로그 아웃 합니다.

[!code-javascript[Main](individual-accounts-in-web-api/samples/sample12.js)]

## <a name="understanding-the-individual-accounts-project-template"></a>개별 계정 프로젝트 템플릿 이해

ASP.NET 웹 응용 프로그램 프로젝트 템플릿에서 **개별 계정을** 선택 하면 프로젝트에 다음 항목이 포함 됩니다.

- OAuth2 권한 부여 서버입니다.
- 사용자 계정을 관리 하기 위한 Web API 끝점
- 사용자 계정을 저장 하기 위한 EF 모델입니다.

다음은 이러한 기능을 구현 하는 기본 응용 프로그램 클래스입니다.

- `AccountController`입니다. 사용자 계정을 관리 하기 위한 Web API 끝점을 제공 합니다. `Register` 작업은이 자습서에서 사용한 유일한 작업입니다. 클래스의 다른 메서드는 암호 재설정, 소셜 로그인 및 기타 기능을 지원 합니다.
- /Models/IdentityModels.cs.에 정의 된 `ApplicationUser` 이 클래스는 멤버 자격 데이터베이스의 사용자 계정에 대 한 EF 모델입니다.
- /App\_Start/IdentityConfig에 정의 된 `ApplicationUserManager`이 클래스는 [Usermanager](https://msdn.microsoft.com/library/dn613290.aspx) 에서 파생 되 고 사용자 계정에 대 한 작업을 수행 합니다 (예: 새 사용자 만들기, 암호 확인 등), 데이터베이스에 대 한 변경 내용을 자동으로 유지 합니다.
- `ApplicationOAuthProvider`입니다. 이 개체는 OWIN 미들웨어에 연결 하 고 미들웨어에 의해 발생 한 이벤트를 처리 합니다. [Oauthauthorizationserverprovider](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserverprovider.aspx)에서 파생 됩니다.

![](individual-accounts-in-web-api/_static/image14.png)

### <a name="configuring-the-authorization-server"></a>권한 부여 서버 구성

StartupAuth.cs에서 다음 코드는 OAuth2 권한 부여 서버를 구성 합니다.

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample13.cs)]

`TokenEndpointPath` 속성은 권한 부여 서버 끝점에 대 한 URL 경로입니다. 앱에서 전달자 토큰을 가져오는 데 사용 하는 URL입니다.

`Provider` 속성은 OWIN 미들웨어에 연결 하 고 미들웨어에 의해 발생 한 이벤트를 처리 하는 공급자를 지정 합니다.

앱에서 토큰을 받으려는 기본 흐름은 다음과 같습니다.

1. 액세스 토큰을 가져오기 위해 앱은 ~/Token.에 요청을 보냅니다.
2. OAuth 미들웨어는 공급자에 대 한 `GrantResourceOwnerCredentials`를 호출 합니다.
3. 공급자는 `ApplicationUserManager`를 호출 하 여 자격 증명의 유효성을 검사 하 고 클레임 id를 만듭니다.
4. 이 작업이 성공 하면 공급자는 토큰을 생성 하는 데 사용 되는 인증 티켓을 만듭니다.

[![](individual-accounts-in-web-api/_static/image16.png)](individual-accounts-in-web-api/_static/image15.png)

OAuth 미들웨어는 사용자 계정에 대 한 어떠한 정보도 알지 못합니다. 공급자는 미들웨어와 ASP.NET Identity 사이를 통신 합니다. 권한 부여 서버를 구현 하는 방법에 대 한 자세한 내용은 [OWIN OAuth 2.0 Authorization server](../../../aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server.md)를 참조 하세요.

### <a name="configuring-web-api-to-use-bearer-tokens"></a>전달자 토큰을 사용 하도록 Web API 구성

`WebApiConfig.Register` 메서드에서 다음 코드는 Web API 파이프라인에 대 한 인증을 설정 합니다.

[!code-csharp[Main](individual-accounts-in-web-api/samples/sample14.cs)]

**Hostauthenticationfilter** 클래스를 사용 하면 전달자 토큰을 사용 하 여 인증을 수행할 수 있습니다.

**Config.suppressdefaulthostauthentication** 메서드는 요청이 웹 api 파이프라인 (IIS 또는 OWIN 미들웨어)에 도달 하기 전에 발생 하는 모든 인증을 무시 하도록 웹 api에 지시 합니다. 이러한 방식으로 Web API가 전달자 토큰만으로 인증하도록 제한할 수 있습니다.

> [!NOTE]
> 특히 응용 프로그램의 MVC 부분은 쿠키에 자격 증명을 저장 하는 폼 인증을 사용할 수 있습니다. 쿠키 기반 인증을 사용 하려면 위조 방지 토큰을 사용 하 여 CSRF 공격을 방지 해야 합니다. 웹 API가 위조 방지 토큰을 클라이언트에 보낼 수 있는 편리한 방법이 없기 때문에 웹 Api의 문제입니다. (이 문제에 대 한 자세한 배경 정보는 [WEB API에서 CSRF 공격 방지](preventing-cross-site-request-forgery-csrf-attacks.md)를 참조 하세요.) **Config.suppressdefaulthostauthentication** 를 호출 하면 Web API가 쿠키에 저장 된 자격 증명의 csrf 공격에 취약 하지 않습니다.

클라이언트에서 보호 된 리소스를 요청할 때 웹 API 파이프라인에서 발생 하는 작업은 다음과 같습니다.

1. **Hostauthentication** 필터는 OAuth 미들웨어를 호출 하 여 토큰의 유효성을 검사 합니다.
2. 미들웨어는 토큰을 클레임 id로 변환 합니다.
3. 이 시점에서 요청은 *인증* 되지만 *권한이 부여*되지 않습니다.
4. 권한 부여 필터는 클레임 id를 검사 합니다. 클레임에서 해당 리소스에 대 한 사용자 권한을 부여 하는 경우 요청에 권한이 부여 됩니다. 기본적으로 **[권한 부여]** 특성은 인증 된 모든 요청에 대 한 권한을 부여 합니다. 그러나 역할 또는 다른 클레임을 통해 권한을 부여할 수 있습니다. 자세한 내용은 [WEB API의 인증 및 권한 부여](authentication-and-authorization-in-aspnet-web-api.md)를 참조 하세요.
5. 이전 단계가 성공적으로 수행 되 면 컨트롤러는 보호 된 리소스를 반환 합니다. 그렇지 않으면 클라이언트에서 401 (권한 없음) 오류를 수신 합니다.

[![](individual-accounts-in-web-api/_static/image18.png)](individual-accounts-in-web-api/_static/image17.png)

## <a name="additional-resources"></a>추가 리소스

- [ASP.NET Identity](../../../identity/index.md)
- [VS2013 RC 용 SPA 템플릿의 보안 기능 이해](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx) MSDN 블로그 게시물 Hongye Sun.
- [개로 나누어서 WEB API 개별 계정 템플릿 – 2 부: 로컬 계정](http://leastprivilege.com/2013/11/26/dissecting-the-web-api-individual-accounts-templatepart-2-local-accounts/). Dominick Baier의 블로그 게시물입니다.
- [OWIN를 사용 하 여 인증 및 WEB API를 호스팅합니다](http://brockallen.com/2013/10/27/host-authentication-and-web-api-with-owin-and-active-vs-passive-authentication-middleware/). Brock Allen의 `SuppressDefaultHostAuthentication` 및 `HostAuthenticationFilter`에 대 한 유용한 설명입니다.
- [VS 2013 템플릿의 ASP.NET Identity에서 프로필 정보를 사용자 지정](https://blogs.msdn.com/b/webdev/archive/2013/10/16/customizing-profile-information-in-asp-net-identity-in-vs-2013-templates.aspx)합니다. MSDN 블로그 게시물 (Pranav Rastogi)
- [ASP.NET Identity에서 UserManager 클래스에 대 한 요청 당 수명 관리](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx) Joshi의 MSDN 블로그 게시물에는 `UserManager` 클래스에 대 한 적절 한 설명이 나와 있습니다.
