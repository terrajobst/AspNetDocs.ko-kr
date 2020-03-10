---
uid: signalr/overview/advanced/dependency-injection
title: SignalR의 종속성 주입 | Microsoft Docs
author: bradygaster
description: 이전 버전의에 대 한 자세한 내용은이 항목에서 사용 된 소프트웨어 버전 Visual Studio 2013 .NET 4.5 SignalR 버전 2 이전 버전의 항목을 참조 하세요.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 52978b10b6c131ac8eff4535216cc60b43fdf3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431867"
---
# <a name="dependency-injection-in-signalr"></a>SignalR에서 종속성 주입

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

종속성 주입은 개체 간에 하드 코드 된 종속성을 제거 하는 방법으로, 테스트 (모의 개체 사용) 또는 런타임 동작을 변경 하 여 개체의 종속성을 쉽게 바꿀 수 있습니다. 이 자습서에서는 SignalR hubs에서 종속성 주입을 수행 하는 방법을 보여 줍니다. 또한 SignalR에서 IoC 컨테이너를 사용 하는 방법을 보여 줍니다. IoC 컨테이너는 종속성 주입을 위한 일반 프레임 워크입니다.

## <a name="what-is-dependency-injection"></a>종속성 주입 이란?

종속성 주입에 이미 익숙한 경우이 섹션을 건너뜁니다.

DI ( *종속성 주입* )는 개체가 자체 종속성을 만들 책임이 없는 패턴입니다. 다음은 DI를 동기로 확인 하는 간단한 예제입니다. 메시지를 기록 해야 하는 개체가 있다고 가정 합니다. 로깅 인터페이스를 정의할 수 있습니다.

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

개체에서 메시지를 기록 하는 `ILogger`를 만들 수 있습니다.

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

이렇게 하는 것이 좋지만 최상의 디자인은 아닙니다. `FileLogger`을 다른 `ILogger` 구현으로 대체 하려는 경우 `SomeComponent`를 수정 해야 합니다. 많은 다른 개체가 `FileLogger`를 사용 하는 경우 모든 개체를 변경 해야 합니다. 또는 단일 항목을 `FileLogger` 하도록 결정 한 경우에는 응용 프로그램 전체에서 변경 해야 합니다.

생성자 인수를 사용 하는 등의 방법으로 개체에 `ILogger`을 "주입" 하는 것이 더 좋습니다.

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

이제 개체는 사용할 `ILogger`를 선택 하는 일을 담당 하지 않습니다. 이에 종속 된 개체를 변경 하지 않고 `ILogger` 구현을 전환할 수 있습니다.

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

이 패턴을 [생성자 주입](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)이라고 합니다. 또 다른 패턴은 setter 삽입으로, setter 메서드 또는 속성을 통해 종속성을 설정 합니다.

## <a name="simple-dependency-injection-in-signalr"></a>SignalR의 간단한 종속성 주입

[SignalR 시작](../getting-started/tutorial-getting-started-with-signalr.md)자습서의 채팅 응용 프로그램을 고려 합니다. 해당 응용 프로그램의 허브 클래스는 다음과 같습니다.

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

메시지를 보내기 전에 서버에 채팅 메시지를 저장 하려는 경우를 가정해 보겠습니다. 이 기능을 추상화 하는 인터페이스를 정의 하 고 DI를 사용 하 여 `ChatHub` 클래스에 인터페이스를 주입할 수 있습니다.

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

유일한 문제는 SignalR 응용 프로그램에서 직접 허브를 만들지 않는 것입니다. SignalR 사용자를 위해 만듭니다. 기본적으로 SignalR에는 매개 변수가 없는 생성자가 있는 허브 클래스가 필요 합니다. 그러나 함수를 쉽게 등록 하 여 허브 인스턴스를 만들고이 함수를 사용 하 여 DI를 수행할 수 있습니다. **DependencyResolver**를 호출 하 여 함수를 등록 합니다.

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

이제 SignalR는 `ChatHub` 인스턴스를 만들어야 할 때마다이 무명 함수를 호출 합니다.

## <a name="ioc-containers"></a>IoC 컨테이너

위의 코드는 간단한 경우에 적합 합니다. 그러나 여전히이를 작성 해야 했습니다.

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

많은 종속성이 있는 복잡 한 응용 프로그램에서는 많은 "배선" 코드를 작성 해야 할 수 있습니다. 특히 종속성이 중첩 된 경우이 코드를 유지 관리 하기 어려울 수 있습니다. 단위 테스트도 어렵습니다.

한 가지 해결 방법은 IoC 컨테이너를 사용 하는 것입니다. IoC 컨테이너는 종속성 관리를 담당 하는 소프트웨어 구성 요소입니다. 컨테이너를 사용 하 여 형식을 등록 한 다음 컨테이너를 사용 하 여 개체를 만듭니다. 컨테이너는 종속성 관계를 자동으로 출력 합니다. 많은 IoC 컨테이너를 사용 하 여 개체 수명 및 범위와 같은 항목을 제어할 수도 있습니다.

> [!NOTE]
> "IoC"는 프레임 워크가 응용 프로그램 코드를 호출 하는 일반적인 패턴 인 "제어 반전"을 의미 합니다. IoC 컨테이너는 사용자에 대 한 개체를 생성 하 여 일반적인 제어 흐름을 "반전" 합니다.

## <a name="using-ioc-containers-in-signalr"></a>SignalR에서 IoC 컨테이너 사용

채팅 응용 프로그램은 매우 간단 하 여 IoC 컨테이너의 이점을 누릴 수 있습니다. 대신 [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) 샘플을 살펴보겠습니다.

StockTicker 샘플은 두 개의 주 클래스를 정의 합니다.

- `StockTickerHub`: 클라이언트 연결을 관리 하는 허브 클래스입니다.
- `StockTicker`: 주식 가격을 보유 하 고 정기적으로 업데이트 하는 단일 항목입니다.

`StockTickerHub`는 `StockTicker` singleton에 대 한 참조를 보유 하 고 `StockTicker`는 `StockTickerHub`에 대 한 **IHubConnectionContext** 에 대 한 참조를 보유 합니다. 이 인터페이스는이 인터페이스를 사용 하 여 `StockTickerHub` 인스턴스와 통신 합니다. 자세한 내용은 [ASP.NET SignalR를 사용 하 여 서버 브로드캐스트](../getting-started/tutorial-server-broadcast-with-signalr.md)를 참조 하세요.

IoC 컨테이너를 사용 하 여 이러한 종속성을 약간 untangle 수 있습니다. 먼저 `StockTickerHub` 및 `StockTicker` 클래스를 단순화 하겠습니다. 다음 코드에서는 필요 하지 않은 부분을 주석으로 처리 했습니다.

`StockTickerHub`에서 매개 변수가 없는 생성자를 제거 합니다. 대신 항상 DI를 사용 하 여 허브를 만듭니다.

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

StockTicker의 경우 singleton 인스턴스를 제거 합니다. 나중에 IoC 컨테이너를 사용 하 여 StockTicker 수명을 제어 합니다. 또한 생성자를 public으로 설정 합니다.

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

그런 다음 `StockTicker`에 대 한 인터페이스를 만들어 코드를 리팩터링할 수 있습니다. 이 인터페이스를 사용 하 여 `StockTicker` 클래스에서 `StockTickerHub`를 분리 합니다.

Visual Studio에서는 이러한 종류의 리팩터링을 쉽게 수행할 수 있습니다. StockTicker.cs 파일을 열고 `StockTicker` 클래스 선언을 마우스 오른쪽 단추로 클릭 한 다음 **리팩터링** ...을 선택 합니다. **인터페이스를 추출**합니다.

![](dependency-injection/_static/image1.png)

**인터페이스 추출** 대화 상자에서 **모두 선택**을 클릭 합니다. 다른 기본값을 그대로 둡니다. **확인**을 클릭합니다.

![](dependency-injection/_static/image2.png)

Visual Studio는 `IStockTicker`이라는 새 인터페이스를 만들고 `IStockTicker`에서 파생 `StockTicker` 변경 합니다.

IStockTicker.cs 파일을 열고 인터페이스를 **public**으로 변경 합니다.

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

`StockTickerHub` 클래스에서 `StockTicker`의 두 인스턴스를 `IStockTicker`로 변경 합니다.

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

`IStockTicker` 인터페이스를 만드는 것은 반드시 필요한 것은 아니지만 DI를 통해 응용 프로그램의 구성 요소 간 결합을 줄이는 방법을 보여 드리겠습니다.

## <a name="add-the-ninject-library"></a>Ninject 라이브러리 추가

.NET 용 오픈 소스 IoC 컨테이너는 여러 가지가 있습니다. 이 자습서에서는 [Ninject](http://www.ninject.org/)를 사용 합니다. (기타 인기 있는 라이브러리에는 [성 Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity)및 [StructureMap](http://docs.structuremap.net)가 있습니다.)

NuGet 패키지 관리자를 사용 하 여 [Ninject 라이브러리](https://nuget.org/packages/Ninject/3.0.1.10)를 설치 합니다. Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a>SignalR 종속성 확인자를 바꿉니다.

SignalR 내에서 Ninject를 사용 하려면 **DefaultDependencyResolver**에서 파생 되는 클래스를 만듭니다.

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

이 클래스는 **DefaultDependencyResolver**의 **GetService** 및 **getservices** 메서드를 재정의 합니다. SignalR는 이러한 메서드를 호출 하 여 런타임에 SignalR에서 내부적으로 사용 되는 다양 한 서비스 뿐만 아니라 허브 인스턴스를 비롯 한 다양 한 개체를 만듭니다.

- **GetService** 메서드는 형식의 단일 인스턴스를 만듭니다. Ninject 커널의 **Trget** 메서드를 호출 하려면이 메서드를 재정의 합니다. 해당 메서드가 null을 반환 하는 경우 기본 해결 프로그램으로 대체 합니다.
- **Getservices** 메서드는 지정 된 형식의 개체 컬렉션을 만듭니다. Ninject의 결과를 기본 해결 프로그램의 결과와 연결 하려면이 메서드를 재정의 합니다.

## <a name="configure-ninject-bindings"></a>Ninject 바인딩 구성

이제 Ninject을 사용 하 여 형식 바인딩을 선언 합니다.

응용 프로그램의 Startup.cs 클래스를 엽니다. `readme.txt`의 패키지 지침에 따라 수동으로 만들었거나 프로젝트에 인증을 추가 하 여 만든 응용 프로그램을 엽니다. `Startup.Configuration` 메서드에서 Ninject가 *커널을*호출 하는 Ninject 컨테이너를 만듭니다.

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

사용자 지정 종속성 해결 프로그램의 인스턴스를 만듭니다.

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

다음과 같이 `IStockTicker`에 대 한 바인딩을 만듭니다.

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

이 코드는 두 가지를 말합니다. 먼저 응용 프로그램에 `IStockTicker`필요할 때마다 커널이 `StockTicker`의 인스턴스를 만들어야 합니다. 둘째, `StockTicker` 클래스는 단일 개체로 생성 되어야 합니다. Ninject는 개체의 인스턴스 하나를 만들고 각 요청에 대해 동일한 인스턴스를 반환 합니다.

다음과 같이 **IHubConnectionContext** 에 대 한 바인딩을 만듭니다.

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

이 코드는 **IHubConnection**를 반환 하는 익명 함수를 만듭니다. **WhenInjectedInto** 메서드는 `IStockTicker` 인스턴스를 만들 때만이 함수를 사용 하도록 Ninject에 지시 합니다. 그 이유는 SignalR는 내부적으로 **IHubConnectionContext** 인스턴스를 만들기 때문에 SignalR가 만드는 방법을 재정의 하려고 하지 않기 때문입니다. 이 함수는 `StockTicker` 클래스에만 적용 됩니다.

허브 구성을 추가 하 여 **MapSignalR** 메서드에 종속성 확인자를 전달 합니다.

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

새 매개 변수를 사용 하 여 샘플의 Startup 클래스에서 ConfigureSignalR 메서드를 업데이트 합니다.

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

이제 SignalR는 기본 해결 프로그램 대신 **MapSignalR**에 지정 된 해결 프로그램을 사용 합니다.

`Startup.Configuration`에 대 한 전체 코드 목록입니다.

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

Visual Studio에서 StockTicker 응용 프로그램을 실행 하려면 F5 키를 누릅니다. 브라우저 창에서 `http://localhost:*port*/SignalR.Sample/StockTicker.html`로 이동 합니다.

![](dependency-injection/_static/image3.png)

응용 프로그램은 이전과 동일 하 게 동일한 기능을가지고 있습니다. 자세한 내용은 [ASP.NET SignalR를 사용 하 여 서버 브로드캐스트](../getting-started/tutorial-server-broadcast-with-signalr.md)를 참조 하세요. 이 동작은 변경 되지 않았습니다. 코드를 쉽게 테스트 하 고, 유지 관리 하 고, 발전 시킬 수 있습니다.
