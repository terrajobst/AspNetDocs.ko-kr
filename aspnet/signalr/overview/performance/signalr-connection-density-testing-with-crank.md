---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: 크랭크를 사용 하 여 연결 밀도 테스트 SignalR Microsoft Docs
author: bradygaster
description: Crank를 사용하여 SignalR 연결 밀도 테스트
ms.author: bradyg
ms.date: 02/22/2015
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: 901e039fbb81651ed18d560c99745b7e7f716e01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449873"
---
# <a name="signalr-connection-density-testing-with-crank"></a>Crank를 사용하여 SignalR 연결 밀도 테스트

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 크랭크 도구를 사용 하 여 여러 시뮬레이트된 클라이언트를 사용 하 여 응용 프로그램을 테스트 하는 방법을 설명 합니다.

응용 프로그램이 호스팅 환경 (Azure 웹 역할, IIS 또는 Owin를 사용 하 여 자체 호스팅)에서 실행 되 면 크랭크 도구를 사용 하 여 응용 프로그램의 응답을 높은 수준의 연결 밀도로 테스트할 수 있습니다. 호스팅 환경은 인터넷 정보 서비스 (IIS) 서버, Owin 호스트 또는 Azure 웹 역할 일 수 있습니다. 참고: Azure App Service Web Apps에는 성능 카운터를 사용할 수 없으므로 연결 밀도 테스트에서 성능 데이터를 가져올 수 없습니다.)

연결 밀도는 서버에서 설정할 수 있는 동시 TCP 연결 수를 나타냅니다. 각 TCP 연결에는 자체 오버 헤드가 발생 하 고 많은 수의 유휴 연결을 열면 결국 메모리 병목 현상이 발생 합니다.

[SignalR 코드 베이스](https://github.com/signalr/signalr) 에는 **크랭크**라는 부하 테스트 도구가 포함 되어 있습니다. 최신 버전의 크랭크는 GitHub의 [Dev 분기](https://github.com/SignalR/signalr/tree/dev) 에서 찾을 수 있습니다. [여기](https://github.com/SignalR/SignalR/archive/dev.zip)에서 SignalR Codebase의 Dev 분기의 Zip 보관 파일을 다운로드할 수 있습니다.

크랭크는 서버 하드웨어에서 가능한 유휴 연결의 총 수를 계산 하기 위해 서버 메모리를 완전히 포화 하는 데 사용할 수 있습니다. 또는 크랭크를 사용 하 여 특정 수 또는 특정 메모리 임계값에 도달할 때까지 연결을 설정 하 여 특정 메모리 압력의 양에 따라 서버를 부하 테스트할 수 있습니다.

테스트할 때 원격 클라이언트를 사용 하 여 리소스 (예: TCP 연결 및 메모리)에 대 한 경쟁을 방지 하는 것이 중요 합니다. 클라이언트를 모니터링 하 여 서버가 전체 용량 (메모리 또는 CPU)에 도달 하는 것을 방해할 수 있는 병목 현상이 발생 하지 않도록 합니다. 서버를 완전히 로드 하기 위해 클라이언트 수를 늘려야 할 수도 있습니다.

### <a name="running-a-connection-density-test"></a>연결 밀도 테스트 실행

이 섹션에서는 SignalR 응용 프로그램에서 연결 밀도 테스트를 실행 하는 데 필요한 단계에 대해 설명 합니다.

1. [SignalR codebase의 Dev 분기](https://github.com/SignalR/SignalR/archive/dev.zip)를 다운로드 하 여 빌드합니다. 명령 프롬프트에서 &lt;프로젝트 디렉터리로 이동 하&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug.
2. 응용 프로그램을 원하는 호스팅 환경에 배포 합니다. 응용 프로그램에서 사용 하는 끝점을 기록해 둡니다. 예를 들어 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md)에서 만든 응용 프로그램에서 끝점이 `http://<yourhost>:8080/signalr`됩니다.
3. 서버에 [SignalR 성능 카운터](signalr-performance.md#perfcounters) 를 설치 합니다. 응용 프로그램이 Azure에서 실행 되는 경우 [Azure 웹 역할에서 SignalR 성능 카운터 사용](using-signalr-performance-counters-in-an-azure-web-role.md)을 참조 하세요.

코드 베이스를 다운로드 하 여 빌드하고 호스트에서 성능 카운터를 설치 하 고 나면 `src\Microsoft.AspNet.SignalR.Crank\bin\Debug` 폴더에서 크랭크 명령줄 도구를 찾을 수 있습니다.

크랭크 도구에 사용할 수 있는 옵션은 다음과 같습니다.

- **/?** : 도움말 화면을 표시 합니다. **Url** 매개 변수가 생략 된 경우에도 사용 가능한 옵션이 표시 됩니다.
- **/Url**: SignalR 연결에 대 한 Url입니다. 이 매개 변수는 필수 항목입니다. 기본 매핑을 사용 하는 SignalR 응용 프로그램의 경우 경로는 "/signalr"로 끝납니다.
- **/Ctransport**: 사용 된 전송의 이름입니다. 기본값은 사용 가능한 가장 적합 한 프로토콜을 선택 하는 `auto`입니다. 옵션에는 `WebSockets`, `ServerSentEvents`및 `LongPolling`가 포함 됩니다. Internet Explorer가 아닌 .NET 클라이언트를 사용 하므로`ForeverFrame`는 크랭크에 대 한 옵션이 아닙니다. SignalR에서 전송을 선택 하는 방법에 대 한 자세한 내용은 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)를 참조 하세요.
- **/BatchSize**: 각 일괄 처리에 추가 된 클라이언트의 수입니다. 기본값은 50입니다.
- **/Connectinterval**: 연결을 추가 하는 간격 (밀리초)입니다. 기본값은 500입니다.
- **/Sconnections**: 응용 프로그램을 로드 테스트 하는 데 사용 되는 연결 수입니다. 기본값은 10만입니다.
- **/Connecttimeout**: 테스트를 중단 하기 전 까지의 제한 시간 (초)입니다. 기본값은 300입니다.
- **Minservermbytes**: 도달할 최소 서버 메가바이트 수입니다. 기본값은 500입니다.
- **Sendbytes**: 서버에 전송 된 페이로드의 크기 (바이트)입니다. 기본값은 0입니다.
- **Sendinterval**: 서버에 대 한 메시지 간의 지연 시간 (밀리초)입니다. 기본값은 500입니다.
- **SendTimeout**: 서버에 대 한 메시지의 제한 시간 (밀리초)입니다. 기본값은 300입니다.
- **Controllerurl**: 한 클라이언트가 컨트롤러 허브를 호스트 하는 url입니다. 기본값은 null (컨트롤러 허브 없음)입니다. 크랭크 세션이 시작 되 면 컨트롤러 허브가 시작 됩니다. 컨트롤러 허브와 크랭크에 대 한 추가 접촉은 없습니다.
- **Numclients**: 응용 프로그램에 연결할 시뮬레이트된 클라이언트의 수입니다. 기본값은 1입니다.
- **Logfile**: 테스트 실행에 대 한 로그 파일의 파일 이름입니다. 기본값은 `crank.csv`입니다.
- **SampleInterval**: 성능 카운터 샘플 사이의 시간 (밀리초)입니다. 기본값은 1000입니다.
- **SignalRInstance**: 서버의 성능 카운터에 대 한 인스턴스 이름입니다. 기본값은 클라이언트 연결 상태를 사용 하는 것입니다.

### <a name="example"></a>예제

다음 명령은 100 연결을 사용 하 여 "ControllerHub" 라는 허브를 사용 하 여 포트 8080에서 응용 프로그램을 호스트 하는 Azure에서 `pfsignalr` 이라는 사이트를 테스트 합니다.

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`
