---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: '자습서: SignalR 2 및 MVC 5와 실시간 채팅 | Microsoft Docs'
author: bradygaster
description: 이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. MVC 5 응용 프로그램에 SignalR를 추가 합니다.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600480"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a>자습서: SignalR 2 및 MVC 5와 실시간 채팅

이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. MVC 5 응용 프로그램에 SignalR를 추가 하 고 메시지를 보내고 표시 하는 채팅 보기를 만듭니다.

이 자습서에서는 다음과 같은 작업을 수행합니다.

> [!div class="checklist"]
> * 프로젝트 설정
> * 예제 실행
> * 코드 검사

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>Prerequisites

* **ASP.NET 및 웹 개발** 워크 로드가 포함 된 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) .

## <a name="set-up-the-project"></a>프로젝트 설정

이 섹션에서는 Visual Studio 2017 및 SignalR 2를 사용 하 여 빈 ASP.NET MVC 5 응용 프로그램을 만들고 SignalR 라이브러리를 추가 하 고 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.

1. Visual Studio에서 .NET Framework 4.5를 C# 대상으로 하는 ASP.NET 응용 프로그램을 만들고 이름을 SignalRChat로 지정 하 고 확인을 클릭 합니다.

    ![웹 만들기](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. **New ASP.NET 웹 응용 프로그램-SignalRMvcChat**에서 **MVC** 를 선택 하 고 **인증 변경**을 선택 합니다.

1. **변경 인증**에서 **인증 안 함** 을 선택 하 고 **확인**을 클릭 합니다.

    ![인증 안 함 선택](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. **New ASP.NET 웹 응용 프로그램-SignalRMvcChat**에서 **확인**을 선택 합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.

1. **새 항목 추가-SignalRChat**에서 **설치** > **Visual C#**  > **Web** > **SignalR** 을 선택한 다음 **SignalR Hub 클래스 (v2)** 를 선택 합니다.

1. 클래스 이름을 *ChatHub* 로 추가 하 고 프로젝트에 추가 합니다.

    이 단계에서는 *ChatHub.cs* 클래스 파일을 만들고 SignalR을 지 원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.

1. 새 *ChatHub.cs* 클래스 파일의 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 > **클래스** **추가** 를 선택 합니다.

1. 새 클래스의 이름을 *시작* 하 고 프로젝트에 추가 합니다.

1. *Startup.cs* 클래스 파일의 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. **솔루션 탐색기**에서 **컨트롤러** > **HomeController.cs**를 선택 합니다.

1. *HomeController.cs*에이 메서드를 추가 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    이 메서드는 이후 단계에서 만든 **채팅** 보기를 반환 합니다.

1. **솔루션 탐색기**에서 **보기** > **홈**을 마우스 오른쪽 단추로 클릭 하 고 >  **보기** **추가** 를 선택 합니다.

1. **보기 추가**에서 새 보기 **채팅** 의 이름을로 표시 하 고 **추가**를 선택 합니다.

1. **채팅** 의 내용을 다음 코드로 바꿉니다.

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. **솔루션 탐색기**에서 **스크립트**를 확장 합니다.

    JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.

    > [!IMPORTANT]
    > 패키지 관리자가 SignalR 스크립트의 최신 버전을 설치 했을 수 있습니다.

1. 코드 블록의 스크립트 참조가 프로젝트의 스크립트 파일 버전에 해당 하는지 확인 합니다.

    원본 코드 블록의 스크립트 참조:

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. 일치 하지 않는 경우에는 *cshtml* 파일을 업데이트 합니다.

1. 메뉴 모음에서 **파일** > **모두 저장**을 선택 합니다.

## <a name="run-the-sample"></a>샘플 실행

1. 도구 모음에서 **스크립트 디버깅** 을 사용 하도록 설정 하 고 재생 단추를 선택 하 여 디버그 모드에서 샘플을 실행 합니다.

    ![사용자 이름 입력](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. 브라우저가 열리면 채팅 id의 이름을 입력 합니다.

1. 브라우저에서 URL을 복사 하 여 다른 두 브라우저를 열고 Url을 주소 표시줄에 붙여넣습니다.

1. 각 브라우저에서 고유한 이름을 입력 합니다.

1. 이제 주석을 추가 하 고 **보내기**를 선택 합니다. 다른 브라우저에서 반복 합니다. 주석은 실시간으로 표시 됩니다.

    > [!NOTE]
    > 이 간단한 채팅 응용 프로그램은 서버에 대 한 토론 컨텍스트를 유지 하지 않습니다. 허브는 모든 현재 사용자에 게 주석을 브로드캐스트합니다. 나중에 채팅에 참여 하는 사용자는 연결 된 시간부터 추가 된 메시지를 볼 수 있습니다.

    채팅 응용 프로그램이 세 가지 브라우저에서 어떻게 실행 되는지 확인 합니다. Tom, Anand 및 김소미로 메시지를 보내면 모든 브라우저가 실시간으로 업데이트 됩니다.

    ![세 브라우저 모두 동일한 채팅 기록을 표시 합니다.](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. **솔루션 탐색기**에서 실행 중인 응용 프로그램에 대 한 **스크립트 문서** 노드를 검사 합니다. SignalR 라이브러리가 런타임에 생성 하는 *허브* 라는 스크립트 파일이 있습니다. 이 파일은 jQuery 스크립트와 서버측 코드 간의 통신을 관리 합니다.

    ![스크립트 문서 노드의 자동 생성 된 허브 스크립트](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a>코드 검사

SignalR chat 응용 프로그램은 두 가지 기본 SignalR 개발 작업을 보여 줍니다. 허브를 만드는 방법을 보여 줍니다. 서버는 주 조정 개체로 해당 허브를 사용 합니다. 허브는 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 받습니다.

### <a name="signalr-hubs-in-the-chathubcs"></a>ChatHub.cs의 SignalR Hubs

코드 샘플에서 `ChatHub` 클래스는 `Microsoft.AspNet.SignalR.Hub` 클래스에서 파생 됩니다. `Hub` 클래스에서 파생 하는 것은 SignalR 응용 프로그램을 빌드하는 데 유용한 방법입니다. 허브 클래스에서 공용 메서드를 만든 다음 웹 페이지의 스크립트에서 해당 메서드를 호출 하 여 액세스할 수 있습니다.

채팅 코드에서 클라이언트는 `ChatHub.Send` 메서드를 호출 하 여 새 메시지를 보냅니다. 그런 다음 허브는 `Clients.All.addNewMessageToPage`를 호출 하 여 모든 클라이언트에 메시지를 보냅니다.

`Send` 메서드는 다음과 같은 몇 가지 허브 개념을 보여 줍니다.

* 클라이언트에서 호출할 수 있도록 허브에 공용 메서드를 선언 합니다.

* `Microsoft.AspNet.SignalR.Hub.Clients` 동적 속성을 사용 하 여이 허브에 연결 된 모든 클라이언트와 통신 합니다.

* 클라이언트에서 함수 (예: `addNewMessageToPage` 함수)를 호출 하 여 클라이언트를 업데이트 합니다.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a>SignalR 및 jQuery 채팅. cshtml

코드 샘플의 SignalR jQuery 뷰 파일은 SignalR hub와 통신 하는 데 jQuery 라이브러리를 사용 *하는 방법을* 보여 줍니다.  이 코드는 여러 중요 한 작업을 수행 합니다. 허브에 대해 자동 생성 된 프록시에 대 한 참조를 만들고, 서버에서 클라이언트에 콘텐츠를 푸시하는 데 호출할 수 있는 함수를 선언 하 고, 허브로 메시지를 보내기 위한 연결을 시작 합니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> JavaScript에서 서버 클래스 및 해당 멤버에 대 한 참조는 camelCase에 있습니다. 코드 샘플에서는 JavaScript의 C# `ChatHub` 클래스를 `chatHub`으로 참조 합니다.

이 코드 블록에서는 스크립트에서 콜백 함수를 만듭니다.

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

서버의 허브 클래스는이 함수를 호출 하 여 각 클라이언트에 콘텐츠 업데이트를 푸시합니다. `htmlEncode` 함수에 대 한 선택적 호출에서는 메시지 내용을 페이지에 표시 하기 전에 HTML로 인코딩하는 방법을 보여 줍니다. 스크립트 삽입을 방지 하는 방법입니다.

이 코드는 허브와의 연결을 엽니다.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> 이 방법을 사용 하면 이벤트 처리기가 실행 되기 전에 연결을 설정할 수 있습니다.

이 코드는 연결을 시작한 다음 채팅 페이지의 **보내기** 단추에서 클릭 이벤트를 처리 하는 함수를 전달 합니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a>추가 자료

SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

* [SignalR 프로젝트](http://signalr.net)

* [SignalR GitHub 및 샘플](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음과 같은 작업을 수행합니다.

> [!div class="checklist"]
> * 프로젝트 설정
> * 샘플 실행
> * 코드 검사

ASP.NET SignalR 2를 사용 하 여 빈도가 높은 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [빈도가 높은 메시징이 있는 웹 앱](tutorial-high-frequency-realtime-with-signalr.md)