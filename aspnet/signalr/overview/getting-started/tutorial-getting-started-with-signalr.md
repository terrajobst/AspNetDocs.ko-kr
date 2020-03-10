---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: '자습서: SignalR 2를 사용한 실시간 채팅 | Microsoft Docs'
author: bradygaster
description: 이 자습서에는 SignalR을 사용하여 실시간 채팅 애플리케이션을 만드는 방법을 보여 줍니다. 빈 ASP.NET 웹 응용 프로그램에 SignalR를 추가 합니다.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431567"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a>자습서: SignalR 2를 사용 하 여 실시간 채팅

이 자습서에서는 SignalR를 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. 빈 ASP.NET 웹 응용 프로그램에 SignalR를 추가 하 고 메시지를 보내고 표시 하는 HTML 페이지를 만듭니다.

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 프로젝트 설정
> * 샘플 실행
> * 코드 검사

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>사전 요구 사항

* [ASP.NET 및 웹 개발](https://visualstudio.microsoft.com/downloads/) 워크로드가 있는 **Visual Studio 2017**

## <a name="set-up-the-project"></a>프로젝트 설정

이 섹션에서는 Visual Studio 2017 및 SignalR 2를 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만들고 SignalR를 추가 하 고 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.

1. Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.

    ![웹 만들기](tutorial-getting-started-with-signalr/_static/image2.png)

1. **New ASP.NET SignalRChat** 창에서 선택 된 상태로 두고 확인 **을 선택 합니다** .

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.

1. **새 항목 추가-SignalRChat**에서 **설치** > **Visual C#**  > **Web** > **SignalR** 을 선택한 다음 **SignalR Hub 클래스 (v2)** 를 선택 합니다.

1. 클래스 이름을 *ChatHub* 로 추가 하 고 프로젝트에 추가 합니다.

    이 단계에서는 *ChatHub.cs* 클래스 파일을 만들고 SignalR을 지 원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.

1. 새 *ChatHub.cs* 클래스 파일의 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.

1. **새 항목 추가-SignalRChat** **Visual C#**  > **웹** > **설치** 를 선택한 다음 **OWIN 시작 클래스**를 선택 합니다.

1. 클래스 이름을 *시작* 으로 하 고 프로젝트에 추가 합니다.

1. *Startup* 클래스의 기본 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 > **HTML 페이지** **추가** 를 선택 합니다.

1. 새 페이지 *인덱스* 의 이름을로 하 고 **확인을**선택 합니다.

1. **솔루션 탐색기**에서 사용자가 만든 HTML 페이지를 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다.

1. HTML 페이지의 기본 코드를 다음 코드로 바꿉니다.

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. **솔루션 탐색기**에서 **스크립트**를 확장 합니다.

    JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.

    > [!IMPORTANT]
    > 패키지 관리자가 SignalR 스크립트의 최신 버전을 설치 했을 수 있습니다.

1. 코드 블록의 스크립트 참조가 프로젝트의 스크립트 파일 버전에 해당 하는지 확인 합니다.

    원본 코드 블록의 스크립트 참조:

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. 일치 하지 않는 경우 *.html* 파일을 업데이트 합니다.

1. 메뉴 모음에서 **파일** > **모두 저장**을 선택 합니다.

## <a name="run-the-sample"></a>샘플 실행

1. 도구 모음에서 **스크립트 디버깅** 을 사용 하도록 설정 하 고 재생 단추를 선택 하 여 디버그 모드에서 샘플을 실행 합니다.

    ![사용자 이름 입력](tutorial-getting-started-with-signalr/_static/image3.png)

1. 브라우저가 열리면 채팅 id의 이름을 입력 합니다.

1. 브라우저에서 URL을 복사 하 여 다른 두 브라우저를 열고 Url을 주소 표시줄에 붙여넣습니다.

1. 각 브라우저에서 고유한 이름을 입력 합니다.

1. 이제 주석을 추가 하 고 **보내기**를 선택 합니다. 다른 브라우저에서 반복 합니다. 주석은 실시간으로 표시 됩니다.

    > [!NOTE]
    > 이 간단한 채팅 응용 프로그램은 서버에 대 한 토론 컨텍스트를 유지 하지 않습니다. 허브는 모든 현재 사용자에 게 주석을 브로드캐스트합니다. 나중에 채팅에 참여 하는 사용자는 연결 된 시간부터 추가 된 메시지를 볼 수 있습니다.

    채팅 응용 프로그램이 세 가지 브라우저에서 어떻게 실행 되는지 확인 합니다. Tom, Anand 및 김소미로 메시지를 보내면 모든 브라우저가 실시간으로 업데이트 됩니다.

    ![세 브라우저 모두 동일한 채팅 기록을 표시 합니다.](tutorial-getting-started-with-signalr/_static/image4.png)

1. **솔루션 탐색기**에서 실행 중인 응용 프로그램에 대 한 **스크립트 문서** 노드를 검사 합니다. SignalR 라이브러리가 런타임에 생성 하는 *허브* 라는 스크립트 파일이 있습니다. 이 파일은 jQuery 스크립트와 서버측 코드 간의 통신을 관리 합니다.

    ![스크립트 문서 노드의 자동 생성 된 허브 스크립트](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a>코드 검사

SignalRChat 응용 프로그램은 두 가지 기본 SignalR 개발 작업을 보여 줍니다. 허브를 만드는 방법을 보여 줍니다. 서버는 주 조정 개체로 해당 허브를 사용 합니다. 허브는 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 받습니다.

### <a name="signalr-hubs-in-the-chathubcs"></a>ChatHub.cs의 SignalR Hubs

위의 코드 샘플에서 `ChatHub` 클래스는 `Microsoft.AspNet.SignalR.Hub` 클래스에서 파생 됩니다. `Hub` 클래스에서 파생 하는 것은 SignalR 응용 프로그램을 빌드하는 데 유용한 방법입니다. 허브 클래스에서 공용 메서드를 만든 다음 웹 페이지의 스크립트에서 호출 하 여 해당 메서드를 사용할 수 있습니다.

채팅 코드에서 클라이언트는 `ChatHub.Send` 메서드를 호출 하 여 새 메시지를 보냅니다. 그런 다음 허브는 `Clients.All.broadcastMessage`를 호출 하 여 모든 클라이언트에 메시지를 보냅니다.

`Send` 메서드는 다음과 같은 몇 가지 허브 개념을 보여 줍니다.

* 클라이언트에서 호출할 수 있도록 허브에 공용 메서드를 선언 합니다.

* `Microsoft.AspNet.SignalR.Hub.Clients` 동적 속성을 사용 하 여이 허브에 연결 된 모든 클라이언트와 통신 합니다.

* 클라이언트에서 함수 (예: `broadcastMessage` 함수)를 호출 하 여 클라이언트를 업데이트 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a>SignalR 및 jQuery의 인덱스. html

코드 샘플의 *SignalR 페이지는* SignalR 허브와 통신 하는 데 jQuery 라이브러리를 사용 하는 방법을 보여 줍니다. 이 코드는 여러 중요 한 작업을 수행 합니다. 허브를 참조 하는 프록시를 선언 하 고, 서버에서 클라이언트에 콘텐츠를 푸시하는 데 호출할 수 있는 함수를 선언 하 고, 허브에 메시지를 보내기 위한 연결을 시작 합니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> JavaScript에서 서버 클래스 및 해당 멤버에 대 한 참조는 camelCase 이어야 합니다. 코드 샘플은 `chatHub`로 C# JavaScript의 *ChatHub* 클래스를 참조 합니다.

이 코드 블록에서는 스크립트에서 콜백 함수를 만듭니다.

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

서버의 허브 클래스는이 함수를 호출 하 여 각 클라이언트에 콘텐츠 업데이트를 푸시합니다. 콘텐츠를 표시 하기 전에 콘텐츠를 HTML로 인코딩하는 두 줄은 선택 사항이 며 스크립트 삽입을 방지 하는 좋은 방법을 보여 줍니다.

이 코드는 허브와의 연결을 엽니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> 이 방법을 사용 하면 이벤트 처리기가 실행 되기 전에 코드에서 연결을 설정 합니다.

이 코드는 연결을 시작한 다음 HTML 페이지의 **보내기** 단추에서 클릭 이벤트를 처리 하는 함수를 전달 합니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a>추가 리소스

SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

* [SignalR 프로젝트](http://signalr.net)

* [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행 합니다.

> [!div class="checklist"]
> * 프로젝트 설정
> * 샘플 실행
> * 코드 검사

SignalR 및 MVC 5를 사용 하는 방법을 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [SignalR 2 및 MVC 5](tutorial-getting-started-with-signalr-and-mvc.md)