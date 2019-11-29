---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
title: 일시적인 오류 처리 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 11/03/2015
ms.assetid: 7ead83bc-c08c-4b26-8617-00e07292e35c
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
msc.type: authoredcontent
ms.openlocfilehash: fc281e3d8f7c9edd4d98b029a67e58113132a8b3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583652"
---
# <a name="transient-fault-handling-building-real-world-cloud-apps-with-azure"></a>일시적인 오류 처리 (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

실제 클라우드 앱을 디자인할 때 고려해 야 할 사항 중 하나는 임시 서비스 중단을 처리 하는 방법입니다. 이 문제는 네트워크 연결 및 외부 서비스에 따라 다르므로 클라우드 앱에서 고유 하 게 중요 합니다. 일반적으로 자체적으로 복구 하는 결함이 거의 없을 수 있으며, 지능적으로 처리할 준비를 하지 않은 경우에는 고객에 게 잘못 된 환경이 발생 합니다.

## <a name="causes-of-transient-failures"></a>일시적인 오류 원인

클라우드 환경에서 실패 및 삭제 된 데이터베이스 연결이 주기적으로 발생 하는 것을 확인할 수 있습니다. 웹 서버와 데이터베이스 서버가 직접 물리적으로 연결 된 온-프레미스 환경에 비해 더 많은 부하 분산 장치를 사용할 수 있기 때문입니다. 또한 경우에 따라, 다중 테 넌 트 서비스를 사용 하는 경우 서비스를 사용 하는 다른 사용자가 과도 하 게 도달 하기 때문에 서비스에 대 한 호출이 느리거나 시간이 초과 되는 것을 볼 수 있습니다. 다른 경우에는 서비스에 너무 자주 도달 하는 사용자가 있을 수 있으며, 서비스는 서비스의 다른 테 넌 트에 부정적인 영향을 주지 않도록 하기 위해 제한을 의도적으로 거부 합니다.

## <a name="use-smart-retryback-off-logic-to-mitigate-the-effect-of-transient-failures"></a>자동 재시도/백오프 논리를 사용 하 여 일시적인 오류의 영향을 완화 합니다.

예외를 throw 하 고 고객에 게 사용할 수 없음 또는 오류 페이지를 표시 하는 대신 일반적으로 일시적인 오류를 인식 하 고 오류를 일으킨 작업을 자동으로 다시 시도 하 여 성공 하기 전까지 시도할 수 있습니다. 대부분의 경우 두 번째 시도에서 작업이 성공적으로 수행 되 고, 고객이 문제를 인식 하지 못하는 상태에서 오류를 복구 합니다.

스마트 재시도 논리를 구현 하는 방법에는 여러 가지가 있습니다.

- Microsoft 패턴 &amp; 실습 그룹에는 SQL Database 액세스에 대해 ADO.NET를 사용 하는 경우 (Entity Framework를 통해 하지 않음) 모든 항목을 수행 하는 [일시적인 오류 처리 응용 프로그램 블록이](https://msdn.microsoft.com/library/dn440719(v=pandp.60).aspx) 있습니다. 재시도에 대 한 정책 (쿼리 또는 명령을 다시 시도 하는 횟수와 시도 사이에 대기 하는 시간)을 설정 하 고 *using* 블록에서 SQL 코드를 래핑합니다.

    [!code-csharp[Main](transient-fault-handling/samples/sample1.cs)]

    TFH는 [Azure In-Role Cache](https://msdn.microsoft.com/library/windowsazure/dn386103.aspx) 및 [Service Bus](https://azure.microsoft.com/services/service-bus/)도 지원 합니다.
- Entity Framework 사용 하는 경우 일반적으로 SQL 연결을 사용 하 여 직접 작업 하지 않으므로이 패턴 및 사례 패키지를 사용할 수 없지만, 6 Entity Framework는 이러한 종류의 재시도 논리를 프레임 워크에 바로 빌드할 수 있습니다. 다시 시도 전략을 지정 하는 것과 비슷한 방식으로 EF는 데이터베이스에 액세스할 때마다 해당 전략을 사용 합니다.

    Fix It 앱에서이 기능을 사용 하려면 *Dbconfiguration* 에서 파생 되는 클래스를 추가 하 고 다시 시도 논리를 설정 하기만 하면 됩니다.

    [!code-csharp[Main](transient-fault-handling/samples/sample2.cs)]

    프레임 워크가 일반적으로 일시적인 오류로 식별 하는 SQL Database 예외의 경우, 표시 되는 코드는 작업을 최대 3 번 다시 시도 하 고 재시도 간 지 수 백오프 지연 시간을 5 초의 최대 지연 시간으로 다시 시도 하도록 EF에 지시 합니다. 지 수 백오프는 각 시도가 실패 한 후 다시 시도 하기 전에 더 오랜 시간 동안 대기 함을 의미 합니다. 행에서 세 번의 시도가 실패 하면 예외가 throw 됩니다. 회로 차단기에 대 한 다음 섹션에서는 지 수 백오프 및 제한 된 횟수의 재시도를 원하는 이유를 설명 합니다.

    Azure Storage 서비스를 사용 하는 경우 It 앱이 Blob에 대해 수행 하는 픽스와 .NET Storage 클라이언트 API는 동일한 종류의 논리를 이미 구현 하는 경우와 유사한 문제를 해결할 수 있습니다. 다시 시도 정책을 지정 하기만 하면 됩니다. 기본 설정에 만족 하는 경우에도이 작업을 수행할 필요가 없습니다.

<a id="circuitbreakers"></a>
## <a name="circuit-breakers"></a>회로 차단기

너무 많은 시간 동안 너무 많은 시간 동안 다시 시도 하지 않으려는 이유는 여러 가지가 있습니다.

- 실패 한 요청을 영구적으로 재시도 하는 너무 많은 사용자가 다른 사용자의 경험을 저하 시킬 수 있습니다. 수백만 명의 사용자가 모두 반복 해 서 다시 시도 하는 경우에는 IIS 디스패치 큐를 설정 하 고 앱에서 요청을 처리 하지 못하게 할 수 있습니다.
- 서비스 오류로 인해 모든 사용자가 다시 시도 하는 경우에는 복구를 시작할 때 서비스가 장애를 유발 하는 많은 요청이 지연 될 수 있습니다.
- 이 오류가 제한으로 인 한 것이 고 서비스에서 조정에 사용 하는 시간이 있는 경우 계속 해 서 재시도를 통해 해당 창을 이동 하 고 제한을 계속 진행할 수 있습니다.
- 웹 페이지가 렌더링 될 때까지 대기 하는 사용자가 있을 수 있습니다. 사용자의 대기 시간이 너무 오래 걸리는 경우 나중에 다시 시도 하는 것이 더 어려울 수 있습니다.

지 수 백오프는 서비스가 응용 프로그램에서 얻을 수 있는 재시도 빈도를 제한 하 여 이러한 문제 중 일부를 해결 합니다. 그러나 *회로 차단기*도 필요 합니다. 즉, 특정 재시도 임계값에서 앱이 다시 시도를 중지 하 고 다음 중 하 나와 같은 다른 작업을 수행 합니다.

- 사용자 지정 대체 (fallback). Reuters에서 주식 가격을 가져올 수 없는 경우 Bloomberg에서 가져올 수 있습니다. 또는 데이터베이스에서 데이터를 가져올 수 없는 경우에는 캐시에서 데이터를 가져올 수 있습니다.
- 자동 오류가 발생 합니다. 응용 프로그램에 대해 서비스에서 필요로 하는 항목이 전부 또는 전혀 없는 경우 데이터를 가져올 수 없는 경우에만 null을 반환 합니다. Fix It 작업을 표시 하 고 Blob service 응답 하지 않는 경우 이미지 없이 작업 세부 정보를 표시할 수 있습니다.
- 빠른 오류. 다른 사용자에 대 한 서비스 중단을 유발 하거나 제한 기간을 확장할 수 있는 다시 시도 요청으로 서비스의 초과를 방지 하기 위해 사용자에 게 오류를 발생 시킵니다. 친숙 한 "나중에 다시 시도" 메시지를 표시할 수 있습니다.

크기에 맞게 모든 재시도 정책이 없습니다. 사용자가 응답을 기다리는 동기 웹 앱에서 보다 많은 시간을 다시 시도 하 고 비동기 백그라운드 작업자 프로세스에서 더 오래 기다릴 수 있습니다. 관계형 데이터베이스 서비스에 대 한 재시도 사이에서 캐시 서비스에 대 한 것 보다 더 오래 기다릴 수 있습니다. 다음은 몇 가지 샘플 권장 재시도 정책입니다. ("Fast First"는 첫 번째 재시도 전에 지연 되지 않음을 의미 합니다.

![샘플 재시도 정책](transient-fault-handling/_static/image1.png)

SQL Database 재시도 정책 지침은 [일시적인 오류 및 SQL Database에 대 한 연결 오류 문제 해결](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/)을 참조 하세요.

## <a name="summary"></a>요약

재시도/백오프 전략은 고객에 게 대부분의 일시적인 오류를 표시 하는 데 도움이 될 수 있으며, Microsoft에서는 ADO.NET, Entity Framework 또는 Azure Storage 서비스를 사용 하는지에 따라 전략을 구현 하는 작업을 최소화 하는 데 사용할 수 있는 프레임 워크를 제공 합니다.

[다음 장에서](distributed-caching.md)는 분산 캐싱을 사용 하 여 성능 및 안정성을 향상 시키는 방법에 대해 살펴보겠습니다.

## <a name="resources"></a>자료

자세한 내용은 다음 참고 자료를 참조하십시오.

Documentation

- [Azure Cloud Services에서 대규모 서비스를 디자인 하는 방법에 대 한 모범 사례](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)입니다. 이 백서에서는 Simm 및 Michael Thomassy을 표시 합니다. 안전 계열과 유사 하지만 자세한 방법에 대해 자세히 설명 합니다. 원격 분석 및 진단 섹션을 참조 하세요.
- [비상 복구: 복원 력 있는 클라우드 아키텍처에 대 한 지침](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)입니다. Marc Mercuri, Ulrich Homann 및 Andrew Townhill의 백서입니다. 복구 비디오 시리즈의 웹 페이지 버전입니다.
- [Microsoft 패턴 및 사례-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx) 재시도 패턴, Scheduler 에이전트 감독자 패턴을 참조 하세요.
- [Azure SQL Database에서 내결함성이](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx)있습니다. Tony Petrossian의 블로그 게시물입니다.
- [Entity Framework 연결 복원 력/재시도 논리](https://msdn.microsoft.com/data/dn456835)입니다. Entity Framework 6의 일시적인 오류 처리 기능을 사용 하 고 사용자 지정 하는 방법입니다.
- [ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 연결 복원 력 및 명령 가로채기](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md) 네 부분으로 구성 된 자습서 시리즈의 네 번째 부분에서는 SQL Database에 대 한 EF 6 연결 복원 력 기능을 설정 하는 방법을 보여 줍니다.

비디오

- [안전 하지 않음: 확장 가능 하 고 복원 가능한 Cloud Services 빌드](https://channel9.msdn.com/Series/FailSafe) Ulrich HoMarc Mercuri 및 Mark Simm에서 9 부분으로 된 시리즈. Microsoft의 Microsoft CAT (고객 자문 팀) 경험을 통해 실제 고객과 함께 제공 되는 스토리를 통해 매우 편리 하 게 액세스할 수 있고 흥미로운 방식으로 높은 수준의 개념 및 아키텍처 원칙을 제공 합니다. 40:55에서 시작 하는 에피소드 3의 회로 차단기에 대 한 설명을 참조 하세요.
- [대규모 빌드: Azure 고객 으로부터 얻은 교훈-2 부](https://channel9.msdn.com/Events/Build/2012/3-030). 표시 Simm은 오류 설계, 일시적인 오류 처리 및 모든 항목 계측에 대해 설명 합니다.

코드 샘플

- [Azure의 클라우드 서비스 기본 사항](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)입니다. [Enterprise Library TFH (일시적인 오류 처리 블록](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/) )를 사용 하는 방법을 보여 주는 Microsoft Azure 고객 자문 팀에서 만든 샘플 응용 프로그램입니다. 자세한 내용은 [클라우드 서비스의 기본 데이터 액세스 계층 – 일시적인 오류 처리](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx)를 참조 하세요. TFH는 ADO.NET를 사용 하 여 데이터베이스에 직접 액세스 하는 것이 좋습니다 (Entity Framework 사용 하지 않음).

> [!div class="step-by-step"]
> [이전](monitoring-and-telemetry.md)
> [다음](distributed-caching.md)
