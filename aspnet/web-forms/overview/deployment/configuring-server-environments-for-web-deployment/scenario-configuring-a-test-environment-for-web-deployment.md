---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: '시나리오: 웹 배포용 테스트 환경 구성 | Microsoft Docs'
author: jrjlee
description: 이 항목에서는 개발자 또는 테스트 환경에 대 한 일반적인 웹 배포 시나리오에 대해 설명 하 고 si를 설정 하기 위해 완료 해야 하는 작업을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: d580e550f2461837f0e8a4e477273348b49cb53e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517985"
---
# <a name="scenario-configuring-a-test-environment-for-web-deployment"></a>시나리오: 웹 배포용 테스트 환경 구성

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 개발자 또는 테스트 환경에 대 한 일반적인 웹 배포 시나리오에 대해 설명 하 고 유사한 환경을 설정 하기 위해 완료 해야 하는 작업에 대해 설명 합니다.

개발자가 웹 응용 프로그램을 사용 하는 경우 실제 설정에서 응용 프로그램에 대 한 변경 내용을 테스트 하는 데 사용할 수 있는 서버 환경에 대 한 액세스 권한을 부여 하는 경우가 많습니다. 이러한 종류의 개발 또는 테스트 환경에는 일반적으로 다음과 같은 특징이 있습니다.

- 환경은 단일 웹 서버와 단일 데이터베이스 서버로 구성 됩니다.
- 개발자는 일반적으로 서버에 대 한 관리자 권한이 있으므로 응용 프로그램의 요구 사항에 맞게 환경을 구성할 수 있습니다.
- 응용 프로그램에 대 한 변경 내용은 자주 배포 되므로 환경에서 단일 단계 또는 자동화 된 배포를 지원 해야 합니다.

예를 들어이 [자습서 시나리오](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)에서 Matt Hink는 Fabrikam의 개발자 이며, inc. Matt는 Contact Manager 솔루션에서 작업 하며, 정기적으로 테스트 환경에 변경 내용을 배포 해야 합니다. Matt는 테스트 웹 서버와 테스트 데이터베이스 서버의 관리자입니다. 처음에는 Matt에서 직접 테스트 환경에 솔루션을 배포할 수 있어야 합니다.

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

작업이 진행 되 고 더 많은 개발자가 팀에 참여 하 게 되 면 TFS (Team Foundation Server)의 CI (지속적인 통합)에 대해 Contact Manager 솔루션이 구성 됩니다. 개발자가 콘텐츠를 체크 인할 때마다 팀 빌드는 솔루션을 빌드하고, 단위 테스트를 실행 하 고, 테스트 환경에 솔루션을 자동으로 배포 해야 합니다.

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a>솔루션 개요

테스트 환경에서는 원격 컴퓨터에서 단일 단계 또는 자동 배포를 지원 해야 하므로 두 가지 주요 방법을 선택할 수 있습니다. 다음을 수행할 수 있습니다.

- 웹 Deployment Agent 서비스 ("원격 에이전트")를 사용 하 여 배포를 지원 하도록 테스트 웹 서버를 구성 합니다.
- 웹 배포 처리기를 사용 하 여 배포를 지원 하도록 테스트 웹 서버를 구성 합니다.

> [!NOTE]
> [요청 시 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx) ("임시 에이전트")를 사용할 수도 있습니다. 이는 요구 사항 및 제약 조건 측면에서 원격 에이전트 방법과 유사 합니다.

이 경우 개발자에 게 대상 서버에 대 한 관리자 권한이 있고 테스트 환경에 엄격한 보안 제약 조건이 적용 되지 않으므로, 원격 에이전트를 사용 하 여 배포를 지원 하도록 테스트 웹 서버를 구성 하는 것이 논리적 선택입니다. 이는 보다 복잡 하며 웹 배포 처리기 접근 방식 보다 초기 구성이 더 적습니다. 또한 원격 액세스 및 배포를 지원 하도록 데이터베이스 서버를 구성 해야 합니다.

이러한 작업을 완료 하기 위해 필요한 모든 정보를 제공 하는 항목입니다.

- [웹 배포 게시를 위해 웹 서버를 구성 합니다 (원격 에이전트)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md). 이 항목에서는 클린 Windows Server 2008 R2 빌드에서 시작 하 여 원격 에이전트 접근 방법을 사용 하 여 웹 배포 게시를 지 원하는 웹 서버를 빌드하는 방법에 대해 설명 합니다.
- [웹 배포 게시용 데이터베이스 서버를 구성](configuring-a-database-server-for-web-deploy-publishing.md)합니다. 이 항목에서는 SQL Server 2008 R2의 기본 설치에서 시작 하 여 원격 액세스 및 배포를 지원 하도록 데이터베이스 서버를 구성 하는 방법에 대해 설명 합니다.

## <a name="further-reading"></a>추가 참고 자료

일반적인 스테이징 환경을 구성 하는 방법에 대 한 지침은 [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)을 참조 하세요. 일반적인 프로덕션 환경을 구성 하는 방법에 대 한 지침은 [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)을 참조 하세요.

> [!div class="step-by-step"]
> [이전](choosing-the-right-approach-to-web-deployment.md)
> [다음](scenario-configuring-a-staging-environment-for-web-deployment.md)
