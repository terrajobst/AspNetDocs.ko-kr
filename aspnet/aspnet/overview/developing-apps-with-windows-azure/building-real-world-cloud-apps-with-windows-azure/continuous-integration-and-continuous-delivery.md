---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
title: 지속적인 통합 및 지속적인 업데이트 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: eaece9f5-f80c-428b-b771-5db66d275b7d
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
msc.type: authoredcontent
ms.openlocfilehash: 52c710053feca7872aa6fcc93c99bce90359f8fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585873"
---
# <a name="continuous-integration-and-continuous-delivery-building-real-world-cloud-apps-with-azure"></a>지속적인 통합 및 지속적인 업데이트 (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

처음 두 가지 권장 되는 개발 프로세스 패턴은 [모든 항목](automate-everything.md) 및 [소스 제어](source-control.md)를 자동화 하 고 세 번째 프로세스 패턴은 이러한 패턴을 결합 합니다. CI (연속 통합)는 개발자가 소스 리포지토리에 코드를 체크 인할 때마다 빌드가 자동으로 트리거됩니다. 지속적인 업데이트 (CD)는이 한 단계를 추가로 수행 합니다. 빌드 및 자동화 된 단위 테스트가 성공한 후에는 추가 심층 테스트를 수행할 수 있는 환경에 응용 프로그램을 자동으로 배포 합니다.

클라우드를 사용 하면 환경 리소스를 사용 하는 동안에만 비용을 지불 하므로 테스트 환경을 유지 관리 하는 비용을 최소화할 수 있습니다. 필요한 경우 CD 프로세스에서 테스트 환경을 설정할 수 있으며 테스트를 완료할 때 환경을 종료할 수 있습니다.

## <a name="continuous-integration-and-continuous-delivery-workflow"></a>연속 통합 및 지속적인 업데이트 워크플로

일반적으로 개발 및 스테이징 환경에 대 한 지속적인 업데이트를 수행 하는 것이 좋습니다. Microsoft의 경우에도 대부분의 팀에는 프로덕션 배포를 위한 수동 검토 및 승인 프로세스가 필요 합니다. 프로덕션 배포의 경우 개발 팀의 주요 사용자를 지원 하거나 트래픽이 낮은 기간에 사용할 때 이러한 상황이 발생 하는지 확인 하는 것이 좋습니다. 하지만 개발 및 테스트 환경을 완전히 자동화 하는 것을 방지 하기 위해 모든 개발자가 변경 내용을 확인 하 고 환경에서 승인 테스트를 수행 하도록 설정 하는 것은 아닙니다.

[Microsoft 패턴 및 방법에 대 한 다음 다이어그램에서는 연속 업데이트에 대 한](https://aka.ms/ReleasePipeline) 일반적인 워크플로를 보여 줍니다. 이미지를 클릭 하 여 원래 컨텍스트에서 전체 크기를 확인 합니다.

[![연속 배달 워크플로](continuous-integration-and-continuous-delivery/_static/image1.png)](https://msdn.microsoft.com/library/dn449955.aspx)

## <a name="how-the-cloud-enables-cost-effective-ci-and-cd"></a>클라우드를 사용 하 여 비용 효율적인 CI 및 CD를 사용 하는 방법

Azure에서 이러한 프로세스를 쉽게 자동화할 수 있습니다. 클라우드에서 모든 항목을 실행 하 고 있기 때문에 빌드 또는 테스트 환경에 대 한 서버를 구입 하거나 관리할 필요가 없습니다. 그리고 서버를 사용 하 여 테스트를 수행할 때까지 기다릴 필요가 없습니다. 사용자가 수행 하는 모든 빌드에서는 자동화 스크립트를 사용 하 여 Azure에서 테스트 환경을 실행 하 고, 수용 테스트를 실행 하 고,이에 대 한 추가 심층 테스트를 실행 하 고, 잠시 후에 종료할 수 있습니다. 또한 2 시간 또는 8 시간 또는 하루 동안만 해당 서버를 실행 하는 경우에는 컴퓨터가 실제로 실행 되는 시간에 대해서만 요금을 지불 하기 때문에 비용을 지불 해야 하는 비용을 최소화 해야 합니다. 예를 들어, Fix it 응용 프로그램에 필요한 환경은 무료 수준에서 한 계층으로 이동 하는 경우 기본적으로 시간당 1tb를 차지 합니다. 한 달 동안 한 번에 한 시간에 한 번만 환경을 실행 하는 경우 테스트 환경은 Starbucks에서 구매한 latte 보다 저렴 한 것일 수 있습니다.

## <a name="azure-devops-services"></a>Azure DevOps Services 

Azure DevOps Services는 배포 계획부터 응용 프로그램 개발에 도움이 되는 다양 한 기능을 제공 합니다.

- Git (distributed) 및 TFVC (중앙 집중식) 소스 제어를 모두 지원 합니다.
- 탄력적 빌드 서비스를 제공 합니다. 즉, 필요할 때 동적으로 빌드 서버를 만들고 작업이 완료 되 면 작동을 중단 합니다. 사용자가 소스 코드 변경 내용을 체크 인할 때 빌드를 자동으로 시작할 수 있으며, 대부분의 시간 동안 유휴 상태에 있는 고유한 빌드 서버에 대 한 할당 및 요금을 지불할 필요가 없습니다. 빌드 서비스는 특정 개수의 빌드를 초과 하지 않는 한 무료입니다. 많은 양의 빌드를 수행 해야 하는 경우 예약 된 빌드 서버에 대해 약간의 추가 비용을 지불할 수 있습니다.
- Azure에 대 한 지속적인 업데이트를 지원 합니다.
- 자동화 된 부하 테스트를 지원 합니다. 부하 테스트는 클라우드 앱에 중요 하지만 너무 늦을 때까지 종종 연락이 중단 될 수 있습니다. 부하 테스트는 수천 명의 사용자가 많은 앱을 사용 하 여 응용 프로그램을 프로덕션 환경으로 릴리스하기 전에 병목 상태를 찾고 처리량을 향상 시킬 수 있도록 합니다.
- 팀 대화방 공동 작업을 지원 하므로 소규모 agile 팀에 대 한 실시간 통신과 공동 작업을 용이 하 게 합니다.
- Agile 프로젝트 관리를 지원 합니다.

Azure DevOps Services의 지속적인 통합 및 배달 기능에 대 한 자세한 내용은 [Azure DevOps 설명서](/azure/devops/index)를 참조 하세요.

키를 사용 하는 프로젝트 관리, 팀 공동 작업 및 소스 제어 솔루션을 찾고 있는 경우 Azure DevOps Services 확인 하세요. [Azure DevOps Services](https://dev.azure.com/)에서 등록 합니다.

## <a name="summary"></a>요약

처음 세 가지 클라우드 개발 패턴은 주기 시간이 짧은 반복 가능 하 고 안정적 이며 예측 가능한 개발 프로세스를 구현 하는 방법에 대 한 것입니다. [다음 장에서](web-development-best-practices.md) 는 아키텍처 및 코딩 패턴을 확인 하기 시작 합니다.

## <a name="resources"></a>자료

자세한 내용은 [Azure App Service에서 웹 앱 배포](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)를 참조 하세요.

또한 다음 리소스를 참조 하세요.

- [Team Foundation Server 2012를 사용 하 여 릴리스 파이프라인 빌드](https://aka.ms/ReleasePipeline) Microsoft 패턴 및 관행에 대 한 e-learning, 실습 교육 및 샘플 코드는 지속적인 업데이트에 대 한 자세한 소개를 제공 합니다. Visual Studio Lab Management 및 Visual Studio Release Management의 사용에 대해 설명 합니다.
- [ALM Rangers DevOps 도구 및 지침을](https://aka.ms/vsarsolutions/)제공 합니다. ALM Rangers는 DevOps 워크 벤치 &amp; 샘플을 소개 하 고 tfs 2012를 사용 하 여 릴리스 파이프라인을 구축 하는 것이 좋은 방법으로 tfs 2012을 *사용 하 여 릴리스 파이프라인을 구축*하 고, tfs에 대 한 devops &amp; Release Management의 개념을 배우고, 타이어를 시작 하는 유용한 방법을 제공 합니다. 이 지침에서는 한 번 빌드하고 여러 환경에 배포 하는 방법을 보여 줍니다.
- [Visual Studio 2012을 사용한 연속 배달 테스트](https://msdn.microsoft.com/library/jj159345.aspx). Microsoft 패턴 및 관행의 전자 서적에서는 지속적인 업데이트를 통해 자동화 된 테스트를 통합 하는 방법을 설명 합니다.
- [Windowsazuredeploymenttracker](https://github.com/RyanTBerry/WindowsAzureDeploymentTracker). TFS에서 빌드를 캡처하고 (레이블 기반) 빌드하고 패키지 하 고, DevOps 역할의 누군가가 특정 측면을 구성 하 고 Azure에 푸시할 수 있도록 설계 된 도구에 대 한 소스 코드입니다. 이 도구는 이전에 배포 된 버전으로 작업이 "롤백" 되도록 설정 하기 위해 배포 프로세스를 추적 합니다. 이 도구에는 외부 종속성이 없고 TFS Api 및 Azure SDK를 사용 하 여 독립 실행형으로 작동할 수 있습니다.
- [지속적인 업데이트: 빌드, 테스트 및 배포 자동화를 통해 신뢰할 수 있는 소프트웨어 릴리스입니다](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1377126361). Jez humble 변변치의 책입니다.
- [릴리스! 프로덕션이 준비 된 소프트웨어를 설계 하 고 배포](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)합니다. Nygard by.

> [!div class="step-by-step"]
> [이전](source-control.md)
> [다음](web-development-best-practices.md)
