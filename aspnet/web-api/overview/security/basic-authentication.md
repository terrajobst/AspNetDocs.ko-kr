---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API의 기본 인증 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 기본 인증을 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447635"
---
# <a name="basic-authentication-in-aspnet-web-api"></a>ASP.NET Web API의 기본 인증

[Mike Wasson](https://github.com/MikeWasson)

기본 인증은 [RFC 2617, HTTP 인증: 기본 및 다이제스트 액세스 인증](http://www.ietf.org/rfc/rfc2617.txt)에 정의 되어 있습니다.

단점

- 사용자 자격 증명은 요청에서 전송 됩니다.
- 자격 증명은 일반 텍스트로 전송 됩니다.
- 자격 증명은 모든 요청과 함께 전송 됩니다.
- 브라우저 세션을 종료 하는 경우를 제외 하 고는 로그 아웃 하는 방법이 없습니다.
- CSRF (교차 사이트 요청 위조)에 취약 합니다. CSRF 측정값이 필요 합니다.

장점

- 인터넷 표준.
- 모든 주요 브라우저에서 지원 됩니다.
- 비교적 간단한 프로토콜입니다.

기본 인증은 다음과 같이 작동 합니다.

1. 요청에 인증이 필요한 경우 서버는 401 (권한 없음)을 반환 합니다. 응답에는 서버가 기본 인증을 지원함을 나타내는 WWW 인증 헤더가 포함 되어 있습니다.
2. 클라이언트는 인증 헤더의 클라이언트 자격 증명을 사용 하 여 다른 요청을 보냅니다. 자격 증명은 문자열 "이름: 암호", base64 인코딩 형식으로 지정 됩니다. 자격 증명은 암호화 되지 않습니다.

기본 인증은 "영역"의 컨텍스트 내에서 수행 됩니다. 서버에는 WWW-인증 헤더에 영역 이름이 포함 됩니다. 사용자의 자격 증명은 해당 영역 내에서 유효 합니다. 영역의 정확한 범위는 서버에 의해 정의 됩니다. 예를 들어 리소스를 분할 하기 위해 여러 영역을 정의할 수 있습니다.

![](basic-authentication/_static/image1.png)

자격 증명이 암호화 되지 않은 상태로 전송 되기 때문에 기본 인증은 HTTPS를 통해서만 안전 합니다. [WEB API에서 SSL](working-with-ssl-in-web-api.md)사용을 참조 하세요.

기본 인증도 CSRF 공격에 취약 합니다. 사용자가 자격 증명을 입력 한 후에는 세션 기간 동안 브라우저가 동일한 도메인에 대 한 후속 요청을 자동으로 보냅니다. 여기에는 AJAX 요청이 포함 됩니다. [CSRF (교차 사이트 요청 위조) 공격 방지를](preventing-cross-site-request-forgery-csrf-attacks.md)참조 하세요.

## <a name="basic-authentication-with-iis"></a>IIS를 사용 하 여 기본 인증

IIS는 기본 인증을 지원 하지만, 사용자가 Windows 자격 증명에 대해 인증 되는 주의 사항이 있습니다. 즉, 사용자가 서버 도메인에 계정이 있어야 합니다. 공용 웹 사이트의 경우 일반적으로 ASP.NET 멤버 자격 공급자에 대해 인증을 수행 합니다.

IIS를 사용 하 여 기본 인증을 사용 하도록 설정 하려면 ASP.NET 프로젝트의 Web.config에서 인증 모드를 "Windows"로 설정 합니다.

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

이 모드에서 IIS는 Windows 자격 증명을 사용 하 여 인증 합니다. 또한 IIS에서 기본 인증을 사용 하도록 설정 해야 합니다. IIS 관리자에서 기능 보기로 이동 하 고, 인증을 선택 하 고, 기본 인증을 사용 하도록 설정 합니다.

![](basic-authentication/_static/image2.png)

웹 API 프로젝트에서 인증이 필요한 컨트롤러 작업에 대 한 `[Authorize]` 특성을 추가 합니다.

클라이언트는 요청에 권한 부여 헤더를 설정 하 여 자신을 인증 합니다. Browser 클라이언트는이 단계를 자동으로 수행 합니다. 비 브라우저 클라이언트는 헤더를 설정 해야 합니다.

## <a name="basic-authentication-with-custom-membership"></a>사용자 지정 멤버 자격으로 기본 인증

앞서 언급 했 듯이 IIS에 기본 제공 되는 인증은 Windows 자격 증명을 사용 합니다. 즉, 호스팅 서버에서 사용자에 대 한 계정을 만들어야 합니다. 그러나 인터넷 응용 프로그램의 경우 사용자 계정은 일반적으로 외부 데이터베이스에 저장 됩니다.

다음 코드에서는 기본 인증을 수행 하는 HTTP 모듈을 보여 줍니다. 이 예제의 더미 메서드인 `CheckPassword` 메서드를 대체 하 여 ASP.NET 멤버 자격 공급자를 쉽게 연결할 수 있습니다.

Web API 2에서는 HTTP 모듈 대신 [인증 필터](authentication-filters.md) 또는 [OWIN 미들웨어](../../../aspnet/overview/owin-and-katana/index.md)를 작성 하는 것이 좋습니다.

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

HTTP 모듈을 사용 하도록 설정 하려면 **system.webserver** 섹션의 web.config 파일에 다음을 추가 합니다.

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

"해당 Assemblyname"을 어셈블리 이름으로 바꿉니다 ("dll" 확장명 포함 안 함).

양식 또는 Windows 인증 등의 다른 인증 체계를 사용 하지 않도록 설정 해야 합니다.
