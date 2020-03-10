---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: '자습서: SignalR 2를 사용 하 여 빈도가 높은 실시간 앱 만들기 | Microsoft Docs'
author: bradygaster
description: 이 자습서에서는 ASP.NET SignalR를 사용 하 여 높은 빈도의 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450119"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a>자습서: SignalR 2를 사용 하 여 빈도가 높은 실시간 앱 만들기

이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 빈도가 높은 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 이 경우 "빈도가 높은 메시징"은 서버가 고정 속도로 업데이트를 보내는 것을 의미 합니다. 초당 최대 10 개의 메시지를 보냅니다.

사용자가 만드는 응용 프로그램은 사용자가 끌 수 있는 셰이프를 표시 합니다. 서버는 모든 연결 된 브라우저에서 셰이프의 위치를 업데이트 하 여 시간 업데이트를 사용 하는 끌어 온 모양의 위치와 일치 시킵니다.

이 자습서에 소개 된 개념에는 실시간 게임과 기타 시뮬레이션 응용 프로그램의 응용 프로그램이 있습니다.

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 프로젝트 설정
> * 기본 응용 프로그램 만들기
> * 앱이 시작 되 면 허브에 매핑
> * 클라이언트 추가
> * 앱 실행
> * 클라이언트 루프 추가
> * 서버 루프 추가
> * 부드러운 애니메이션 추가

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>사전 요구 사항

* [ASP.NET 및 웹 개발](https://visualstudio.microsoft.com/downloads/) 워크로드가 있는 **Visual Studio 2017**

## <a name="set-up-the-project"></a>프로젝트 설정

이 섹션에서는 Visual Studio 2017에서 프로젝트를 만듭니다.

이 섹션에서는 Visual Studio 2017을 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만들고 SignalR 및 jQuery. u s 라이브러리를 추가 하는 방법을 보여 줍니다.

1. Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.

    ![웹 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. **New ASP.NET 웹 응용 프로그램-MoveShapeDemo** 창에서 **비어 있음** 을 선택 된 상태로 두고 **확인**을 선택 합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.

1. **새 항목 추가-MoveShapeDemo**에서 **설치** > **Visual C#**  > **Web** > **SignalR** 을 선택한 다음 **SignalR Hub 클래스 (v2)** 를 선택 합니다.

1. 클래스 이름을 *MoveShapeHub* 로 추가 하 고 프로젝트에 추가 합니다.

    이 단계에서는 *MoveShapeHub.cs* 클래스 파일을 만듭니다. 동시에 SignalR를 지 원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.

1. **도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.

1. **패키지 관리자 콘솔**에서 다음 명령을 실행 합니다.

    ```console
    Install-Package jQuery.UI.Combined
    ```

    명령은 jQuery UI 라이브러리를 설치 합니다. 이를 사용 하 여 도형에 애니메이션 효과를 주는 데 사용 합니다.

1. **솔루션 탐색기**에서 스크립트 노드를 확장 합니다.

    ![스크립트 라이브러리 참조](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    JQuery, jQueryUI 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.

## <a name="create-the-base-application"></a>기본 응용 프로그램 만들기

이 섹션에서는 브라우저 응용 프로그램을 만듭니다. 앱은 각 마우스 이동 이벤트 동안 셰이프의 위치를 서버에 보냅니다. 서버는 연결 된 다른 모든 클라이언트에 실시간으로이 정보를 브로드캐스트합니다. 이 응용 프로그램에 대 한 자세한 내용은 이후 섹션에서 확인할 수 있습니다.

1. *MoveShapeHub.cs* 파일을 엽니다.

1. *MoveShapeHub.cs* 파일의 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. 파일을 저장합니다.

`MoveShapeHub` 클래스는 SignalR hub의 구현입니다. [SignalR 시작](tutorial-getting-started-with-signalr.md) 자습서에서와 같이 허브에는 클라이언트가 직접 호출 하는 메서드가 있습니다. 이 경우 클라이언트는 셰이프의 새 X 및 Y 좌표가 포함 된 개체를 서버에 보냅니다. 이러한 좌표는 연결 된 다른 모든 클라이언트에 브로드캐스트 됩니다. SignalR는 JSON을 사용 하 여이 개체를 자동으로 직렬화 합니다.

앱은 `ShapeModel` 개체를 클라이언트에 보냅니다. 이 클래스에는 셰이프의 위치를 저장할 멤버가 있습니다. 서버에 있는 개체의 버전에는 저장 되는 클라이언트 데이터를 추적 하는 멤버도 있습니다. 이 개체는 서버에서 클라이언트의 데이터를 다시 전송 하는 것을 방지 합니다. 이 멤버는 `JsonIgnore` 특성을 사용 하 여 응용 프로그램이 데이터를 직렬화 하 고 클라이언트로 다시 전송 하는 것을 방지 합니다.

## <a name="map-to-the-hub-when-app-starts"></a>앱이 시작 되 면 허브에 매핑

다음에는 응용 프로그램이 시작 될 때 허브에 대 한 매핑을 설정 합니다. SignalR 2에서는 OWIN startup 클래스를 추가 하 여 매핑을 만듭니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 항목**을 선택 합니다.

1. **새 항목 추가-MoveShapeDemo** **Visual C#**  > **웹** > **설치** 를 선택한 다음 **OWIN 시작 클래스**를 선택 합니다.

1. 클래스 이름을 *시작* 으로 하 고 **확인**을 선택 합니다.

1. *Startup.cs* 파일의 기본 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

OWIN startup 클래스는 앱이 `Configuration` 메서드를 실행할 때 `MapSignalR`를 호출 합니다. 앱은 `OwinStartup` 어셈블리 특성을 사용 하 여 OWIN의 시작 프로세스에 클래스를 추가 합니다.

## <a name="add-the-client"></a>클라이언트 추가

클라이언트에 대 한 HTML 페이지를 추가 합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 > **HTML 페이지** **추가** 를 선택 합니다.

1. 페이지의 이름을 **Default** 로 하 고 **확인을**선택 합니다.

1. **솔루션 탐색기**에서 *default.aspx* 를 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다.

1. *기본 .html* 파일의 기본 코드를 다음 코드로 바꿉니다.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. **솔루션 탐색기**에서 **스크립트**를 확장 합니다.

    JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.

    > [!IMPORTANT]
    > 패키지 관리자는 SignalR 스크립트의 최신 버전을 설치 합니다.

1. 프로젝트의 스크립트 파일 버전에 해당 하는 코드 블록의 스크립트 참조를 업데이트 합니다.

이 HTML 및 JavaScript 코드는 `shape`라는 빨간색 `div`를 만듭니다. JQuery 라이브러리를 사용 하 여 셰이프의 끌기 동작을 사용 하도록 설정 하 고 `drag` 이벤트를 사용 하 여 셰이프의 위치를 서버에 보냅니다.

## <a name="run-the-app"></a>앱 실행

앱을 실행 하 여 it 업무를 se'e 수 있습니다. 셰이프를 브라우저 창 주위로 끌면 셰이프는 다른 브라우저 에서도 이동 합니다.

1. 도구 모음에서 **스크립트 디버깅** 을 사용 하도록 설정 하 고 재생 단추를 선택 하 여 디버그 모드에서 응용 프로그램을 실행 합니다.

    ![디버깅 모드를 켜고 재생을 선택 하는 사용자의 스크린샷](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    오른쪽 위 모서리에 빨간색 모양의 브라우저 창이 열립니다.

1. 페이지의 URL을 복사 합니다.

1. 다른 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.

1. 셰이프를 브라우저 창 중 하나로 끌어 옵니다. 다른 브라우저 창의 모양은 다음과 같습니다.

응용 프로그램에서이 메서드를 사용 하는 동안에는 권장 되는 프로그래밍 모델이 아닙니다. 전송 되는 메시지 수에 대 한 상한 값은 없습니다. 결과적으로, 클라이언트와 서버는 메시지와 성능이 저하 됩니다. 또한 응용 프로그램은 클라이언트에서 연결이 끊긴 애니메이션을 표시 합니다. 이 jerky 애니메이션은 각 메서드에서 셰이프를 즉시 이동 하기 때문에 발생 합니다. 셰이프를 각 새 위치로 부드럽게 이동 하는 것이 더 좋습니다. 다음으로 이러한 문제를 해결 하는 방법을 알아봅니다.

## <a name="add-the-client-loop"></a>클라이언트 루프 추가

모든 마우스 이동 이벤트에서 셰이프의 위치를 보내면 불필요 한 양의 네트워크 트래픽이 생성 됩니다. 응용 프로그램은 클라이언트에서 메시지를 제한 해야 합니다.

Javascript `setInterval` 함수를 사용 하 여 고정 속도로 서버에 새 위치 정보를 보내는 루프를 설정 합니다. 이 루프는 "게임 루프"의 기본 표현입니다. 게임의 모든 기능을 구동 하는 반복적으로 호출 되는 함수입니다.

1. *기본 .html* 파일의 클라이언트 코드를 다음 코드로 바꿉니다.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > 스크립트 참조를 다시 바꾸어야 합니다. 프로젝트의 스크립트 버전과 일치 해야 합니다.

    이 새 코드는 `updateServerModel` 함수를 추가 합니다. 고정 된 빈도로 호출 됩니다. 함수는 `moved` 플래그가 보낼 새 위치 데이터가 있음을 나타내는 경우 항상 서버에 위치 데이터를 보냅니다.

1. 응용 프로그램을 시작 하려면 재생 단추를 선택 합니다.

1. 페이지의 URL을 복사 합니다.

1. 다른 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.

1. 셰이프를 브라우저 창 중 하나로 끌어 옵니다. 다른 브라우저 창의 모양은 다음과 같습니다.

앱은 서버로 전송 되는 메시지 수를 제한 처음에는 애니메이션이 부드러운 것으로 표시 되지 않습니다.

## <a name="add-the-server-loop"></a>서버 루프 추가

현재 응용 프로그램에서는 서버에서 클라이언트로 전송 된 메시지가 수신 되는 횟수 만큼 계속 이동 합니다. 이 네트워크 트래픽은 클라이언트에 표시 되는 것과 비슷한 문제를 표시 합니다.

앱은 필요한 것 보다 더 자주 메시지를 보낼 수 있습니다. 결과적으로 연결에 대 한 연결이 초과 될 수 있습니다. 이 섹션에서는 보내는 메시지의 요금을 제한 타이머를 추가 하도록 서버를 업데이트 하는 방법을 설명 합니다.

1. `MoveShapeHub.cs` 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. 재생 단추를 선택 하 여 응용 프로그램을 시작 합니다.

1. 페이지의 URL을 복사 합니다.

1. 다른 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.

1. 셰이프를 브라우저 창 중 하나로 끌어 옵니다.

이 코드는 클라이언트를 확장 하 여 `Broadcaster` 클래스를 추가 합니다. 새 클래스는 .NET framework의 `Timer` 클래스를 사용 하 여 나가는 메시지를 제한 합니다.

허브 자체가 일시적 이라고 이해 하는 것이 좋습니다. 필요할 때마다 생성 됩니다. 따라서 앱은 단일 항목으로 `Broadcaster`를 만듭니다. 지연 초기화를 사용 하 여 필요할 때까지 `Broadcaster`생성을 지연 시킵니다. 이렇게 하면 앱이 타이머를 시작 하기 전에 첫 번째 허브 인스턴스를 완전히 만듭니다.

그런 다음 클라이언트의 `UpdateShape` 함수에 대 한 호출이 허브의 `UpdateModel` 메서드에서 이동 합니다. 앱이 들어오는 메시지를 받을 때마다 즉시 더 이상 호출 되지 않습니다. 대신, 앱에서 초당 25 번의 호출 속도로 클라이언트에 메시지를 보냅니다. 프로세스는 `Broadcaster` 클래스 내에서 `_broadcastLoop` 타이머를 통해 관리 됩니다.

마지막으로, 허브에서 직접 클라이언트 메서드를 호출 하는 대신 `Broadcaster` 클래스가 현재 작동 하는 `_hubContext` 허브에 대 한 참조를 가져와야 합니다. `GlobalHost`를 사용 하 여 참조를 가져옵니다.

## <a name="add-smooth-animation"></a>부드러운 애니메이션 추가

응용 프로그램이 거의 완료 되었지만 한 가지 향상 된 기능을 만들 수 있습니다. 앱은 서버 메시지에 대 한 응답으로 클라이언트에서 셰이프를 이동 합니다. 서버에서 제공 하는 새 위치로 셰이프의 위치를 설정 하는 대신 JQuery UI 라이브러리의 `animate` 함수를 사용 합니다. 현재 위치와 새 위치 간에 셰이프를 매끄럽게 이동할 수 있습니다.

1. *기본 .html* 파일의 클라이언트 `updateShape` 메서드를 강조 표시 된 코드와 같이 업데이트 합니다.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. 재생 단추를 선택 하 여 응용 프로그램을 시작 합니다.

1. 페이지의 URL을 복사 합니다.

1. 다른 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.

1. 셰이프를 브라우저 창 중 하나로 끌어 옵니다.

다른 창에서 셰이프의 이동이 jerky 작은 것으로 나타납니다. 앱은 들어오는 메시지 마다 한 번만 설정 되는 것이 아니라 시간에 따라 이동 하는 동작을 보간합니다.

이 코드는 셰이프를 이전 위치에서 새 위치로 이동 합니다. 서버는 애니메이션 간격 과정에서 셰이프의 위치를 제공 합니다. 이 경우 100 밀리초입니다. 앱은 새 애니메이션을 시작 하기 전에 셰이프에서 실행 중인 이전 애니메이션을 모두 지웁니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a>추가 리소스

위에서 배운 통신 패러다임은 [SignalR를 사용 하 여 만든 ShootR 게임과](https://shootr.azurewebsites.net/)같이 온라인 게임 및 기타 시뮬레이션을 개발 하는 데 유용 합니다.

SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

* [SignalR 프로젝트](http://signalr.net)

* [SignalR GitHub 및 샘플](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 프로젝트 설정
> * 기본 응용 프로그램을 만듦
> * 앱이 시작 될 때 허브에 매핑됨
> * 클라이언트 추가
> * 앱 실행
> * 클라이언트 루프가 추가 됨
> * 서버 루프가 추가 됨
> * 부드러운 애니메이션 추가

ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [SignalR 2 및 서버 브로드캐스팅](tutorial-server-broadcast-with-signalr.md)