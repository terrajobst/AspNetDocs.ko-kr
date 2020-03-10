---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
title: 큐 중심 작업 패턴 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: cc1ad51b-40c3-4c68-8620-9aaa0fd1f6cf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
msc.type: authoredcontent
ms.openlocfilehash: 1177336b25479c06706227e5c8ff4d027cdaebb8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472571"
---
# <a name="queue-centric-work-pattern-building-real-world-cloud-apps-with-azure"></a>큐 중심 작업 패턴 (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

이전에는 여러 서비스를 사용 하 여 "복합" SLA를 만들 수 있다는 것을 확인 했습니다. 여기서 앱의 유효 SLA는 개별 Sla의 *제품* 입니다. 예를 들어 Fix It 앱은 웹 사이트, 저장소 및 SQL Database를 사용 합니다. 이러한 서비스 중 하나라도 실패 하면 앱이 사용자에 게 오류를 반환 합니다.

캐싱은 읽기 전용 콘텐츠의 일시적인 오류를 처리 하는 좋은 방법입니다. 그러나 응용 프로그램이 작업을 수행 해야 하는 경우는 어떻게 되나요? 예를 들어 사용자가 새 Fix It 작업을 제출 하면 앱은 작업을 캐시에 배치할 수 없습니다. 앱은 수정 It 작업을 영구 데이터 저장소에 써야 하므로 처리 될 수 있습니다.

큐 중심 작업 패턴이 제공 되는 위치입니다. 이 패턴은 웹 계층과 백 엔드 서비스 간의 느슨한 결합을 가능 하 게 합니다.

패턴의 작동 방식은 다음과 같습니다. 응용 프로그램은 요청을 가져오는 경우 작업 항목을 큐에 넣고 즉시 응답을 반환 합니다. 그런 다음 별도의 백 엔드 프로세스에서 작업 항목을 큐에서 끌어오고 작업을 수행 합니다.

큐 중심 작업 패턴은 다음에 유용 합니다.

- 시간이 많이 걸리는 작업입니다 (대기 시간이 긴 경우).
- 항상 사용 가능 하지 않을 수 있는 외부 서비스를 필요로 하는 작업입니다.
- 리소스를 많이 사용 하는 작업 (높은 CPU).
- 속도 평준화를 통해 이점을 누릴 수 있는 작업입니다 (갑작스러운 부하 급증에 따름).

## <a name="reduced-latency"></a>대기 시간 감소

큐는 시간이 많이 걸리는 작업을 수행할 때마다 유용 합니다. 태스크가 최종 사용자를 차단 하는 대신 몇 초 이상 소요 되 면 작업 항목을 큐에 넣습니다. 사용자에 게 "작업 중입니다." 라는 사실을 알리고 큐 수신기를 사용 하 여 백그라운드에서 작업을 처리 합니다.

예를 들어 온라인 대리점에서 구매 하는 경우 웹 사이트에서 주문을 즉시 확인 합니다. 그러나이는 이미 제공 되는 트럭에 있는 것을 의미 하지는 않습니다. 큐에 작업을 배치 하 고 백그라운드에서 신용 검사를 수행 하 고 배송을 위해 항목을 준비 하는 등의 작업을 수행 합니다.

대기 시간이 짧은 시나리오의 경우 작업을 동기적으로 수행 하는 것과 비교 하 여 총 종단 간 시간이 큐를 사용 하는 데 더 오래 걸릴 수 있습니다. 하지만 그 외에도 그와 같은 이점이 있습니다.

## <a name="increased-reliability"></a>향상 된 안정성

최신 버전을 확인 하기 위해 웹 프런트 엔드는 SQL Database 백 엔드와 긴밀 하 게 연관 되어 있습니다. SQL database 서비스를 사용할 수 없는 경우 사용자에 게 오류가 발생 합니다. 다시 시도가 작동 하지 않는 경우 (즉, 오류가 일시적인 경우)에는 오류를 표시 하 고 나중에 다시 시도 하도록 사용자에 게 요청할 수 있습니다.

![SQL Database 백 엔드가 실패할 때 웹 프런트 엔드 실패를 보여 주는 다이어그램](queue-centric-work-pattern/_static/image1.png)

큐를 사용 하 여 사용자가 Fix It 작업을 제출 하면 앱이 큐에 메시지를 기록 합니다. 메시지 페이로드는 태스크의 [JSON](http://json.org/) 표현입니다. 메시지가 큐에 기록 되는 즉시 앱이 반환 되 고 사용자에 게 성공 메시지가 즉시 표시 됩니다.

백 엔드 서비스 (예: SQL 데이터베이스 또는 큐 수신기)가 있는 경우 오프 라인으로 전환 하면 사용자는 새 Fix It 작업을 계속 제출할 수 있습니다. 백 엔드 서비스를 다시 사용할 수 있을 때까지 메시지가 큐에 대기 됩니다. 이 시점에서 백 엔드 서비스는 백로그를 처리 합니다.

![SQL Database 오류가 발생할 때 지속적으로 작동 하는 웹 프런트 엔드를 보여 주는 다이어그램](queue-centric-work-pattern/_static/image2.png)

또한 이제 프런트 엔드의 복원 력을 걱정 하지 않고 백 엔드 논리를 더 추가할 수 있습니다. 예를 들어 새 수정 사항이 할당 될 때마다 소유자에 게 전자 메일 또는 SMS 메시지를 보낼 수 있습니다. 전자 메일 또는 SMS 서비스를 사용할 수 없게 되 면 다른 모든 항목을 처리 한 다음 전자 메일/SMS 메시지를 보내기 위해 별도의 큐에 메시지를 넣을 수 있습니다.

이전에는 효과적인 SLA를 &times; 저장소 &times; SQL Database = 99.7% Web Apps 했습니다. ( [실패를 유지 하려면 디자인을](design-to-survive-failures.md)참조 하세요.)

큐를 사용 하도록 앱을 변경 하는 경우 웹 프런트 엔드는 Web Apps 및 저장소에만 의존 하며,이는 복합 SLA 99.8%에 해당 합니다. 큐는 Azure storage 서비스의 일부 이므로 blob storage와 동일한 SLA에 포함 됩니다.

99.8% 보다 더 잘 필요한 경우 두 개의 다른 지역에 두 개의 큐를 만들 수 있습니다. 하나를 기본으로 지정 하 고 다른 하나를 보조로 지정 합니다. 앱에서 기본 큐를 사용할 수 없는 경우 보조 큐로 장애 조치 (failover) 합니다. 둘 다 동시에 사용할 수 없게 될 가능성이 매우 낮습니다.

## <a name="rate-leveling-and-independent-scaling"></a>비율 평준화 및 독립적인 크기 조정

큐는 *요율 평준화* 또는 *로드 평준화*라는 항목에도 유용 합니다.

웹 앱은 종종 트래픽이 갑자기 증가 하는 것이 쉽습니다. 자동 크기 조정을 사용 하 여 웹 서버를 자동으로 추가 하 여 증가 하는 웹 트래픽을 처리할 수 있지만, 자동 크기 조정은 부하가 급증 하는 급증을 처리 하기에 충분 하지 않을 수 있습니다. 웹 서버에서 큐에 메시지를 기록 하 여 수행 해야 하는 작업 중 일부를 오프 로드할 수 있는 경우 더 많은 트래픽을 처리할 수 있습니다. 백 엔드 서비스는 큐에서 메시지를 읽고 처리할 수 있습니다. 들어오는 부하가 변경 됨에 따라 큐의 깊이가 커지거나 줄어듭니다.

시간이 많이 걸리는 작업은 백 엔드 서비스에 대해 과도 하 게 로드 되므로 웹 계층은 트래픽 급증 급증에 더 쉽게 대응할 수 있습니다. 그리고 지정 된 트래픽 양이 덜 많은 웹 서버에서 처리 될 수 있기 때문에 비용을 절감할 수 있습니다.

웹 계층 및 백 엔드 서비스를 독립적으로 확장할 수 있습니다. 예를 들어 3 개의 웹 서버가 필요 하지만 큐 메시지를 처리 하는 서버는 하나 뿐입니다. 또는 백그라운드에서 계산 집약적인 작업을 실행 하는 경우 더 많은 백엔드 서버가 필요할 수 있습니다.

![](queue-centric-work-pattern/_static/image3.png)

자동 크기 조정은 백 엔드 서비스 뿐만 아니라 웹 계층 에서도 작동 합니다. 백 엔드 Vm의 CPU 사용량에 따라 큐의 작업을 처리 중인 Vm 수를 확장 하거나 축소할 수 있습니다. 또는 큐에 있는 항목 수에 따라 크기를 자동으로 조정할 수 있습니다. 예를 들어 큐에 10 개 이하의 항목을 유지 하도록 자동 크기 조정에 지시할 수 있습니다. 큐에 항목이 10 개 이상 있는 경우 자동 크기 조정에서 Vm을 추가 합니다. 이러한 작업을 마치면 자동 크기 조정에서 추가 Vm이 중단 됩니다.

## <a name="adding-queues-to-the-fix-it-application"></a>Fix It 응용 프로그램에 큐 추가

큐 패턴을 구현 하려면 Fix It 앱에 대 한 두 가지 변경 작업을 수행 해야 합니다.

- 사용자가 새 Fix It 작업을 제출 하는 경우 데이터베이스에 쓰는 대신 큐에 작업을 넣습니다.
- 큐에 있는 메시지를 처리 하는 백 엔드 서비스를 만듭니다.

큐의 경우 [Azure Queue Storage 서비스](https://www.windowsazure.com/develop/net/how-to-guides/queue-service/)를 사용 합니다. 다른 옵션은 [Azure Service Bus](https://docs.microsoft.com/azure/service-bus/)를 사용 하는 것입니다.

사용할 큐 서비스를 결정 하려면 앱이 큐에서 메시지를 보내고 받는 방법을 고려 합니다.

- 생산자와 경쟁 하는 소비자가 있는 경우 Azure Queue Storage 서비스를 사용 하는 것이 좋습니다. "생산자"는 여러 프로세스에서 큐에 메시지를 추가 하는 것을 의미 합니다. "경쟁 소비자"는 여러 프로세스가 메시지를 처리 하기 위해 큐에서 끌어오는 것을 의미 하지만 지정 된 모든 메시지는 하나의 "소비자"만 처리할 수 있습니다. 단일 큐를 사용 하 여 얻을 수 있는 것 보다 더 많은 처리량이 필요한 경우 추가 큐 및/또는 추가 저장소 계정을 사용 합니다.
- [게시/구독 모델이](http://en.wikipedia.org/wiki/Publish/subscribe)필요한 경우 Azure Service Bus 큐를 사용 하는 것이 좋습니다.

Fix It 앱은 협동 생산자와 경쟁 소비자 모델에 적합 합니다.

또 다른 고려 사항은 응용 프로그램 가용성입니다. Queue Storage 서비스는 blob 저장소에 사용 하는 것과 동일한 서비스에 포함 되어 있으므로 SLA에 영향을 주지 않습니다. Azure Service Bus은 고유한 SLA를 포함 하는 별도의 서비스입니다. Service Bus 큐를 사용 하는 경우 추가 SLA 비율을 고려해 야 하며, 복합 SLA는 더 낮습니다. 큐 서비스를 선택 하는 경우 응용 프로그램 가용성에 대 한 선택의 영향을 이해 해야 합니다. 자세한 내용은 [리소스](#resources) 섹션을 참조 하세요.

## <a name="creating-queue-messages"></a>큐 메시지 만들기

큐에 Fix It 작업을 추가 하기 위해 웹 프런트 엔드는 다음 단계를 수행 합니다.

1. [CloudQueueClient](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueueclient.aspx) 인스턴스를 만듭니다. `CloudQueueClient` 인스턴스는 큐 서비스에 대 한 요청을 실행 하는 데 사용 됩니다.
2. 아직 존재 하지 않는 경우 큐를 만듭니다.
3. Fix It 작업을 직렬화 합니다.
4. [AddMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.addmessageasync.aspx) 를 호출 하 여 메시지를 큐에 넣습니다.

새 `FixItQueueManager` 클래스의 생성자 및 `SendMessageAsync` 메서드에서이 작업을 수행 합니다.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample1.cs?highlight=11-12,16,18-25)]

여기서는 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 라이브러리를 사용 하 여 FIXIT를 Json 형식으로 직렬화 합니다. 원하는 모든 serialization 방법을 사용할 수 있습니다. JSON은 사용자가 읽을 수 있는 장점이 있지만 XML 보다는 더 낮은 정보를 제공 합니다.

프로덕션 품질 코드는 오류 처리 논리를 추가 하 고, 데이터베이스를 사용할 수 없게 되 면 일시 중지 하 고, 복구를 보다 명확 하 게 처리 하 고, 응용 프로그램 시작 시 큐를 만들고 "[포이즌" 메시지](https://msdn.microsoft.com/library/ms789028(v=vs.110).aspx)를 관리 합니다. 포이즌 메시지는 어떤 이유로 처리할 수 없는 메시지입니다. 큐에 포이즌 메시지를 저장 하지 않으려는 경우, 작업자 역할은 계속 해 서 처리를 시도 하 고 실패 한 후 다시 시도 하는 등의 작업을 수행 합니다.

프런트 엔드 MVC 응용 프로그램에서는 새 작업을 만드는 코드를 업데이트 해야 합니다. 리포지토리에 작업을 배치 하는 대신 위에 표시 된 `SendMessageAsync` 메서드를 호출 합니다.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample2.cs?highlight=10)]

## <a name="processing-queue-messages"></a>큐 메시지 처리

큐에 있는 메시지를 처리 하기 위해 백 엔드 서비스를 만듭니다. 백 엔드 서비스는 다음 단계를 수행 하는 무한 루프를 실행 합니다.

1. 큐에서 다음 메시지를 가져옵니다.
2. 메시지를 Fix It 작업으로 Deserialize 합니다.
3. 데이터베이스에 Fix It 작업을 씁니다.

백 엔드 서비스를 호스트 하기 위해 *작업자 역할*을 포함 하는 Azure 클라우드 서비스를 만듭니다. 작업자 역할은 백 엔드 처리를 수행할 수 있는 하나 이상의 Vm으로 구성 됩니다. 이러한 Vm에서 실행 되는 코드는 메시지를 사용할 수 있게 되 면 큐에서 메시지를 끌어옵니다. 각 메시지에 대해 이전에 웹 계층에서 사용한 것과 동일한 리포지토리를 사용 하 여 JSON 페이로드를 deserialize 하 고 Fix It 작업 엔터티의 인스턴스를 데이터베이스에 씁니다.

다음 단계에서는 표준 웹 프로젝트가 있는 솔루션에 작업자 역할 프로젝트를 추가 하는 방법을 보여 줍니다. 이러한 단계는 다운로드할 수 있는 Fix It 프로젝트에서 이미 수행 되었습니다.

먼저 Visual Studio 솔루션에 클라우드 서비스 프로젝트를 추가 합니다. 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 프로젝트**를 차례로 선택 합니다. 왼쪽 창에서 **시각적 개체 C#**  를 확장 하 고 **클라우드**를 선택 합니다.

[![](queue-centric-work-pattern/_static/image5.png)](queue-centric-work-pattern/_static/image4.png)

**새 Azure 클라우드 서비스** 대화 상자에서 왼쪽 창의 **시각적 C#**  노드를 확장 합니다. **작업자 역할** 을 선택 하 고 오른쪽 화살표 아이콘을 클릭 합니다.

![](queue-centric-work-pattern/_static/image6.png)

*웹 역할*을 추가할 수도 있습니다. Azure 웹 사이트에서 실행 하는 대신 동일한 클라우드 서비스에서 프런트 엔드를 수정할 수 있습니다. 프런트 엔드와 백 엔드 간의 연결을 보다 쉽게 조정할 때 약간의 이점이 있습니다. 그러나이 데모를 간단 하 게 유지 하기 위해 프런트 엔드를 Azure App Service 웹 앱으로 유지 하 고 클라우드 서비스에서 백 엔드만 실행 합니다.)

기본 이름은 작업자 역할에 할당 됩니다. 이름을 변경 하려면 오른쪽 창에서 작업자 역할 위로 마우스를 가져간 다음 연필 아이콘을 클릭 합니다.

![](queue-centric-work-pattern/_static/image7.png)

**확인** 을 클릭 하 여 대화 상자를 완료 합니다. 그러면 두 개의 프로젝트가 Visual Studio 솔루션에 추가 됩니다.

- 구성 정보를 포함 하 여 클라우드 서비스를 정의 하는 Azure 프로젝트입니다.
- 작업자 역할을 정의 하는 작업자 역할 프로젝트입니다.

![](queue-centric-work-pattern/_static/image8.png)

자세한 내용은 [Visual Studio를 사용 하 여 Azure 프로젝트 만들기](https://msdn.microsoft.com/library/windowsazure/ee405487.aspx) 를 참조 하세요.

작업자 역할 내에서 앞서 살펴본 `FixItQueueManager` 클래스의 `ProcessMessageAsync` 메서드를 호출 하 여 메시지를 폴링합니다.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample3.cs?highlight=25)]

`ProcessMessagesAsync` 메서드는 대기 중인 메시지가 있는지 확인 합니다. 있는 경우 메시지를 `FixItTask` 엔터티로 deserialize 하 고 데이터베이스에 엔터티를 저장 합니다. 큐가 비어 있을 때까지 루프를 실행 합니다.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample4.cs)]

큐 메시지를 폴링하는 경우 트랜잭션 요금이 발생 하므로 처리 대기 중인 메시지가 없는 경우 작업자 역할의 `RunAsync` 메서드는 `Task.Delay(1000)`를 호출 하 여 다시 폴링하기 전에 1 초 동안 대기 합니다.

웹 프로젝트에서 IIS는 제한 된 스레드 풀을 관리 하므로 비동기 코드를 추가 하면 성능이 자동으로 향상 될 수 있습니다. 작업자 역할 프로젝트에는 그렇지 않습니다. 작업자 역할의 확장성을 향상 시키기 위해 다중 스레드 코드를 작성 하거나 비동기 코드를 사용 하 여 [병렬 프로그래밍](https://msdn.microsoft.com/library/ff963553.aspx)을 구현할 수 있습니다. 이 샘플은 병렬 프로그래밍을 구현 하지는 않지만 병렬 프로그래밍을 구현할 수 있도록 코드를 비동기 방식으로 만드는 방법을 보여 줍니다.

## <a name="summary"></a>요약

이 장에서는 큐 중심 작업 패턴을 구현 하 여 응용 프로그램 응답성, 안정성 및 확장성을 개선 하는 방법을 살펴보았습니다.

이는이 e-learning에서 다룬 13 가지 패턴 중 마지막 이지만, 성공적인 클라우드 앱을 빌드하는 데 도움이 될 수 있는 다른 많은 패턴 및 사례가 있습니다. [마지막 챕터](more-patterns-and-guidance.md) 에서는 이러한 13 개 패턴에서 다루지 않은 항목에 대 한 리소스 링크를 제공 합니다.

<a id="resources"></a>
## <a name="resources"></a>리소스

큐에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

설명서:

- [Microsoft Azure Storage 큐 1 부: 시작 하기](https://www.red-gate.com/simple-talk/cloud/platform-as-a-service/microsoft-azure-storage-queues-part-1-getting-started/) Roman Schacherl 문서.
- [백그라운드 작업 실행](https://msdn.microsoft.com/library/ff803365.aspx), [응용 프로그램을 클라우드로 이동](https://msdn.microsoft.com/library/ff728592.aspx) 하는 5 장, Microsoft 패턴 및 관행의 세 번째 버전입니다. 특히 ["Azure Storage 큐 사용"](https://msdn.microsoft.com/library/ff803365.aspx#sec7)섹션을 사용 하십시오.
- [Azure에서 큐 기반 메시징 솔루션의 확장성 및 비용 효율성을 극대화 하기 위한 모범 사례](https://msdn.microsoft.com/library/windowsazure/hh697709.aspx)입니다. 백서 Valery Mizonov.
- [Azure 큐와 Service Bus 큐 비교](https://msdn.microsoft.com/magazine/jj159884.aspx) MSDN Magazine 문서에서는 사용할 큐 서비스를 선택 하는 데 도움이 되는 추가 정보를 제공 합니다. 이 문서에서는 Service Bus 인증을 위한 ACS에 종속 되어 있음을 언급 합니다. 즉, ACS를 사용할 수 없을 때 SB 큐를 사용할 수 없습니다. 그러나이 문서를 작성 했으므로 SB가 ACS 대신 [SAS 토큰](https://msdn.microsoft.com/library/windowsazure/dn170477.aspx) 을 사용할 수 있도록 변경 되었습니다.
- [Microsoft 패턴 및 사례-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx) 비동기 메시징 입문, 파이프 및 필터 패턴, 보정 트랜잭션 패턴, 경쟁 소비자 패턴, CQRS 패턴을 참조 하세요.
- [CQRS](https://msdn.microsoft.com/library/jj554200). CQRS for Microsoft 패턴 및 관행에 대 한 문서입니다.

비디오:

- [안전 하지 않음: 확장 가능 하 고 복원 가능한 Cloud Services 빌드](https://channel9.msdn.com/Series/FailSafe) 9 개 부분으로 구성 된 비디오 시리즈, Marc Mercuri 및 Mark Simm. Microsoft의 Microsoft CAT (고객 자문 팀) 경험을 통해 실제 고객과 함께 제공 되는 스토리를 통해 매우 편리 하 게 액세스할 수 있고 흥미로운 방식으로 높은 수준의 개념 및 아키텍처 원칙을 제공 합니다. Azure Storage 서비스 및 큐에 대 한 소개는 35:13에서 시작 하는 에피소드 5를 참조 하십시오.

> [!div class="step-by-step"]
> [이전](distributed-caching.md)
> [다음](more-patterns-and-guidance.md)
