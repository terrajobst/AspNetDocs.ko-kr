---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
title: '시나리오: 웹 배포용 프로덕션 환경 구성 | Microsoft Docs'
author: jrjlee
description: 이 항목에서는 프로덕션 환경의 일반적인 웹 배포 시나리오에 대해 설명 하 고 유사한 ...를 설정 하기 위해 완료 해야 하는 작업을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2e861511-450e-4752-a61e-4a01933f9b6e
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2d76e715cdbf6ec484fa0ff98b3b3d1d8dfd3961
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515933"
---
# <a name="scenario-configuring-a-production-environment-for-web-deployment"></a>시나리오: 웹 배포용 프로덕션 환경 구성

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 프로덕션 환경의 일반적인 웹 배포 시나리오에 대해 설명 하 고 유사한 환경을 설정 하기 위해 완료 해야 하는 작업에 대해 설명 합니다.

프로덕션 환경은 웹 응용 프로그램 또는 웹 사이트의 최종 대상입니다. 이 시점에서 응용 프로그램은 테스트를 통과 하 고 스테이징 환경에 배포 되었으며 "라이브" 상태가 될 준비가 되었습니다. 프로덕션 환경의 특성은 웹 콘텐츠의 특성 및 용도, 조직의 규모, 대상 사용자 및 기타 수많은 요인에 따라 크게 달라질 수 있습니다. 엔터프라이즈 규모의 시나리오에서 프로덕션 환경에는 다음과 같은 특징이 있을 수 있습니다.

- 이 환경은 주로 장애 조치 (failover) 클러스터링 및 데이터베이스 미러링을 사용 하는 부하 분산 된 여러 웹 서버와 하나 이상의 데이터베이스 서버로 구성 됩니다.
- 환경이 인터넷에 연결 된 경우 내부 네트워크에서 분리 될 가능성이 높습니다. 이 네트워크는 경계 네트워크의 다른 서브넷에 있을 수 있으며, 다른 도메인에 있을 수 있으며 완전히 다른 네트워크 인프라에 있을 수 있습니다.
- 개발자와 빌드 서버 프로세스 계정에는 프로덕션 서버에 대 한 관리자 권한이 있을 가능성이 매우 낮습니다.
- 응용 프로그램에 대 한 변경 내용은 테스트 또는 스테이징 배포 보다 더 자주 배포 되지 않습니다.

> [!NOTE]
> 여러 서버에 걸쳐 데이터베이스 배포를 확장 하는 것은이 자습서의 범위를 벗어나는 것입니다. 이 영역에 대 한 자세한 내용은 [SQL Server 온라인 설명서](https://technet.microsoft.com/library/ms130214.aspx)를 참조 하세요.

예를 들어, [자습서 시나리오](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)에서 팀 빌드 서버에는 사용자가 연락 관리자 솔루션을 빌드하여 단일 단계에서 스테이징 환경에 배포할 수 있도록 하는 빌드 정의가 포함 되어 있습니다. 응용 프로그램을 프로덕션 환경에 배포할 준비가 되 면 보안 요구 사항 및 네트워크 인프라에 의해 적용 되는 제약 조건으로 인해 프로덕션 환경 관리자는 수동으로 웹 패키지를 프로덕션 웹 서버에 복사 하 고 가져와야 합니다. 인터넷 정보 서비스 (IIS) 관리자를 통해 관리 됩니다.

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a>솔루션 개요

이 시나리오에서는 다음과 같은 배포 요구 사항 분석에서 이러한 팩트를 추론할 수 있습니다.

- 보안 제한 및 네트워크 구성으로 인해 단일 클릭 또는 자동화 된 배포를 지원 하도록 프로덕션 환경을 구성할 수 없습니다. 오프 라인 배포는이 시나리오에서 유일 하 게 사용할 수 있는 방법입니다.
- 프로덕션 환경에는 여러 웹 서버가 포함 되어 있으므로 WFF (웹 팜 프레임 워크)를 사용 하 여 서버 팜을 만들 수 있습니다. 관리자는이 방법을 사용 하 여 응용 프로그램을 하나의 웹 서버 (주 서버)로 가져와야 하는데, WFF는 프로덕션 환경의 다른 모든 웹 서버에서 배포를 복제 합니다.

이러한 작업을 완료 하기 위해 필요한 모든 정보를 제공 하는 항목입니다.

- [웹 팜 프레임 워크를 사용 하 여 서버 팜을 만듭니다](configuring-a-database-server-for-web-deploy-publishing.md). 이 항목에서는 WFF를 사용 하 여 서버 팜을 만들고 구성 하는 방법에 대해 설명 합니다. 따라서 웹 플랫폼 제품 및 구성 요소, 구성 설정, 웹 사이트 및 응용 프로그램은 부하 분산 된 여러 웹 서버에서 복제 됩니다.
- [웹 배포 게시를 위해 웹 서버를 구성 합니다 (오프 라인 배포)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md). 이 항목에서는 관리자가 완전 한 Windows Server 2008 R2 빌드에서 시작 하 여 웹 패키지를 수동으로 가져오고 배포할 수 있게 해 주는 웹 서버를 빌드하는 방법에 대해 설명 합니다.
- [웹 배포 게시용 데이터베이스 서버를 구성](configuring-a-database-server-for-web-deploy-publishing.md)합니다. 이 항목에서는 SQL Server 2008 R2의 기본 설치에서 시작 하 여 원격 액세스 및 배포를 지원 하도록 데이터베이스 서버를 구성 하는 방법에 대해 설명 합니다.

## <a name="further-reading"></a>추가 참고 자료

일반적인 개발자 테스트 환경을 구성 하는 방법에 대 한 지침은 [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)을 참조 하세요. 일반적인 스테이징 환경을 구성 하는 방법에 대 한 지침은 [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)을 참조 하세요.

> [!div class="step-by-step"]
> [이전](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [다음](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
