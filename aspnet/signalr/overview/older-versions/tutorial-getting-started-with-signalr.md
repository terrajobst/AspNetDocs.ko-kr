---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: '자습서: SignalR 1.x 시작 하기 | Microsoft Docs'
author: bradygaster
description: ASP.NET SignalR를 사용 하 여 HTML 페이지에서 실시간 채팅 응용 프로그램을 빌드합니다.
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505751"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a>자습서: SignalR 1.x 시작

[Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 자습서에는 SignalR을 사용하여 실시간 채팅 애플리케이션을 만드는 방법을 보여 줍니다. 빈 ASP.NET 웹 응용 프로그램에 SignalR를 추가 하 고 메시지를 보내고 표시 하는 HTML 페이지를 만듭니다.

## <a name="overview"></a>개요

이 자습서에서는 간단한 브라우저 기반 채팅 응용 프로그램을 빌드하는 방법을 보여 SignalR 개발을 소개 합니다. 빈 ASP.NET 웹 응용 프로그램에 SignalR 라이브러리를 추가 하 고, 클라이언트에 메시지를 보내기 위한 허브 클래스를 만들고, 사용자가 채팅 메시지를 보내고 받을 수 있도록 하는 HTML 페이지를 만듭니다. Mvc 뷰를 사용 하 여 MVC 4에서 채팅 응용 프로그램을 만드는 방법을 보여 주는 유사한 자습서는 [SignalR 및 MVC 4 시작](index.md)을 참조 하세요.

> [!NOTE]
> 이 자습서에서는 릴리스 (1.x) 버전의 SignalR를 사용 합니다. SignalR 1.x와 2.0 간의 변경 내용에 대 한 자세한 내용은 [SignalR 1.X 프로젝트 업그레이드](../releases/upgrading-signalr-1x-projects-to-20.md)를 참조 하세요.

SignalR는 라이브 사용자 상호 작용 또는 실시간 데이터 업데이트를 필요로 하는 웹 응용 프로그램을 빌드하기 위한 오픈 소스 .NET 라이브러리입니다. 예를 들면 소셜 응용 프로그램, 다중 사용자 게임, 비즈니스 공동 작업, 뉴스, 날씨 또는 재무 업데이트 응용 프로그램이 있습니다. 이러한 응용 프로그램은 종종 실시간 응용 프로그램 이라고 합니다.

SignalR는 실시간 응용 프로그램을 빌드하는 프로세스를 간소화 합니다. 여기에는 클라이언트-서버 연결을 보다 쉽게 관리 하 고 클라이언트에 콘텐츠 업데이트를 푸시할 수 있도록 하는 ASP.NET 서버 라이브러리와 JavaScript 클라이언트 라이브러리가 포함 됩니다. SignalR 라이브러리를 기존 ASP.NET 응용 프로그램에 추가 하 여 실시간 기능을 얻을 수 있습니다.

이 자습서에서는 다음과 같은 SignalR 개발 작업을 보여 줍니다.

- ASP.NET 웹 응용 프로그램에 SignalR 라이브러리 추가
- 클라이언트에 콘텐츠를 푸시하는 허브 클래스 만들기
- 웹 페이지에서 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 허브에서 업데이트를 표시 합니다.

다음 스크린샷은 브라우저에서 실행 중인 채팅 응용 프로그램을 보여 줍니다. 각 새 사용자는 메모를 게시 하 고 사용자가 채팅에 가입한 후 추가 된 주석을 볼 수 있습니다.

![채팅 인스턴스](tutorial-getting-started-with-signalr/_static/image1.png)

섹션이

- [프로젝트 설정](#setup)
- [샘플 실행](#run)
- [코드 검사](#code)
- [다음 단계](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>프로젝트 설정

이 섹션에서는 빈 ASP.NET 웹 응용 프로그램을 만들고, SignalR를 추가 하 고, 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.

필수 조건:

- Visual Studio 2010 SP1 또는 2012. Visual Studio가 없는 경우 [ASP.NET 다운로드](https://www.asp.net/downloads) 를 참조 하 여 무료 visual Studio 2012 Express 개발 도구를 다운로드 하세요.
- [Microsoft ASP.NET 및 Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941). Visual Studio 2012의 경우이 설치 관리자는 SignalR 템플릿을 포함 한 새 ASP.NET 기능을 Visual Studio에 추가 합니다. Visual Studio 2010 s p 1의 경우 설치 관리자를 사용할 수 없지만 설치 단계에 설명 된 대로 SignalR NuGet 패키지를 설치 하 여 자습서를 완료할 수 있습니다.

다음 단계에서는 Visual Studio 2012을 사용 하 여 ASP.NET 빈 웹 응용 프로그램을 만들고 SignalR 라이브러리를 추가 합니다.

1. Visual Studio에서 ASP.NET 빈 웹 응용 프로그램을 만듭니다.

    ![빈 웹 만들기](tutorial-getting-started-with-signalr/_static/image2.png)
2. 도구 |를 선택 하 여 **패키지 관리자 콘솔** 을 엽니다.  **NuGet 패키지 관리자 | 패키지 관리자 콘솔**. 콘솔 창에 다음 명령을 입력 합니다.

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    이 명령은 SignalR 1.x의 최신 버전을 설치 합니다.
3. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 클래스**. 새 클래스의 이름을 **ChatHub**로 합니다.
4. **솔루션 탐색기** 스크립트 노드를 확장 합니다. JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.

    ![라이브러리 참조](tutorial-getting-started-with-signalr/_static/image3.png)
5. **ChatHub** 클래스의 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **추가 |를 클릭 합니다. 새 항목**입니다. **새 항목 추가** 대화 상자에서 **전역 응용 프로그램 클래스** 를 선택 하 고 **추가**를 클릭 합니다.

    ![전역 추가](tutorial-getting-started-with-signalr/_static/image4.png)
7. Global.asax.cs 클래스에서 제공 된 `using` 문 뒤에 다음 `using` 문을 추가 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. SignalR hubs의 기본 경로를 등록 하려면 전역 클래스의 `Application_Start` 메서드에 다음 코드 줄을 추가 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **추가 |를 클릭 합니다. 새 항목**입니다. **새 항목 추가** 대화 상자에서 Html 페이지를 선택 하 고 **추가**를 클릭 합니다.
10. **솔루션 탐색기**에서 방금 만든 HTML 페이지를 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 클릭 합니다.
11. HTML 페이지의 기본 코드를 다음 코드로 바꿉니다.

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. 프로젝트에 대 한 **모든를 저장** 합니다.

<a id="run"></a>

## <a name="run-the-sample"></a>샘플 실행

1. F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다. HTML 페이지가 브라우저 인스턴스에 로드 되 고 사용자 이름을 입력 하 라는 메시지가 표시 됩니다.

    ![사용자 이름 입력](tutorial-getting-started-with-signalr/_static/image5.png)
2. 사용자 이름을 입력합니다.
3. 브라우저의 주소 줄에서 URL을 복사 하 고이를 사용 하 여 두 개의 브라우저 인스턴스를 엽니다. 각 브라우저 인스턴스에서 고유한 사용자 이름을 입력 합니다.
4. 각 브라우저 인스턴스에서 주석을 추가 하 고 **보내기**를 클릭 합니다. 주석은 모든 브라우저 인스턴스에 표시 되어야 합니다.

    > [!NOTE]
    > 이 간단한 채팅 응용 프로그램은 서버에 대 한 토론 컨텍스트를 유지 하지 않습니다. 허브는 모든 현재 사용자에 게 주석을 브로드캐스트합니다. 나중에 채팅에 참여 하는 사용자는 연결 된 시간부터 추가 된 메시지를 볼 수 있습니다.

    다음 스크린샷에서는 세 개의 브라우저 인스턴스에서 실행 되는 채팅 응용 프로그램을 보여 주며,이는 모두 한 인스턴스가 메시지를 보낼 때 업데이트 됩니다.

    ![채팅 브라우저](tutorial-getting-started-with-signalr/_static/image6.png)
5. **솔루션 탐색기**에서 실행 중인 응용 프로그램에 대 한 **스크립트 문서** 노드를 검사 합니다. SignalR 라이브러리가 런타임에 동적으로 생성 하는 **허브** 라는 스크립트 파일이 있습니다. 이 파일은 jQuery 스크립트와 서버측 코드 간의 통신을 관리 합니다.

    ![생성 된 허브 스크립트](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a>코드 검사

SignalR chat 응용 프로그램은 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 받는 두 가지 기본 SignalR 개발 작업을 보여 줍니다.

### <a name="signalr-hubs"></a>SignalR 허브

코드 샘플에서 **ChatHub** 클래스는 **SignalR** 클래스에서 파생 됩니다. **허브** 클래스에서 파생 하는 것은 SignalR 응용 프로그램을 빌드하는 데 유용한 방법입니다. 허브 클래스에서 공용 메서드를 만든 다음 웹 페이지의 jQuery 스크립트에서 해당 메서드를 호출 하 여 액세스할 수 있습니다.

채팅 코드에서 클라이언트는 **ChatHub** 메서드를 호출 하 여 새 메시지를 보냅니다. 그러면 허브는 **broadcastMessage**를 호출 하 여 모든 클라이언트에 메시지를 보냅니다.

**Send** 메서드는 다음과 같은 몇 가지 허브 개념을 보여 줍니다.

- 클라이언트에서 호출할 수 있도록 허브에 공용 메서드를 선언 합니다.
- **SignalR** 동적 속성을 사용 하 여이 허브에 연결 된 모든 클라이언트에 액세스 합니다.
- 클라이언트 (예: `broadcastMessage` 함수)에서 jQuery 함수를 호출 하 여 클라이언트를 업데이트 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR 및 jQuery

코드 샘플의 HTML 페이지에서는 SignalR jQuery 라이브러리를 사용 하 여 SignalR hub와 통신 하는 방법을 보여 줍니다. 코드의 필수 작업은 허브를 참조 하도록 프록시를 선언 하 고, 서버에서 클라이언트에 콘텐츠를 푸시하는 데 호출할 수 있는 함수를 선언 하 고, 허브로 메시지를 보내기 위한 연결을 시작 하는 것입니다.

다음 코드는 허브에 대 한 프록시를 선언 합니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> JQuery에서 서버 클래스 및 해당 멤버에 대 한 참조는 카멜식 대/소문자로 되어 있습니다. 코드 샘플은 jQuery의 C# **ChatHub** 클래스를 **ChatHub**로 참조 합니다.

다음 코드는 스크립트에서 콜백 함수를 만드는 방법입니다. 서버의 허브 클래스는이 함수를 호출 하 여 각 클라이언트에 콘텐츠 업데이트를 푸시합니다. 콘텐츠를 표시 하기 전에 HTML로 인코딩하는 두 줄은 선택 사항이 며 스크립트 삽입을 방지 하는 간단한 방법을 보여 줍니다.

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

다음 코드에서는 허브와의 연결을 여는 방법을 보여 줍니다. 이 코드는 연결을 시작한 다음 HTML 페이지의 **보내기** 단추에서 클릭 이벤트를 처리 하는 함수를 전달 합니다.

> [!NOTE]
> 이 방법을 사용 하면 이벤트 처리기가 실행 되기 전에 연결이 설정 됩니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>다음 단계

SignalR는 실시간 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다. 또한 ASP.NET 응용 프로그램에 SignalR를 추가 하는 방법, 허브 클래스를 만드는 방법 및 허브에서 메시지를 보내고 받는 방법에 대 한 몇 가지 SignalR 개발 작업을 배웠습니다.

이 자습서의 샘플 응용 프로그램 또는 인터넷을 통해 사용할 수 있는 다른 SignalR 응용 프로그램을 호스팅 공급자에 게 배포할 수 있습니다. Microsoft는 무료 [Windows Azure 평가판 계정](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)에 최대 10 개의 웹 사이트를 위한 무료 웹 호스팅을 제공 합니다. 샘플 SignalR 응용 프로그램을 배포 하는 방법에 대 한 연습은 [Windows Azure 웹 사이트로 SignalR 시작 샘플 게시](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx)를 참조 하십시오. Microsoft Azure 웹 사이트에 Visual Studio 웹 프로젝트를 배포 하는 방법에 대 한 자세한 내용은 [Windows Azure 웹 사이트에 ASP.NET 응용 프로그램 배포](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)를 참조 하십시오. (참고: WebSocket 전송은 현재 Windows Azure 웹 사이트에 대해 지원 되지 않습니다. WebSocket 전송을 사용할 수 없는 경우 SignalR는 [SignalR 소개 항목](index.md)의 전송 섹션에 설명 된 대로 사용 가능한 다른 전송을 사용 합니다.

고급 SignalR 개발 개념에 대 한 자세한 내용은 다음 사이트에서 SignalR 소스 코드 및 리소스를 참조 하세요.

- [SignalR 프로젝트](http://signalr.net)
- [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
