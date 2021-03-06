---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
title: 고급 엔터프라이즈 웹 배포 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 많은 엔터프라이즈 배포 시나리오에서 필요한 다양 한 작업을 수행 하는 방법을 보여 줍니다. 이탈리아어 translati 경우 ...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 7dcaba80-f2ec-4db3-ad98-daadc3afdb49
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: bf4c7d021763017592483df35cb717295c4924aa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474959"
---
# <a name="advanced-enterprise-web-deployment"></a>고급 엔터프라이즈 웹 배포

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에서는 많은 엔터프라이즈 배포 시나리오에서 필요한 다양 한 작업을 수행 하는 방법을 보여 줍니다.
> 
> 이러한 자습서의 이탈리아어 번역은 [http://www.lucamorelli.it](http://www.lucamorelli.it)를 참조 하세요.

이는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 일련의 자습서 중 일부를 형성 합니다. 이 자습서 [시리즈에서는 샘플](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션&#x2014;&#x2014;을 사용 하 여 ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 빌드&#x2014; [프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)에서 설명 하는 빌드 프로세스 이해에 설명 된 분할 프로젝트 파일 방식을 기반으로 합니다. 빌드 프로세스는 모든 대상 환경에 적용 되는 빌드 명령을 포함 하 고 다른 하나는 환경 특정 빌드 및 배포 설정을 포함 합니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="scenario-overview"></a>시나리오 개요

이러한 자습서에 대 한 개략적인 시나리오는 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)에 설명 되어 있습니다. 이 자습서를 시작 하기 전에이 항목을 검토 하는 것이 좋습니다.

## <a name="how-to-use-this-tutorial"></a>이 자습서의 사용 방법

- 이 자습서의 각 항목은 자체 포함 되어 있으며 엔터프라이즈 배포 시나리오에서 발생 하는 특정 챌린지 또는 문제를 해결 합니다. 이러한 항목을 특정 순서로 사용 하지 않아도 됩니다. 그러나이 자습서에서는 몇 가지 고급 작업을 다룹니다. 따라서이 콘텐츠를 활용 하기 위해 [엔터프라이즈 자습서의 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md) 에 포함 되는 개념과 기술에 대해 잘 알고 있어야 합니다.
- 이 자습서에는 다음 항목이 포함 되어 있습니다.
- ["What If" 배포 수행](performing-a-what-if-deployment.md) 많은 시나리오에서 대상 환경이 나 기존 콘텐츠에서 제안 된 배포의 영향을 확인 하 여 실제로 변경 하는 것이 좋습니다. 이 항목에서는 "what if" 배포를 실행 하 여 대상 환경에 콘텐츠를 배포 하는 것 처럼 실제로 변경 하지 않고 로그 파일 및 데이터베이스 업데이트 스크립트를 생성 하는 방법에 대해 설명 합니다. 이러한 리소스를 분석 하면 라이브 배포에서 발생 하는 잠재적인 문제를 쉽게 해결할 수 있습니다.
- [여러 환경에 대 한 데이터베이스 배포 사용자 지정](customizing-database-deployments-for-multiple-environments.md) 데이터베이스 프로젝트를 여러 대상에 배포 하는 경우 각 대상 환경에 대 한 배포 속성을 사용자 지정 하는 것이 좋습니다. 예를 들어 테스트 환경에서는 일반적으로 모든 배포에서 데이터베이스를 다시 만드는 반면 스테이징 또는 프로덕션 환경에서는 데이터를 보존 하기 위해 증분 업데이트를 수행 하는 것이 훨씬 더 많을 것입니다. 이 항목에서는 각 대상 환경에 대해 환경 특정 배포 구성 (sqldeployment) 파일을 만들어 이러한 속성 변경 내용을 배포 논리에 통합할 수 있는 방법에 대해 설명 합니다.
- 데이터베이스 역할 멤버 자격을 테스트 환경에 배포 합니다. 모든 배포&#x2014;에서 데이터베이스를 다시 만드는 경우, 예를 들어 CI (지속적인 통합) 빌드 및 테스트 환경&#x2014;에 배포 하는 과정에서 항상 데이터베이스 역할 멤버 자격을 구성 해야 합니다. 예를 들어 일반적으로 웹 응용 프로그램과 연결 된 응용 프로그램 풀 id에 대 한 사용 권한을 부여 해야 합니다. 이 항목에서는 배포 후 SQL 스크립트를 배포 논리에 추가 하 여이 프로세스를 자동화할 수 있는 방법에 대해 설명 합니다.
- [엔터프라이즈 환경에 멤버 자격 데이터베이스 배포](deploying-membership-databases-to-enterprise-environments.md) ASP.NET 멤버 자격 데이터베이스에는 배포 프로세스를 복잡 하 게 만들 수 있는 다양 한 특성이 있습니다. 예를 들어 스키마 전용 배포에서는 데이터베이스를 작동 하지 않는 상태로 유지 합니다. 대부분의 시나리오에서는 각 대상 환경에서 직접 멤버 자격 데이터베이스를 만드는 것이 좋습니다. 그러나 멤버 자격 데이터베이스를 배포 해야 하는 경우이 항목에서는 내재 된 과제를 충족 하는 데 사용할 수 있는 몇 가지 방법을 설명 합니다.
- [배포에서 파일 및 폴더 제외](excluding-files-and-folders-from-deployment.md) 일부 시나리오에서는 특정 대상 환경에 맞게 웹 패키지의 콘텐츠를 조정 하는 것이 좋습니다. 예를 들어 테스트 환경에 배포할 때 전체 버전의 JavaScript 라이브러리를 포함 하 여 클라이언트 쪽 디버깅을 지원할 수 있지만, 스테이징 또는 프로덕션 환경에 배포할 때 라이브러리의 버전을 사용 하지 않는 것이 좋습니다. 이 항목에서는 패키지 생성 프로세스에서 특정 파일 및 폴더를 제외할 수 있는 방법에 대해 설명 합니다.
- [웹 배포를 사용 하 여 웹 응용 프로그램을 오프 라인으로 전환](taking-web-applications-offline-with-web-deploy.md) 스테이징 또는 프로덕션 환경에 솔루션을 배포 하는 경우 배포 프로세스 동안 웹 응용 프로그램을 오프 라인으로 전환 하는 경우가 많습니다. 이 항목에서는 배포 프로세스를 시작할 때 웹 응용 프로그램에 *오프 라인 .htm 파일\_앱* 을 추가 하 고 끝에 제거 하는 방법에 대해 설명 합니다. *앱\_오프 라인 .htm* 파일이 준비 되는 동안 웹 응용 프로그램을 검색 하는 모든 사용자는 *오프 라인 .Htm 파일\_앱* 으로 자동 리디렉션됩니다.
- [MSBuild에서 Windows PowerShell 스크립트를 실행](running-windows-powershell-scripts-from-msbuild-project-files.md)합니다. 많은 배포 시나리오에는 사용자 지정 이벤트 원본을 레지스트리에 추가 하거나 SQL Server 인스턴스 간에 복제를 구성 하는 등 더 복잡 한 배포 후 작업이 필요 합니다. 이러한 작업은 Windows PowerShell 스크립트를 통해 수행 되는 경우가 많습니다. 이 항목에서는 빌드 및 배포 프로세스의 일부로 MSBuild (Microsoft Build Engine) 프로젝트 파일에서 Windows PowerShell 스크립트를 실행 하는 방법에 대해 설명 합니다.
- [패키징 프로세스 문제 해결](troubleshooting-the-packaging-process.md) WPP (웹 게시 파이프라인)는 웹 응용 프로그램 프로젝트의 패키징 프로세스에 대 한 자세한 정보를 생성 하는 데 사용할 수 있는 **EnablePackageProcessLoggingAndAssert** 라는 MSBuild 속성을 정의 합니다. 이 항목에서는 속성의 정의와 사용 방법에 대해 설명 합니다.

## <a name="key-technologies"></a>주요 기술

이 자습서에서는 자동화 된 빌드 및 웹 배포를 지 원하는 데 이러한 제품과 기술을 사용 하는 방법을 중점적으로 설명 합니다.

- Visual Studio 2010 및 Team Foundation Server (TFS) 2010
- MSBuild 및 TFS 팀 빌드
- 인터넷 정보 서비스 (IIS) 7.5
- IIS 웹 배포 도구 (웹 배포) 2.1
- VSDBCMD 데이터베이스 배포 유틸리티

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이는 엔터프라이즈급 웹 배포에 대 한 일련의 다섯 가지 자습서 중 일부를 형성 합니다. 시리즈의 다른 자습서는 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). 이 소개 내용은 자습서 시리즈에 대 한 상황에 맞는 배경을 제공 합니다. 자습서 시나리오를 설명 하 고 시리즈 전체에서 설명 하는 작업과 연습이 더 광범위 한 ALM (응용 프로그램 수명 주기 관리) 프로세스에 적합 한지 보여 줍니다.
- [엔터프라이즈의 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). 이 자습서에서는 MSBuild 프로젝트 파일, WPP, 웹 배포 및 기타 관련 기술에 대해 개념적인 소개를 제공 합니다. 이러한 도구를 함께 사용 하 여 복잡 한 배포 프로세스를 관리 하는 방법을 설명 합니다.
- [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md) 이 자습서에서는 웹 Deployment Agent 서비스 (원격 에이전트) 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 하 여 다양 한 배포 시나리오를 지원 하도록 Windows server를 구성 하는 방법을 설명 합니다. 사용자 환경에 적합 한 배포 방법을 선택 하는 방법에 대 한 지침을 제공 하 고, WFF (웹 팜 프레임 워크)를 사용 하 여 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하는 방법을 설명 합니다.
- [웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) 이 자습서에서는 CI 프로세스의 일부로 자동화 된 배포를 비롯 하 여 다양 한 배포 시나리오를 지원 하도록 TFS를 구성 하 고 특정 빌드의 배포를 수동으로 트리거한 방법을 설명 합니다.

> [!div class="step-by-step"]
> [다음](performing-a-what-if-deployment.md)
