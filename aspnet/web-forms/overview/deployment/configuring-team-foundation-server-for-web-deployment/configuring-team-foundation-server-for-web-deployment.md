---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: 웹 배포에 대 한 Team Foundation Server 구성 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 솔루션을 구축 하 고 다양 한 대상 환경에 웹 콘텐츠를 배포 하기 위해 TFS (Team Foundation Server) 2010를 구성 하는 방법을 보여 줍니다. ...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 638d696abbc5f05957c0ed2eb7ebb65fce7813ea
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424205"
---
# <a name="configuring-team-foundation-server-for-web-deployment"></a>웹 배포용 Team Foundation Server 구성

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에서는 솔루션을 구축 하 고 다양 한 대상 환경에 웹 콘텐츠를 배포 하기 위해 TFS (Team Foundation Server) 2010를 구성 하는 방법을 보여 줍니다. 여기에는 개발자가 변경할 때마다 콘텐츠를 자동으로 배포 하는 CI (지속적인 통합) 시나리오가 포함 됩니다. 또한 테스트 환경에서 빌드를 확인 하 고 유효성을 검사 한 후 관리자가 스테이징 환경에 대 한 특정 빌드 배포를 트리거할 수 있는 수동 트리거 시나리오를 포함할 수 있습니다. 이 자습서의 항목에서는 다음을 비롯 한 전체 구성 프로세스를 안내 합니다.
> 
> - TFS에서 새 팀 프로젝트를 만드는 방법
> - 소스 제어에 콘텐츠를 추가 하는 방법
> - CI 및 배포를 지원 하도록 빌드 서버를 구성 하는 방법입니다.
> - 배포 논리를 포함 하는 빌드 정의를 만드는 방법
> - 자동 배포에 대 한 사용 권한을 구성 하는 방법
> 
> 이러한 자습서의 이탈리아어 번역은 [http://www.lucamorelli.it](http://www.lucamorelli.it)를 참조 하세요.

이 자습서에서는 초기 구성 프로세스의 일부로 TFS 2010을 설치 하 고 팀 프로젝트 컬렉션을 만든 것으로 가정 합니다. [Visual Studio 2010에 대 한 Team Foundation 설치 가이드](https://go.microsoft.com/?linkid=9805132) 에서는 이러한 작업에 대 한 포괄적인 지침을 제공 합니다.

## <a name="context"></a>Context

이는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항에 따라 일련의 자습서 중 일부를 형성 합니다. 이 자습서 [시리즈에서는 샘플](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션&#x2014;&#x2014;을 사용 하 여 ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 빌드&#x2014; [프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)에서 설명 하는 빌드 프로세스 이해에 설명 된 분할 프로젝트 파일 방식을 기반으로 합니다. 빌드 프로세스는 모든 대상 환경에 적용 되는 빌드 명령을 포함 하 고 다른 하나는 환경 특정 빌드 및 배포 설정을 포함 합니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="scenario-overview"></a>시나리오 개요

이러한 자습서에 대 한 개략적인 시나리오는 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)에 설명 되어 있습니다. 이 자습서를 시작 하기 전에이 항목을 검토 하는 것이 좋습니다.

## <a name="how-to-use-this-tutorial"></a>이 자습서의 사용 방법

이 자습서에서 설명 하는 작업을 처음으로 수행 하거나 샘플 솔루션을 사용 하는 예제를 수행 하려는 경우 자습서 항목을 순서 대로 수행 해야 합니다. 또는 개별 항목을 특정 작업에 대 한 지침으로 사용할 수 있습니다. 이 자습서에는 다음 항목이 포함 되어 있습니다.

- [TFS에서 팀 프로젝트 만들기](creating-a-team-project-in-tfs.md) 팀 프로젝트는 소스 제어, 프로세스 관리 및 TFS의 빌드에 대 한 핵심 단위입니다. 소스 제어에 콘텐츠를 추가 하거나 빌드 정의를 만들려면 먼저 팀 프로젝트를 만들어야 합니다.
- [소스 제어에 콘텐츠를 추가 하는 중](adding-content-to-source-control.md)입니다. 팀 프로젝트를 만든 후에는 소스 제어에 콘텐츠를 추가 하기 시작할 수 있습니다. 빌드 구성을 시작 하려면 먼저 외부 종속성과 함께 프로젝트와 솔루션을 추가 해야 합니다.
- [웹 배포용 TFS 빌드 서버 구성](configuring-a-tfs-build-server-for-web-deployment.md) 팀 프로젝트 콘텐츠를 빌드 하려는 경우 빌드 서버를 구성 해야 합니다. 대부분의 경우이는 TFS 설치와 별도의 컴퓨터에 있어야 합니다. 빌드 서버를 구성 하려면 TFS 빌드 서비스를 설치 및 구성 하 고, Visual Studio 2010을 설치 하 고, 빌드 컨트롤러 및 빌드 에이전트를 만들고, 빌드에 필요한 모든 제품이 나 구성 요소를 설치 하 고, 설치를 완료 하는 데 필요한 코드의 구성 요소를 설치 해야 합니다. 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포).
- [배포를 지 원하는 빌드 정의 만들기](creating-a-build-definition-that-supports-deployment.md) TFS에서 빌드 큐를 시작 하거나 트리거를 트리거하기 전에 팀 프로젝트에 대 한 빌드 정의를 하나 이상 만들어야 합니다. 빌드 정의는 빌드에 포함 해야 하는 항목, 빌드를 트리거하는 항목 및 팀 빌드에서 빌드 출력을 전송 해야 하는 위치를 포함 하 여 빌드의 모든 측면을 정의 합니다. 빌드 정의를 구성 하 여 MSBuild (사용자 지정 Microsoft Build Engine) 프로젝트 파일을 실행할 수 있습니다 .이를 통해 자동화 된 빌드에 배포 논리를 포함할 수 있습니다.
- [특정 빌드를 배포 하는](deploying-a-specific-build.md)중입니다. 많은 시나리오에서 대상 환경에 최신 빌드 대신 특정 빌드를 배포 하는 것이 좋습니다. 이 경우 특정 저장 폴더의 콘텐츠를 배포 하는 빌드 정의를 구성할 수 있습니다.
- [팀 빌드 배포에 대 한 사용 권한을 구성](configuring-permissions-for-team-build-deployment.md)합니다. 빌드 서비스에서 자동화 된 빌드 프로세스의 일부로 콘텐츠를 배포 하는 경우 대상 웹 서버와 데이터베이스 서버의 빌드 서비스 계정에 다양 한 사용 권한을 부여 해야 합니다.

## <a name="key-technologies"></a>주요 기술

이 자습서에서는 자동화 된 빌드 및 웹 배포를 지 원하는 데 이러한 제품과 기술을 사용 하는 방법을 중점적으로 설명 합니다.

- Visual Studio Team Foundation Server 2010
- 팀 빌드 및 MSBuild
- 웹 배포

이 자습서에서는 Windows Server 2008 R2, IIS 7.5, SQL Server 2008 R2, ASP.NET 4.0 및 ASP.NET MVC 3 사용에 대해서도 다룹니다.

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이는 엔터프라이즈급 웹 배포에 대 한 일련의 다섯 가지 자습서 중 일부를 형성 합니다. 시리즈의 다른 자습서는 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). 이 소개 내용은 자습서 시리즈에 대 한 상황에 맞는 배경을 제공 합니다. 자습서 시나리오를 설명 하 고 시리즈 전체에서 설명 하는 작업과 연습이 더 광범위 한 ALM (응용 프로그램 수명 주기 관리) 프로세스에 적합 한지 보여 줍니다.
- [엔터프라이즈의 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). 이 자습서에서는 MSBuild 프로젝트 파일, WPP (웹 게시 파이프라인), 웹 배포 및 기타 관련 기술에 대해 개념적인 소개를 제공 합니다. 이러한 도구를 함께 사용 하 여 복잡 한 배포 프로세스를 관리 하는 방법을 설명 합니다.
- [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md) 이 자습서에서는 웹 Deployment Agent 서비스 (원격 에이전트) 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 하 여 다양 한 배포 시나리오를 지원 하도록 Windows server를 구성 하는 방법을 설명 합니다. 사용자 환경에 적합 한 배포 방법을 선택 하는 방법에 대 한 지침을 제공 하 고, WFF (웹 팜 프레임 워크)를 사용 하 여 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하는 방법을 설명 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). 이 자습서에서는 여러 환경에 데이터베이스 배포를 사용자 지정 하 고, 배포에서 파일 및 폴더를 제외 하 고, 배포 프로세스 중에 웹 응용 프로그램을 오프 라인 상태로 만드는 등의 다양 한 고급 배포 작업을 수행 하는 방법을 .

> [!div class="step-by-step"]
> [다음](creating-a-team-project-in-tfs.md)
