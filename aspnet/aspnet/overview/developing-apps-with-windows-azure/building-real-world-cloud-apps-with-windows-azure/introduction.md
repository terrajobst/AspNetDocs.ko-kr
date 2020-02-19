---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: Azure를 사용 하 여 실제 클라우드 앱 빌드 | Microsoft Docs
author: MikeWasson
description: 이 문서에서는 실제 클라우드 솔루션을 빌드하는 패턴 기반 접근 방식을 안내 합니다. 패턴은 개발 프로세스 뿐만 아니라 ...에도 적용 됩니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: b88573b3702b755b155e8da35f5f8a67931bafc6
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457117"
---
# <a name="building-real-world-cloud-apps-with-azure"></a>Azure를 사용 하 여 실제 클라우드 앱 빌드

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 이 문서에서는 실제 클라우드 솔루션을 빌드하는 패턴 기반 접근 방식을 안내 합니다. 패턴은 아키텍처 및 코딩 방식 뿐만 아니라 개발 프로세스에도 적용 됩니다.
> 
> 콘텐츠는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 하며 2013, 2013 년 6 월 ([1](http://vimeo.com/68215538)부, [2 부](http://vimeo.com/68215602))의 Microsoft Tech Ed 오스트레일리아 ([1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)부, [2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)부)에서 Scott이 개발한 프레젠테이션을 기반으로 합니다. 비디오에서 필기 형식으로 전환 하는 동안 [다른 많은 사람들이](more-patterns-and-guidance.md#acknowledgments) 콘텐츠를 업데이트 하 고 보강 했습니다.

## <a name="intended-audience"></a>대상 그룹

클라우드를 위한 개발, 클라우드로의 이동, 클라우드 개발에 대해 관심이 있는 개발자는 여기에서 알아야 하는 가장 중요 한 개념과 방법에 대 한 간결한 개요를 확인할 수 있습니다. 개념은 구체적인 예제와 함께 설명 되어 있으며, 각 챕터는 다른 리소스에 연결 되어 자세한 정보를 제공 합니다. Microsoft 프레임 워크 및 서비스에 대 한 추가 리소스의 예제와 링크는 다른 웹 개발 프레임 워크 및 클라우드 환경에도 적용 됩니다.

이미 클라우드 용으로 개발 하 고 있는 개발자는이에 대 한 아이디어를 파악 하 여 더 성공적으로 만들 수 있습니다. 계열의 각 챕터를 독립적으로 읽을 수 있으므로 관심 있는 항목을 선택 하 고 선택할 수 있습니다.

Scott Guthrie에서 *Azure 프레젠테이션을 사용 하 여 실제 클라우드 앱을 개발* 하 고 자세한 정보 및 업데이트 정보를 원하는 모든 사용자에 게 여기에서 찾을 수 있습니다.

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a>클라우드 개발 패턴

이 전자 서적에서는 클라우드 개발을 위한 13 권장 패턴을 설명 합니다. "Pattern"은 이러한 작업을 수행 하는 데 권장 되는 방법 (클라우드 앱 개발, 디자인 및 코딩에 대 한 최상의 방법)을 의미 하는 데 사용 됩니다. 이러한 패턴은 뒤에 오는 경우 "성공의 pit를 포함" 하는 데 도움이 되는 주요 패턴입니다.

- [모든](automate-everything.md)기능을 자동화 합니다.

    - 스크립트를 사용 하 여 반복 되는 프로세스에서 효율성을 최대화 하 고 오류를 최소화 합니다.
    - 데모: Azure 관리 스크립트
- [소스 제어](source-control.md). 

    - DevOps 워크플로를 용이 하 게 하기 위해 소스 제어에서 분기 구조를 설정 합니다.
    - Demo: 소스 제어에 스크립트를 추가 합니다.
    - 데모: 중요 한 데이터를 소스 제어에서 유지 합니다.
    - 데모: Visual Studio에서 Git를 사용 합니다.
- [지속적인 통합 및 제공](continuous-integration-and-continuous-delivery.md) 

    - 각 소스 제어 체크 인을 사용 하 여 빌드 및 배포를 자동화 합니다.
- [웹 개발 모범 사례](web-development-best-practices.md). 

    - 웹 계층 상태 비저장 유지.
    - 데모: Azure App Service의 Web Apps 크기 조정 및 자동 크기 조정
    - 세션 상태를 방지 합니다.
    - CDN을 사용할 수 없는 경우 대체 (fallback)를 사용 합니다.
    - 비동기 프로그래밍 모델을 사용 합니다.
    - Demo: ASP.NET MVC 및 Entity Framework의 async
- [Single sign-on](single-sign-on.md). 

    - Azure Active Directory 소개.
    - 데모: Azure Active Directory을 사용 하는 ASP.NET 앱을 만듭니다.
- [데이터 저장소 옵션](data-storage-options.md)입니다. 

    - 데이터 저장소의 유형입니다.
    - 올바른 데이터 저장소를 선택 하는 방법
    - 데모: Azure SQL Database.
- [데이터 분할 전략](data-partitioning-strategies.md). 

    - 관계형 데이터베이스의 크기를 쉽게 조정할 수 있도록 데이터를 가로 또는 세로로 분할 합니다.
- [비구조적 blob 저장소](unstructured-blob-storage.md)입니다. 

    - Blob service를 사용 하 여 클라우드에 파일을 저장 합니다.
    - 데모: Fix It 앱에서 blob 저장소를 사용 합니다.
- [오류가 계속 발생 하도록 디자인](design-to-survive-failures.md) 

    - 오류 유형입니다.
    - 실패 범위.
    - Sla 이해.
- [모니터링 및 원격 분석](monitoring-and-telemetry.md). 

    - 원격 분석 앱을 구입 하 고 앱을 계측 하는 사용자 고유의 코드를 작성 해야 하는 이유입니다.
    - 데모: Azure에 대 한 새 유물
    - 데모: Fix It 앱에서 코드를 기록 합니다.
    - 데모: Fix It 앱에서 종속성 주입
    - 데모: Azure에서 기본 제공 되는 로깅 지원.
- [일시적인 오류 처리](transient-fault-handling.md) 

    - 일시적 오류의 영향을 완화 하기 위해 스마트 재시도/백오프 논리를 사용 합니다.
    - 데모: Entity Framework 6에서 다시 시도/백오프
- [분산 캐싱](distributed-caching.md). 

    - 분산 캐싱을 사용 하 여 확장성을 높이고 데이터베이스 트랜잭션 비용을 줄입니다.
- [큐 중심 작업 패턴](queue-centric-work-pattern.md)입니다. 

    - 웹 및 작업자 계층을 느슨하게 결합 하 여 고가용성을 지원 하 고 확장성을 향상할 수 있습니다.
    - 데모: Fix It 앱의 Azure storage 큐
- [더 많은 클라우드 앱 패턴 및 지침](more-patterns-and-guidance.md)
- [부록: Fix It 애플리케이션 예제](the-fix-it-sample-application.md)

    - 알려진 문제
    - 모범 사례
    - 다운로드, 빌드, 실행 및 배포 하는 방법을 설명 합니다.

이러한 패턴은 모든 클라우드 환경에 적용 되지만 Microsoft 기술 및 서비스 (예: Visual Studio, Team Foundation Service, ASP.NET, Azure)를 기반으로 하는 예제를 사용 하 여 설명 하겠습니다.

이 장의 나머지 부분에서는 fix it 샘플 응용 프로그램 및 Fix It 앱이 실행 되는 Azure App Service 클라우드 환경의 Web Apps를 소개 합니다.

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a>Fix it 샘플 응용 프로그램

이 설명서에 표시 되는 대부분의 스크린 샷 및 코드 예제는 권장 되는 클라우드 앱 개발 패턴 및 사례를 보여 주기 위해 [Scott Guthrie](https://weblogs.asp.net/scottgu/) 에서 원래 개발한 Fix It 앱을 기반으로 합니다.

![It 앱 홈 페이지 수정](introduction/_static/image1.png)

샘플 앱은 간단한 작업 항목 티켓 시스템입니다. 수정 된 항목이 필요한 경우 티켓을 만들어 다른 사람에 게 할당 하 고, 다른 사용자는 로그인 하 여 자신에 게 할당 된 티켓을 확인 하 고 작업이 완료 되 면 티켓을 완료로 표시할 수 있습니다.

표준 Visual Studio 웹 프로젝트입니다. ASP.NET MVC를 기반으로 하며 SQL Server 데이터베이스를 사용 합니다. IIS Express에서 로컬로 실행할 수 있으며 클라우드에서 실행할 수 있도록 Azure 웹 사이트에 배포할 수 있습니다. 양식 인증 및 로컬 데이터베이스를 사용 하거나 Google과 같은 소셜 공급자를 사용 하 여 로그인 할 수 있습니다. (나중에 Active Directory 조직 계정으로 로그인 하는 방법도 보여 드리겠습니다.)

![로그인 페이지](introduction/_static/image2.png)

로그인 한 후에는 티켓을 만들고, 사용자에 게 할당 하 고, 수정 하려는 항목의 그림을 업로드할 수 있습니다.

![Fix It 작업 만들기](introduction/_static/image3.png)

![만든 It 작업 수정](introduction/_static/image4.png)

사용자가 만든 작업 항목의 진행률을 추적 하 고, 자신에 게 할당 된 티켓을 확인 하 고, 티켓 세부 정보를 보고, 항목을 완료로 표시할 수 있습니다.

이 앱은 기능 관점에서 매우 간단한 앱 이지만 수백만 명의 사용자로 확장할 수 있고 데이터베이스 오류 및 연결 종료와 같은 작업에 탄력적으로 대처할 수 있도록 빌드하는 방법을 확인할 수 있습니다. 또한 간단 하 고 신속 하 게 개발 주기를 반복 하 여 간단 하 게 시작 하 고 앱을 더 효과적이 고 효율적으로 만들 수 있는 자동화 된 agile 개발 워크플로를 만드는 방법을 확인할 수 있습니다.

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a>Azure App Service Web Apps

Fix It 응용 프로그램에 사용 되는 클라우드 환경은 웹 사이트를 호출 하는 Azure의 서비스입니다. 이 서비스는 Vm을 만들고, 업데이트를 유지 하 고, IIS를 설치 및 구성 하지 않고도 Azure에서 사용자 고유의 웹 앱을 호스트할 수 있는 방법입니다. Microsoft는 Vm에서 사이트를 호스팅하고 자동으로 백업 및 복구 및 기타 서비스를 제공 합니다. 웹 사이트 서비스는 ASP.NET, node.js, PHP 및 Python과 함께 작동 합니다. Visual Studio, 웹 배포, FTP, Git 또는 TFS를 사용 하 여 매우 빠르게 배포할 수 있습니다. 배포를 시작 하는 시간과 인터넷을 통해 업데이트를 사용할 수 있는 시간 사이에는 일반적으로 몇 초 밖에 안 걸립니다. 모든 작업을 무료로 시작할 수 있으며 트래픽이 증가 함에 따라 확장할 수 있습니다.

백그라운드에서 Azure App Service의 Web Apps는 사용자 고유의 Vm에서 IIS를 사용 하 여 웹 사이트를 호스트 하려는 경우 사용자가 직접 작성 해야 하는 다양 한 아키텍처 구성 요소 및 기능을 제공 합니다. 한 구성 요소는 자동으로 IIS를 구성 하 고 응용 프로그램을 실행 하려는 Vm의 수에 따라 응용 프로그램을 설치 하는 배포 끝점입니다.

![배포 서비스](introduction/_static/image5.png)

사용자가 웹 사이트에 도달 하면 IIS Vm에 직접 도달 하지 않고 [ARR (응용 프로그램 요청 라우팅](https://www.iis.net/downloads/microsoft/application-request-routing) ) 부하 분산 장치를 통해 이동 합니다. 사용자의 서버에서 이러한 기능을 사용할 수 있지만, 여기서의 장점은 자동으로 설정 된다는 것입니다. 세션 선호도, IIS의 큐 크기 및 각 컴퓨터의 CPU 사용과 같은 고려 사항을 고려 하는 스마트 추론을 사용 하 여 웹 사이트를 호스트 하는 Vm으로 트래픽을 전달 합니다.

![ARR 부하 분산 장치](introduction/_static/image6.png)

컴퓨터가 중단 되 면 Azure에서 자동으로이를 순환에서 가져오고, 새 VM 인스턴스를 회전 하 고, 새 인스턴스로 트래픽을 전송 하기 시작 합니다. 즉, 응용 프로그램에 대해 중단 시간을 사용 하지 않습니다.

![컴퓨터의 자동 복구 오류](introduction/_static/image7.png)

이 모든 작업은 자동으로 수행 됩니다. Windows PowerShell, Visual Studio 또는 Azure 관리 포털을 사용 하 여 웹 사이트를 만들고 응용 프로그램을 배포 하기만 하면 됩니다.

Visual Studio에서 웹 응용 프로그램을 만들고 Azure 웹 사이트에 배포 하는 방법을 보여 주는 빠르고 쉬운 단계별 자습서는 [azure 및 ASP.NET 시작](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)을 참조 하세요.

<a id="summary"></a>
## <a name="summary"></a>요약

이 소개에서는 책에서 다루는 항목의 목록, 샘플 응용 프로그램의 스크린샷 및 Azure App Service 클라우드 환경의 Web Apps에 대 한 간략 한 개요를 제공 했습니다. 및 클라우드에서 앱을 개발할 때의 뛰어난 이점 중 하나는 테스트 환경 만들기 및 코드 배포와 같은 반복적인 개발 작업을 쉽게 자동화할 수 있다는 것입니다. 이 작업을 수행 하는 방법은 [다음 장의](automate-everything.md)주제입니다.

## <a name="resources"></a>리소스

이 장에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

설명서:

- [Azure App Service에서 Web Apps](https://azure.microsoft.com/services/app-service/web/)합니다. Web Apps에 대 한 Azure 설명서 포털 페이지입니다.
- [Web Apps, Cloud Services 및 Vm: 사용 시기](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) 이 장에 표시 된 것 처럼 WAWS는 Azure에서 웹 앱을 실행할 수 있는 세 가지 방법 중 하나입니다. 이 문서에서는 세 가지 방법의 차이점에 대해 설명 하 고 시나리오에 적합 한 항목을 선택 하는 방법에 대 한 지침을 제공 합니다. 웹 사이트와 마찬가지로 Cloud Services는 Azure의 PaaS 기능입니다. Vm은 IaaS 기능입니다. PaaS 및 IaaS에 대 한 설명은 [데이터 옵션](data-storage-options.md#paasiaas) 챕터를 참조 하세요.

비디오:

- [Scott Guthrie는 0 단계에서 시작 됩니다. Azure 클라우드 OS 무엇입니까?](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- [웹 사이트 아키텍처-Stefan Schackow를 사용](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)합니다.
- [Nir Mashkowski를 사용 하는 Azure 웹 사이트의 내부](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).

> [!div class="step-by-step"]
> [다음](automate-everything.md)
