---
uid: mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
title: ASP.NET MVC 4에서 비동기 메서드 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 무료로 제공 되는 웹에 대 한 Visual Studio Express 2012를 사용 하 여 비동기 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항에 대해 설명 합니다.
ms.author: riande
ms.date: 06/06/2012
ms.assetid: a56572ba-81c3-47af-826d-941e9c4775ec
msc.legacyurl: /mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 15692b18fc112c4c6cce4d50a243a0e8d5fb52a4
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457754"
---
# <a name="using-asynchronous-methods-in-aspnet-mvc-4"></a>ASP.NET MVC 4에서의 비동기 메서드 사용

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 [웹의 Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11)를 사용 하 여 비동기 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항에 대해 설명 합니다. [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)을 사용할 수도 있습니다.
> 
> Github에서이 자습서에 대 한 전체 샘플을 제공 [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/)

[.Net 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx) 를 조합 하 여 ASP.NET MVC 4 [컨트롤러](https://msdn.microsoft.com/library/system.web.mvc.controller(VS.108).aspx) 클래스를 사용 하면 [Task&lt;actionresult&gt;](https://msdn.microsoft.com/library/dd321424(VS.110).aspx)형식의 개체를 반환 하는 비동기 작업 메서드를 작성할 수 있습니다. .NET Framework 4에서는 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 이라고 하는 비동기 프로그래밍 개념을 도입 했으며 ASP.NET MVC 4는 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)을 지원 합니다. 작업은 **작업** 형식 및 [system.object](https://msdn.microsoft.com/library/system.threading.tasks.aspx) 네임 스페이스의 관련 형식으로 표시 됩니다. .NET Framework 4.5는 이전 비동기 방법 보다 훨씬 더 복잡 한 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 개체 작업을 수행 하는 [wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드를 사용 하 여이 비동기 지원을 기반으로 합니다. [Wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드는 코드 조각이 다른 코드 부분에서 비동기적으로 대기 해야 함을 나타내는 구문상의 약어입니다. [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드는 메서드를 작업 기반 비동기 메서드로 표시 하는 데 사용할 수 있는 힌트를 나타냅니다. **Wait**, **async**및 **Task** 개체의 조합을 사용 하면 .net 4.5에서 비동기 코드를 훨씬 쉽게 작성할 수 있습니다. 비동기 메서드에 대 한 새 모델을 *작업 기반 비동기 패턴* (**탭**) 이라고 합니다. 이 자습서에서는 [wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드 및 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 네임 스페이스를 사용 하는 비동기 프로그래밍에 대해 잘 알고 있다고 가정 합니다.

[Wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드 및 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 네임 스페이스 사용에 대 한 자세한 내용은 다음 참조를 참조 하세요.

- [백서: .NET의 비동기](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Async/Wait FAQ](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio 비동기 프로그래밍](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>스레드 풀에서 요청을 처리 하는 방법

웹 서버에서 .NET Framework는 ASP.NET 요청을 처리 하는 데 사용 되는 스레드 풀을 유지 관리 합니다. 요청이 도착하면 해당 요청을 처리하기 위해 풀에서 하나의 스레드가 디스패치됩니다. 요청이 동기적으로 처리 되는 경우 요청이 처리 되는 동안 요청을 처리 하는 스레드가 사용 중이 고 해당 스레드가 다른 요청을 처리할 수 없습니다.   
  
스레드 풀을 많은 사용량이 많은 스레드를 수용할 수 있을 만큼 충분히 크게 만들 수 있으므로이는 문제가 되지 않을 수 있습니다. 그러나 스레드 풀의 스레드 수는 제한 됩니다 (.NET 4.5의 기본 최대값은 5000 임). 장기 실행 요청의 동시성이 높은 대규모 응용 프로그램에서는 사용 가능한 모든 스레드가 사용 중일 수 있습니다. 이러한 상황을 스레드 고갈이라고 합니다. 이 조건에 도달 하면 웹 서버는 요청을 큐에 대기 시킵니다. 요청 큐가 가득 차면 웹 서버는 HTTP 503 상태 (서버 사용량이 많음)를 포함 하는 요청을 거부 합니다. CLR 스레드 풀에는 새 스레드 주입에 대 한 제한이 있습니다. 동시성이 버스 티 (즉, 웹 사이트에 갑자기 많은 수의 요청이 있을 수 있음), 대기 시간이 긴 백 엔드 호출로 인해 사용 가능한 모든 요청 스레드가 사용 중인 경우 제한 된 스레드 주입 속도로 인해 응용 프로그램의 응답 성능이 저하 될 수 있습니다. 또한 스레드 풀에 추가 된 각 새 스레드에는 오버 헤드 (예: 1mb 스택 메모리)가 있습니다. 스레드 풀이 .NET 4.5 기본 최대값인 5로 증가 하는 대기 시간 호출을 처리 하는 동기 메서드를 사용 하는 웹 응용 프로그램은 응용 프로그램이 동일한 요청을 처리할 수 있는 것 보다 약 5gb의 메모리를 사용할 수 있습니다. 비동기 메서드 및 50 스레드만 비동기 작업을 수행 하는 경우 항상 스레드를 사용 하는 것은 아닙니다. 예를 들어 비동기 웹 서비스 요청을 수행 하는 경우 ASP.NET는 **비동기** 메서드 호출과 대기 사이의 스레드를 사용 하지 **않습니다.** 대기 시간이 긴 서비스 요청에 스레드 풀을 사용 하면 메모리 사용 공간이 많고 서버 하드웨어 사용률이 저하 될 수 있습니다.

## <a name="processing-asynchronous-requests"></a>비동기 요청 처리

시작 시 많은 수의 동시 요청을 확인 하거나 버스 티 부하가 있는 웹 앱 (동시성이 갑자기 증가할 경우)에서 웹 서비스 호출을 통해 응용 프로그램의 응답성이 향상 됩니다. 하나의 비동기 요청을 처리하는 시간은 하나의 동기 요청을 처리하는 시간과 동일합니다. 요청을 완료 하는 데 2 초가 필요한 웹 서비스 호출을 수행 하는 경우이 요청은 동기적으로 수행 되 든 비동기식으로 수행 될 때 2 초가 걸립니다. 그러나 비동기 호출 중에는 첫 번째 요청이 완료 되기를 기다리는 동안 스레드가 다른 요청에 응답 하지 못하도록 차단 되지 않습니다. 따라서 비동기 요청은 장기 실행 작업을 호출 하는 동시 요청이 많은 경우 요청 큐 및 스레드 풀 증가를 방지 합니다.

## <a id="ChoosingSyncVasync"></a>동기 또는 비동기 작업 메서드 선택

이 단원에서는 어떤 경우에 동기 또는 비동기 작업 메서드를 사용하는지에 대한 지침을 나열합니다. 단지 지침입니다. 각 응용 프로그램을 개별적으로 검사 하 여 비동기 메서드가 성능에 도움이 되는지 확인 합니다.

일반적으로 다음과 같은 경우에는 동기 메서드를 사용 합니다.

- 작업이 단순하거나 단기 실행 작업인 경우
- 단순성이 효율성보다 더 중요한 경우
- 작업이 광범위한 디스크 또는 네트워크 오버헤드를 유발하는 작업이 아닌 주로 CPU 작업인 경우. CPU 관련 작업에 비동기 작업 메서드를 사용하는 경우 이점은 없고 오버헤드만 증가합니다.

일반적으로 다음 조건에 대해 비동기 메서드를 사용 합니다.

- 비동기 메서드를 통해 사용할 수 있는 서비스를 호출 하 고 있으며 .NET 4.5 이상을 사용 하 고 있습니다.
- 작업이 CPU 관련 작업이 아닌 네트워크 또는 I/O 관련 작업인 경우
- 병렬 처리가 코드의 단순성보다 더 중요한 경우
- 사용자에게 장기 실행 요청을 취소할 수 있는 메커니즘을 제공하려는 경우
- 스레드 전환의 혜택이 컨텍스트 전환 비용을 능가 하는 경우 일반적으로 동기 메서드가 작업을 수행 하지 않고 ASP.NET request 스레드에서 대기 하는 경우 메서드를 비동기식으로 설정 해야 합니다. 비동기 호출을 수행 하 여 ASP.NET request 스레드는 웹 서비스 요청이 완료 될 때까지 대기 하는 동안 작업을 수행 하지 않습니다.
- 테스트를 통해 차단 작업은 사이트 성능의 병목 상태 이며 IIS는 이러한 차단 호출에 비동기 메서드를 사용 하 여 더 많은 요청을 수행할 수 있음을 보여 줍니다.

다운로드 가능한 샘플에서는 비동기 작업 메서드를 효율적으로 사용하는 방법을 보여 줍니다. 제공 된 샘플은 .NET 4.5을 사용 하 여 ASP.NET MVC 4의 비동기 프로그래밍에 대 한 간단한 데모를 제공 하도록 설계 되었습니다. 이 샘플은 ASP.NET MVC의 비동기 프로그래밍에 대 한 참조 아키텍처를 위한 것이 아닙니다. 샘플 프로그램은 작업을 호출 하는 [ASP.NET Web API](../../../web-api/index.md) 메서드를 호출 합니다. 장기 실행 웹 서비스 호출을 시뮬레이션 하기 위해 [지연 됩니다.](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 대부분의 프로덕션 응용 프로그램에는 비동기 작업 메서드를 사용 하는 경우 이러한 분명 한 이점이 표시 되지 않습니다.   
  
모든 작업 메서드가 비동기 방식이어야 하는 응용 프로그램은 극소수입니다. 필요한 작업량을 감안할 때, 몇 개의 동기 작업 메서드를 비동기 메서드로 변환하는 것이 효율성 증대에 최적인 경우가 많습니다.

## <a id="SampleApp"></a>응용 프로그램 예제

[GitHub](https://github.com/) 사이트의 [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET) 에서 샘플 응용 프로그램을 다운로드할 수 있습니다. 리포지토리는 세 가지 프로젝트로 구성 됩니다.

- *Mvc4Async*:이 자습서에 사용 된 코드를 포함 하는 ASP.NET MVC 4 프로젝트입니다. **WebAPIpgw** 서비스에 대 한 Web API 호출을 수행 합니다.
- *WebAPIpgw*: `Products, Gizmos and Widgets` 컨트롤러를 구현 하는 ASP.NET MVC 4 Web API 프로젝트입니다. *WebAppAsync* 프로젝트 및 *Mvc4Async* 프로젝트에 대 한 데이터를 제공 합니다.
- *WebAppAsync*: 다른 자습서에서 사용 되는 ASP.NET Web Forms 프로젝트입니다.

## <a id="GizmosSynch"></a>Gizmo 그리려면 동기 작업 메서드

 다음 코드에서는 gizmo 그리려면 목록을 표시 하는 데 사용 되는 `Gizmos` 동기 작업 메서드를 보여 줍니다. 이 문서에서 gizmo는 가상 기계적 장치입니다. 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample1.cs)]

다음 코드에서는 gizmo 서비스의 `GetGizmos` 메서드를 보여 줍니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample2.cs)]

`GizmoService GetGizmos` 메서드는 gizmo 그리려면 데이터 목록을 반환 하는 ASP.NET Web API HTTP 서비스에 URI를 전달 합니다. *WebAPIpgw* 프로젝트에는 Web API `gizmos, widget` 및 `product` 컨트롤러의 구현이 포함 되어 있습니다.  
다음 이미지는 샘플 프로젝트의 gizmo 그리려면 뷰를 보여 줍니다.

![Gizmo 그리려면](using-asynchronous-methods-in-aspnet-mvc-4/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>비동기 Gizmo 그리려면 동작 메서드 만들기

이 샘플에서는 새로운 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 및 [wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드 (.Net 4.5 및 Visual Studio 2012에서 사용 가능)를 사용 하 여 컴파일러가 비동기 프로그래밍에 필요한 복잡 한 변환을 유지 관리할 수 있도록 합니다. 컴파일러를 사용 하면 C#의 동기 제어 흐름 구문을 사용 하 여 코드를 작성할 수 있으며, 컴파일러는 스레드 차단을 방지 하기 위해 콜백을 사용 하는 데 필요한 변환을 자동으로 적용 합니다.

다음 코드는 `Gizmos` 동기 메서드 및 `GizmosAsync` 비동기 메서드를 보여 줍니다. 브라우저에서 [HTML 5 `<mark>` 요소](http://www.w3.org/wiki/HTML/Elements/mark)를 지 원하는 경우 노란색 강조 표시에서 `GizmosAsync`의 변경 내용이 표시 됩니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample3.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample4.cs?highlight=1,3,5)]

 `GizmosAsync` 비동기 일 수 있도록 다음 변경 내용이 적용 되었습니다.

- 메서드는 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드로 표시 되어 있습니다. 그러면 컴파일러가 본문의 부분에 대 한 콜백을 생성 하 고 반환 되는 `Task<ActionResult>`을 자동으로 만들도록 지시 합니다.
- 비동기&quot; &quot;메서드 이름에 추가 되었습니다. "Async"를 추가 하는 것은 필요 하지 않지만 비동기 메서드를 작성 하는 경우에는 규칙입니다.
- 반환 형식이 `ActionResult`에서 `Task<ActionResult>`로 변경 되었습니다. `Task<ActionResult>`의 반환 형식은 진행 중인 작업을 나타내며 비동기 작업의 완료를 기다리는 핸들을 사용 하 여 메서드의 호출자에 게 제공 합니다. 이 경우 호출자는 웹 서비스입니다. `Task<ActionResult>` `ActionResult.`의 결과로 진행 중인 작업을 나타냅니다.
- [Wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드가 웹 서비스 호출에 적용 되었습니다.
- 비동기 웹 서비스 API가 호출 된 경우 (`GetGizmosAsync`)

`GetGizmosAsync` 메서드 본문 내에서 다른 비동기 메서드인 `GetGizmosAsync`를 호출 합니다. `GetGizmosAsync`은 데이터를 사용할 수 있을 때 최종적으로 완료 되는 `Task<List<Gizmo>>`를 즉시 반환 합니다. Gizmo 데이터가 있을 때까지 다른 작업을 수행 하지 않으려는 경우 코드는 **wait** 키워드를 사용 하 여 작업을 기다립니다 합니다. **Wait** 키워드는 **async** 키워드로 주석이 지정 된 메서드에만 사용할 수 있습니다.

**Wait** 키워드는 태스크가 완료 될 때까지 스레드를 차단 하지 않습니다. 메서드의 나머지 부분을 작업의 콜백으로 등록 하 고를 즉시 반환 합니다. 대기 작업이 최종적으로 완료 되 면 해당 콜백을 호출 하 고, 중단 된 위치에서 즉시 메서드 실행을 다시 시작 합니다. [Wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드 및 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 네임 스페이스를 사용 하는 방법에 대 한 자세한 내용은 [비동기 참조](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async)를 참조 하세요.

다음 코드에서는 `GetGizmos` 및 `GetGizmosAsync` 메서드를 보여 줍니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample5.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample6.cs?highlight=1,4-8)]

 비동기 변경은 위의 **GizmosAsync** 와 비슷합니다. 

- 메서드 시그니처에 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드로 주석이 추가 되었고, 반환 형식이 `Task<List<Gizmo>>`로 변경 되었으며, *async* 가 메서드 이름에 추가 되었습니다.
- 비동기 [Httpclient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) 클래스는 [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) 클래스 대신 사용 됩니다.
- [Wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드가 [httpclient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) 비동기 메서드에 적용 되었습니다.

다음 이미지는 비동기 gizmo 뷰를 보여 줍니다.

![async](using-asynchronous-methods-in-aspnet-mvc-4/_static/image2.png)

Gizmo 그리려면 데이터의 브라우저 프레젠테이션은 동기 호출로 생성 된 뷰와 동일 합니다. 유일한 차이점은 비동기 버전이 부하가 많은 경우 성능이 더 높을 수 있다는 것입니다.

## <a id="Parallel"></a>여러 작업을 병렬로 수행

비동기 작업 메서드는 작업에서 여러 독립적인 작업을 수행 해야 하는 경우 동기 메서드에 비해 상당한 이점이 있습니다. 제공 된 샘플에서 `PWG`(Products, Widget 및 Gizmo 그리려면)에 대 한 동기 메서드는 세 개의 웹 서비스 호출 결과를 표시 하 여 products, widget 및 gizmo 그리려면의 목록을 가져옵니다. 이러한 서비스를 제공 하는 [ASP.NET Web API](../../../web-api/index.md) 프로젝트는 작업을 사용 [합니다. 지연](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 시간을 시뮬레이션 하거나 네트워크 호출을 느리게 합니다. 지연이 500 밀리초로 설정 된 경우 동기 `PWG` 버전이 1500 밀리초를 초과 하는 동안 비동기 `PWGasync` 메서드를 완료 하는 데 약간의 500 밀리초가 소요 됩니다. 동기 `PWG` 메서드는 다음 코드에 나와 있습니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample7.cs)]

비동기 `PWGasync` 메서드는 다음 코드에 나와 있습니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample8.cs?highlight=1,3,12)]

다음 이미지는 **PWGasync** 메서드에서 반환 된 뷰를 보여 줍니다.

![pwgAsync](using-asynchronous-methods-in-aspnet-mvc-4/_static/image3.png)

## <a id="CancelToken"></a>취소 토큰 사용

`Task<ActionResult>`를 반환 하는 비동기 작업 메서드는 취소할 수 있으며, [Asynctimeout](https://msdn.microsoft.com/library/system.web.mvc.asynctimeoutattribute(VS.108).aspx) 특성과 함께 제공 되는 경우 [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) 매개 변수를 사용 합니다. 다음 코드에서는 시간 제한이 150 밀리초 인 `GizmosCancelAsync` 메서드를 보여 줍니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample9.cs?highlight=1-3,5,10)]

다음 코드에서는 [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) 매개 변수를 사용 하는 GetGizmosAsync 오버 로드를 보여 줍니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample10.cs)]

제공 된 샘플 응용 프로그램에서 *취소 토큰 데모* 링크를 선택 하면 `GizmosCancelAsync` 메서드가 호출 되 고 비동기 호출을 취소 하는 것을 보여 줍니다.

## <a id="ServerConfig"></a>높은 동시성/대기 시간이 긴 웹 서비스 호출을 위한 서버 구성

비동기 웹 응용 프로그램의 이점을 실현 하려면 기본 서버 구성을 변경 해야 할 수 있습니다. 비동기 웹 응용 프로그램을 구성 하 고 스트레스 테스트할 때 다음 사항에 유의 하세요.

- Windows 7, Windows Vista 및 모든 Windows 클라이언트 운영 체제에는 최대 10 개의 동시 요청이 있습니다. 높은 부하 상태에서 비동기 메서드의 이점을 확인 하려면 Windows Server 운영 체제가 필요 합니다.
- 관리자 권한 명령 프롬프트에서 IIS에 .NET 4.5을 등록 합니다.  
  %windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet\_regiis-i  
  [ASP.NET Iis 등록 도구 (Aspnet\_regiis .exe)를](https://msdn.microsoft.com/library/k6h9cz8h.aspx) 참조 하세요.
- [Http.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) 큐 제한을 기본값 1000에서 5000로 늘려야 할 수 있습니다. 설정이 너무 낮으면 http 503 상태를 포함 하는 [http.sys 거부 요청이](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) 표시 될 수 있습니다. HTTP.SYS 큐 제한을 변경 하려면 다음을 수행 합니다.

    - IIS 관리자를 열고 응용 프로그램 풀 창으로 이동 합니다.
    - 대상 응용 프로그램 풀을 마우스 오른쪽 단추로 클릭 하 고 **고급 설정**을 선택 합니다.  
        ![고급](using-asynchronous-methods-in-aspnet-mvc-4/_static/image4.png)
    - **고급 설정** 대화 상자에서 *큐 길이* 를 1000에서 5000로 변경 합니다.  
        ![큐 길이](using-asynchronous-methods-in-aspnet-mvc-4/_static/image5.png)  
  
  위의 이미지에서 응용 프로그램 풀이 .NET 4.5을 사용 하 고 있더라도 .NET framework는 v 4.0으로 표시 됩니다. 이러한 불일치를 이해 하려면 다음을 참조 하십시오.

    - [.Net 버전 관리 및 다중 대상 지정-.net 4.5은 .NET 4.0로의 전체 업그레이드입니다.](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
    - [2.0이 아닌 ASP.NET 3.5를 사용 하도록 IIS 응용 프로그램 또는 AppPool을 설정 하는 방법](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
    - [.NET Framework 버전 및 종속성](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)
- 응용 프로그램에서 웹 서비스 또는 System.NET를 사용 하 여 HTTP를 통해 백 엔드와 통신 하는 경우 [Connectionmanagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) 요소를 늘려야 할 수 있습니다. ASP.NET 응용 프로그램의 경우 자동 구성 기능으로 Cpu 수의 12 배까지 제한 됩니다. 즉, 쿼드 프로시저에서 IP 끝점에 대 한 최대 12 \* 4 = 48 동시 연결을 사용할 수 있습니다. 이는 자동 [구성에 연결](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)되기 때문에 ASP.NET 응용 프로그램에서 `maxconnection`를 늘리는 가장 쉬운 방법은 *global.asax* 파일의 from `Application_Start` 메서드에서 프로그래밍 방식으로를 설정 하는 것입니다 [.](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) 예제는 샘플 다운로드를 참조 하세요.
- .NET 4.5에서 [MaxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) 에 대 한 5000의 기본값은 적절 해야 합니다.
