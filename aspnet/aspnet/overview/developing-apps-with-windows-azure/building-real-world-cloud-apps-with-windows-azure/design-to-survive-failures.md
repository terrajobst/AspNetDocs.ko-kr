---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
title: 장애 상태를 유지 하기 위한 디자인 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 364ce84e-5af8-4e08-afc9-75a512b01f84
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
msc.type: authoredcontent
ms.openlocfilehash: 348232af531b5d53dc3cb46d6d2c7931d95a572d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500765"
---
# <a name="design-to-survive-failures-building-real-world-cloud-apps-with-azure"></a>장애 상태를 유지 하기 위한 디자인 (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

모든 종류의 응용 프로그램을 빌드할 때 고려해 야 할 사항 중 하나는 특히 많은 사람들이 사용할 수 있는 클라우드에서 실행 되는 응용 프로그램을 디자인 하는 방법입니다. 오류를 정상적으로 처리 하 고 다음 만큼의 값을 계속 제공할 수 있도록 앱을 디자인 하는 방법입니다. 가능한. 충분 한 시간이 지정 되 면 어떤 환경이 나 모든 소프트웨어 시스템에서 문제가 발생 합니다. 앱이 이러한 상황을 처리 하는 방법에 따라 고객이 upset 하는 방법과 문제를 분석 하 고 해결 하는 데 소요 되는 시간이 결정 됩니다.

## <a name="types-of-failures"></a>오류 유형

서로 다르게 처리 하려는 두 가지 기본 범주 범주가 있습니다.

- 일시적인 네트워크 연결 문제 등의 일시적인 자동 복구 오류
- 간섭이 필요한 오류가 발생 합니다.

일시적인 오류의 경우 앱이 신속 하 게 자동으로 복구 되도록 다시 시도 정책을 구현할 수 있습니다. 고객은 응답 시간이 약간 길어질 수 있지만 그렇지 않은 경우에는 영향을 받지 않습니다. [일시적인 오류 처리 장에서](transient-fault-handling.md)이러한 오류를 처리 하는 몇 가지 방법을 보여 드리겠습니다.

오류가 발생 하는 경우 문제를 즉시 알리고 근본 원인 분석을 용이 하 게 하는 모니터링 및 로깅 기능을 구현할 수 있습니다. [모니터링 및 원격 분석 장에서](monitoring-and-telemetry.md)이러한 종류의 오류를 해결 하는 데 도움이 되는 몇 가지 방법을 보여 드리겠습니다.

## <a name="failure-scope"></a>오류 범위

또한 단일 컴퓨터가 영향을 받는지, SQL Database 또는 저장소와 같은 전체 서비스 또는 전체 지역에 있는지에 관계 없이 실패 범위에 대해 생각해 야 합니다.

![오류 범위](design-to-survive-failures/_static/image1.png)

### <a name="machine-failures"></a>컴퓨터 오류

Azure에서 오류가 발생 한 서버는 자동으로 새 서버로 대체 되 고 잘 설계 된 클라우드 앱은 이러한 종류의 오류를 자동으로 빠르게 복구 합니다. 이전에는 상태 비저장 웹 계층의 확장성 이점을 상태 비저장, 실패 한 서버에서 복구 하는 것은 또 다른 이점이 있습니다. 복구 용이성은 SQL Database 및 Azure App Service Web Apps와 같은 PaaS (platform as a service) 기능의 이점 중 하나 이기도 합니다. 하드웨어 오류는 드물게 발생 하지만 이러한 서비스가 발생 하면 자동으로 처리 됩니다. 이러한 서비스 중 하나를 사용 하는 경우 시스템 오류를 처리 하는 코드를 작성 하지 않아도 됩니다.

### <a name="service-failures"></a>서비스 오류

클라우드 앱은 일반적으로 여러 서비스를 사용 합니다. 예를 들어 Fix It 앱은 SQL Database 서비스, 저장소 서비스 및 웹 앱을 사용 하 여 Azure App Service에 배포 합니다. 종속 된 서비스 중 하나가 실패 하면 앱에서 수행할 작업은 무엇 인가요? 일부 서비스 오류는 "죄송 합니다. 나중에 다시 시도 하세요." 라는 메시지가 표시 될 수 있습니다. 그러나 많은 시나리오에서 더 나은 성능을 볼 수 있습니다. 예를 들어 백 엔드 데이터 저장소가 다운 된 경우 사용자 입력을 수락 하 고 "귀하의 요청을 받았습니다"으로 표시 하 고 입력을 일시적으로 저장할 수 있습니다. 그런 다음 필요한 서비스가 다시 작동 하면 입력을 검색 하 여 처리할 수 있습니다.

[큐 중심 작업 패턴](queue-centric-work-pattern.md) 장에서는이 시나리오를 처리 하는 한 가지 방법을 보여 줍니다. Fix It 앱은 SQL Database에 작업을 저장 하지만 SQL Database 중단 된 경우 작업을 종료할 필요가 없습니다. 이 장에서는 큐에 작업에 대 한 사용자 입력을 저장 하는 방법과 작업자 프로세스를 사용 하 여 큐를 읽고 작업을 업데이트 하는 방법을 알아봅니다. SQL이 다운 된 경우 수정 작업을 만드는 기능은 영향을 받지 않습니다. SQL Database 사용 가능한 경우 작업자 프로세스는 새 작업을 대기 하 고 처리할 수 있습니다.

### <a name="region-failures"></a>지역 오류

전체 지역이 실패할 수 있습니다. 자연 재해는 데이터 센터를 제거할 수 있으며,이는 유성에 의해 결합 될 수 있으며, 데이터 센터에 대 한 트렁크 줄은 백 hoe를 사용 하 여 소을 farmer 하는 것과 같은 방식으로 잘릴 수 있습니다. 앱이 stricken 데이터 센터에서 호스트 되는 경우 어떤 작업을 수행 하나요? 여러 지역에서 동시에 실행 되도록 Azure에서 앱을 설정 하 여 재해가 발생 한 경우 다른 지역에서 계속 실행 되도록 할 수 있습니다. 이러한 오류는 거의 발생 하지 않으며, 대부분의 앱은 이러한 종류의 오류를 통해 중단 없이 서비스를 보장 하는 데 필요한 후프를 통해 이동 하지 않습니다. 지역 장애에도 불구 하 고 앱을 계속 사용할 수 있도록 하는 방법에 대 한 자세한 내용은 챕터의 끝 부분에 있는 리소스 섹션을 참조 하세요.

Azure의 목표는 이러한 종류의 모든 오류를 훨씬 더 쉽게 처리 하는 것이 고, 다음 장에서 설명 하는 방법에 대 한 몇 가지 예를 확인 하는 것입니다.

## <a name="slas"></a>SLA

사용자는 클라우드 환경의 Sla (서비스 수준 계약)에 대 한 정보를 자주 듣고 있습니다. 기본적으로 회사에서 서비스의 신뢰성을 확인 하는 데 사용 됩니다. 99.9% SLA는 서비스가 정확히 99.9%의 시간 동안 작동 하는 것을 의미 합니다. SLA에 대 한이 값은 매우 일반적 이며 매우 높은 값 처럼 보이지만, 실제로 남은 시간 (%)을 알 수 없습니다. 다음 표에서는 연도, 월 및 주에 대 한 다양 한 SLA 비율을 보여 줍니다.

![SLA 테이블](design-to-survive-failures/_static/image2.png)

따라서 99.9% SLA는 서비스의 작동이 43.2 8.76 중단 될 수 있습니다. 이는 대부분의 사람들이 실현 하는 시간 보다 더 작동 중단 됩니다. 따라서 개발자는 특정 휴지 시간을 사용할 수 있음을 인식 하 고 적절 한 방법으로 처리할 수 있습니다. 어느 시점에서 누군가가 앱을 사용 중이 고 서비스가 다운 될 예정 이며 고객에 게 미치는 부정적인 영향을 최소화 하려고 합니다.

SLA에 대해 알고 있어야 하는 한 가지 사항은, 매월, 매월 또는 매년 클록이 다시 설정 되나요? Azure에서는 매년 sla를 설정 하 여 매년 SLA를 설정 하는 것이 좋습니다. 월 sla는 일련의 적절 한 달로 오프셋 하 여 잘못 된 달을 숨길 수 있기 때문입니다.

물론 SLA 보다는 항상 따르는 것이 좋습니다. 일반적으로 그 보다 훨씬 더 낮습니다. 이 약속은 최대 중단 시간 보다 오랫동안 다운 되는 경우 비용을 다시 요청할 수 있다는 것입니다. 다시 얻게 되는 money의 양은 중단 시간에 대 한 비즈니스 영향을 완벽 하 게 보완 하지 못할 수 있지만 SLA의 해당 측면은 적용 정책으로 작동 하며 매우 심각 하 게 사용할 수 있다는 것을 알 수 있습니다.

### <a name="composite-slas"></a>복합 SLA

Sla를 살펴볼 때 고려해 야 할 중요 한 사항은 앱에서 여러 서비스를 사용 하는 경우 각 서비스에 별도의 SLA를 사용 하는 것입니다. 예를 들어 Fix It 앱은 Azure App Service Web Apps, Azure Storage 및 SQL Database를 사용 합니다. 다음은이 e-learning이 12 월 2013 일에 작성 되는 날짜를 기준으로 하는 SLA 번호입니다.

![SLA 웹 사이트, 저장소, SQL Database](design-to-survive-failures/_static/image3.png)

이러한 서비스 Sla를 기반으로 하 여 앱에 대해 필요한 최대 휴지 시간은 무엇 인가요? 이 경우 다운 시간은 최악의 SLA 비율 또는 99.9%와 동일 하다 고 생각할 수 있습니다. 이는 세 서비스가 모두 동시에 실패 한 경우에도 마찬가지입니다. 각 서비스는 서로 독립적으로 실패할 수 있으므로 개별 SLA 번호를 곱하여 복합 SLA를 계산 해야 합니다.

![복합 SLA](design-to-survive-failures/_static/image4.png)

따라서 앱은 한 달에 43.2 분이 아니라, 3 배, 108 분, Azure SLA 제한 내에 남아 있을 수 있습니다.

이 문제는 Azure에서 고유 하지 않습니다. Microsoft는 실제로 모든 클라우드 서비스에 대 한 최고의 클라우드 Sla를 제공 하 고, 공급 업체의 클라우드 서비스를 사용 하는 경우 처리 하는 데 유사한 문제가 있습니다. 이 하이라이트는 고객이 나 사용자에 게 영향을 줄 수 있기 때문에 의도 하지 않은 서비스 오류를 정상적으로 처리 하도록 앱을 설계 하는 방법을 고려 하는 것이 중요 합니다.

### <a name="cloud-slas-compared-to-enterprise-down-time-experience"></a>엔터프라이즈 다운 시간 환경에 비해 클라우드 Sla

경우에 따라 "내 엔터프라이즈 앱에서 이러한 문제가 발생 하지 않습니다." 라고 합니다. 한 달에 실제로 보유 한 시간을 확인 하는 경우 일반적으로 "잘 발생 합니다." 라고 표시 됩니다. 그리고 얼마나 자주 질문 하는 경우 "새 서버를 백업 또는 설치 하거나 소프트웨어를 업데이트 해야 하는 경우가 있습니다." 라고 인정 합니다. 물론 중단 시간으로 계산 됩니다. 특히 업무상 중요 하지 않은 경우 대부분의 엔터프라이즈 앱은 서비스 Sla에서 허용 하는 시간을 초과 하 여 중단 됩니다. 서버와 인프라의 역할을 하 고 사용자가이를 담당 하 고 제어 하는 경우에는 낮은 시간에 대 한 정보를 절감 하는 경향이 있습니다. 클라우드 환경에서 다른 사람에 게 의존 하 고 있는 것을 알 수 없으므로이에 대 한 걱정을 얻는 경향이 있습니다.

기업에서 클라우드 SLA를 가져오는 것 보다 더 높은 시간 비율을 달성 하는 경우 하드웨어에 많은 비용을 할애 하 여이 작업을 수행 합니다. 클라우드 서비스는이 작업을 수행할 수 있지만 해당 서비스에 대해 훨씬 더 많은 요금을 청구 해야 합니다. 대신 비용 효율적인 서비스를 활용 하 고 의도 하지 않은 오류로 인해 고객의 혼란을 최소화 하도록 소프트웨어를 디자인 합니다. 클라우드 앱 디자이너로 서의 작업은 재해가 발생 하지 않도록 방지 하기 위한 것이 아닙니다 .이 작업은 재해가 발생 하지 않도록 하는 것이 아니라 하드웨어가 아닌 소프트웨어에 집중 하는 것입니다. 엔터프라이즈 응용 프로그램은 오류 사이의 평균 시간을 최대화 하기 위해 노력 하는 반면, 클라우드 앱은 평균 복구 시간을 최소화 하려고 노력 합니다.

### <a name="not-all-cloud-services-have-slas"></a>모든 클라우드 서비스에 Sla가 있는 것은 아닙니다.

또한 모든 클라우드 서비스에는 SLA가 없어도 됩니다. 앱이 가동 시간을 보장 하지 않는 서비스에 종속 되는 경우에는 더 오래 걸릴 수 있습니다. 예를 들어 Facebook 또는 Twitter와 같은 소셜 공급자를 사용 하 여 사이트에 로그인 할 수 있도록 설정 하는 경우 SLA가 있는지 여부를 확인 하려면 서비스 공급자에 게 확인 하세요. 그러나 인증 서비스의 작동이 중단 되거나 사용자가 발생 시키는 요청 볼륨을 지원할 수 없는 경우 고객은 앱에서 잠깁니다. 일 이상 종료할 수 있습니다. 새 앱의 작성자는 수백만 개의 다운로드를 예상 하 여 Facebook 인증에 대 한 종속성을 가지 며, 실시간으로 이동 하 여 해당 서비스에 대 한 SLA가 없다는 사실을 검색 하지 않았습니다.

### <a name="not-all-downtime-counts-toward-slas"></a>모든 가동 중지 시간을 Sla로 계산 하는 것은 아닙니다.

일부 클라우드 서비스는 앱에서 서비스를 사용 하는 경우 의도적으로 서비스를 거부할 수 있습니다. 이를 *제한*이라고 합니다. 서비스에 SLA가 있는 경우 제한 해야 하는 조건의 상태를 지정 해야 하며, 앱 디자인은 이러한 조건을 피하고 적절 한 제한에 대응 해야 합니다. 예를 들어, 초당 특정 수를 초과 하는 경우 서비스에 대 한 요청이 실패 하는 경우 자동 재시도를 수행 하 여 제한이 계속 되도록 하는 것이 좋습니다. [일시적인 오류 처리 챕터](transient-fault-handling.md)의 제한에 대 한 추가 정보를 제공 합니다.

## <a name="summary"></a>요약

이 장에서는 실제 클라우드 앱이 오류를 정상적으로 유지 하기 위해 설계 되어야 하는 이유를 실현 하려고 했습니다. [다음 챕터](monitoring-and-telemetry.md)부터이 시리즈의 나머지 패턴은이 작업을 수행 하는 데 사용할 수 있는 몇 가지 전략에 대해 자세히 설명 합니다.

- 적절 한 [모니터링 및 원격 분석](monitoring-and-telemetry.md)을 통해 개입이 필요한 오류를 신속 하 게 파악 하 고 문제 해결을 위한 충분 한 정보를 얻을 수 있습니다.
- 지능형 재시도 논리를 구현 하 여 [일시적인 오류를 처리](transient-fault-handling.md) 합니다. 그러면 앱이 자동으로 다시 복구 될 수 없을 때 [회로 차단기](transient-fault-handling.md#circuitbreakers) 논리를 자동으로 복구 합니다.
- 데이터베이스 액세스와 관련 된 처리량, 대기 시간 및 연결 문제를 최소화 하기 위해 [분산 캐싱을](distributed-caching.md) 사용 합니다.
- 백 엔드가 종료 될 때 앱 프런트 엔드가 계속 작동할 수 있도록 [큐 중심 작업 패턴](queue-centric-work-pattern.md)을 통해 느슨한 결합을 구현 합니다.

## <a name="resources"></a>리소스

자세한 내용은이 전자 책의 이후 장과 다음 리소스를 참조 하세요.

설명서:

- [비상 복구: 복원 력 있는 클라우드 아키텍처에 대 한 지침](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)입니다. Marc Mercuri, Ulrich Homann 및 Andrew Townhill의 백서입니다. 복구 비디오 시리즈의 웹 페이지 버전입니다.
- [Azure Cloud Services에서 대규모 서비스를 디자인 하는 방법에 대 한 모범 사례](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)입니다. 이 백서에서는 Simm 및 Michael Thomassy을 표시 합니다.
- [Azure 비즈니스 연속성 기술 지침](https://msdn.microsoft.com/library/windowsazure/hh873027.aspx)을 제공 합니다. 백서 Patrick Wickline 및 Jason Roth.
- [Azure 응용 프로그램에 대 한 재해 복구 및 고가용성](https://msdn.microsoft.com/library/windowsazure/dn251004.aspx). Michael McKeown, Hanu Kommalapati 및 Jason Roth 별 백서.
- [Microsoft 패턴 및 사례-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx) 다중 데이터 센터 배포 지침, 회로 차단기 패턴을 참조 하세요.
- [Azure 지원-서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/).
- [Azure SQL Database의 비즈니스 연속성](https://msdn.microsoft.com/library/windowsazure/hh852669.aspx) SQL Database 고가용성 및 재해 복구 기능에 대 한 설명서입니다.
- [Azure Virtual Machines에서 SQL Server에 대 한 고가용성 및 재해 복구](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx).

비디오:

- [안전 하지 않음: 확장 가능 하 고 복원 가능한 Cloud Services 빌드](https://channel9.msdn.com/Series/FailSafe) Ulrich HoMarc Mercuri 및 Mark Simm에서 9 부분으로 된 시리즈. Microsoft의 Microsoft CAT (고객 자문 팀) 경험을 통해 실제 고객과 함께 제공 되는 스토리를 통해 매우 편리 하 게 액세스할 수 있고 흥미로운 방식으로 높은 수준의 개념 및 아키텍처 원칙을 제공 합니다. 에피소드 1과 8은 장애 발생 시 클라우드 앱을 설계 하는 이유를 심층적으로 설명 합니다. 또한 49:57에서 시작 하는 에피소드 2의 조정에 대 한 후속 논의, 56:05에서 시작 하는 에피소드 2의 오류 지점 및 오류 모드에 대 한 설명, 3 에피소드의 회로 차단기에 대 한 논의 (40:55부터 시작)를 참조 하세요.
- [대규모 빌드: Azure 고객 으로부터 얻은 교훈-2 부](https://channel9.msdn.com/Events/Build/2012/3-030). Simm 표시는 오류 설계 및 모든 항목 계측에 대 한 것입니다. 안전 계열과 유사 하지만 자세한 방법에 대해 자세히 설명 합니다.

> [!div class="step-by-step"]
> [이전](unstructured-blob-storage.md)
> [다음](monitoring-and-telemetry.md)
