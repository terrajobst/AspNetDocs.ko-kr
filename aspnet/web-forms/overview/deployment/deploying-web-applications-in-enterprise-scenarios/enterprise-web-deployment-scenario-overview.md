---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
title: '엔터프라이즈 웹 배포: 시나리오 개요 | Microsoft Docs'
author: jrjlee
description: 이 자습서 집합은 가상의 엔터프라이즈 배포 시나리오와 함께 현실적인 복잡성 수준이 있는 샘플 솔루션을 사용 하 여 ref ...
ms.author: riande
ms.date: 05/03/2012
ms.assetid: aa862153-4cd8-4e33-beeb-abf502c6664f
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
msc.type: authoredcontent
ms.openlocfilehash: 9786879844da13c21e6a953b1ab24b29ca8121e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463409"
---
# <a name="enterprise-web-deployment-scenario-overview"></a>엔터프라이즈 웹 배포: 시나리오 개요

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서 집합에서는 가상의 엔터프라이즈 배포 시나리오와 함께 현실적인 복잡성 수준의 샘플 솔루션을 사용 하 여 참조 구현을 제공 하 고 작업 및 연습에 일반적인 컨텍스트를 제공 합니다. 이 항목에서는 자습서 시나리오에 대해 설명 하 고 샘플 솔루션을 소개 합니다.

## <a name="scenario-description"></a>시나리오 설명

가상 회사인 Fabrikam, i n c .는 원격 판매 팀이 웹 인터페이스에서 연락처 정보를 저장 하 고 검색할 수 있는 솔루션을 만드는 중입니다.

Fabrikam, i n c .의 ALM (응용 프로그램 수명 주기 관리) 프로세스에서는 소프트웨어 개발 프로세스의 다양 한 단계에서 3 개의 서버 환경에 솔루션을 배포 해야 합니다.

- 개발자 테스트 또는 "샌드박스" 환경.
- 인트라넷 기반 스테이징 환경.
- 인터넷 연결 프로덕션 환경.

이러한 각 환경에는 다양 한 구성 및 보안 요구 사항이 있으며 각 환경에는 고유한 배포 과제가 있습니다.

### <a name="the-fabrikam-inc-server-infrastructure"></a>Fabrikam, Inc. 서버 인프라

이는 Fabrikam, i n c .에서 높은 수준의 개발 및 배포 인프라입니다.

![](enterprise-web-deployment-scenario-overview/_static/image1.png)

개발자 워크스테이션, 소스 제어 인프라, 개발자 테스트 환경 및 스테이징 환경은 모두 Fabrikam.net 도메인 내의 인트라넷 네트워크에 상주 합니다. 프로덕션 환경은 방화벽으로 인트라넷 네트워크에서 격리 되는 경계 네트워크 (DMZ, 완충 영역 및 스크린 된 서브넷이 라고도 함)에 있습니다. 이는 일반적인 배포 시나리오입니다. 일반적으로 방화벽 또는 게이트웨이 서버를 사용 하 여 내부 서버 인프라에서 인터넷 연결 웹 서버를 격리 합니다.

이 예제에서:

- 별도의 빌드 서버를 포함 하는 Team Foundation Server (TFS) 2010 서버는 원본 제어 및 CI (연속 통합) 기능을 제공 합니다.
- 개발자 테스트 환경에는 인터넷 정보 서비스 (IIS) 7.5 웹 서버와 SQL Server 2008 R2 데이터베이스 서버가 포함 되어 있습니다.
- 프로덕션 환경에는 SQL Server 2008 R2 데이터베이스 서버와 함께 WFF (웹 팜 프레임 워크) 컨트롤러 서버에서 동기화 된 여러 IIS 7.5 웹 서버가 포함 되어 있습니다. 실제로 데이터베이스 서버는 클러스터링 또는 미러링을 사용 하 여 확장성 및 가용성을 향상 시킬 수 있습니다.
- 스테이징 환경은 프로덕션 환경의 구성을 최대한 긴밀 하 게 복제 하도록 설계 되었습니다.
- 방화벽 및 네트워크 격리 정책은 인트라넷에서 경계 네트워크에 대 한 직접 자동화 된 배포를 허용 하지 않습니다.

이러한 각 환경의 구성에 대해서는 두 번째 자습서 인 [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)에 자세히 설명 되어 있습니다.

### <a name="team-roles-for-alm"></a>ALM 팀 역할

이러한 사용자는 연락처 관리자 솔루션을 만들고, 관리 하 고, 빌드하고, 게시 하는 데 관련 됩니다.

- Matt Hink는 Fabrikam, i n c .의 웹 응용 프로그램 개발자입니다. Visual Studio 2010을 사용 하 여 Contact Manager 솔루션을 개발한 팀의 일부입니다. Matt는 개발자 테스트 환경의 서버에 대 한 모든 관리자 권한을 가지 며,이를 통해 해당 요구 사항을 충족 하도록 환경을 구성할 수 있습니다. 또한 사용자에 게는 Contact Manager 솔루션의 소스 코드를 저장 하는 Visual Studio 2010 TFS 인스턴스에 대 한 사용자 액세스 권한이 있습니다.
- Rob Walters는 Fabrikam, Inc. 개발 팀의 서버 관리자입니다. Rob은 tfs 서버에 대 한 관리 액세스 권한을 가지 므로 TFS 및 팀 빌드의 모든 측면을 구성할 수 있습니다. 또한 Rob은 테스트 및 스테이징 웹 서버에 대 한 관리 액세스 권한을 가지 며 테스트 및 스테이징 환경에서 데이터베이스 서버의 DBA (데이터베이스 관리자) 역할을 합니다. Rob은 다음 작업을 수행 하기 위해 TFS 서버에서 팀 빌드를 구성 했습니다.

    - 사용자가 TFS에 대 한 파일을 체크 인할 때마다 응용 프로그램에서 단위 테스트를 빌드하고 실행 합니다. 이를 CI 라고 합니다.
    - 응용 프로그램에서 단위 테스트를 통과 하면 자동으로 연락처 관리자 응용 프로그램을 테스트 환경에 배포 합니다. 여기에는 초기 배포 시 테스트 서버에 데이터베이스를 게시 하는 것과 초기 배포 후에 데이터베이스에 대 한 업데이트가 포함 됩니다.
    - 단일 단계 프로세스에서 스테이징 환경에 연락처 관리자 응용 프로그램을 배포 합니다.
    - 웹 서버 관리자와 DBA가 응용 프로그램을 프로덕션 환경에 게시 하는 데 사용할 수 있는 웹 패키지를 만듭니다.
- 리사 Andrews는 Fabrikam, Inc. 프로덕션 서버에 응용 프로그램을 배포 하는 서버 관리자입니다. 연락처 관리자 응용 프로그램을 작성 한 후 TFS 팀 빌드에서 웹 배포 패키지를 저장 하는 공유에 대 한 읽기 액세스 권한이 있습니다. 또한 프로덕션 웹 서버에 대 한 관리 액세스 권한을 보유 하 여 프로덕션 환경에 응용 프로그램을 배포할 수 있습니다. 또한 프로덕션 환경의 데이터베이스 서버에 데이터베이스 및 데이터베이스 업데이트를 배포 하는 DBA 역할을 합니다.

<a id="_The_Contact_Manager"></a>

### <a name="the-contact-manager-solution"></a>Contact Manager 솔루션

Contact Manager 솔루션은 등록, 로그인 한 사용자가 웹 인터페이스를 통해 연락처 정보를 추가 및 편집할 수 있도록 설계 되었습니다. Contact Manager 솔루션은 다음과 같은 4 개의 개별 프로젝트로 구성 됩니다.

![](enterprise-web-deployment-scenario-overview/_static/image2.png)

- **연락처 관리자. Mvc**. 솔루션에 대 한 진입점을 나타내는 ASP.NET MVC3 웹 응용 프로그램 프로젝트입니다. 사용자에 게 연락처 정보를 만들고 볼 수 있는 기능을 제공 하는 것과 같은 몇 가지 기본 웹 응용 프로그램 기능을 제공 합니다. 응용 프로그램은 WCF (Windows Communication Foundation) 서비스를 사용 하 여 연락처 및 ASP.NET 응용 프로그램 서비스 데이터베이스를 관리 하 여 인증 및 권한 부여를 관리 합니다.
- **연락처 관리자. 데이터베이스**. Visual Studio 2010 데이터베이스 프로젝트입니다. 프로젝트는 연락처 세부 정보를 저장 하는 데이터베이스에 대 한 스키마를 정의 합니다.
- **연락처 관리자. 서비스**. WCF 웹 서비스 프로젝트입니다. WCF는 호출자가 Contact Manager 데이터베이스에서 만들기, 검색, 업데이트 및 삭제 (CRUD) 작업을 수행할 수 있도록 하는 끝점을 노출 합니다. 이 서비스는 Contact manager 데이터베이스와 연락처 관리자. 일반적인 .dll 어셈블리를 사용 합니다.
- **연락처 관리자. 일반적인**. 클래스 라이브러리 프로젝트입니다. WCF 서비스는이 어셈블리에 정의 된 형식을 사용 합니다.

이 시리즈의 첫 번째 자습서 인 [Enterprise의 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)에서 솔루션 및 해당 배포 요구 사항에 대 한 전체 검토가 제공 됩니다.

<a id="_Deployment_Tasks"></a>

## <a name="deployment-tasks"></a>배포 작업

응용 프로그램을 대기업의 여러 환경에 배포 하는 데는 몇 가지 고유한 작업이 있습니다. 자습서에서 다루는 주요 작업은 다음과 같습니다.

![](enterprise-web-deployment-scenario-overview/_static/image3.png)

다음은이 문서의 앞부분에서 설명 하는 사용자의 관점에서 배포 프로세스의 각 단계 목록입니다.

1. 팀의 모든 멤버는 Visual Studio 2010의 Contact Manager 솔루션을 검토 하 여 주요 배포 요구 사항 및 문제를 확인 합니다.
2. Matt Hink는 개발자 워크스테이션에서 개발자 테스트 환경으로 직접 Contact Manager 솔루션을 배포 하 여 배포 논리의 초기 테스트를 수행할 수 있습니다.
3. Matt Hink는 TFS의 소스 제어에 응용 프로그램을 추가 합니다.
4. Rob Walters는 팀 빌드에서 Contact Manager 솔루션에 대 한 다양 한 빌드 정의를 만듭니다. 사용자가 새 코드를 체크 인할 때마다 단일 빌드 정의에서 CI를 사용 하 여 개발자 테스트 환경에 솔루션을 배포 합니다. 다른 빌드 정의를 통해 사용자는 필요에 따라 스테이징 환경에 대 한 배포를 트리거할 수 있습니다.
5. 사용자가 새 코드를 체크 인할 때마다 팀 빌드는 자동으로 솔루션 구성 요소를 빌드하고, 단위 테스트를 실행 하 고, 빌드에 성공 하 고 단위 테스트를 통과 한 경우 개발자 테스트 환경에 솔루션을 배포 합니다.
6. 사용자가 스테이징 환경에 대 한 배포를 트리거하는 경우 솔루션은 단일 단계 프로세스로 패키지 되 고 배포 됩니다. 또한이 프로세스는 프로덕션 환경에 수동 배포를 위한 패키지를 생성 합니다.
7. 리사 Andrews는 6 단계에서 만든 웹 패키지를 수동으로 가져와 프로덕션 환경에 응용 프로그램을 배포 합니다.

### <a name="key-deployment-issues"></a>키 배포 문제

연락처 관리자 솔루션과 Fabrikam, Inc. 시나리오는 복잡 한 엔터프라이즈급 솔루션을 배포할 때 발생할 수 있는 다양 한 일반적인 문제 및 과제를 강조 표시 합니다. 다음은 그 예입니다.

- 개발자 또는 테스트 환경, 스테이징 플랫폼 및 프로덕션 서버와 같은 여러 환경에 프로젝트를 배포할 수 있어야 합니다. 각 환경에 대해 서로 다른 구성 설정을 사용 하 여 솔루션을 배포 해야 합니다.
- 단일 단계 또는 자동화 된 빌드 및 배포 프로세스의 일부로 동시에 여러 종속 프로젝트를 배포 해야 합니다.
- 자동화 된 프로세스에서 배포를 시작할 수 있어야 합니다. 예를 들어 새 코드를 체크 인할 때 CI 프로세스를 사용 하 여 웹 응용 프로그램을 스테이징 환경에 배포 하려고 합니다.
- 개발자는 모든 대상 환경에 올바른 구성 설정이 나 필요한 자격 증명을 가질 가능성이 거의 없으므로 배포 프로세스를 제어 하 고 Visual Studio 외부에서 배포 변수를 설정할 수 있어야 합니다.
- 이후 배포에서 스키마 기반 데이터베이스 프로젝트를 배포 하 고 기존 데이터를 유지 해야 합니다.
- 사용자 계정 데이터를 배포 하지 않고 임시 방식으로 멤버 자격 데이터베이스를 배포 해야 합니다. 기존 사용자 계정 데이터를 손실 하지 않고 배포 된 멤버 자격 데이터베이스의 스키마를 업데이트 해야 할 수도 있습니다.
- 다양 한 대상 환경에 콘텐츠를 배포할 때 특정 파일 또는 폴더를 제외 해야 합니다.

또한 업데이트가 잦은 경우 배포를 관리 하 고 증분을 통해 몇 가지 추가 문제를 발생 시킵니다. 다음은 그 예입니다.

- 개발자가 새 코드를 체크 인할 때마다 단위 테스트를 실행 합니다. 코드에서 단위 테스트를 통과 하는 경우에만 솔루션을 배포 합니다.
- 스테이징 또는 프로덕션 환경에 웹 응용 프로그램을 배포 하는 경우 배포 프로세스 기간 동안 사용자를 *앱\_오프 라인 .htm* 파일로 리디렉션해야 합니다.
- 배포 작업을 기록 하려고 합니다. 배포 프로세스는 지정 된 받는 사람에 게 성공 또는 실패 한 배포에 대 한 전자 메일 알림을 보내야 합니다.
- 자동 배포에 실패 하는 경우 배포 프로세스는 현재 배포를 다시 시도 하거나 대신 이전 웹 패키지를 배포 해야 합니다.

> [!div class="step-by-step"]
> [이전](deploying-web-applications-in-enterprise-scenarios.md)
> [다음](application-lifecycle-management-from-development-to-production.md)
