---
uid: signalr/overview/older-versions/scaleout-with-redis
title: SignalR 확장 with Redis (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431207"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a>Redis로 SignalR 규모 확장(SignalR 1.x)

사람, [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

이 자습서에서는 [Redis](http://redis.io/) 를 사용 하 여 별도의 두 IIS 인스턴스에 배포 된 SignalR 응용 프로그램을 통해 메시지를 분산 합니다.

Redis는 메모리 내 키-값 저장소입니다. 또한 게시/구독 모델을 사용 하는 메시징 시스템을 지원 합니다. SignalR Redis 후면판은 pub/sub 기능을 사용 하 여 메시지를 다른 서버로 전달 합니다.

![](scaleout-with-redis/_static/image1.png)

이 자습서에서는 다음 3 개의 서버를 사용 합니다.

- SignalR 응용 프로그램을 배포 하는 데 사용할 Windows를 실행 하는 두 대의 서버
- Redis를 실행 하는 데 사용할 Linux를 실행 하는 하나의 서버. 이 자습서의 스크린샷에서는 Ubuntu 12.04 TLS를 사용 했습니다.

사용할 물리적 서버가 세 대 이상 없는 경우 Hyper-v에서 Vm을 만들 수 있습니다. 또 다른 옵션은 Azure에서 Vm을 만드는 것입니다.

이 자습서에서는 공식 Redis 구현을 사용 하지만 MSOpenTech에서 [Redis의 Windows 포트](https://github.com/MSOpenTech/redis) 도 있습니다. 설정 및 구성은 서로 다르지만 단계는 동일 합니다.

> [!NOTE] 
> 
> SignalR 확장 with Redis는 Redis 클러스터를 지원 하지 않습니다.

## <a name="overview"></a>개요

자세한 자습서를 시작 하기 전에 수행할 작업에 대 한 간략 한 개요를 참조 하세요.

1. Redis를 설치 하 고 Redis 서버를 시작 합니다.
2. 응용 프로그램에 다음 NuGet 패키지를 추가 합니다. 

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR. Redis](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. SignalR 응용 프로그램을 만듭니다.
4. Global.asax에 다음 코드를 추가 하 여 후면판을 구성 합니다. 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a>Hyper-v의 Ubuntu

Windows Hyper-v를 사용 하 여 Windows Server에서 Ubuntu VM을 쉽게 만들 수 있습니다.

[http://www.ubuntu.com](http://www.ubuntu.com/)에서 Ubuntu ISO를 다운로드 합니다.

Hyper-v에서 새 VM을 추가 합니다. **가상 하드 디스크 연결** 단계에서 **가상 하드 디스크 만들기**를 선택 합니다.

![](scaleout-with-redis/_static/image2.png)

**설치 옵션** 단계에서 **이미지 파일 (.iso)** 을 선택 하 고 **찾아보기**를 클릭 한 다음 Ubuntu 설치 iso로 이동 합니다.

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a>Redis 설치

[http://redis.io/download](http://redis.io/download) 의 단계에 따라 Redis를 다운로드 하 고 빌드합니다.

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

그러면 `src` 디렉터리에 Redis 바이너리가 빌드됩니다.

기본적으로 Redis에는 암호가 필요 하지 않습니다. 암호를 설정 하려면 소스 코드의 루트 디렉터리에 있는 `redis.conf` 파일을 편집 합니다. 편집 하기 전에 파일의 백업 복사본을 만듭니다. `redis.conf`에 다음 지시문을 추가 합니다.

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

이제 Redis 서버를 시작 합니다.

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

Redis에서 수신 대기 하는 기본 포트인 포트 6379를 엽니다. 구성 파일에서 포트 번호를 변경할 수 있습니다.

## <a name="create-the-signalr-application"></a>SignalR 응용 프로그램 만들기

다음 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.

- [SignalR 시작 하기](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR 및 MVC 4 시작](tutorial-getting-started-with-signalr-and-mvc-4.md)

다음으로, Redis와의 확장을 지원 하도록 채팅 응용 프로그램을 수정 합니다. 먼저 SignalR Redis NuGet 패키지를 프로젝트에 추가 합니다. Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

그런 다음, Global.asax 파일을 엽니다. **응용 프로그램\_Start** 메서드에 다음 코드를 추가 합니다.

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- "server"는 Redis를 실행 하는 서버의 이름입니다.
- *포트* 는 포트 번호입니다.
- "password"는 redis 파일에서 정의한 암호입니다.
- "AppName"은 임의의 문자열입니다. SignalR는이 이름을 사용 하 여 Redis pub/sub 채널을 만듭니다.

다음은 그 예입니다.

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a>응용 프로그램 배포 및 실행

Windows Server 인스턴스를 준비 하 여 SignalR 응용 프로그램을 배포 합니다.

IIS 역할을 추가 합니다. WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.

![](scaleout-with-redis/_static/image5.png)

관리 서비스 ("관리 도구" 아래에 나열 됨)도 포함 합니다.

![](scaleout-with-redis/_static/image6.png)

**웹 배포 3.0을 설치 합니다.** IIS 관리자를 실행 하는 경우 Microsoft 웹 플랫폼을 설치 하 라는 메시지가 표시 되거나 [설치 관리자를 다운로드할](https://go.microsoft.com/fwlink/?LinkId=255386)수 있습니다. 플랫폼 설치 관리자에서 웹 배포을 검색 하 고 웹 배포 3.0를 설치 합니다.

![](scaleout-with-redis/_static/image7.png)

웹 관리 서비스가 실행 중인지 확인 합니다. 그렇지 않은 경우 서비스를 시작 합니다. Windows 서비스 목록에 웹 관리 서비스가 표시 되지 않으면 IIS 역할을 추가할 때 관리 서비스를 설치 했는지 확인 합니다.

기본적으로 웹 관리 서비스는 TCP 포트 8172에서 수신 합니다. Windows 방화벽에서 포트 8172에 TCP 트래픽을 허용 하는 새 인바운드 규칙을 만듭니다. 자세한 내용은 [방화벽 규칙 구성](https://technet.microsoft.com/library/dd448559(WS.10).aspx)을 참조 하세요. (Azure에서 Vm을 호스트 하는 경우 Azure Portal에서 직접 수행할 수 있습니다. [가상 컴퓨터에 대 한 끝점을 설정 하는 방법을](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)참조 하세요.)

이제 개발 컴퓨터의 Visual Studio 프로젝트를 서버에 배포할 준비가 되었습니다. 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.

웹 배포에 대 한 자세한 설명서는 [Visual Studio 및 ASP.NET 용 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)을 참조 하세요.

두 개의 서버에 응용 프로그램을 배포 하는 경우 별도의 브라우저 창에서 각 인스턴스를 열 수 있으며 각 인스턴스는 서로 SignalR 메시지를 수신 하는 것을 볼 수 있습니다. 물론 프로덕션 환경에서는 두 서버가 부하 분산 장치 뒤에 앉아 있습니다.

![](scaleout-with-redis/_static/image8.png)

Redis로 전송 되는 메시지를 확인 하는 방법에 대 한 자세한 내용은 Redis와 함께 설치 되는 **Redis cli** 클라이언트를 사용할 수 있습니다.

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
