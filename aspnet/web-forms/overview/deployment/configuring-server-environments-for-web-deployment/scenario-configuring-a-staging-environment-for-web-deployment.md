---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: '시나리오: 웹 배포용 스테이징 환경 구성 | Microsoft Docs'
author: jrjlee
description: 이 항목에서는 스테이징 환경에 대 한 일반적인 웹 배포 시나리오에 대해 설명 하 고 유사한 env를 설정 하기 위해 완료 해야 하는 작업을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: eaa61ca850817f8dd98955b59e94be93389bf256
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518009"
---
# <a name="scenario-configuring-a-staging-environment-for-web-deployment"></a>시나리오: 웹 배포용 스테이징 환경 구성

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 스테이징 환경의 일반적인 웹 배포 시나리오에 대해 설명 하 고 유사한 환경을 설정 하기 위해 완료 해야 하는 작업에 대해 설명 합니다.

많은 조직에서 스테이징 환경을 사용 하 여 웹 응용 프로그램 또는 웹 사이트에 대 한 업데이트를 미리 봅니다. 이를 통해 조직 내의 사람들은 사이트가 "라이브" 상태가 되기 전에 새 기능이 나 콘텐츠를 탐색 하 고 검토할 수 있으며, 그렇지 않은 경우에는 프로덕션 환경에 배포 됩니다. 스테이징 환경은 현실적인 미리 보기를 제공 하기 위해 프로덕션 환경을 최대한 긴밀 하 게 복제 하도록 설계 되었습니다. 이러한 종류의 스테이징 환경에는 일반적으로 다음과 같은 특징이 있습니다.

- 이 환경은 주로 장애 조치 (failover) 클러스터링 및 데이터베이스 미러링을 사용 하는 부하 분산 된 여러 웹 서버와 하나 이상의 데이터베이스 서버로 구성 됩니다.
- 응용 프로그램은 개발 팀에서 수동으로 배포 하거나 팀 빌드 서버에 의해 자동으로 배포 될 수 있습니다.
- 응용 프로그램을 배포 하는 사용자 또는 프로세스 계정은 스테이징 서버에 대 한 관리자 권한이 없을 가능성이 높습니다.
- 응용 프로그램에 대 한 변경 내용은 자주 배포 되므로 환경에서 단일 단계 또는 자동화 된 배포를 지원 해야 합니다.

> [!NOTE]
> 여러 서버에 걸쳐 데이터베이스 배포를 확장 하는 것은이 자습서의 범위를 벗어나는 것입니다. 이 영역에 대 한 자세한 내용은 [SQL Server 온라인 설명서](https://technet.microsoft.com/library/ms130214.aspx)를 참조 하세요.

예를 들어이 [자습서 시나리오](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)에서 TFS (Team Foundation Server)는 Contact Manager 솔루션을 관리 합니다. TFS 관리자 인 Rob Walters는 개발자가 필요에 따라 스테이징 환경에 대 한 배포를 트리거할 수 있는 빌드 정의를 만들었습니다.

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

대부분의 경우 최신 빌드를 스테이징 환경에 배포할 필요는 없습니다. 대신 테스트 환경에서 이미 유효성을 검사 하 고 확인 한 특정 빌드를 배포 하려는 경우가 많습니다.

## <a name="solution-overview"></a>솔루션 개요

이 시나리오에서는 다음과 같은 배포 요구 사항 분석에서 이러한 팩트를 추론할 수 있습니다.

- 배포를 수행 하는 사용자 또는 프로세스 계정에는 스테이징 서버에 대 한 관리자 권한이 없으므로 스테이징 웹 서버에서 비관리자 배포를 지원 해야 합니다. 따라서 원격 에이전트가 아닌 웹 배포 처리기를 사용 하도록 스테이징 웹 서버를 구성 해야 합니다.
- 스테이징 환경에는 여러 웹 서버가 포함 되어 있지만 단일 클릭 또는 자동 배포를 지원 해야 하므로 WFF (웹 팜 프레임 워크)를 사용 하 여 서버 팜을 만들어야 합니다. 이 방법을 사용 하 여 응용 프로그램을 하나의 웹 서버 (주 서버)에 배포할 수 있으며, WFF는 스테이징 환경의 다른 모든 웹 서버에서 배포를 복제 합니다.
- 배포를 수행 하는 사용자 또는 프로세스 계정에는 데이터베이스를 만들 수 있는 권한이 있어야 합니다. 따라서 원격 액세스 및 배포를 지원 하도록 데이터베이스 서버를 구성 하는 것 외에도, 데이터베이스 서버의 **dbcreator** 서버 역할에 계정을 추가 해야 합니다.

이러한 작업을 완료 하기 위해 필요한 모든 정보를 제공 하는 항목입니다.

- [웹 팜 프레임 워크를 사용 하 여 서버 팜을 만듭니다](creating-a-server-farm-with-the-web-farm-framework.md). 이 항목에서는 WFF를 사용 하 여 서버 팜을 만들고 구성 하는 방법에 대해 설명 합니다. 따라서 웹 플랫폼 제품 및 구성 요소, 구성 설정, 웹 사이트 및 응용 프로그램은 부하 분산 된 여러 웹 서버에서 복제 됩니다.
- [웹 배포 게시용 웹 서버 (웹 배포 처리기)를 구성](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다. 이 항목에서는 클린 Windows Server 2008 R2 빌드에서 시작 하 여 원격 에이전트 접근 방법을 사용 하 여 웹 배포 게시를 지 원하는 웹 서버를 빌드하는 방법에 대해 설명 합니다.
- [웹 배포 게시용 데이터베이스 서버를 구성](configuring-a-database-server-for-web-deploy-publishing.md)합니다. 이 항목에서는 SQL Server 2008 R2의 기본 설치에서 시작 하 여 원격 액세스 및 배포를 지원 하도록 데이터베이스 서버를 구성 하는 방법에 대해 설명 합니다.

## <a name="further-reading"></a>추가 참고 자료

일반적인 개발자 테스트 환경을 구성 하는 방법에 대 한 지침은 [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)을 참조 하세요. 일반적인 프로덕션 환경을 구성 하는 방법에 대 한 지침은 [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)을 참조 하세요.

> [!div class="step-by-step"]
> [이전](scenario-configuring-a-test-environment-for-web-deployment.md)
> [다음](scenario-configuring-a-production-environment-for-web-deployment.md)
