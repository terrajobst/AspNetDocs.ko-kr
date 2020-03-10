---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: SignalR 1.x를 사용 하는 높은 빈도 실시간 Microsoft Docs
author: bradygaster
description: 이 자습서에서는 ASP.NET SignalR를 사용 하 여 높은 빈도의 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 빈도가 높은 메시징 ...
ms.author: bradyg
ms.date: 04/16/2013
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: e37e63a410952ec170cbbaadeeb54eae7e82b3b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505715"
---
# <a name="high-frequency-realtime-with-signalr-1x"></a>SignalR 1.x를 사용하는 고주파수 실시간

[Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 자습서에서는 ASP.NET SignalR를 사용 하 여 높은 빈도의 메시징 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 이 경우 빈도가 높은 메시징은 고정 속도로 전송 되는 업데이트를 의미 합니다. 이 응용 프로그램의 경우 최대 10 개의 메시지가 1 초입니다.
> 
> 이 자습서에서 만들 응용 프로그램은 사용자가 끌 수 있는 셰이프를 표시 합니다. 그러면 연결 된 다른 모든 브라우저의 셰이프 위치가 시간 업데이트를 사용 하 여 끌어 온 모양의 위치와 일치 하도록 업데이트 됩니다.
> 
> 이 자습서에 소개 된 개념에는 실시간 게임과 기타 시뮬레이션 응용 프로그램의 응용 프로그램이 있습니다.
> 
> 자습서에 대 한 의견을 환영 합니다. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com)에 게시할 수 있습니다.

## <a name="overview"></a>개요

이 자습서에서는 다른 브라우저와 개체의 상태를 실시간으로 공유 하는 응용 프로그램을 만드는 방법을 보여 줍니다. 만들 응용 프로그램을 MoveShape 이라고 합니다. MoveShape 페이지에는 사용자가 끌 수 있는 HTML Div 요소가 표시 됩니다. 사용자가 Div를 끌면 새 위치가 서버에 전송 되 고, 그 다음에는 연결 된 다른 모든 클라이언트가 일치 하도록 셰이프 위치를 업데이트 하는 것을 알려 줍니다.

![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

이 자습서에서 만든 응용 프로그램은 Damian Edwards 데모를 기반으로 합니다. 이 데모를 포함 하는 비디오는 [여기](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)에서 볼 수 있습니다.

이 자습서에서는 셰이프를 끌 때 발생 하는 각 이벤트에서 SignalR 메시지를 보내는 방법을 보여 줍니다. 그러면 연결 된 각 클라이언트는 메시지를 받을 때마다 셰이프의 로컬 버전 위치를 업데이트 합니다.

응용 프로그램은이 메서드를 사용 하 여 작동 하는 동안에는 전송 되는 메시지 수에 대 한 상한 제한이 없기 때문에 권장 되는 프로그래밍 모델이 아닙니다. 따라서 클라이언트와 서버에서 메시지와 성능이 저하 될 수 있습니다. . 셰이프를 각 메서드에서 즉시 이동 하는 것이 아니라 각 새 위치로 이동 하는 것이 아니라 클라이언트에서 표시 되는 애니메이션도 연결 되지 않습니다. 자습서의 뒷부분에 나오는 섹션에서는 클라이언트 또는 서버에서 메시지를 전송 하는 최대 속도를 제한 하는 타이머 함수를 만드는 방법과 위치 간에 셰이프를 부드럽게 이동 하는 방법을 보여 줍니다. 이 자습서에서 만든 응용 프로그램의 최종 버전은 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)에서 다운로드할 수 있습니다.

이 자습서에는 다음과 같은 섹션이 포함 되어 있습니다.

- [필수 구성 요소](#prerequisites)
- [프로젝트 만들기](#createtheproject)
- [ASP.NET SignalR 및 JQuery NuGet 패키지를 추가 합니다.](#nugetpackages)
- [기본 응용 프로그램 만들기](#baseapp)
- [클라이언트 루프 추가](#clientloop)
- [서버 루프 추가](#serverloop)
- [클라이언트에서 부드러운 애니메이션 추가](#animation)
- [추가 단계](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에는 Visual Studio 2012 또는 Visual Studio 2010이 필요 합니다. Visual Studio 2010을 사용 하는 경우 프로젝트는 .NET Framework 4.5이 아닌 .NET Framework 4를 사용 합니다.

Visual Studio 2012을 사용 하는 경우 [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)를 설치 하는 것이 좋습니다. 이 업데이트에는 게시, 새 기능 및 새 템플릿과 같은 새로운 기능이 포함 되어 있습니다.

Visual Studio 2010을 사용 하는 경우 [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 이 설치 되어 있는지 확인 합니다.

<a id="createtheproject"></a>

## <a name="create-the-project"></a>프로젝트 만들기

이 섹션에서는 Visual Studio에서 프로젝트를 만듭니다.

1. **파일** 메뉴에서 **새 프로젝트**를 클릭합니다.
2. **새 프로젝트** 대화 상자에서 **템플릿** 을 확장 **C#** 하 고 **웹**을 선택 합니다.
3. **ASP.NET Empty 웹 응용 프로그램** 템플릿을 선택 하 고 프로젝트 이름을 *MoveShapeDemo*로 선택한 다음 **확인**을 클릭 합니다.

    ![새 프로젝트 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a>SignalR 및 JQuery NuGet 패키지를 추가 합니다.

NuGet 패키지를 설치 하 여 프로젝트에 SignalR 기능을 추가할 수 있습니다. 이 자습서에서는 또한 셰이프를 끌어서 애니메이션 효과를 주는 데 사용할 수 있도록 JQuery 패키지를 사용 합니다.

1. 도구 |를 클릭 합니다.  **NuGet 패키지 관리자 | 패키지 관리자 콘솔**.
2. 패키지 관리자에서 다음 명령을 입력 합니다.

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    SignalR 패키지는 다양 한 NuGet 패키지를 종속성으로 설치 합니다. 설치가 완료 되 면 ASP.NET 응용 프로그램에서 SignalR를 사용 하는 데 필요한 모든 서버 및 클라이언트 구성 요소가 있습니다.
3. 패키지 관리자 콘솔에 다음 명령을 입력 하 여 JQuery 및 JQuery. n u l l 패키지를 설치 합니다.

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a>기본 응용 프로그램 만들기

이 섹션에서는 각 마우스 이동 이벤트 동안 셰이프의 위치를 서버로 보내는 브라우저 응용 프로그램을 만듭니다. 그런 다음 서버는 수신 될 때 연결 된 다른 모든 클라이언트에이 정보를 브로드캐스트합니다. 이후 섹션에서이 응용 프로그램을 확장 합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **클래스 ...** 를 차례로 선택 합니다. 클래스 이름을 **MoveShapeHub** 로 하 고 **추가**를 클릭 합니다.
2. 새 **MoveShapeHub** 클래스의 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    위의 `MoveShapeHub` 클래스는 SignalR hub의 구현입니다. [SignalR 시작](index.md) 자습서에서와 같이 허브에는 클라이언트가 직접 호출 하는 메서드가 있습니다. 이 경우 클라이언트는 셰이프의 새 X 및 Y 좌표를 포함 하는 개체를 서버에 전송 합니다. 그러면 연결 된 다른 모든 클라이언트에 브로드캐스트 됩니다. SignalR는 JSON을 사용 하 여이 개체를 자동으로 직렬화 합니다.

    클라이언트에 전송 되는 개체 (`ShapeModel`)에는 셰이프의 위치를 저장 하는 멤버가 포함 되어 있습니다. 서버에 있는 개체의 버전에는 저장 되는 클라이언트 데이터를 추적 하는 멤버도 포함 되어 있으므로 지정 된 클라이언트는 자신의 데이터를 전송 하지 않습니다. 이 멤버는 `JsonIgnore` 특성을 사용 하 여 serialize 되어 클라이언트에 전송 되지 않도록 합니다.
3. 다음으로, 응용 프로그램이 시작 될 때 허브를 설정 합니다. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **추가 |를 클릭 합니다. 전역 응용 프로그램 클래스**입니다. *Global* 의 기본 이름을 그대로 적용 하 고 **확인을**클릭 합니다.

    ![전역 응용 프로그램 클래스 추가](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. Global.asax.cs 클래스에서 제공 된 **using** 문 뒤에 다음 `using` 문을 추가 합니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. SignalR에 대 한 기본 경로를 등록 하려면 전역 클래스의 `Application_Start` 메서드에 다음 코드 줄을 추가 합니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    Global.asax 파일은 다음과 같습니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. 다음으로 클라이언트를 추가 합니다. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **추가 |를 클릭 합니다. 새 항목**입니다. **새 항목 추가** 대화 상자에서 **Html 페이지**를 선택 합니다. 페이지에 적절 한 이름 (예: **.html**)을 지정 하 고 **추가**를 클릭 합니다.
7. **솔루션 탐색기**에서 방금 만든 페이지를 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 클릭 합니다.
8. HTML 페이지의 기본 코드를 다음 코드 조각으로 바꿉니다.

    > [!NOTE]
    > 아래의 스크립트 참조가 Scripts 폴더의 프로젝트에 추가 된 패키지와 일치 하는지 확인 합니다. Visual Studio 2010에서는 프로젝트에 추가 된 JQuery 및 SignalR 버전이 아래 버전 번호와 일치 하지 않을 수 있습니다.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    위의 HTML 및 JavaScript 코드는 Shape 라는 빨간 Div를 만들고, jQuery 라이브러리를 사용 하 여 셰이프의 끌기 동작을 사용 하도록 설정 하 고, 셰이프의 `drag` 이벤트를 사용 하 여 셰이프의 위치를 서버로 보냅니다.
9. F5 키를 눌러 응용 프로그램을 시작 합니다. 페이지의 URL을 복사 하 여 두 번째 브라우저 창에 붙여넣습니다. 셰이프를 브라우저 창 중 하나로 끌어 옵니다. 다른 브라우저 창의 셰이프는 이동 해야 합니다.

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a>클라이언트 루프 추가

모든 마우스 이동 이벤트에서 셰이프의 위치를 전송 하면 불필요 한 양의 네트워크 트래픽이 생성 되므로 클라이언트의 메시지를 제한 해야 합니다. Javascript `setInterval` 함수를 사용 하 여 고정 속도로 서버에 새 위치 정보를 보내는 루프를 설정 합니다. 이 루프는 게임 또는 기타 시뮬레이션의 모든 기능을 구동 하는 반복적인 호출 함수 인 "게임 루프"를 매우 기본적으로 표현한 것입니다.

1. HTML 페이지의 클라이언트 코드를 다음 코드 조각과 일치 하도록 업데이트 합니다.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    위의 업데이트는 고정 된 빈도로 호출 되는 `updateServerModel` 함수를 추가 합니다. 이 함수는 `moved` 플래그가 보낼 새 위치 데이터가 있음을 나타내는 경우 항상 서버에 위치 데이터를 보냅니다.
2. F5 키를 눌러 응용 프로그램을 시작 합니다. 페이지의 URL을 복사 하 여 두 번째 브라우저 창에 붙여넣습니다. 셰이프를 브라우저 창 중 하나로 끌어 옵니다. 다른 브라우저 창의 셰이프는 이동 해야 합니다. 서버로 전송 되는 메시지 수가 제한 되기 때문에 이전 섹션에서 애니메이션은 부드러운 모양으로 표시 되지 않습니다.

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a>서버 루프 추가

현재 응용 프로그램에서는 서버에서 클라이언트로 전송 되는 메시지가 수신 되는 횟수 만큼 이동 합니다. 이는 클라이언트에 표시 된 것과 비슷한 문제를 표시 합니다. 메시지는 필요한 것 보다 더 자주 전송 될 수 있으며, 그에 따라 연결이 유발 될 수 있습니다. 이 섹션에서는 보내는 메시지의 요금을 제한 하는 타이머를 구현 하도록 서버를 업데이트 하는 방법을 설명 합니다.

1. `MoveShapeHub.cs` 내용을 다음 코드 조각으로 바꿉니다.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    위의 코드는 클라이언트를 확장 하 여 `Broadcaster` 클래스를 추가 합니다 .이 클래스는 .NET framework에서 `Timer` 클래스를 사용 하 여 나가는 메시지를 제한 합니다.

    허브 자체는 일시적 이므로 (필요할 때마다 만들어짐) `Broadcaster` 단일 항목으로 생성 됩니다. 초기화 지연 (.NET 4에 도입 됨)은 필요할 때까지 생성을 지연 하 여 타이머를 시작 하기 전에 첫 번째 허브 인스턴스가 완전히 만들어졌는지 확인 하는 데 사용 됩니다.

    클라이언트의 `UpdateShape` 함수에 대 한 호출은 허브의 `UpdateModel` 메서드에서 이동 하 여 들어오는 메시지가 수신 될 때마다 즉시 호출 되지 않도록 합니다. 대신 클라이언트에 대 한 메시지는 `Broadcaster` 클래스 내에서 `_broadcastLoop` 타이머에 의해 관리 되는 초당 25 개의 호출 속도로 전송 됩니다.

    마지막으로, 허브에서 직접 클라이언트 메서드를 호출 하는 대신 `Broadcaster` 클래스가 `GlobalHost`를 사용 하 여 현재 운영 허브 (`_hubContext`)에 대 한 참조를 가져와야 합니다.
2. F5 키를 눌러 응용 프로그램을 시작 합니다. 페이지의 URL을 복사 하 여 두 번째 브라우저 창에 붙여넣습니다. 셰이프를 브라우저 창 중 하나로 끌어 옵니다. 다른 브라우저 창의 셰이프는 이동 해야 합니다. 브라우저에는 이전 섹션의 차이점이 표시 되지 않지만 클라이언트에 전송 되는 메시지 수가 제한 됩니다.

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a>클라이언트에서 부드러운 애니메이션 추가

응용 프로그램은 거의 완전 하지만 서버 메시지에 대 한 응답으로 이동 하는 클라이언트의 셰이프 동작에서 더 많은 개선을 수행할 수 있습니다. 셰이프 위치를 서버에서 제공 하는 새 위치로 설정 하는 대신 JQuery UI 라이브러리의 `animate` 함수를 사용 하 여 현재 위치와 새 위치 간에 셰이프를 부드럽게 이동 합니다.

1. 아래 강조 표시 된 코드 처럼 보이도록 클라이언트의 `updateShape` 메서드를 업데이트 합니다.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    위의 코드는 애니메이션 간격 (이 경우 100 밀리초) 동안 서버에서 제공 하는 새 위치에서 이전 위치까지 셰이프를 이동 합니다. 셰이프를 실행 하는 모든 이전 애니메이션은 새 애니메이션이 시작 되기 전에 지워집니다.
2. F5 키를 눌러 응용 프로그램을 시작 합니다. 페이지의 URL을 복사 하 여 두 번째 브라우저 창에 붙여넣습니다. 셰이프를 브라우저 창 중 하나로 끌어 옵니다. 다른 브라우저 창의 셰이프는 이동 해야 합니다. 들어오는 메시지 마다 한 번만 설정 하는 것이 아니라 시간이 지남에 따라 이동이 보간된 경우 다른 창에서 셰이프의 이동이 jerky 더 작은 수준으로 표시 됩니다.

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a>추가 단계

이 자습서에서는 클라이언트와 서버 간에 높은 빈도의 메시지를 전송 하는 SignalR 응용 프로그램을 프로그래밍 하는 방법에 대해 알아보았습니다. 이 통신 패러다임은 [SignalR를 사용 하 여 만든 ShootR 게임과](http://shootr.signalr.net)같이 온라인 게임 및 기타 시뮬레이션을 개발 하는 데 유용 합니다.

이 자습서에서 만든 전체 응용 프로그램은 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)에서 다운로드할 수 있습니다.

SignalR 개발 개념에 대해 자세히 알아보려면 SignalR 원본 코드 및 리소스에 대 한 다음 사이트를 방문 하세요.

- [SignalR 프로젝트](http://signalr.net)
- [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
