---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
title: '응용 프로그램 수명 주기 관리: 개발에서 프로덕션으로 | Microsoft Docs'
author: jrjlee
description: 이 항목에서는 가상 회사에서 테스트, 스테이징 및 프로덕션 환경을 통해 ASP.NET 웹 응용 프로그램의 배포를 관리 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f97a1145-6470-4bca-8f15-ccfb25fb903c
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
msc.type: authoredcontent
ms.openlocfilehash: 230cf4393db0ee19cfc42ed54359d61e7926a49d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520427"
---
# <a name="application-lifecycle-management-from-development-to-production"></a>응용 프로그램 수명 주기 관리: 개발에서 프로덕션으로

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 가상의 회사에서 테스트, 스테이징 및 프로덕션 환경을 통해 ASP.NET 웹 응용 프로그램의 배포를 관리 하는 방법을 보여 줍니다. 항목 전체에서 특정 작업을 수행 하는 방법에 대 한 추가 정보 및 연습에 대 한 링크가 제공 됩니다.
> 
> 이 항목은 엔터프라이즈의 웹 배포에 대 한 [일련의 자습서](deploying-web-applications-in-enterprise-scenarios.md) 에 대 한 개략적인 개요를 제공 하기 위한 것입니다. 여기&#x2014;에 설명 된 몇 가지 개념을 잘 모르는 경우 다음 자습서에서 이러한 모든 작업 및 기술에 대 한 자세한 정보를 제공 합니다.
> 
> > [!NOTE]
> > 편의상이 항목에서는 배포 프로세스의 일부로 데이터베이스를 업데이트 하는 방법에 대해 설명 하지 않습니다. 그러나 데이터베이스 기능에 대해 증분 업데이트를 수행 하는 것은 많은 엔터프라이즈 배포 시나리오의 요구 사항이 며,이 자습서 시리즈의 뒷부분에서이 작업을 수행 하는 방법에 대 한 지침을 찾을 수 있습니다. 자세한 내용은 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)를 참조 하세요.

## <a name="overview"></a>개요

여기에 설명 된 배포 프로세스는 [엔터프라이즈 웹 배포: 시나리오 개요](enterprise-web-deployment-scenario-overview.md)에 설명 된 Fabrikam, inc. 배포 시나리오를 기반으로 합니다. 이 항목을 학습 하기 전에 시나리오 개요를 읽어야 합니다. 기본적으로이 시나리오에서는 조직에서 일반적인 엔터프라이즈 환경에서 다양 한 [단계를 통해](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)합리적인 복합 웹 응용 프로그램의 배포를 관리 하는 방법을 살펴봅니다.

개략적인 수준에서 Contact Manager 솔루션은 개발 및 배포 프로세스의 일부로 이러한 단계를 진행 합니다.

1. 개발자는 일부 코드를 Team Foundation Server (TFS) 2010으로 확인 합니다.
2. TFS는 코드를 빌드하고 팀 프로젝트와 연결 된 단위 테스트를 실행 합니다.
3. TFS는 테스트 환경에 솔루션을 배포 합니다.
4. 개발자 팀은 테스트 환경에서 솔루션을 확인 하 고 유효성을 검사 합니다.
5. 스테이징 환경 관리자는 스테이징 환경에 대 한 "가상의 경우" 배포를 수행 하 여 배포 시 문제가 발생 하는지 여부를 설정 합니다.
6. 스테이징 환경 관리자는 스테이징 환경에 대 한 라이브 배포를 수행 합니다.
7. 이 솔루션은 스테이징 환경에서 사용자 승인 테스트를 수행 합니다.
8. 웹 배포 패키지를 프로덕션 환경으로 수동으로 가져옵니다.

이러한 단계는 연속 개발 주기의 일부를 형성 합니다.

![](application-lifecycle-management-from-development-to-production/_static/image1.png)

실제로이 프로세스는이 보다 약간 더 복잡 합니다. 각 단계를 좀 더 자세히 살펴보겠습니다. Fabrikam, i n c .는 각 대상 환경에 대해 다른 배포 방법을 사용 합니다.

![](application-lifecycle-management-from-development-to-production/_static/image2.png)

이 항목의 나머지 부분에서는이 배포 수명 주기의 주요 단계를 살펴봅니다.

- **필수 조건**: 배포 논리를 적용 하기 전에 서버 인프라를 구성 해야 하는 방법입니다.
- **초기 개발 및 배포**: 솔루션을 처음 배포 하기 전에 수행 해야 하는 작업입니다.
- **테스트에 대 한 배포**: 개발자가 새 코드를 체크 인할 때 콘텐츠를 자동으로 패키지 하 고 테스트 환경에 배포 하는 방법입니다.
- **스테이징에 배포**: 스테이징 환경에 특정 빌드를 배포 하는 방법 및 배포 시 문제가 발생 하지 않도록 "what if" 배포를 수행 하는 방법을 설명 합니다.
- **프로덕션에 배포**: 네트워크 인프라에서 원격 배포를 방지 하는 경우 프로덕션 환경으로 웹 패키지를 가져오는 방법입니다.

## <a name="prerequisites"></a>사전 요구 사항

배포 시나리오의 첫 번째 작업은 서버 인프라가 배포 도구 및 기술의 요구 사항을 충족 하는지 확인 하는 것입니다. 이 경우 Fabrikam, i n c .는 다음과 같이 서버 인프라를 구성 했습니다.

- TFS는 팀 프로젝트 컬렉션, 빌드 컨트롤러 및 빌드 에이전트를 포함 하도록 구성 되어 있습니다. 자세한 내용은 [자동화 된 웹 배포에 대 한 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) 을 참조 하세요.
- 테스트 환경은 웹 [배포용 테스트 환경 구성](../configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment.md) 및 [웹 배포 게시용 웹 서버 구성 (원격 에이전트)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)에 설명 된 대로 웹 Deployment Agent 서비스 ("원격 에이전트")를 사용 하 여 원격 배포를 허용 하도록 구성 됩니다.
- 스테이징 환경은 [시나리오: 웹 배포용 스테이징 환경 구성](../configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment.md) 및 [웹 배포 게시용 웹 서버 구성 (웹 배포 처리기)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)에 설명 된 대로 웹 배포 처리기 끝점을 사용 하 여 원격 배포를 허용 하도록 구성 됩니다.
- 프로덕션 환경은 관리자가 웹 [배포를 위한 프로덕션 환경 구성](../configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment.md) 및 [웹 배포 게시용 웹 서버 구성 (오프 라인 배포)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)에 설명 된 대로 웹 배포 패키지를 인터넷 정보 서비스 (IIS)로 수동으로 가져올 수 있도록 구성 됩니다.

## <a name="initial-development-and-deployment"></a>초기 개발 및 배포

Fabrikam, Inc. 개발 팀은 먼저 Contact Manager 솔루션을 배포할 수 있으므로 다음 작업을 수행 해야 합니다.

- TFS에서 새 팀 프로젝트를 만듭니다.
- 배포 논리를 포함 하는 Microsoft Build Engine (MSBuild) 프로젝트 파일을 만듭니다.
- 배포 프로세스를 트리거하는 TFS 빌드 정의를 만듭니다.

### <a name="create-a-new-team-project"></a>새 팀 프로젝트 만들기

- Tfs 관리자 인 Rob Walters는 [tfs에서 팀 프로젝트 만들기](../configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs.md)에 설명 된 대로 응용 프로그램에 대 한 새 팀 프로젝트를 만듭니다. 그런 다음 선임 개발자 인 Matt Hink는 기본 솔루션을 만듭니다. [소스 제어에 콘텐츠 추가](../configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control.md)에 설명 된 대로 TFS의 새 팀 프로젝트에 파일을 체크 인 합니다.

### <a name="create-the-deployment-logic"></a>배포 논리 만들기

Matt Hink는 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 분할 프로젝트 파일 방법을 사용 하 여 다양 한 사용자 지정 MSBuild 프로젝트 파일을 만듭니다. Matt는 다음을 만듭니다.

- 배포 프로세스를 실행 하는 *Publish. proj* 라는 프로젝트 파일 이 파일에는 솔루션에서 프로젝트를 빌드하고, 웹 패키지를 만들고, 대상 서버 환경에 패키지를 배포 하는 MSBuild 대상이 포함 되어 있습니다.
- 환경 관련 프로젝트 파일 *(env-Dev. proj* 및 *env)* . 여기에는 연결 문자열, 서비스 끝점, 웹 패키지를 수신 하는 원격 서비스의 세부 정보와 같이 각각 테스트 환경 및 스테이징 환경과 관련 된 설정이 포함 됩니다. 특정 대상 환경에 대 한 올바른 설정을 선택 하는 방법에 대 한 지침은 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)을 참조 하세요.

배포를 실행 하려면 사용자가 MSBuild 또는 팀 빌드를 사용 하 여 *Publish. proj* 파일을 실행 하 고 명령줄 인수로 관련 환경 특정 프로젝트 파일 (*env* 또는 *env*)의 위치를 지정 합니다. 그런 다음 *Publish. proj* 파일은 각 대상 환경에 대 한 전체 게시 명령 집합을 만들기 위해 환경 관련 프로젝트 파일을 가져옵니다.

> [!NOTE]
> 이러한 사용자 지정 프로젝트 파일의 작동 방식은 MSBuild를 호출 하는 데 사용 하는 메커니즘과는 독립적입니다. 예를 들어 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 대로 MSBuild 명령줄을 직접 사용할 수 있습니다. [배포 명령 파일 만들기 및 실행](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)에 설명 된 대로 명령 파일에서 프로젝트 파일을 실행할 수 있습니다. 또는 [배포를 지 원하는 빌드 정의 만들기](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)에 설명 된 대로 TFS의 빌드 정의에서 프로젝트 파일을 실행할 수 있습니다.  
> 각 사례에서 최종 결과는 동일한&#x2014;MSBuild가 병합 된 프로젝트 파일을 실행 하 고 대상 환경에 솔루션을 배포 합니다. 이렇게 하면 게시 프로세스를 트리거하는 방법에 상당한 유연성을 제공 합니다.

사용자 지정 프로젝트 파일을 만든 후에는 Matt가 해당 파일을 솔루션 폴더에 추가 하 고 소스 제어에 체크 인 합니다.

### <a name="create-build-definitions"></a>빌드 정의 만들기

마지막 준비 작업으로, Matt 및 Rob은 함께 작동 하 여 새 팀 프로젝트에 대 한 세 가지 빌드 정의를 만듭니다.

- **Deploytotest**. 그러면 연락처 관리자 솔루션이 빌드되고 체크 인이 발생할 때마다 테스트 환경에 배포 됩니다.
- **Deploytostaging**. 개발자가 빌드를 큐에 대기 시킬 때 지정 된 이전 빌드의 리소스를 스테이징 환경에 배포 합니다.
- **Deploytostaging-WhatIf**. 개발자가 빌드를 큐에 대기 시킬 때 스테이징 환경에 대 한 "가상의 경우" 배포를 수행 합니다.

다음 섹션에서는 이러한 각 빌드 정의에 대해 더 자세한 정보를 제공 합니다.

## <a name="deployment-to-test"></a>테스트에 대 한 배포

Fabrikam, i n c .의 개발 팀은 확인 및 유효성 검사, 유용성 테스트, 호환성 테스트, 임시 테스트, 예비 테스트와 같은 다양 한 소프트웨어 테스트 작업을 수행 하기 위한 테스트 환경을 유지 관리 합니다.

개발 팀에서 **Deploytotest**라는 TFS에 빌드 정의를 만들었습니다. 이 빌드 정의는 연속 통합 트리거를 사용 합니다. 즉, Fabrikam, Inc. 개발 팀의 멤버가 체크 인을 수행할 때마다 빌드 프로세스가 실행 됩니다. 빌드가 트리거되면 빌드 정의는 다음을 수행 합니다.

- 연락처 관리자 .sln 솔루션을 빌드합니다. 그러면 솔루션 내의 모든 프로젝트가 빌드됩니다.
- 솔루션이 성공적으로 빌드되면 솔루션 폴더 구조에서 단위 테스트를 실행 합니다.
- 배포 프로세스를 제어 하는 사용자 지정 프로젝트 파일을 실행 합니다 (솔루션이 성공적으로 빌드되고 단위 테스트를 통과 하는 경우).

최종 결과는 솔루션이 성공적으로 빌드되고 단위 테스트를 통과 하면 웹 패키지 및 기타 배포 리소스가 테스트 환경에 배포 되는 것입니다.

![](application-lifecycle-management-from-development-to-production/_static/image3.png)

### <a name="how-does-the-deployment-process-work"></a>배포 프로세스는 어떻게 작동 하나요?

**Deploytotest** 빌드 정의는 이러한 인수를 MSBuild에 제공 합니다.

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample1.cmd)]

**Deployonbuild = true** 및 **deploytarget = Package** 속성은 팀 빌드에서 솔루션 내에서 프로젝트를 빌드할 때 사용 됩니다. 프로젝트가 웹 응용 프로그램 프로젝트인 경우 이러한 속성은 프로젝트의 웹 배포 패키지를 만들도록 MSBuild에 지시 합니다. **TargetEnvPropsFile** 속성은 내보낼 환경 관련 프로젝트 파일을 찾을 위치를 *Publish. proj* 파일에 알려 줍니다.

> [!NOTE]
> 이와 같은 빌드 정의를 만드는 방법에 대 한 자세한 연습은 [배포를 지 원하는 빌드 정의 만들기](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)를 참조 하세요.

*Publish. proj* 파일에는 솔루션의 각 프로젝트를 빌드하는 대상이 포함 되어 있습니다. 그러나 팀 빌드에서 파일을 실행 하는 경우 이러한 빌드 대상을 건너뛰는 조건부 논리도 포함 됩니다. 이렇게 하면 단위 테스트를 실행 하는 기능과 같이 팀 빌드에서 제공 하는 추가 빌드 기능을 활용할 수 있습니다. 솔루션 빌드 또는 단위 테스트가 실패할 경우에는 *Publish. proj* 파일이 실행 되지 않고 응용 프로그램이 배포 되지 않습니다.

조건부 논리는 **BuildingInTeamBuild** 속성을 평가 하 여 수행 됩니다. 팀 빌드를 사용 하 여 프로젝트를 빌드할 때 자동으로 **true** 로 설정 되는 MSBuild 속성입니다.

## <a name="deployment-to-staging"></a>스테이징에 배포

빌드가 테스트 환경에서 개발자 팀의 요구 사항을 모두 충족 하는 경우 팀은 동일한 빌드를 스테이징 환경에 배포 하려고 할 수 있습니다. 스테이징 환경은 일반적으로 서버 사양, 운영 체제 및 소프트웨어 및 네트워크 구성과 같이 최대한 긴밀 하 게 프로덕션 또는 "라이브" 환경의 특성과 일치 하도록 구성 됩니다. 스테이징 환경은 일반적으로 부하 테스트, 사용자 승인 테스트 및 광범위 한 내부 검토에 사용 됩니다. 빌드는 빌드 서버에서 직접 스테이징 환경에 배포 됩니다.

![](application-lifecycle-management-from-development-to-production/_static/image4.png)

스테이징 환경에 솔루션을 배포 하는 데 사용 되는 빌드 정의 ( **deploytostaging-WhatIf** 및 **deploytostaging**)는 다음 특성을 공유 합니다.

- 실제로 아무것도 빌드하지 않습니다. Rob이 스테이징 환경에 솔루션을 배포 하는 경우 테스트 환경에서 이미 확인 되 고 유효성이 검사 된 특정 기존 빌드를 배포 하려고 합니다. 빌드 정의는 배포 프로세스를 제어 하는 사용자 지정 프로젝트 파일을 실행 하기만 하면 됩니다.
- Rob은 빌드를 트리거할 때 빌드 매개 변수를 사용 하 여 빌드 서버에서 배포 하려는 리소스를 포함 하는 빌드를 지정 합니다.
- 빌드 정의는 자동으로 트리거되지 않습니다. Rob은 스테이징 환경에 솔루션을 배포 하려는 경우 수동으로 빌드를 큐에 대기 시킵니다.

스테이징 환경에 배포 하기 위한 개략적인 프로세스는 다음과 같습니다.

1. 스테이징 환경 관리자 인 Rob Walters는 **Deploytostaging-WhatIf** 빌드 정의를 사용 하 여 빌드를 큐에 대기 시킵니다. Rob은 빌드 정의 매개 변수를 사용 하 여 배포 하려는 빌드를 지정 합니다.
2. **Deploytostaging-WhatIf** 빌드 정의는 "what if" 모드에서 사용자 지정 프로젝트 파일을 실행 합니다. 이는 Rob이 라이브 배포를 수행 하는 것 처럼 로그 파일을 생성 하지만 실제로 대상 환경을 변경 하지는 않습니다.
3. Rob은 로그 파일을 검토 하 여 스테이징 환경에 대 한 배포의 영향을 확인 합니다. 특히, Rob은 추가할 항목, 업데이트 되는 내용 및 삭제할 항목을 확인 하려고 합니다.
4. Rob이 배포에서 기존 리소스나 데이터를 원치 않는 변경을 수행 하지 않는 경우 **Deploytostaging** 빌드 정의를 사용 하 여 빌드를 큐에 대기 시킵니다.
5. **Deploytostaging** 빌드 정의는 사용자 지정 프로젝트 파일을 실행 합니다. 배포 리소스를 스테이징 환경의 주 웹 서버에 게시 합니다.
6. WFF (웹 팜 프레임 워크) 컨트롤러는 스테이징 환경의 웹 서버를 동기화 합니다. 이렇게 하면 서버 팜의 모든 웹 서버에서 응용 프로그램을 사용할 수 있습니다.

### <a name="how-does-the-deployment-process-work"></a>배포 프로세스는 어떻게 작동 하나요?

**Deploytostaging** 빌드 정의는 이러한 인수를 MSBuild에 제공 합니다.

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample2.cmd)]

**TargetEnvPropsFile** 속성은 내보낼 환경 관련 프로젝트 파일을 찾을 위치를 *Publish. proj* 파일에 알려 줍니다. **Outputroot** 속성은 기본 제공 값을 재정의 하 고 배포 하려는 리소스가 포함 된 빌드 폴더의 위치를 나타냅니다. Rob이 빌드를 큐에 대기 시킬 때 **매개 변수** 탭을 사용 하 여 **outputroot** 속성에 업데이트 된 값을 제공 합니다.

![](application-lifecycle-management-from-development-to-production/_static/image5.png)

> [!NOTE]
> 이와 같은 빌드 정의를 만드는 방법에 대 한 자세한 내용은 [특정 빌드 배포](../configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build.md)를 참조 하세요.

**Deploytostaging-WhatIf** 빌드 정의는 **deploytostaging** 빌드 정의와 동일한 배포 논리를 포함 합니다. 그러나 추가 인수 **WhatIf = true**를 포함 합니다.

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample3.cmd)]

*Publish. proj* 파일 내에서 **WhatIf** 속성은 모든 배포 리소스를 "what if" 모드로 게시 해야 함을 나타냅니다. 즉, 로그 파일은 배포가 이전에 발생 한 것 처럼 생성 되지만 실제로는 대상 환경에서 변경 되지 않습니다. 이를 통해 제안 된 배포&#x2014;의 영향, 특히 추가 될 내용, 업데이트 되는 내용 및 실제로 변경 작업을 수행 하기 전에 삭제&#x2014;되는 내용을 평가할 수 있습니다.

> [!NOTE]
> "What if" 배포를 구성 하는 방법에 대 한 자세한 내용은 ["What If" 배포 수행](../advanced-enterprise-web-deployment/performing-a-what-if-deployment.md)을 참조 하세요.

스테이징 환경의 주 웹 서버에 응용 프로그램을 배포 하면 WFF가 서버 팜의 모든 서버에서 응용 프로그램을 자동으로 동기화 합니다.

> [!NOTE]
> 웹 서버를 동기화 하도록 WFF를 구성 하는 방법에 대 한 자세한 내용은 [웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기](../configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework.md)를 참조 하세요.

## <a name="deployment-to-production"></a>프로덕션 환경에 배포

스테이징 환경에서 빌드가 승인 되 면 Fabrikam, Inc. 팀은 프로덕션 환경에 응용 프로그램을 게시할 수 있습니다. 프로덕션 환경에서는 응용 프로그램이 "live"로 이동 하 여 최종 사용자의 대상 사용자에 게 도달 합니다.

프로덕션 환경은 인터넷 연결 경계 네트워크에 있습니다. 이는 빌드 서버를 포함 하는 내부 네트워크에서 격리 됩니다. 프로덕션 환경 관리자 리사 Andrews는 빌드 서버에서 웹 배포 패키지를 수동으로 복사 하 여 주 프로덕션 웹 서버의 IIS로 가져와야 합니다.

![](application-lifecycle-management-from-development-to-production/_static/image6.png)

프로덕션 환경에 배포 하기 위한 개략적인 프로세스는 다음과 같습니다.

1. 개발자 팀은 빌드를 프로덕션 환경에 배포할 준비가 되었음을 유가을에 게 제안 합니다. 팀은 리사를 빌드 서버의 drop 폴더 내에 있는 웹 배포 패키지의 위치에 대해 알려줍니다.
2. 리사는 빌드 서버에서 웹 패키지를 수집 하 여 프로덕션 환경의 주 웹 서버에 복사 합니다.
3. 리사는 IIS 관리자를 사용 하 여 기본 웹 서버에서 웹 패키지를 가져오고 게시 합니다.
4. WFF 컨트롤러는 프로덕션 환경의 웹 서버를 동기화 합니다. 이렇게 하면 서버 팜의 모든 웹 서버에서 응용 프로그램을 사용할 수 있습니다.

### <a name="how-does-the-deployment-process-work"></a>배포 프로세스는 어떻게 작동 하나요?

IIS 관리자에는 웹 패키지를 IIS 웹 사이트에 쉽게 게시할 수 있도록 하는 응용 프로그램 패키지 가져오기 마법사가 포함 되어 있습니다. 이 절차를 수행 하는 방법에 대 한 연습은 [수동으로 웹 패키지 설치](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)를 참조 하세요.

## <a name="conclusion"></a>결론

이 항목에서는 일반적인 엔터프라이즈급 웹 응용 프로그램에 대 한 배포 수명 주기를 보여 줍니다.

이 항목에서는 웹 응용 프로그램 배포의 다양 한 측면에 대 한 지침을 제공 하는 일련의 자습서 중 일부를 구성 합니다. 실제로는 배포 프로세스의 각 단계에서 많은 추가 작업 및 고려 사항이 있으며,이 작업은 단일 연습에서 모두 다룰 수 없습니다. 자세한 내용은 다음 자습서를 참조 하세요.

- [엔터프라이즈의 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). 이 자습서에서는 MSBuild 및 IIS 웹 배포 도구 (웹 배포)를 사용 하는 웹 배포 기술에 대 한 포괄적인 소개를 제공 합니다.
- [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md) 이 자습서에서는 다양 한 배포 시나리오를 지원 하도록 Windows server 환경을 구성 하는 방법에 대 한 지침을 제공 합니다.
- [자동화 된 웹 배포에 대 한 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) 이 자습서에서는 배포 논리를 TFS 빌드 프로세스에 통합 하는 방법에 대 한 지침을 제공 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). 이 자습서에서는 조직에서 직면 하는 보다 복잡 한 배포 문제 중 일부를 충족 하는 방법에 대 한 지침을 제공 합니다.

> [!div class="step-by-step"]
> [이전](enterprise-web-deployment-scenario-overview.md)
