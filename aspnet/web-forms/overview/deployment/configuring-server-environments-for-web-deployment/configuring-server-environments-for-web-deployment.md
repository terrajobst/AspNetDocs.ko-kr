---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: 웹 배포용 서버 환경 구성 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 여러 다른 scen에서 한 번 클릭 하거나 자동화 된 웹 사이트 배포 및 게시를 지원 하도록 서버 환경을 설정 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 073161ce4faa3b7ba6749d7dfbaa5309eeca4f74
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515117"
---
# <a name="configuring-server-environments-for-web-deployment"></a>웹 배포용 서버 환경 구성

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에서는 여러 가지 시나리오에서 한 번 클릭 하거나 자동화 된 웹 사이트 배포 및 게시를 지원 하도록 서버 환경을 설정 하는 방법을 보여 줍니다. 이 자습서에는 배포에 대 한 특정 접근 방법을 지원 하도록 웹 서버를 구성 하 고,에서 제공 하는 시나리오 기반 개요와 함께 WFF (웹 팜 프레임 워크) 서버 팜을 설정 하는 등 다양 한 작업을 완료 하는 과정을 안내 하는 항목이 포함 되어 있습니다 수준 높은 종단 간 지침
> 
> 이 자습서에서는 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) 에 설명 된 Fabrikam, inc. 배포 시나리오를 예제 및 네트워크 인프라의 참조 지점으로 사용 합니다.
> 
> 이러한 자습서의 이탈리아어 번역은 [http://www.lucamorelli.it](http://www.lucamorelli.it)를 참조 하세요.

이 자습서에는 다음 항목이 포함 되어 있습니다.

- [웹 배포에 적합한 접근 방식 선택](choosing-the-right-approach-to-web-deployment.md)
- [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)
- [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)
- [웹 배포 게시용 웹 서버 구성(원격 에이전트)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [웹 배포 게시용 웹 서버 구성(웹 배포 처리기)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [웹 배포 게시용 웹 서버 구성(오프라인 배포)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [웹 배포 게시용 데이터베이스 서버 구성](configuring-a-database-server-for-web-deploy-publishing.md)
- [웹 팜 프레임워크를 사용하여 서버 팜 만들기](creating-a-server-farm-with-the-web-farm-framework.md)
- [대상 환경의 배포 속성 구성](configuring-deployment-properties-for-a-target-environment.md)

[웹 배포에 대 한 적절 한 접근 방식을 선택](choosing-the-right-approach-to-web-deployment.md)하는 첫 번째 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 (웹 배포 도구) 2.0를 사용 하 여 웹 응용 프로그램을 게시 하는 데 사용할 수 있는 주요 방법을 설명 합니다. 또한 각 방법에 매핑되는 시나리오를 식별 합니다. 여기에서 각 시나리오 항목은 완료 해야 하는 작업에 대 한 개략적인 개요를 제공 하 고 이러한 작업을 완료 하는 데 도움이 되는 작업을 수행 하는 데 필요한 항목을 식별 합니다.

솔루션을 빌드 및 배포 하 [는 빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md) 에 설명 된 분할 프로젝트 파일 방법을 사용 하는 경우 [대상 환경에 대 한 배포 속성 구성](configuring-deployment-properties-for-a-target-environment.md)최종 항목에서는 다른 대상 환경에 배포 하기 위해 환경 관련 프로젝트 파일을 구성 하는 방법을 설명 합니다.

## <a name="key-technologies"></a>주요 기술

이 자습서에서는 이러한 제품과 기술을 사용 하 여 웹 배포를 지 원하는 방법을 중점적으로 설명 합니다.

- IIS 7.5
- 웹 배포 2.x
- WFF 2.x
- IIS 웹 관리 서비스 (WMSvc)

이 자습서에서는 Windows Server 2008 R2, SQL Server 2008 R2, ASP.NET 4.0 및 ASP.NET MVC 3 사용에 대해서도 다룹니다.

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이는 엔터프라이즈급 웹 배포에 대 한 일련의 다섯 가지 자습서 중 일부를 형성 합니다. 시리즈의 다른 자습서는 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). 이 소개 내용은 자습서 시리즈에 대 한 상황에 맞는 배경을 제공 합니다. 자습서 시나리오를 설명 하 고 시리즈 전체에서 설명 하는 작업과 연습이 더 광범위 한 ALM (응용 프로그램 수명 주기 관리) 프로세스에 적합 한지 보여 줍니다.
- [엔터프라이즈의 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). 이 자습서에서는 Microsoft Build Engine (MSBuild) 프로젝트 파일, 웹 게시 파이프라인, 웹 배포 및 기타 관련 기술에 대해 개념적인 소개를 제공 합니다. 이러한 도구를 함께 사용 하 여 복잡 한 배포 프로세스를 관리 하는 방법을 설명 합니다.
- [웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) 이 자습서에서는 CI (지속적인 통합) 프로세스의 일부로 자동화 된 배포를 비롯 하 여 다양 한 배포 시나리오를 지원 하도록 TFS (Team Foundation Server)를 구성 하 고, 특정 빌드의 배포를 수동으로 트리거한 방법을 설명 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). 이 자습서에서는 여러 환경에 데이터베이스 배포를 사용자 지정 하 고, 배포에서 파일 및 폴더를 제외 하 고, 배포 프로세스 중에 웹 응용 프로그램을 오프 라인 상태로 만드는 등의 다양 한 고급 배포 작업을 수행 하는 방법을 .

> [!div class="step-by-step"]
> [다음](choosing-the-right-approach-to-web-deployment.md)
