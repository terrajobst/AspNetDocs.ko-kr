---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Katana에서 Windows 인증 사용 | Microsoft Docs
author: MikeWasson
description: 이 문서에서는 Katana에서 Windows 인증을 사용 하도록 설정 하는 방법을 보여 줍니다. IIS를 사용 하 여 Katana를 호스트 하 고 HttpListener를 사용 하 여 자체 호스트 하는 두 가지 시나리오를 다룹니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500297"
---
# <a name="enabling-windows-authentication-in-katana"></a>Katana에서 Windows 인증 사용

[Mike Wasson](https://github.com/MikeWasson)

> 이 문서에서는 Katana에서 Windows 인증을 사용 하도록 설정 하는 방법을 보여 줍니다. IIS를 사용 하 여 Katana를 호스트 하 고 HttpListener를 사용 하 여 사용자 지정 프로세스에서 Katana를 호스트 하는 두 가지 시나리오를 다룹니다. Barry Dorrans, David Matson 및 Chris Ross 덕분에이 문서를 검토 합니다.

Katana는 .NET 용 개방형 웹 인터페이스인 [OWIN](http://owin.org/)의 Microsoft 구현입니다. [여기](an-overview-of-project-katana.md)에서 OWIN 및 Katana에 대 한 소개를 읽을 수 있습니다. OWIN 아키텍처에는 다음과 같은 여러 계층이 있습니다.

- Host: OWIN 파이프라인이 실행 되는 프로세스를 관리 합니다.
- 서버: 네트워크 소켓을 열고 요청을 수신 합니다.
- 미들웨어: HTTP 요청 및 응답을 처리 합니다.

Katana는 현재 두 개의 서버를 제공 하며, 두 서버 모두 Windows 통합 인증을 지원 합니다.

- **Owin 웹**입니다. ASP.NET 파이프라인에서 IIS를 사용 합니다.
- **Owin. HttpListener**. [시스템 HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)를 사용 합니다. 이 서버는 현재 자체 호스팅 Katana 때 기본 옵션입니다.

> [!NOTE]
> 현재 서버에서이 기능을 사용할 수 있기 때문에 Katana는 현재 Windows 인증용 OWIN 미들웨어를 제공 하지 않습니다.

## <a name="windows-authentication-in-iis"></a>IIS의 Windows 인증

Owin를 사용 하 여 IIS에서 Windows 인증을 사용 하도록 설정 하기만 하면 됩니다.

먼저 "ASP.NET Empty 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여 새 ASP.NET 응용 프로그램을 만들어 보겠습니다.

![](enabling-windows-authentication-in-katana/_static/image1.png)

다음으로 NuGet 패키지를 추가 합니다. **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

이제 다음 코드를 사용 하 여 `Startup` 라는 클래스를 추가 합니다.

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

이것은 IIS에서 실행 되는 OWIN에 대 한 "Hello 세계" 응용 프로그램을 만드는 데 필요 합니다. F5 키를 눌러 애플리케이션을 디버깅합니다. 콘솔에 "Hello World!" 브라우저 창에서

![](enabling-windows-authentication-in-katana/_static/image2.png)

다음으로 IIS Express에서 Windows 인증을 사용 하도록 설정 합니다. **보기** 메뉴에서 **속성**을 선택 합니다. 프로젝트 속성을 보려면 솔루션 탐색기에서 프로젝트 이름을 클릭 합니다.

**속성** 창에서 **익명 인증** 을 **사용 안 함** 으로 설정 하 고 **Windows 인증** 을 **사용**으로 설정 합니다.

![](enabling-windows-authentication-in-katana/_static/image3.png)

Visual Studio에서 응용 프로그램을 실행 하는 경우 IIS Express 사용자의 Windows 자격 증명이 필요 합니다. [Fiddler](http://fiddler2.com/home) 또는 다른 HTTP 디버깅 도구를 사용 하 여이를 확인할 수 있습니다. HTTP 응답 예제는 다음과 같습니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

이 응답의 WWW-인증 헤더는 서버에서 Kerberos 또는 NTLM을 사용 하는 [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) 프로토콜을 지원함을 의미 합니다.

나중에 응용 프로그램을 서버에 배포 하는 경우 [다음 단계](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) 에 따라 해당 서버의 IIS에서 Windows 인증을 사용 하도록 설정 합니다.

## <a name="windows-authentication-in-httplistener"></a>HttpListener의 Windows 인증

Owin를 사용 하 여 Katana를 자체 호스트 하는 경우 **HttpListener** 인스턴스에서 직접 Windows 인증을 사용 하도록 설정할 수 있습니다.

먼저 새 콘솔 응용 프로그램을 만듭니다. 다음으로 NuGet 패키지를 추가 합니다. **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

이제 다음 코드를 사용 하 여 `Startup` 라는 클래스를 추가 합니다.

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

이 클래스는 이전에서와 동일한 "Hello 세계" 예제를 구현 하지만 인증 체계로도 Windows 인증을 설정 합니다.

`Main` 함수 내에서 OWIN 파이프라인을 시작 합니다.

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

Fiddler에서 요청을 보내 응용 프로그램이 Windows 인증을 사용 하 고 있는지 확인할 수 있습니다.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a>관련 항목

[프로젝트 Katana 개요](an-overview-of-project-katana.md)

[System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[MVC 5에서 OWIN 폼 인증 이해](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
