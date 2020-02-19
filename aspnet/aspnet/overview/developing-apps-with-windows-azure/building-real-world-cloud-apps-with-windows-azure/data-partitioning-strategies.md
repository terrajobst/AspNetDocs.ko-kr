---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
title: 데이터 분할 전략 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 513837a7-cfea-4568-a4e9-1f5901245d24
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
msc.type: authoredcontent
ms.openlocfilehash: efc3fa0255aa765e515412c5fa4098303a9d9234
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457026"
---
# <a name="data-partitioning-strategies-building-real-world-cloud-apps-with-azure"></a>데이터 분할 전략 (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 시리즈에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

이전에는 웹 서버를 추가 및 제거 하 여 클라우드 응용 프로그램의 웹 계층을 확장 하는 것이 얼마나 쉬운지 알아보았습니다. 그러나 모두 동일한 데이터 저장소에 도달 하는 경우 응용 프로그램의 병목 상태가 프런트 엔드에서 백 엔드로 이동 하 고 데이터 계층은 크기를 조정 하는 것이 가장 좋습니다. 이 장에서는 데이터를 여러 관계형 데이터베이스로 분할 하거나 관계형 데이터베이스 저장소를 다른 데이터 저장소 옵션과 결합 하 여 데이터 계층을 확장 가능 하 게 만드는 방법을 살펴봅니다.

앞에서 설명한 것과 같은 이유로 파티션 구성표를 설정 하는 것이 가장 좋습니다. 앱이 프로덕션 환경에 있는 후에는 데이터 저장소 전략을 변경 하기가 매우 어렵습니다. 다른 방법에 대해 앞으로 생각 하는 경우 앱의 데이터 및 데이터 액세스 코드를 다시 구성 하는 동안 앱이 충돌 하거나 오랜 시간 동안 중단 될 때 "Twitter 순간"이 발생 하지 않도록 방지할 수 있습니다.

## <a name="the-three-vs-of-data-storage"></a>데이터 저장소의 세 가지 Vs

분할 전략이 필요한 지 여부를 확인 하기 위해 데이터에 대 한 세 가지 질문을 고려해 야 합니다.

- 볼륨 – 궁극적으로 얼마나 많은 데이터를 저장할 수 있나요? 몇 기가바이트 입니까? 수백 기가바이트 테라바이트? 페타바이트?
- 속도 – 데이터가 증가 하는 속도는 어떻습니까? 많은 양의 데이터를 생성 하지 않는 내부 앱 입니까? 고객이 이미지 및 비디오를 업로드 하는 외부 앱은 무엇 인가요?
- 다양 한 내용 – 어떤 유형의 데이터를 저장 하나요? 관계형, 이미지, 키-값 쌍, 소셜 그래프?

많은 볼륨, 개발 속도 또는 다양 한 기능을 사용 하는 경우 앱이 증가 함에 따라 효율적이 고 효율적으로 확장할 수 있도록 하 고 병목 현상이 발생 하지 않도록 하는 데 가장 적합 한 파티션 구성표의 종류를 신중 하 게 고려해 야 합니다.

기본적으로 분할에는 세 가지 방법이 있습니다.

- 수직 분할
- 행 분할
- 하이브리드 분할

## <a name="vertical-partitioning"></a>수직 분할

수직 portioning는 열을 기준으로 테이블을 분할 하는 것과 같습니다. 한 열 집합은 하나의 데이터 저장소로 이동 하 고 다른 열 집합은 다른 데이터 저장소로 이동 합니다.

예를 들어 내 앱에서 이미지를 포함 하 여 사용자에 대 한 데이터를 저장 한다고 가정 합니다.

![데이터 테이블](data-partitioning-strategies/_static/image1.png)

이 데이터를 테이블로 표시 하 고 다른 종류의 데이터를 살펴보면 왼쪽에 있는 세 개의 열에는 관계형 데이터베이스에서 효율적으로 저장할 수 있는 문자열 데이터가 있고, 오른쪽에 있는 두 열은 기본적으로 바이트 배열 이라는 것을 알 수 있습니다. 이미지 파일에서 ome 합니다. 이미지 파일 데이터를 관계형 데이터베이스에 저장할 수 있으며, 많은 사람들이 데이터를 파일 시스템에 저장 하지 않기 때문에이 작업을 수행 합니다. 필요한 데이터 볼륨을 저장할 수 있는 파일 시스템이 없거나 별도의 백업 및 복원 시스템을 관리 하지 않으려고 할 수 있습니다. 이 방법은 온-프레미스 데이터베이스 및 클라우드 데이터베이스에서 소량의 데이터에 적합 합니다. 온-프레미스 환경에서는 DBA가 모든 작업을 처리 하는 것이 더 쉬울 수 있습니다.

그러나 클라우드 데이터베이스에서 저장소는 상대적으로 비용이 많이 들고, 많은 이미지를 사용 하는 경우 데이터베이스가 효율적으로 작동할 수 있는 한도를 초과 하 여 데이터베이스 크기가 증가할 수 있습니다. 데이터를 세로로 분할 하 여 이러한 문제를 해결할 수 있습니다. 즉, 데이터 테이블의 각 열에 가장 적합 한 데이터 저장소를 선택 합니다. 이 예에서는 문자열 데이터를 관계형 데이터베이스에 저장 하 고 이미지는 Blob 저장소에 저장 하는 것이 가장 적합 합니다.

![수직 분할 된 데이터 테이블](data-partitioning-strategies/_static/image2.png)

데이터베이스 대신 Blob 저장소에 이미지를 저장 하는 작업은 파일 서버를 설정 하거나 관계형 데이터베이스 외부에 저장 된 데이터의 백업 및 복원을 관리할 필요가 없기 때문에 온-프레미스 환경 보다 클라우드에서 더 실용적입니다. Blob storage 서비스에서 자동으로 처리 됩니다.

이는 Fix It 앱에서 구현 된 분할 방식 이며 [Blob storage 챕터](unstructured-blob-storage.md)의 코드를 살펴보겠습니다. 이 파티션 구성표를 사용 하지 않고 평균 이미지 크기를 3mb로 가정할 경우 Fix It 앱은 150 기가바이트의 최대 데이터베이스 크기에 도달 하기 전에 약 4만 작업을 저장할 수 있습니다. 이미지를 제거한 후에는 데이터베이스에 여러 태스크를 10 배 저장할 수 있습니다. 행 분할 구성표를 구현 하는 방법에 대해 생각해 야 하기 전에 훨씬 더 오랜 시간이 걸릴 수 있습니다. 앱이 확장 됨에 따라 대량의 저장소 요구가 매우 저렴 한 Blob storage로 이동 하기 때문에 비용이 더 느리게 증가 합니다.

## <a name="horizontal-partitioning-sharding"></a>행 분할(분할)

수평 portioning는 테이블을 행으로 분할 하는 것과 같습니다. 한 행 집합은 하나의 데이터 저장소로 이동 하 고 다른 행 집합은 다른 데이터 저장소로 이동 합니다.

동일한 데이터 집합을 지정 하는 경우 다른 옵션은 다양 한 범위의 고객 이름을 다른 데이터베이스에 저장 하는 것입니다.

![행 분할 된 데이터 테이블](data-partitioning-strategies/_static/image3.png)

핫 스폿을 방지 하기 위해 데이터가 균등 하 게 분산 되도록 분할 체계에 대해 매우 주의를 기울여야 합니다. 많은 사람들이 특정 공통 문자로 시작 하는 성을 사용 하기 때문에 성의 첫 글자를 사용 하는이 간단한 예제는이 요구 사항을 충족 하지 않습니다. 대부분의 경우에는 약간의 작은 데이터베이스를 사용할 수 있기 때문에 이전에는 테이블 크기 제한에 도달 하는 것이 좋습니다.

수평 분할의 한 쪽은 모든 데이터에 대해 쿼리를 수행 하기 어려울 수 있습니다. 이 예제에서 쿼리는 앱에 저장 된 모든 데이터를 가져오기 위해 최대 26 개의 다른 데이터베이스를 그려야 합니다.

## <a name="hybrid-partitioning"></a>하이브리드 분할

수직 분할과 수평 분할을 결합할 수 있습니다. 예를 들어 예제 데이터에서 이미지를 Blob 저장소에 저장 하 고 문자열 데이터를 수평으로 분할할 수 있습니다.

![데이터 테이블 하이브리드 분할](data-partitioning-strategies/_static/image4.png)

## <a name="partitioning-a-production-application"></a>프로덕션 응용 프로그램 분할

개념적으로 파티션 구성표의 작동 방식을 쉽게 확인할 수 있지만, 모든 분할 체계를 사용 하면 코드 복잡성이 증가 하 고 처리 해야 하는 여러 가지 새로운 문제가 발생 합니다. Blob 저장소로 이미지를 이동 하는 경우 저장소 서비스가 다운 될 때 어떻게 해야 하나요? Blob 보안을 처리 하는 방법 데이터베이스와 blob 저장소가 동기화 되지 않으면 어떻게 되나요? 분할 하는 경우 모든 데이터베이스에서 쿼리를 처리 하는 방법은 무엇 인가요?

프로덕션으로 이동 하기 전에 계획 하는 경우에는 이러한 문제를 관리할 수 있습니다. 이러한 작업을 수행 하지 않은 많은 사람들이 나중에 수행 했습니다. 평균적으로 고객 자문 팀 (CAT) 팀은 앱이 매우 큰 방식으로 진행 중인 고객 으로부터 한 달에 한 번 당황한 전화 통화를 하 고이 계획을 수행 하지 않았습니다. 예를 들면 다음과 같습니다. "Help! 단일 데이터 저장소에 모든 항목을 저장 하 고 45 일 후에 공간이 부족 합니다. " 데이터 저장소에 액세스 하는 방법에 많은 비즈니스 논리를 구축 하 고 사용자가 앱을 사용 하는 고객을 보유 하 고 있는 경우 마이그레이션 중 하루 종일 다운 하는 것은 좋지 않습니다. Herculean 노력을 통해 고객은 중단 시간 없이 즉시 데이터를 분할할 수 있습니다. 이를 방지할 수 있는 경우에는 매우 흥미롭고 매우 유용 하며 참여 하지 않을 것입니다. 이에 대 한 최신 정보를 고려 하 여 앱에 통합 하면 앱이 나중에 성장 하는 경우 훨씬 더 쉽게 사용할 수 있습니다.

## <a name="summary"></a>요약

효과적인 분할 체계를 사용 하면 클라우드 앱에서 병목 현상이 발생 하지 않고 클라우드의 데이터를 페타바이트 확장할 수 있습니다. 그리고 온-프레미스 데이터 센터에서 앱을 실행 하는 경우 처럼 대규모 컴퓨터 또는 광범위 한 인프라에 대해 앞으로 지불할 필요가 없습니다. 클라우드에서는 필요에 따라 용량을 점진적으로 추가할 수 있으며, 사용할 때 사용 하는 만큼만 요금을 지불 하 게 됩니다.

[다음 장에서](unstructured-blob-storage.md) 는 Fix It 앱이 Blob storage에 이미지를 저장 하 여 수직 분할을 구현 하는 방법을 알아봅니다.

## <a name="resources"></a>리소스

분할 전략에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

설명서:

- [Microsoft Azure Cloud Services에서 대규모 서비스를 디자인 하는 방법에 대 한 모범 사례](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)입니다. 이 백서에서는 Simm 및 Michael Thomassy을 표시 합니다.
- [Microsoft 패턴 및 사례-클라우드 디자인 패턴](https://msdn.microsoft.com/library/dn568099.aspx). 데이터 분할 지침, 분할 패턴을 참조 하세요.

비디오:

- [안전 하지 않음: 확장 가능 하 고 복원 가능한 Cloud Services 빌드](https://channel9.msdn.com/Series/FailSafe) Ulrich HoMarc Mercuri 및 Mark Simm에서 9 부분으로 된 시리즈. Microsoft의 Microsoft CAT (고객 자문 팀) 경험을 통해 실제 고객과 함께 제공 되는 스토리를 통해 매우 편리 하 게 액세스할 수 있고 흥미로운 방식으로 높은 수준의 개념 및 아키텍처 원칙을 제공 합니다. 에피소드 7의 분할 논의를 참조 하세요.
- [대규모 빌드: Windows Azure 고객 으로부터 얻은 교훈-파트 I](https://channel9.msdn.com/Events/Build/2012/3-029). 19:49에서 시작 하 여 분할 전략, 분할를 구현 하는 방법 및 SQL Database 페더레이션을 설명 합니다. 안전 계열과 유사 하지만 자세한 방법에 대해 자세히 설명 합니다.

샘플 코드:

- [Microsoft Azure의 클라우드 서비스 기본 사항](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)입니다. 분할 된 데이터베이스를 포함 하는 샘플 응용 프로그램입니다. 구현 된 분할 체계에 대 한 설명은 Windows Azure 블로그의 [DAL – 분할 OF RDBMS](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx) 를 참조 하세요.

> [!div class="step-by-step"]
> [이전](data-storage-options.md)
> [다음](unstructured-blob-storage.md)
