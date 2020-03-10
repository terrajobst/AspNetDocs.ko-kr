---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: '자습서: SignalR 1.x 및 MVC 4 시작 | Microsoft Docs'
author: bradygaster
description: ASP.NET SignalR 및 ASP.NET MVC 4를 사용 하 여 실시간 채팅 응용 프로그램을 빌드합니다.
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468071"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a>자습서: SignalR 1.x 및 MVC 4 시작

[Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 자습서에서는 ASP.NET SignalR를 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. MVC 4 응용 프로그램에 SignalR를 추가 하 고 메시지를 보내고 표시 하는 채팅 보기를 만듭니다.

## <a name="overview"></a>개요

이 자습서에서는 ASP.NET SignalR 및 ASP.NET MVC 4를 사용 하 여 실시간 웹 응용 프로그램을 개발 하는 방법을 소개 합니다. 이 자습서에서는 [SignalR 시작 자습서](tutorial-getting-started-with-signalr.md)와 동일한 채팅 응용 프로그램 코드를 사용 하지만 인터넷 템플릿을 기반으로 하는 MVC 4 응용 프로그램에 추가 하는 방법을 보여 줍니다.

이 항목에서는 다음과 같은 SignalR 개발 작업에 대해 알아봅니다.

- SignalR 라이브러리를 MVC 4 응용 프로그램에 추가 합니다.
- 클라이언트에 콘텐츠를 푸시하는 허브 클래스 만들기
- 웹 페이지에서 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 허브에서 업데이트를 표시 합니다.

다음 스크린샷은 브라우저에서 실행 되는 완료 된 채팅 응용 프로그램을 보여 줍니다.

![채팅 인스턴스](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

섹션이

- [프로젝트 설정](#setup)
- [샘플 실행](#run)
- [코드 검사](#code)
- [다음 단계](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>프로젝트 설정

필수 조건:

- Visual Studio 2010 SP1, Visual Studio 2012 또는 Visual Studio 2012 Express Visual Studio가 없는 경우 [ASP.NET 다운로드](https://www.asp.net/downloads) 를 참조 하 여 무료 visual Studio 2012 Express 개발 도구를 다운로드 하세요.
- Visual Studio 2010의 경우 [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)를 설치 합니다.

이 섹션에서는 ASP.NET MVC 4 응용 프로그램을 만들고, SignalR 라이브러리를 추가 하 고, 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.

1. 1. Visual Studio에서 ASP.NET MVC 4 응용 프로그램을 만들고, 이름을 SignalRChat로, 확인을 클릭 합니다.

        > [!NOTE]
        > VS 2010의 프레임 워크 버전 드롭다운 컨트롤에서 **.NET Framework 4** 를 선택 합니다. SignalR 코드는 .NET Framework 버전 4 및 4.5에서 실행 됩니다.

        ![Mvc 웹 만들기](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. 인터넷 응용 프로그램 템플릿을 선택 하 고 **단위 테스트 프로젝트를 만드는**옵션을 선택 취소 한 다음 확인을 클릭 합니다.

         ![Mvc 인터넷 사이트 만들기](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. **패키지 관리자 콘솔 > NuGet 패키지 관리자 > 도구** 를 열고 다음 명령을 실행 합니다. 이 단계에서는 SignalR 기능을 사용할 수 있도록 하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. **솔루션 탐색기** 에서 Scripts 폴더를 확장 합니다. SignalR에 대 한 스크립트 라이브러리는 프로젝트에 추가 되었습니다.

         ![라이브러리 참조](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 폴더**를 추가 하 고 **허브**라는 새 폴더를 추가 합니다.
      6. **허브** 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가를 클릭 합니다.  **클래스**를 만들고 ChatHub.cs 이라는 새 C# 클래스를만듭니다. 모든 클라이언트에 메시지를 보내는 SignalR 서버 허브로이 클래스를 사용 합니다.

> [!NOTE]
> Visual Studio 2012을 사용 하 고 [ASP.NET 및 Web Tools 2012.2 업데이트](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation)를 설치한 경우 새 SignalR 항목 템플릿을 사용 하 여 허브 클래스를 만들 수 있습니다. 이렇게 하려면 **허브** 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가를 클릭 합니다.  **새 항목**에서 **SignalR Hub 클래스 (v1)** 를 선택 하 고 클래스 이름을 **ChatHub.cs**로 선택 합니다.

1. **ChatHub** 클래스의 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. 프로젝트에 대 한 global.asax 파일을 열고 메서드 `RouteTable.Routes.MapHubs();`에 대 한 호출을 `Application_Start` 메서드의 코드의 첫 번째 줄로 **추가 합니다.** 이 코드는 SignalR hubs의 기본 경로를 등록 하며 다른 경로를 등록 하기 전에 호출 해야 합니다. 완료 된 `Application_Start` 메서드는 다음 예제와 같습니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. **Controllers/HomeController** 에 있는 `HomeController` 클래스를 편집 하 고 클래스에 다음 메서드를 추가 합니다. 이 메서드는 이후 단계에서 만들 **채팅** 보기를 반환 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. 방금 만든 `Chat` 메서드 내에서 마우스 오른쪽 단추를 클릭 하 고 **뷰 추가** 를 클릭 하 여 새 뷰 파일을 만듭니다.
5. **보기 추가** 대화 상자에서 **레이아웃 또는 마스터 페이지** (다른 확인란의 선택을 취소)를 사용 하도록 확인란을 선택 했는지 확인 한 다음 **추가**를 클릭 합니다.

    ![보기 추가](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. **Chat. cshtml**이라는 새 뷰 파일을 편집 합니다. &lt;h2&gt; 태그 뒤에 다음 &lt;div&gt; 섹션 및 `@section scripts` 코드 블록을 페이지에 붙여 넣습니다. 이 스크립트를 사용 하면 페이지에서 채팅 메시지를 보내고 서버에서 메시지를 표시할 수 있습니다. 채팅 보기의 전체 코드는 다음 코드 블록에 표시 됩니다.

    > [!IMPORTANT]
    > SignalR 및 기타 스크립트 라이브러리를 Visual Studio 프로젝트에 추가 하는 경우 패키지 관리자는이 항목에 표시 된 버전 보다 최신 버전의 스크립트를 설치할 수 있습니다. 코드의 스크립트 참조가 프로젝트에 설치 된 스크립트 라이브러리 버전과 일치 하는지 확인 합니다.

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. 프로젝트에 대 한 **모든를 저장** 합니다.

<a id="run"></a>

## <a name="run-the-sample"></a>샘플 실행

1. F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다.
2. 브라우저 주소 줄에서 프로젝트에 대 한 기본 페이지의 URL에 **/home/chat** 를 추가 합니다. 채팅 페이지가 브라우저 인스턴스에 로드 되 고 사용자 이름을 입력 하 라는 메시지가 표시 됩니다.

    ![사용자 이름 입력](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. 사용자 이름을 입력합니다.
4. 브라우저의 주소 줄에서 URL을 복사 하 고이를 사용 하 여 두 개의 브라우저 인스턴스를 엽니다. 각 브라우저 인스턴스에서 고유한 사용자 이름을 입력 합니다.
5. 각 브라우저 인스턴스에서 주석을 추가 하 고 **보내기**를 클릭 합니다. 주석은 모든 브라우저 인스턴스에 표시 되어야 합니다.

    > [!NOTE]
    > 이 간단한 채팅 응용 프로그램은 서버에 대 한 토론 컨텍스트를 유지 하지 않습니다. 허브는 모든 현재 사용자에 게 주석을 브로드캐스트합니다. 나중에 채팅에 참여 하는 사용자는 연결 된 시간부터 추가 된 메시지를 볼 수 있습니다.
6. 다음 스크린샷은 브라우저에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.

    ![채팅 브라우저](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. **솔루션 탐색기**에서 실행 중인 응용 프로그램에 대 한 **스크립트 문서** 노드를 검사 합니다. Internet Explorer를 브라우저로 사용 하는 경우이 노드가 디버그 모드에서 표시 됩니다. SignalR 라이브러리가 런타임에 동적으로 생성 하는 **허브** 라는 스크립트 파일이 있습니다. 이 파일은 jQuery 스크립트와 서버측 코드 간의 통신을 관리 합니다. Internet Explorer 이외의 브라우저를 사용 하는 경우 동적 **허브** 파일을 직접 탐색 하 여 액세스할 수도 있습니다 (예: http://mywebsite/signalr/hubs).

    ![생성 된 허브 스크립트](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a>코드 검사

SignalR chat 응용 프로그램은 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 받는 두 가지 기본 SignalR 개발 작업을 보여 줍니다.

### <a name="signalr-hubs"></a>SignalR 허브

코드 샘플에서 **ChatHub** 클래스는 **SignalR** 클래스에서 파생 됩니다. **허브** 클래스에서 파생 하는 것은 SignalR 응용 프로그램을 빌드하는 데 유용한 방법입니다. 허브 클래스에서 공용 메서드를 만든 다음 웹 페이지의 jQuery 스크립트에서 해당 메서드를 호출 하 여 액세스할 수 있습니다.

채팅 코드에서 클라이언트는 **ChatHub** 메서드를 호출 하 여 새 메시지를 보냅니다. 그러면 허브는 **addNewMessageToPage**를 호출 하 여 모든 클라이언트에 메시지를 보냅니다.

**Send** 메서드는 다음과 같은 몇 가지 허브 개념을 보여 줍니다.

- 클라이언트에서 호출할 수 있도록 허브에 공용 메서드를 선언 합니다.
- **SignalR** 속성을 사용 하 여이 허브에 연결 된 모든 클라이언트에 액세스 합니다.
- 클라이언트 (예: `addNewMessageToPage` 함수)에서 jQuery 함수를 호출 하 여 클라이언트를 업데이트 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR 및 jQuery

코드 샘플의 SignalR jQuery 뷰 파일은 SignalR hub와 통신 하는 데 jQuery 라이브러리를 사용 **하는 방법을** 보여 줍니다. 코드의 필수 작업은 허브에 대해 자동 생성 된 프록시에 대 한 참조를 만들고, 서버에서 클라이언트에 콘텐츠를 푸시하는 데 사용할 수 있는 함수를 선언 하 고, 허브로 메시지를 보내기 위한 연결을 시작 하는 것입니다.

다음 코드는 허브에 대 한 프록시를 선언 합니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> JQuery에서 서버 클래스 및 해당 멤버에 대 한 참조는 카멜식 대/소문자로 되어 있습니다. 코드 샘플은 jQuery의 C# **ChatHub** 클래스를 **ChatHub**로 참조 합니다. 에서 C#와 같이 기존 파스칼식 대/소문자를 사용 하 여 jQuery에서 `ChatHub` 클래스를 참조 하려면 ChatHub.cs 클래스 파일을 편집 합니다. `Microsoft.AspNet.SignalR.Hubs` 네임 스페이스를 참조 하는 `using` 문을 추가 합니다. 그런 다음 `ChatHub` 클래스에 `HubName` 특성을 추가 합니다 (예: `[HubName("ChatHub")]`). 마지막으로 `ChatHub` 클래스에 대 한 jQuery 참조를 업데이트 합니다.

다음 코드에서는 스크립트에서 콜백 함수를 만드는 방법을 보여 줍니다. 서버의 허브 클래스는이 함수를 호출 하 여 각 클라이언트에 콘텐츠 업데이트를 푸시합니다. `htmlEncode` 함수에 대 한 선택적 호출에서는 스크립트 삽입을 방지 하는 방법으로 메시지 내용을 페이지에 표시 하기 전에 HTML로 인코딩하는 방법을 보여 줍니다.

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

다음 코드에서는 허브와의 연결을 여는 방법을 보여 줍니다. 이 코드는 연결을 시작한 다음 채팅 페이지의 **보내기** 단추에서 클릭 이벤트를 처리 하는 함수를 전달 합니다.

> [!NOTE]
> 이 방법을 사용 하면 이벤트 처리기가 실행 되기 전에 연결이 설정 됩니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>다음 단계

SignalR는 실시간 웹 응용 프로그램을 빌드하기 위한 프레임 워크입니다. 또한 ASP.NET 응용 프로그램에 SignalR를 추가 하는 방법, 허브 클래스를 만드는 방법 및 허브에서 메시지를 보내고 받는 방법에 대 한 몇 가지 SignalR 개발 작업을 배웠습니다.

고급 SignalR 개발 개념에 대 한 자세한 내용은 다음 사이트에서 SignalR 소스 코드 및 리소스를 참조 하세요.

- [SignalR 프로젝트](http://signalr.net)
- [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
