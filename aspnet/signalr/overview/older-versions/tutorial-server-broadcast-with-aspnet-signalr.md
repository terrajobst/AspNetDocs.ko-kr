---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: '자습서: ASP.NET SignalR 1.x를 사용 하 여 서버 브로드캐스트 | Microsoft Docs'
author: bradygaster
description: 이 자습서에서는 ASP.NET SignalR를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 서버 브로드캐스팅은 communic.
ms.author: bradyg
ms.date: 04/10/2013
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: 68908be34f6b010e512677fe5f5e31bfdefab592
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467933"
---
# <a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a>자습서: ASP.NET SignalR 1.x를 사용 하 여 서버 브로드캐스트

[Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 자습서에서는 ASP.NET SignalR를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 서버 브로드캐스트는 클라이언트에 전송 되는 통신이 서버에 의해 시작 됨을 의미 합니다. 이 시나리오에는 클라이언트에 전송 되는 통신이 하나 이상의 클라이언트에 의해 시작 되는 채팅 응용 프로그램과 같은 피어 투 피어 시나리오와 다른 프로그래밍 방식이 필요 합니다.
> 
> 이 자습서에서 만들 응용 프로그램은 서버 브로드캐스트 기능을 위한 일반적인 시나리오인 주식 시세 표시기를 시뮬레이션 합니다.
> 
> 자습서에 대 한 의견을 환영 합니다. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com)에 게시할 수 있습니다.

## <a name="overview"></a>개요

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 패키지는 샘플 시뮬레이션 된 주식 시세 표시기 응용 프로그램을 Visual Studio 프로젝트에 설치 합니다. 이 자습서의 첫 번째 부분에서는 해당 응용 프로그램의 단순화 된 버전을 처음부터 만듭니다. 자습서의 나머지 부분에서는 NuGet 패키지를 설치 하 고 생성 되는 추가 기능 및 코드를 검토 합니다.

주식 시세 응용 프로그램은 서버에서 연결 된 모든 클라이언트에 대 한 알림을 정기적으로 "푸시" 하거나 브로드캐스트하는 일종의 실시간 응용 프로그램을 나타냅니다.

이 자습서의 첫 번째 부분에서 빌드할 응용 프로그램은 재고 데이터가 포함 된 표를 표시 합니다.

![StockTicker 초기 버전](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

정기적으로 서버는 주식 가격을 임의로 업데이트 하 고 연결 된 모든 클라이언트에 업데이트를 푸시합니다. 브라우저에서 **변경** 및 **%** 열의 숫자 및 기호는 서버의 알림에 대 한 응답으로 동적으로 변경 됩니다. 동일한 URL에 대 한 추가 브라우저를 열 경우 모두 동일한 데이터 및 동일한 데이터 변경 내용을 동시에 표시 합니다.

이 자습서에는 다음과 같은 섹션이 포함 되어 있습니다.

- [필수 구성 요소](#prerequisites)
- [프로젝트 만들기](#createproject)
- [SignalR NuGet 패키지 추가](#nugetpackages)
- [서버 코드 설정](#server)
- [클라이언트 코드 설정](#client)
- [애플리케이션 테스트](#test)
- [로깅 사용](#enablelogging)
- [Full StockTicker 샘플 설치 및 검토](#fullsample)
- [다음 단계](#nextsteps)

> [!NOTE]
> 응용 프로그램을 빌드하는 단계를 수행 하지 않으려면 비어 있는 새 **ASP.NET 웹 응용 프로그램** 프로젝트에 SignalR 패키지를 설치 하 고 이러한 단계를 통해 코드에 대 한 설명을 얻을 수 있습니다. 자습서의 첫 번째 부분에서는 SignalR 코드의 하위 집합에 대해 설명 하 고, 두 번째 부분은 SignalR 패키지의 추가 기능에 대 한 주요 기능을 설명 합니다.

<a id="prerequisites"></a>

## <a name="prerequisites"></a>사전 요구 사항

시작 하기 전에 컴퓨터에 Visual Studio 2012 또는 2010 s p 1이 설치 되어 있는지 확인 합니다. Visual Studio가 없는 경우 [ASP.NET 다운로드](https://www.asp.net/downloads) 를 참조 하 여 무료로 제공 되는 visual Studio 2012 Express for Web을 다운로드 하세요.

Visual Studio 2010을 사용 하는 경우 [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 이 설치 되어 있는지 확인 합니다.

<a id="createproject"></a>

## <a name="create-the-project"></a>프로젝트 만들기

1. **파일** 메뉴에서 **새 프로젝트**를 클릭합니다.
2. **새 프로젝트** 대화 상자에서 **템플릿** 을 확장 **C#** 하 고 **웹**을 선택 합니다.
3. **ASP.NET Empty 웹 응용 프로그램** 템플릿을 선택 하 고 프로젝트 이름을 *SignalR로 StockTicker*하 고 **확인**을 클릭 합니다.

    ![새 프로젝트 대화 상자](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a>SignalR NuGet 패키지 추가

### <a name="add-the-signalr-and-jquery-nuget-packages"></a>SignalR 및 JQuery NuGet 패키지 추가

NuGet 패키지를 설치 하 여 프로젝트에 SignalR 기능을 추가할 수 있습니다.

1. 도구 |를 클릭 합니다.  **NuGet 패키지 관리자 | 패키지 관리자 콘솔**.
2. 패키지 관리자에서 다음 명령을 입력 합니다.

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    SignalR 패키지는 다양 한 NuGet 패키지를 종속성으로 설치 합니다. 설치가 완료 되 면 ASP.NET 응용 프로그램에서 SignalR를 사용 하는 데 필요한 모든 서버 및 클라이언트 구성 요소가 있습니다.

<a id="server"></a>

## <a name="set-up-the-server-code"></a>서버 코드 설정

이 섹션에서는 서버에서 실행 되는 코드를 설정 합니다.

### <a name="create-the-stock-class"></a>스톡 클래스 만들기

먼저 주식 정보를 저장 하 고 전송 하는 데 사용할 스톡 모델 클래스를 만듭니다.

1. 프로젝트 폴더에 새 클래스 파일을 만들고 이름을 *Stock.cs*로 지정한 다음 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    주식을 만들 때 설정 하는 두 가지 속성은 기호 (예: MSFT for Microsoft)와 가격입니다. 다른 속성은 가격을 설정 하는 방법과 시기에 따라 달라 집니다. 가격을 처음으로 설정 하는 경우 값이 DayOpen으로 전파 됩니다. 다음 번에 Price를 설정 하는 경우 Price와 DayOpen의 차이에 따라 Change 및 PercentChange 속성 값이 계산 됩니다.

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a>StockTicker 및 StockTickerHub 클래스 만들기

SignalR Hub API를 사용 하 여 서버와 클라이언트 간의 상호 작용을 처리 합니다. SignalR Hub 클래스에서 파생 되는 StockTickerHub 클래스는 클라이언트의 수신 연결 및 메서드 호출을 처리 합니다. 또한 클라이언트 연결과 독립적으로 가격 업데이트를 주기적으로 트리거하기 위해 주식 데이터를 유지 관리 하 고 타이머 개체를 실행 해야 합니다. 허브 인스턴스는 일시적 이므로 허브 클래스에 이러한 함수를 넣을 수 없습니다. 허브 클래스 인스턴스는 허브의 각 작업 (예: 클라이언트에서 서버로의 연결 및 호출)에 대해 만들어집니다. 따라서 주식 데이터를 유지 하 고, 가격을 업데이트 하 고, 가격 업데이트를 브로드캐스팅하는 메커니즘이 별도의 클래스에서 실행 되어야 하며,이는 StockTicker 이름을 표시 합니다.

![StockTicker에서 브로드캐스팅](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

StockTicker 클래스의 인스턴스 하나를 서버에서 실행 하려는 경우에만 각 StockTickerHub 인스턴스에서 singleton StockTicker 인스턴스로 참조를 설정 해야 합니다. StockTicker 클래스는 주식 데이터를 포함 하 고 업데이트를 트리거 하지만 StockTicker는 허브 클래스가 아니므로 클라이언트에 브로드캐스트할 수 있어야 합니다. 따라서 StockTicker 클래스는 SignalR Hub 연결 컨텍스트 개체에 대 한 참조를 가져와야 합니다. 그런 다음 SignalR 연결 컨텍스트 개체를 사용 하 여 클라이언트에 브로드캐스트할 수 있습니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **새 항목 추가**를 클릭 합니다.
2. [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=279941)를 사용 하 여 visual Studio 2012가 있는 경우  **C# visual** 에서 **웹** 을 클릭 하 고 **SignalR Hub 클래스** 항목 템플릿을 선택 합니다. 그렇지 않으면 **클래스** 템플릿을 선택 합니다.
3. 새 클래스의 이름을 *StockTickerHub.cs*로 지정한 다음 **추가**를 클릭 합니다.

    ![StockTickerHub.cs 추가](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    [허브](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클래스는 클라이언트가 서버에서 호출할 수 있는 메서드를 정의 하는 데 사용 됩니다. 메서드 하나를 정의 하 고 `GetAllStocks()`합니다. 클라이언트는 처음 서버에 연결할 때이 메서드를 호출 하 여 현재 가격으로 모든 주식의 목록을 가져옵니다. 메서드는 메모리에서 데이터를 반환 하므로 동기적으로 실행 하 고 `IEnumerable<Stock>`를 반환할 수 있습니다. 데이터베이스 조회 나 웹 서비스 호출과 같이 대기와 관련 된 작업을 수행 하 여 메서드가 데이터를 가져와야 하는 경우 비동기 처리를 사용 하도록 `Task<IEnumerable<Stock>>`를 반환 값으로 지정 합니다. 자세한 내용은 [ASP.NET SignalR HUBS API 가이드-서버-비동기적으로 실행 하는 경우](index.md)를 참조 하세요.

    HubName 특성은 클라이언트에서 JavaScript 코드에서 허브를 참조 하는 방법을 지정 합니다. 이 특성을 사용 하지 않는 경우 클라이언트의 기본 이름은 stockTickerHub 인 클래스 이름의 카멜식 대/소문자 버전입니다.

    나중에 StockTicker 클래스를 만들 때 해당 클래스의 singleton 인스턴스가 해당 정적 인스턴스 속성에 생성 됩니다. StockTicker의 단일 인스턴스는 연결 하거나 연결을 끊는 클라이언트 수에 관계 없이 메모리에 남아 있으며,이 인스턴스는 GetAllStocks 메서드에서 현재 주식 정보를 반환 하는 데 사용 하는 것입니다.
5. 프로젝트 폴더에 새 클래스 파일을 만들고 이름을 *StockTicker.cs*로 지정한 다음 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    여러 스레드가 동일한 StockTicker 코드 인스턴스를 실행 하므로 StockTicker 클래스는 threadsafe 여야 합니다.

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a>단일 인스턴스를 정적 필드에 저장

    이 코드는 인스턴스 속성을 클래스의 인스턴스로 지 원하는 정적 \_인스턴스 필드를 초기화 하 고 생성자가 private로 표시 되어 있기 때문에 만들 수 있는 클래스의 유일한 인스턴스입니다. [초기화 지연](https://msdn.microsoft.com/library/dd997286.aspx) 은 성능상의 이유로는 불가능 하지만 인스턴스 생성이 threadsafe를 보장 하기 위해 \_instance 필드에 사용 됩니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    클라이언트가 서버에 연결할 때마다 별도의 스레드에서 실행 되는 StockTickerHub 클래스의 새 인스턴스는 StockTickerHub 클래스의 앞부분에서 살펴본 것 처럼 StockTicker 정적 속성에서 StockTicker singleton 인스턴스를 가져옵니다.

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a>ConcurrentDictionary에 주식 데이터 저장

    생성자는 일부 샘플 재고 데이터를 사용 하 여 \_스톡 컬렉션을 초기화 하 고, GetAllStocks은 주식을 반환 합니다. 앞서 살펴본 것 처럼이 주식 컬렉션은 클라이언트가 호출할 수 있는 허브 클래스의 서버 메서드인 StockTickerHub에서 반환 됩니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    스톡 컬렉션은 스레드 보안을 위해 [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) 형식으로 정의 됩니다. 또는 [사전](https://msdn.microsoft.com/library/xfhwa508.aspx) 개체를 사용 하 고 변경할 때 사전을 명시적으로 잠글 수 있습니다.

    이 응용 프로그램 예제에서는 StockTicker 인스턴스가 삭제 될 때 응용 프로그램 데이터를 메모리에 저장 하 고 데이터를 잃지는 것이 좋습니다. 실제 응용 프로그램에서는 데이터베이스와 같은 백 엔드 데이터 저장소로 작업 하 게 됩니다.

    ### <a name="periodically-updating-stock-prices"></a>정기적으로 주식 가격 업데이트

    생성자는 임의 기준으로 주식 가격을 업데이트 하는 메서드를 주기적으로 호출 하는 타이머 개체를 시작 합니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    UpdateStockPrices 상태 매개 변수에 null을 전달 하는 타이머에 의해 호출 됩니다. 가격을 업데이트 하기 전에 \_updateStockPricesLock 개체에서 잠금이 수행 됩니다. 이 코드는 다른 스레드가 이미 가격을 업데이트 하 고 있는지 확인 한 다음 목록에 있는 각 주식에 대해 TryUpdateStockPrice를 호출 합니다. TryUpdateStockPrice 메서드는 주식 가격을 변경할 것인지 여부와 변경 하는 정도를 결정 합니다. 주가 변경 되 면 BroadcastStockPrice가 호출 되어 주식 가격 변경을 모든 연결 된 클라이언트에 브로드캐스트합니다.

    \_updatingStockPrices 플래그는이에 대 한 액세스가 threadsafe를 보장 하기 위해 [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) 로 표시 됩니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    실제 응용 프로그램에서 TryUpdateStockPrice 메서드는 웹 서비스를 호출 하 여 가격을 조회 합니다. 이 코드에서는 난수 생성기를 사용 하 여 임의로 변경을 수행 합니다.

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>StockTicker 클래스가 클라이언트에 브로드캐스트할 수 있도록 SignalR 컨텍스트 가져오기

    StockTicker 개체에서 가격 변경이 발생 하기 때문에 연결 된 모든 클라이언트에서 updateStockPrice 메서드를 호출 해야 하는 개체입니다. 허브 클래스에는 클라이언트 메서드를 호출 하기 위한 API가 있지만 StockTicker는 허브 클래스에서 파생 되지 않으며 허브 개체에 대 한 참조를 포함 하지 않습니다. 따라서 연결 된 클라이언트에 브로드캐스트하려면 StockTicker 클래스는 StockTickerHub 클래스에 대 한 SignalR 컨텍스트 인스턴스를 가져온 다음이를 사용 하 여 클라이언트에서 메서드를 호출 해야 합니다.

    이 코드는 singleton 클래스 인스턴스를 만들고 해당 참조를 생성자에 전달 하 고 생성자가이를 Clients 속성에 배치 하는 경우 SignalR 컨텍스트에 대 한 참조를 가져옵니다.

    컨텍스트를 한 번만 가져오는 두 가지 이유는 다음과 같습니다. 컨텍스트 가져오기는 비용이 많이 드는 작업이 며 한 번 가져오면 클라이언트에 전송 되는 메시지의 순서가 유지 됩니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    컨텍스트의 Clients 속성을 가져와서 StockTickerClient 속성에 배치 하면 허브 클래스와 동일한 것으로 보이는 클라이언트 메서드를 호출 하는 코드를 작성할 수 있습니다. 예를 들어 모든 클라이언트에 브로드캐스트하려면 클라이언트를 작성할 수 있습니다. 모든 updateStockPrice (재고).

    BroadcastStockPrice에서 호출 하는 updateStockPrice 메서드가 아직 존재 하지 않습니다. 나중에 클라이언트에서 실행 되는 코드를 작성할 때 추가 합니다. 클라이언트는 동적 이므로 여기서 updateStockPrice를 참조할 수 있습니다. 즉, 식이 런타임에 계산 됩니다. 이 메서드 호출이 실행 되 면 SignalR는 메서드 이름과 매개 변수 값을 클라이언트에 보내고, 클라이언트에 updateStockPrice 라는 메서드가 있으면 해당 메서드가 호출 되 고 매개 변수 값이이 메서드에 전달 됩니다.

    클라이언트. All은 모든 클라이언트에 보내는 것을 의미 합니다. SignalR는 보낼 클라이언트 또는 클라이언트 그룹을 지정 하는 다른 옵션을 제공 합니다. 자세한 내용은 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)를 참조 하세요.

### <a name="register-the-signalr-route"></a>SignalR 경로 등록

서버에서 가로채서 SignalR에 지시할 URL을 알고 있어야 합니다. 이렇게 하려면 *global.asax* 파일에 일부 코드를 추가 합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **새 항목 추가**를 클릭 합니다.
2. **전역 응용 프로그램 클래스** 항목 템플릿을 선택 하 고 **추가**를 클릭 합니다.

    ![Global.asax 추가](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. 응용 프로그램\_Start 메서드에 SignalR 경로 등록 코드를 추가 합니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    기본적으로 모든 SignalR 트래픽에 대 한 기본 URL은 "/signalr"이 고, "/signalr/hubs"는 응용 프로그램에 있는 모든 허브에 대 한 프록시를 정의 하는 동적으로 생성 된 JavaScript 파일을 검색 하는 데 사용 됩니다. MapHubs 메서드에는 [HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx) 클래스의 인스턴스에서 다른 기본 URL 및 특정 SignalR 옵션을 지정할 수 있도록 하는 오버 로드가 포함 되어 있습니다.
4. 파일의 맨 위에 using 문을 추가 합니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. *Global.asax* 파일을 저장 하 고 닫은 다음 프로젝트를 빌드합니다.

이제 서버 코드를 설정 했습니다. 다음 섹션에서는 클라이언트를 설정 합니다.

<a id="client"></a>

## <a name="set-up-the-client-code"></a>클라이언트 코드 설정

1. 프로젝트 폴더에 새 HTML 파일을 만들고 이름을 *StockTicker*로 다시 만듭니다.
2. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    HTML은 5 개 열, 머리글 행 및 5 개 열 전체에 걸쳐 있는 단일 셀을 포함 하는 데이터 행이 있는 테이블을 만듭니다. 데이터 행에 "로드 중 ..."이 표시 됩니다. 응용 프로그램이 시작 될 때 및는 일시적으로 표시 됩니다. JavaScript 코드는 해당 행을 제거 하 고 서버에서 검색 된 주식 데이터를 사용 하 여 해당 행을 추가 합니다.

    스크립트 태그는 jQuery 스크립트 파일, SignalR core 스크립트 파일, SignalR 프록시 스크립트 파일 및 나중에 만들 StockTicker 스크립트 파일을 지정 합니다. "/Signalr/hubs" URL을 지정 하는 SignalR proxy 스크립트 파일은 동적으로 생성 되며 허브 클래스 (이 경우 StockTickerHub)의 메서드에 대 한 프록시 메서드를 정의 합니다. 원한다 면 [SignalR 유틸리티](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) 를 사용 하 여이 JavaScript 파일을 수동으로 생성 하 고 maphubs 메서드 호출에서 동적 파일 생성을 사용 하지 않도록 설정할 수 있습니다.
3. > [!IMPORTANT]
   > *StockTicker* 의 JavaScript 파일 참조가 올바른지 확인 하십시오. 즉, 스크립트 태그의 jQuery 버전 (예제에서는 1.8.2)이 프로젝트의 *scripts* 폴더에 있는 jquery 버전과 동일 하 고 스크립트 태그의 SignalR 버전이 프로젝트의 *scripts* 폴더에 있는 SignalR 버전과 동일한 지 확인 합니다. 필요한 경우 스크립트 태그의 파일 이름을 변경 합니다.
4. **솔루션 탐색기**에서 *StockTicker*을 마우스 오른쪽 단추로 클릭 한 다음 **시작 페이지로 설정**을 클릭 합니다.
5. 프로젝트 폴더에 새 JavaScript 파일을 만들고 이름을 *StockTicker*.
6. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    $. 연결은 SignalR 프록시를 참조 합니다. 이 코드는 StockTickerHub 클래스의 프록시에 대 한 참조를 가져오고이를 종목 변수에 넣습니다. 프록시 이름은 [HubName] 특성에 의해 설정 된 이름입니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    모든 변수 및 함수가 정의 된 후 파일의 마지막 코드 줄은 SignalR start 함수를 호출 하 여 SignalR 연결을 초기화 합니다. 시작 함수는 비동기적으로 실행 되 고 [JQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/)를 반환 합니다. 즉, done 함수를 호출 하 여 비동기 작업이 완료 될 때 호출할 함수를 지정할 수 있습니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    Init 함수는 서버에서 getAllStocks 함수를 호출 하 고 서버에서 반환 하는 정보를 사용 하 여 스톡 테이블을 업데이트 합니다. 서버에서 메서드 이름이 파스칼식 대/소문자를 사용 하는 경우에도 기본적으로 클라이언트에서 카멜식 대/소문자를 사용 해야 합니다. 카멜식 대/소문자 구분 규칙은 개체가 아닌 메서드에만 적용 됩니다. 예를 들어 재고를 참조 합니다. 기호 및 스톡. 주가 나 주가 아닌 가격입니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    클라이언트에서 파스칼식 대/소문자를 사용 하려는 경우 또는 완전히 다른 메서드 이름을 사용 하려는 경우에는 HubName 특성을 사용 하 여 허브 클래스 자체를 데코 레이트 하는 것과 동일한 방식으로 허브 메서드를 HubMethodName 특성으로 데코레이팅 할 수 있습니다.

    Init 메서드에서는 formatStock을 호출 하 여 스톡 개체의 속성에 서식을 지정 하 고 기능이 아닙니다 ( *StockTicker*의 맨 위에 정의 됨)를 호출 하 여 rowtemplate 변수의 자리 표시자를 스톡 개체 속성 값으로 대체 하 여 서버에서 받은 각 스톡 개체에 대해 테이블 행의 HTML을 만듭니다. 그러면 결과 HTML이 스톡 테이블에 추가 됩니다.

    Init는 비동기 시작 함수가 완료 된 후 실행 되는 콜백 함수로 전달 하 여 호출 합니다. Start를 호출한 후 별도의 JavaScript 문으로 init를 호출 하는 경우 시작 함수가 연결 설정을 완료할 때까지 기다리지 않고 즉시 실행 되기 때문에 함수가 실패 합니다. 이 경우 init 함수는 서버 연결이 설정 되기 전에 getAllStocks 함수를 호출 하려고 합니다.

    서버는 주식 시세를 변경할 때 연결 된 클라이언트에서 updateStockPrice를 호출 합니다. 함수는 서버에서 호출할 수 있도록 stockTicker 프록시의 client 속성에 추가 됩니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    UpdateStockPrice 함수는 init 함수와 동일한 방식으로 서버에서 받은 스톡 개체의 형식을 테이블 행으로 지정 합니다. 그러나 테이블에 행을 추가 하는 대신 테이블에서 주식의 현재 행을 찾아 해당 행을 새 행으로 바꿉니다.

<a id="test"></a>

## <a name="test-the-application"></a>애플리케이션 테스트

1. F5 키를 눌러 디버그 모드에서 애플리케이션을 실행합니다.

    Stock 테이블에는 처음에 "로드 중 ..."이 표시 됩니다. 그런 다음, 짧은 지연 후 초기 주식 데이터를 표시 한 다음 주가 변경 되기 시작 합니다.

    ![로드](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![초기 스톡 테이블](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![서버에서 변경 내용을 받는 주식 테이블](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. 브라우저 주소 표시줄에서 URL을 복사 하 여 하나 이상의 새 브라우저 창에 붙여 넣습니다.

    초기 주식 표시는 첫 번째 브라우저와 동일 하며 변경 내용이 동시에 발생 합니다.
3. 모든 브라우저를 닫고 새 브라우저를 연 다음 동일한 URL로 이동 합니다.

    StockTicker singleton 개체는 서버에서 계속 실행 되므로 주식 테이블 표시는 주가 계속 변경 되었음을 보여 줍니다. 변경 수치가 0 인 초기 테이블은 표시 되지 않습니다.
4. 브라우저를 닫습니다.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>로깅 사용

SignalR에는 문제 해결을 지원 하기 위해 클라이언트에서 사용할 수 있는 기본 제공 로깅 함수가 있습니다. 이 섹션에서는 로깅을 사용 하도록 설정 하 고 SignalR에서 사용 하는 전송 방법에 대 한 로그를 표시 하는 예제를 표시 합니다.

- [Websocket](http://en.wikipedia.org/wiki/WebSocket)-IIS 8 및 현재 브라우저에서 지원 됩니다.
- Internet Explorer 이외의 브라우저에서 지원 되는 [서버에서 보낸 이벤트](http://en.wikipedia.org/wiki/Server-sent_events)
- [영구적 프레임](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)으로, Internet Explorer에서 지원 됩니다.
- 모든 브라우저에서 지원 되는 [Ajax 긴 폴링](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling).

SignalR는 지정 된 모든 연결에 대해 서버와 클라이언트가 지 원하는 최상의 전송 방법을 선택 합니다.

1. StockTicker를 열고 파일 끝에서 연결을 초기화 하는 코드 바로 앞에서 로깅을 사용할 수 있도록 코드 줄을 추가 *합니다* .

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. F5 키를 눌러 프로젝트를 실행합니다.
3. 브라우저의 개발자 도구 창을 열고 콘솔을 선택 하 여 로그를 확인 합니다. 새 연결에 대 한 전송 방법을 협상 하는 Signalr의 로그를 확인 하려면 페이지를 새로 고쳐야 할 수도 있습니다.

    Windows 8 (IIS 8)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 Websocket입니다.

    ![IE 10 IIS 8 콘솔](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    Windows 7 (IIS 7.5)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 iframe입니다.

    ![IE 10 콘솔, IIS 7.5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    Firefox에서 Firebug 추가 기능을 설치 하 여 콘솔 창을 가져옵니다. Windows 8 (IIS 8)에서 Firefox 19를 실행 하는 경우 전송 방법은 Websocket입니다.

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    Windows 7 (IIS 7.5)에서 Firefox 19를 실행 하는 경우 전송 방법은 서버에서 보낸 이벤트입니다.

    ![Firefox 19 IIS 7.5 콘솔](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a>Full StockTicker 샘플 설치 및 검토

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 패키지에 의해 설치 된 StockTicker 응용 프로그램은 처음부터 새로 만든 단순화 된 버전 보다 많은 기능을 포함 합니다. 자습서의이 섹션에서는 NuGet 패키지를 설치 하 고 새 기능 및이를 구현 하는 코드를 검토 합니다.

### <a name="install-the-signalrsample-nuget-package"></a>SignalR NuGet 패키지를 설치 합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **NuGet 패키지 관리**를 클릭 합니다.
2. **NuGet 패키지 관리** 대화 상자에서 **온라인**을 클릭 하 고 **온라인 검색** 상자에 *SignalR* 를 입력 한 다음 **SignalR** 패키지에서 **설치** 를 클릭 합니다.

    ![SignalR 패키지를 설치 합니다.](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. *Global.asax* 파일에서 RouteTable ()를 주석으로 처리 합니다. 응용 프로그램에서 이전에 추가한 줄\_시작 메서드입니다.

    SignalR 패키지는 *App\_Start/RegisterHubs .cs* 파일에 SignalR 경로를 등록 하므로 *global.asax의 코드* 는 더 이상 필요 하지 않습니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    Assembly 특성에서 참조 하는 WebActivator 클래스는 SignalR 패키지의 종속성으로 설치 되는 Webactiventex NuGet 패키지에 포함 되어 있습니다.
4. **솔루션 탐색기**에서 SignalR 패키지를 설치 하 여 만든 *SignalR* 폴더를 확장 합니다.
5. *SignalR* 폴더에서 *StockTicker*를 마우스 오른쪽 단추로 클릭 한 다음 **시작 페이지로 설정**을 클릭 합니다.

    > [!NOTE]
    > SignalR NuGet 패키지를 설치 하면 *Scripts* 폴더에 있는 jQuery 버전이 변경 될 수 있습니다. 패키지가 *SignalR* 폴더에 설치 하는 새 *StockTicker* 파일은 패키지가 설치 하는 jQuery 버전과 동기화 되지만 원래 *StockTicker* 파일을 다시 실행 하려는 경우에는 먼저 스크립트 태그에서 jquery 참조를 업데이트 해야 할 수 있습니다.

### <a name="run-the-application"></a>애플리케이션 실행

1. F5 키를 눌러 애플리케이션을 실행합니다.

    앞에서 살펴본 그리드 외에도 전체 주식 시세 응용 프로그램에는 동일한 주식 데이터를 표시 하는 가로로 스크롤 창이 표시 됩니다. 응용 프로그램을 처음 실행 하는 경우 "market"은 "닫힘" 이며, 스크롤 되지 않는 정적 눈금과 표시기 창이 표시 됩니다.

    ![StockTicker 화면 시작](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    **시장 출시**를 클릭 하면 **라이브 재고 표시기** 상자가 가로로 스크롤 되기 시작 하 고 서버에서 정기적으로 주식 시세 변경을 정기적으로 브로드캐스트 하기 시작 합니다. 주가 변경 될 때마다 **라이브 재고 테이블** 눈금과 **라이브 주식 종목** 상자가 모두 업데이트 됩니다. 주가 변경 된 주가 양수인 경우 주가 녹색 배경으로 표시 되 고, 변경 내용이 음수인 경우 주가 빨간색 배경으로 표시 됩니다.

    ![StockTicker 앱, 시장 오픈](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    **시장 닫기** 단추를 클릭 하면 변경 내용이 중지 되 고 표시기 스크롤이 중지 되며, **다시 설정** 단추를 클릭 하면 가격 변경이 시작 되기 전의 모든 재고 데이터가 초기 상태로 다시 설정 됩니다. 더 많은 브라우저 창을 열고 동일한 URL로 이동 하는 경우 각 브라우저에서 동시에 동일한 데이터를 동적으로 업데이트 하는 것을 볼 수 있습니다. 단추 중 하나를 클릭 하면 모든 브라우저가 동시에 동일한 방식으로 응답 합니다.

### <a name="live-stock-ticker-display"></a>라이브 주식 종목 표시

**라이브 주식 시세** 표시는 CSS 스타일로 한 줄로 형식이 지정 된 div 요소의 순서가 지정 되지 않은 목록입니다. 표시기는 &lt;li&gt; 템플릿 문자열에서 자리 표시자를 대체 하 고 &lt;li&gt; 요소를 &lt;ul&gt; 요소에 동적으로 추가 하 여 테이블과 같은 방식으로 초기화 되 고 업데이트 됩니다. 스크롤은 jQuery 애니메이션 함수를 사용 하 여 div 내에서 순서가 지정 되지 않은 목록의 왼쪽 여백을 변경 하는 방식으로 수행 됩니다.

주식 시세 HTML:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

주식 시세 CSS:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

스크롤할 수 있도록 하는 jQuery 코드:

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>클라이언트에서 호출할 수 있는 서버에 대 한 추가 메서드

StockTickerHub 클래스는 클라이언트에서 호출할 수 있는 다음 네 가지 메서드를 추가로 정의 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

OpenMarket, CloseMarket 및 Reset은 페이지 맨 위에 있는 단추에 대 한 응답으로 호출 됩니다. 모든 클라이언트에 즉시 전파 되는 상태 변경을 트리거하는 한 클라이언트의 패턴을 보여 줍니다. 이러한 각 메서드는 시장 상태 변경에 영향을 주는 StockTicker 클래스의 메서드를 호출한 다음 새 상태를 브로드캐스트합니다.

StockTicker 클래스에서 시장 상태는 MarketState 열거형 값을 반환 하는 MarketState 속성에 의해 유지 관리 됩니다.

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

StockTicker 클래스는 threadsafe 여야 하므로 시장 상태를 변경 하는 각 메서드는 잠금 블록 내에서이 작업을 수행 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

이 코드가 threadsafe 인지 확인 하기 위해 MarketState 속성을 지 원하는 \_marketState 필드가 volatile로 표시 됩니다.

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

BroadcastMarketStateChange 및 BroadcastMarketReset 메서드는 클라이언트에 정의 된 다른 메서드를 호출 하는 경우를 제외 하 고 이미 보았던 BroadcastStockPrice 메서드와 유사 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>서버에서 호출할 수 있는 클라이언트의 추가 함수

이제 updateStockPrice 함수는 그리드와 표시기를 모두 처리 하 고, jQuery를 사용 하 여 빨강 및 녹색 색을 표시 합니다.

StockTicker의 새로운 함수는 시장 상태를 기반으로 하는 단추를 사용 하거나 사용 하지 않도록 설정 하 고, *SignalR* 은 표시기 창의 가로 스크롤을 중지 하거나 시작 합니다. 여러 함수가 종목에 추가 되기 때문에 [jQuery 확장 함수](http://api.jquery.com/jQuery.extend/) 를 사용 하 여 추가 합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>연결을 설정한 후 추가 클라이언트 설정

클라이언트에서 연결을 설정한 후에는 적절 한 marketOpened 또는 marketClosed 함수를 호출 하기 위해 시장이 열려 있는지 아니면 닫혀 있는지 확인 하 고, 서버 메서드 호출을 단추에 연결 하기 위해 몇 가지 추가 작업을 수행 합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

서버 메서드는 연결이 설정 될 때까지 단추에 연결 되지 않으므로 코드가 사용 가능 하기 전에 서버 메서드를 호출할 수 없습니다.

<a id="nextsteps"></a>

## <a name="next-steps"></a>다음 단계

이 자습서에서는 정기적으로 그리고 모든 클라이언트의 알림에 대 한 응답으로 서버에서 연결 된 모든 클라이언트로 메시지를 브로드캐스팅하는 SignalR 응용 프로그램을 프로그래밍 하는 방법에 대해 알아보았습니다. 다중 스레드 singleton 인스턴스를 사용 하 여 서버 상태를 유지 하는 패턴은 다중 플레이어 온라인 게임 시나리오 에서도 사용할 수 있습니다. 예제를 보려면 SignalR을 [기반으로 하는 Sho이상 r 게임](https://github.com/NTaylorMullen/ShootR)을 참조 하십시오.

피어 투 피어 통신 시나리오를 보여 주는 자습서는 [SignalR 시작](index.md) 하기 및 [SignalR를 사용 하 여 실시간 업데이트](index.md)를 참조 하세요.

고급 SignalR 개발 개념에 대 한 자세한 내용은 다음 사이트에서 SignalR 소스 코드 및 리소스를 참조 하세요.

- [ASP.NET SignalR](https://asp.net/signalr/)
- [SignalR 프로젝트](http://signalr.net/)
- [SignalR Github 및 샘플](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
