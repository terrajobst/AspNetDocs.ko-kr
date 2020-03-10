---
uid: signalr/overview/performance/scaleout-with-sql-server
title: SQL Server SignalR 확장 | Microsoft Docs
author: bradygaster
description: 이전 버전의에 대 한 자세한 내용은이 항목에서 사용 된 소프트웨어 버전 Visual Studio 2013 .NET 4.5 SignalR 버전 2 이전 버전의 항목을 참조 하세요.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467741"
---
# <a name="signalr-scaleout-with-sql-server"></a>SQL Server로 SignalR 규모 확장

사람, [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 버전 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
>
> 이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.
>
> ## <a name="questions-and-comments"></a>질문 및 설명
>
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.

이 자습서에서는 SQL Server를 사용 하 여 별도의 두 IIS 인스턴스에 배포 된 SignalR 응용 프로그램을 통해 메시지를 배포 합니다. 단일 테스트 컴퓨터에서이 자습서를 실행할 수도 있지만, 전체 결과를 얻으려면 SignalR 응용 프로그램을 둘 이상의 서버에 배포 해야 합니다. 또한 서버 중 하나 또는 별도의 전용 서버에 SQL Server를 설치 해야 합니다. 또 다른 옵션은 Azure에서 Vm을 사용 하 여 자습서를 실행 하는 것입니다.

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>사전 요구 사항

2005 이상 Microsoft SQL Server 합니다. 후면판은 SQL Server의 데스크톱 및 서버 버전을 모두 지원 합니다. SQL Server Compact Edition 또는 Azure SQL Database를 지원 하지 않습니다. 응용 프로그램이 Azure에서 호스트 되는 경우에는 Service Bus 후면판을 고려 하세요.)

## <a name="overview"></a>개요

자세한 자습서를 시작 하기 전에 수행할 작업에 대 한 간략 한 개요를 참조 하세요.

1. 비어 있는 새 데이터베이스를 만듭니다. 후면판이이 데이터베이스에 필요한 테이블을 만듭니다.
2. 응용 프로그램에 다음 NuGet 패키지를 추가 합니다.

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR.](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. SignalR 응용 프로그램을 만듭니다.
4. Startup.cs에 다음 코드를 추가 하 여 후면판을 구성 합니다.

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   이 코드는 [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) 및 [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)에 대 한 기본값을 사용 하 여 후면판을 구성 합니다. 이러한 값을 변경 하는 방법에 대 한 자세한 내용은 [SignalR Performance: 확장 메트릭](signalr-performance.md#scaleout_metrics)을 참조 하세요.

## <a name="configure-the-database"></a>데이터베이스 구성

응용 프로그램에서 데이터베이스에 액세스 하는 데 Windows 인증을 사용할지 또는 SQL Server 인증을 사용할지 결정 합니다. 에 관계 없이 데이터베이스 사용자에 게 로그인 하 고, 스키마를 만들고, 테이블을 만들 수 있는 권한이 있는지 확인 합니다.

후면판에서 사용할 새 데이터베이스를 만듭니다. 데이터베이스 이름을 지정할 수 있습니다. 데이터베이스에 테이블을 만들 필요가 없습니다. 후면판에서 필요한 테이블을 만듭니다.

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>Service Broker 사용

후면판 데이터베이스에 대해 Service Broker를 사용 하도록 설정 하는 것이 좋습니다. Service Broker은 SQL Server의 메시징 및 큐에 대 한 기본 지원을 제공 하므로 후면판에서 업데이트를 보다 효율적으로 받을 수 있습니다. 그러나 후면판은 Service Broker 없이도 작동 합니다.

Service Broker 사용 하도록 설정 되어 있는지 여부를 확인 하려면를 사용 **하 여** **\_Broker\_사용** 열을 쿼리 합니다.

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

Service Broker를 사용 하도록 설정 하려면 다음 SQL 쿼리를 사용 합니다.

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> 이 쿼리가 교착 상태로 표시 되는 경우 DB에 연결 된 응용 프로그램이 없는지 확인 합니다.

추적을 사용 하도록 설정한 경우 추적에 Service Broker 사용 되는지 여부도 표시 됩니다.

## <a name="create-a-signalr-application"></a>SignalR 응용 프로그램 만들기

다음 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.

- [SignalR 2.0 시작](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR 2.0 및 MVC 5 시작](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

다음으로 SQL Server와의 확장을 지원 하도록 채팅 응용 프로그램을 수정 합니다. 먼저 SignalR NuGet 패키지를 프로젝트에 추가 합니다. Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

그런 다음 Startup.cs 파일을 엽니다. **Configure** 메서드에 다음 코드를 추가 합니다.

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>응용 프로그램 배포 및 실행

Windows Server 인스턴스를 준비 하 여 SignalR 응용 프로그램을 배포 합니다.

IIS 역할을 추가 합니다. WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.

![](scaleout-with-sql-server/_static/image4.png)

관리 서비스 ("관리 도구" 아래에 나열 됨)도 포함 합니다.

![](scaleout-with-sql-server/_static/image5.png)

**웹 배포 3.0을 설치 합니다.** IIS 관리자를 실행 하는 경우 Microsoft 웹 플랫폼을 설치 하 라는 메시지가 표시 되거나 [설치 관리자를 다운로드할](https://go.microsoft.com/fwlink/?LinkId=255386)수 있습니다. 플랫폼 설치 관리자에서 웹 배포을 검색 하 고 웹 배포 3.0를 설치 합니다.

![](scaleout-with-sql-server/_static/image6.png)

웹 관리 서비스가 실행 중인지 확인 합니다. 그렇지 않은 경우 서비스를 시작 합니다. Windows 서비스 목록에 웹 관리 서비스가 표시 되지 않으면 IIS 역할을 추가할 때 관리 서비스를 설치 했는지 확인 합니다.

마지막으로 TCP에 대해 8172 포트를 엽니다. 웹 배포 도구에서 사용 하는 포트입니다.

이제 개발 컴퓨터의 Visual Studio 프로젝트를 서버에 배포할 준비가 되었습니다. 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.

웹 배포에 대 한 자세한 설명서는 [Visual Studio 및 ASP.NET 용 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)을 참조 하세요.

두 개의 서버에 응용 프로그램을 배포 하는 경우 별도의 브라우저 창에서 각 인스턴스를 열 수 있으며 각 인스턴스는 서로 SignalR 메시지를 수신 하는 것을 볼 수 있습니다. 물론 프로덕션 환경에서는 두 서버가 부하 분산 장치 뒤에 앉아 있습니다.

![](scaleout-with-sql-server/_static/image7.png)

응용 프로그램을 실행 한 후 SignalR에서 데이터베이스에 자동으로 생성 된 테이블을 볼 수 있습니다.

![](scaleout-with-sql-server/_static/image8.png)

SignalR는 테이블을 관리 합니다. 응용 프로그램이 배포 되는 동안에는 행을 삭제 하거나 테이블을 수정 하지 않습니다.
