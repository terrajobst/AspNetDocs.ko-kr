---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API의 폼 인증 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 폼 인증을 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484379"
---
# <a name="forms-authentication-in-aspnet-web-api"></a>ASP.NET Web API의 폼 인증

[Mike Wasson](https://github.com/MikeWasson)

폼 인증은 HTML 폼을 사용 하 여 사용자의 자격 증명을 서버에 보냅니다. 인터넷 표준이 아닙니다. 폼 인증은 사용자가 HTML 양식과 상호 작용할 수 있도록 웹 응용 프로그램에서 호출 되는 웹 Api에만 적합 합니다.

| 장점 | 단점 |
| --- | --- |
| -간편한 구현: ASP.NET에 기본 제공 됩니다. -ASP.NET 멤버 자격 공급자를 사용 하 여 사용자 계정을 쉽게 관리할 수 있습니다. | -표준 HTTP 인증 메커니즘이 아닙니다. 표준 권한 부여 헤더 대신 HTTP 쿠키를 사용 합니다. -브라우저 클라이언트가 필요 합니다. -자격 증명이 일반 텍스트로 전송 됩니다. -CSRF (교차 사이트 요청 위조)에 취약 합니다. CSRF 측정값이 필요 합니다. -비 브라우저 클라이언트에서 사용 하기 어렵습니다. 로그인 하려면 브라우저가 필요 합니다. -사용자 자격 증명이 요청에서 전송 됩니다. -일부 사용자가 쿠키를 사용 하지 않도록 설정 합니다. |

간단히 말해서 ASP.NET의 폼 인증은 다음과 같이 작동 합니다.

1. 클라이언트가 인증을 요구 하는 리소스를 요청 합니다.
2. 사용자가 인증 되지 않은 경우 서버는 HTTP 302 (찾음)을 반환 하 고 로그인 페이지로 리디렉션합니다.
3. 사용자가 자격 증명을 입력 하 고 양식을 전송 합니다.
4. 서버는 다시 원래 URI로 리디렉션하는 다른 HTTP 302을 반환 합니다. 이 응답에는 인증 쿠키가 포함 되어 있습니다.
5. 클라이언트에서 리소스를 다시 요청 합니다. 요청은 인증 쿠키를 포함 하므로 서버에서 요청을 부여 합니다.

![](forms-authentication/_static/image1.png)

자세한 내용은 [폼 인증 개요](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md) 를 참조 하세요.

## <a name="using-forms-authentication-with-web-api"></a>Web API에서 폼 인증 사용

폼 인증을 사용 하는 응용 프로그램을 만들려면 MVC 4 프로젝트 마법사에서 "인터넷 응용 프로그램" 템플릿을 선택 합니다. 이 템플릿은 계정 관리를 위한 MVC 컨트롤러를 만듭니다. ASP.NET-2012 업데이트에서 사용할 수 있는 "단일 페이지 응용 프로그램" 템플릿을 사용할 수도 있습니다.

Web API 컨트롤러에서 [[권한 부여] 특성 사용](authentication-and-authorization-in-aspnet-web-api.md#auth3)에 설명 된 대로 `[Authorize]` 특성을 사용 하 여 액세스를 제한할 수 있습니다.

폼 인증은 세션 쿠키를 사용 하 여 요청을 인증 합니다. 브라우저는 모든 관련 쿠키를 대상 웹 사이트로 자동으로 보냅니다. 이 기능을 통해 폼 인증은 CSRF (교차 사이트 요청 위조) 공격에 취약할 수 있습니다. [CSRF (교차 사이트 요청 위조) 공격 방지](preventing-cross-site-request-forgery-csrf-attacks.md)를 참조 하세요.

폼 인증에서는 사용자의 자격 증명을 암호화 하지 않습니다. 따라서 폼 인증은 SSL과 함께 사용 하지 않는 한 안전 하지 않습니다. [WEB API에서 SSL](working-with-ssl-in-web-api.md)사용을 참조 하세요.
