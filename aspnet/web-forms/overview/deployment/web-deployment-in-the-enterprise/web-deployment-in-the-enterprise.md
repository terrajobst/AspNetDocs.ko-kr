---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: 엔터프라이즈의 웹 배포 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 엔터프라이즈급 웹 응용 프로그램을 devel에 배포 하는 경우 발생 하는 많은 문제를 해결 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: bc7bb676a71af4ec3451aa3adf3c03ce3b5200d5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509717"
---
# <a name="web-deployment-in-the-enterprise"></a>기업에서 웹 배포

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에서는 엔터프라이즈 규모의 웹 응용 프로그램을 개발, 테스트, 스테이징 및 프로덕션 환경으로 배포 하는 경우 발생 하는 많은 문제를 해결 하는 방법을 설명 합니다. 자습서에는 다양 한 일반 작업 및 절차를 안내해 주는 개념 및 작업 기반 콘텐츠가 혼합 된 참조 솔루션이 포함 되어 있습니다.
> 
> 이러한 자습서의 이탈리아어 번역은 [http://www.lucamorelli.it](http://www.lucamorelli.it)를 참조 하세요.

## <a name="enterprise-deployment-challenges"></a>엔터프라이즈 배포 문제

조직에서는 복잡 한 엔터프라이즈급 솔루션의 배포를 관리 하기 위해 다음과 같은 문제가 종종 발생 합니다.

- 개발자 또는 테스트 환경, 스테이징 플랫폼 및 프로덕션 서버와 같은 여러 환경에 프로젝트를 배포할 수 있어야 합니다. 각 환경에 대해 서로 다른 구성 설정을 사용 하 여 솔루션을 배포 해야 합니다.
- 단일 단계 또는 자동화 된 빌드 및 배포 프로세스의 일부로 동시에 여러 종속 프로젝트를 배포 해야 합니다.
- 자동화 된 프로세스에서 배포를 시작할 수 있어야 합니다. 예를 들어, 새 코드를 체크 인할 때 CI (지속적인 통합) 프로세스를 사용 하 여 웹 응용 프로그램을 테스트 환경에 배포 하려고 합니다.
- 개발자는 모든 대상 환경에 올바른 구성 설정이 나 필요한 자격 증명을 가질 가능성이 거의 없으므로 배포 프로세스를 제어 하 고 Visual Studio 외부에서 배포 변수를 설정할 수 있어야 합니다.
- 이후 배포에서 스키마 기반 데이터베이스 프로젝트를 배포 하 고 기존 데이터를 유지 해야 합니다.
- 사용자 계정 데이터를 배포 하지 않고 임시 방식으로 멤버 자격 데이터베이스를 배포 해야 합니다. 기존 사용자 계정 데이터를 손실 하지 않고 배포 된 멤버 자격 데이터베이스의 스키마를 업데이트 해야 할 수도 있습니다.
- 다양 한 대상 환경에 콘텐츠를 배포할 때 특정 파일 또는 폴더를 제외 해야 합니다.

## <a name="overview-of-approach"></a>접근 방식 개요

이 자습서에서는이 시리즈의 다른 자습서와 함께 위에 설명 된 문제를 해결 하기 위해이 고급 방법을 사용 합니다.

- **MSBuild (사용자 지정 Microsoft Build Engine) 프로젝트 파일을 사용 하 여 전체 빌드 및 배포 프로세스를 제어 합니다.**
- 이렇게 하면 스크립트 가능한 단일 작업의 일부로 솔루션의 모든 프로젝트를 빌드하고 배포할 수 있습니다.
- 환경 관련 설정은 간단한 환경 관련 프로젝트 파일을 사용 하 여 구성 됩니다. 솔루션 구성 및 게시 프로필을 사용 하 여 다양 한 환경에 대 한 배포를 구성 하는 Visual Studio 중심 방식과 달리,이 방법을 사용 하면 Visual Studio 외부에서 배포 프로세스를 구성 하 고 관리할 수 있습니다. 즉, 개발자는 대상 환경에 대 한 연결 문자열, 서비스 끝점, 서버 자격 증명 및 기타 배포 변수에 대 한 고급 지식이 필요 하지 않습니다.
- 사용자 지정 프로젝트 파일은 TFS (Team Foundation Server) 워크플로의 일부로 팀 빌드에서 호출 될 수 있습니다. 따라서 CI 시나리오에 대 한 자동화 된 배포를 구성할 수 있습니다.

**인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 웹 응용 프로그램 프로젝트를 패키지 및 배포 합니다.**

- 웹 배포는 종속성, 구성 설정, 보안 설정 및 기타 요구 사항과 함께 웹 응용 프로그램 콘텐츠를 패키지 하 고 대상 IIS 웹 서버에 배포할 수 있는 프레임 워크를 제공 합니다.
- 사용자 지정 MSBuild 프로젝트 파일 내에서 전체 패키징 및 배포 프로세스를 제어할 수 있습니다. 연결 문자열, 서비스 끝점 및 IIS 대상 세부 정보와 같은 웹 배포 패키지와 함께 제공 되는 구성 설정을 조작할 수도 있습니다.
- 웹 배포는 웹 게시 파이프라인과 함께 배포를 사용자 지정할 수 있는 다양 한 확장성 지점이 제공 됩니다. 예를 들어 웹 배포 패키지에서 원치 않는 파일 및 폴더를 제외 하는 것이 쉽습니다.

**VSDBCMD 유틸리티를 사용 하 여 데이터베이스 스키마를 배포 하 고 업데이트 합니다.**

- VSDBCMD를 사용 하면 Visual Studio 데이터베이스 프로젝트를 빌드할 때 생성 되는 데이터베이스 스키마 파일 (.dbschema)에서 데이터베이스를 배포할 수 있습니다. 반면 웹 배포에 포함 된 데이터베이스 배포 기능은 로컬 SQL Server 인스턴스에서 기존 데이터베이스를 배포 하는 데 더 적합 합니다.
- 데이터베이스 프로젝트 배포를 위한 Visual Studio의 기능과 달리 VSDBCMD를 사용 하면 기존 대상 데이터베이스에 차등 업데이트를 배포할 수 있습니다. 이를 통해 데이터베이스 스키마를 업그레이드 하는 동안 기존 데이터를 유지할 수 있습니다.
- 사용자 지정 MSBuild 프로젝트 파일 내에서 VSDBCMD 명령을 실행할 수 있습니다.

## <a name="content-map"></a>콘텐츠 맵

이 자습서에는 네 가지 주요 영역에 해당 하는 항목이 포함 되어 있습니다.

이러한 항목에서는 참조 솔루션&#x2014;에 대해 설명 하&#x2014;고,이 솔루션을 다운로드 하 고 로컬 컴퓨터에서 구성 하는 방법을 설명 합니다.

- [Contact Manager 솔루션](the-contact-manager-solution.md)
- [Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)

이러한 항목에서는 MSBuild 프로젝트 파일을 소개 하 고, 사용자 지정 프로젝트 파일을 만들고 사용 하는 방법을 설명 하며, Contact Manager 솔루션에 대 한 배포 프로세스를 안내 합니다.

- [프로젝트 파일 이해](understanding-the-project-file.md)
- [빌드 프로세스 이해](understanding-the-build-process.md)

이러한 항목에서는 빌드 및 패키징 프로세스의 작동 방식, 빌드 프로세스를 웹 게시 파이프라인과 통합 하는 방법, 배포 매개 변수를 수정 하는 방법 및 대상에 웹 패키지를 배포 하는 방법을 포함 하 여 웹 응용 프로그램 배포에 대해 설명 합니다. 에서는

- [웹 애플리케이션 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)
- [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)
- [웹 패키지 배포](deploying-web-packages.md)

- [데이터베이스 프로젝트 배포](deploying-database-projects.md) 는 Visual Studio 데이터베이스 프로젝트를 배포 하는 데 사용할 수 있는 여러 가지 방법과 각 방법의 장점과 단점을 설명 합니다. [배포 명령 파일을 만들고 실행](creating-and-running-a-deployment-command-file.md) 하면 배포 논리를 캡슐화 하는 간단한 명령 파일을 만드는 방법에 대해 설명 하 고 복잡 한 솔루션을 단일 단계 프로세스로 배포할 수 있습니다.
- 마지막으로 [웹 패키지를 수동으로 설치](manually-installing-web-packages.md) 하면 웹 패키지를 IIS로 가져오는 방법을 보여 주는 자습서를 마칩니다.

## <a name="key-technologies"></a>주요 기술

이 자습서의 항목에서는 주로 이러한 기술을 사용 하 여 빌드 및 배포를 관리 합니다.

- Visual Studio 2010
- MSBuild
- IIS 7.5
- 웹 배포 2.0
- VSDBCMD 데이터베이스 배포 유틸리티

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이는 엔터프라이즈급 웹 배포에 대 한 일련의 다섯 가지 자습서 중 일부를 형성 합니다. 시리즈의 다른 자습서는 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). 이 소개 내용은 자습서 시리즈에 대 한 상황에 맞는 배경을 제공 합니다. 자습서 시나리오를 설명 하 고 시리즈 전체에서 설명 하는 작업과 연습이 더 광범위 한 ALM (응용 프로그램 수명 주기 관리) 프로세스에 적합 한지 보여 줍니다.
- [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md) 이 자습서에서는 웹 Deployment Agent 서비스 (원격 에이전트) 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 하 여 다양 한 배포 시나리오를 지원 하도록 Windows server를 구성 하는 방법을 설명 합니다. 사용자 환경에 적합 한 배포 방법을 선택 하는 방법에 대 한 지침을 제공 하 고, WFF (웹 팜 프레임 워크)를 사용 하 여 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하는 방법을 설명 합니다.
- [웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) 이 자습서에서는 CI 프로세스의 일부로 자동화 된 배포를 비롯 하 여 다양 한 배포 시나리오를 지원 하도록 TFS를 구성 하 고 특정 빌드의 배포를 수동으로 트리거한 방법을 설명 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). 이 자습서에서는 여러 환경에 데이터베이스 배포를 사용자 지정 하 고, 배포에서 파일 및 폴더를 제외 하 고, 배포 프로세스 중에 웹 응용 프로그램을 오프 라인 상태로 만드는 등의 다양 한 고급 배포 작업을 수행 하는 방법을 .

> [!div class="step-by-step"]
> [다음](the-contact-manager-solution.md)
