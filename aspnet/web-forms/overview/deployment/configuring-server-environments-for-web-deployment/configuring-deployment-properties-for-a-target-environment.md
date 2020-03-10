---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
title: 대상 환경에 대 한 배포 속성 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 특정 대상 환경에 샘플 Contact Manager 솔루션을 배포 하기 위해 환경 특정 속성을 구성 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b5b86e03-b8ed-46e6-90fa-e1da88ef34e9
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
msc.type: authoredcontent
ms.openlocfilehash: 9742be7d718384c1b108d5f2c0c43e8e8d4fe8a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516809"
---
# <a name="configuring-deployment-properties-for-a-target-environment"></a>대상 환경의 배포 속성 구성

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 특정 대상 환경에 샘플 Contact Manager 솔루션을 배포 하기 위해 환경 특정 속성을 구성 하는 방법에 대해 설명 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 [시리즈에서는 샘플](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션&#x2014;&#x2014;을 사용 하 여 ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 빌드&#x2014; [프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)에서 설명 하는 빌드 프로세스 이해에 설명 된 분할 프로젝트 파일 방식을 기반으로 합니다. 빌드 프로세스는 모든 대상 환경에 적용 되는 빌드 명령을 포함 하 고 다른 하나는 환경 특정 빌드 및 배포 설정을 포함 합니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="process-overview"></a>프로세스 개요

Contact Manager 솔루션을 빌드하고 배포 하는 데 사용할 프로젝트 파일은 두 개의 물리적 파일로 분할 됩니다.

- 유니버설 빌드 설정 및 명령 ( *Publish. proj* 파일)을 포함 하는 항목입니다.
- 환경 특정 빌드 설정 (*env*, *env, env*등)을 포함 하는 하나입니다.

빌드 시 적절 한 환경 관련 프로젝트 파일이 유니버설 *Publish. proj* 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다. 고유한 배포 시나리오를 설명 하는 설정을 사용 하 여 환경 특정 프로젝트 파일을 만들거나 사용자 지정 하 여 특정 대상 환경에 대 한 배포를 구성할 수 있습니다.

이러한 값의 대부분은 대상 웹 서버가 웹 Deployment Agent 서비스 (원격&#x2014;에이전트) 또는 웹 배포 처리기를 사용 하도록 구성 되어 있는지 여부에 따라 특정 대상 환경을 구성 하는 방법에 따라 결정 됩니다. 이러한 접근 방식에 대 한 자세한 내용과 사용자 환경에 적합 한 접근 방식을 선택 하는 방법에 대 한 자세한 내용은 [웹 배포에 대 한 적절 한 접근 방법 선택](choosing-the-right-approach-to-web-deployment.md)을 참조 하세요.

[연락처 관리자 시나리오](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) 에는 다음과 같은 두 가지 환경 관련 프로젝트 파일이 필요 합니다.

- 개발자 테스트 환경에 배포 (*Env-Dev. proj*) [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)에 설명 된 대로 원격 에이전트를 사용 하 여 원격 배포를 허용 하도록 개발자 테스트 환경을 구성 합니다. 이 파일은 원격 에이전트 끝점 주소 뿐만 아니라 연결 문자열 및 서비스 끝점과 같은 위치 관련 설정도 제공 해야 합니다.
- 스테이징 환경에 배포 (*Env-단계 proj*). 스테이징 환경은 [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)에 설명 된 대로 웹 배포 처리기를 사용 하 여 원격 배포를 허용 하도록 구성 됩니다. 이 파일에는 연결 문자열 및 서비스 끝점과 같은 위치 관련 설정 뿐만 아니라 웹 배포 처리기 끝점 주소를 제공 해야 합니다.

환경 관련 프로젝트 파일에서 구성 하는 설정은 웹 패키지 자체&#x2014;의 내용에 영향을 주지 않습니다. 대신 패키지가 배포 되는 방법과 패키지를 추출할 때 제공 되는 매개 변수 값을 제어 합니다. [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md) 및 [웹 패키지 수동 설치](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)시나리오에 설명 된 대로 웹 패키지를 프로덕션 환경으로 수동으로 가져오는 것이 좋습니다. 따라서 패키지를 생성할 때 환경 관련 프로젝트 파일에서 사용 하는 설정이 중요 하지 않습니다. 인터넷 정보 서비스 (IIS) 관리자는 패키지를 가져올 때 연결 문자열 및 서비스 끝점과 같은 매개 변수가 있는 값을 묻는 메시지를 표시 합니다.

사용자 고유의 대상 환경에 연락 관리자 솔루션을 배포 하려면이 파일을 사용자 지정 하거나 템플릿으로 사용 하 여 고유한 파일을 만들 수 있습니다.

**Contact Manager 솔루션에 대 한 환경 특정 배포 설정을 구성 하려면**

1. Visual Studio 2010에서 연락처 관리자-WCF 솔루션을 엽니다.
2. **솔루션 탐색기** 창에서 **게시** 폴더를 확장 하 고 **EnvConfig** 폴더를 확장 한 다음 **Env-Dev. proj**를 두 번 클릭 합니다.

    ![](configuring-deployment-properties-for-a-target-environment/_static/image1.png)
3. *Env-Dev. proj* 파일의 속성 값을 고유한 테스트 환경에 맞는 올바른 값으로 바꿉니다.

    > [!NOTE]
    > 이 절차 다음에 나오는 표에서는 이러한 각 속성에 대 한 자세한 정보를 제공 합니다.
4. 작업 내용을 저장 하 고 *Env-Dev.* n e f 파일을 닫습니다.

## <a name="choosing-the-right-deployment-properties"></a>올바른 배포 속성 선택

이 표에서는 샘플 환경 관련 프로젝트 파일인 *Env-Dev*에서 각 속성의 용도를 설명 하 고 제공 해야 하는 값에 대 한 몇 가지 지침을 제공 합니다.

|                                                        속성 이름                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        세부 정보                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <strong>MSDeployComputerName</strong> 대상 웹 서버 또는 서비스 끝점의 이름입니다.               |                                                                                                                                                                                                                                              대상 웹 서버에서 원격 에이전트 서비스에 배포 하는 경우 대상 컴퓨터 이름 (예: <strong>TESTWEB1</strong> 또는 <strong>TESTWEB1.fabrikam.net</strong>)을 지정 하거나 원격 에이전트 끝점 (예: `http://TESTWEB1/MSDEPLOYAGENTSERVICE`)을 지정할 수 있습니다. 배포는 각각의 경우와 동일한 방식으로 작동 합니다. 대상 웹 서버에서 웹 배포 처리기에 배포 하는 경우 서비스 끝점을 지정 하 고 IIS 웹 사이트의 이름을 쿼리 문자열 매개 변수로 포함 해야 합니다 (예: `https://STAGEWEB1:8172/MSDeploy.axd?site=DemoSite`).                                                                                                                                                                                                                                              |
|         <strong>MSDeployAuth</strong> 웹 배포에서 원격 컴퓨터에 인증 하는 데 사용 해야 하는 메서드입니다.          |                                                                                                                                                                                                                          <strong>NTLM</strong> 또는 <strong>기본</strong>으로 설정 해야 합니다. 일반적으로 웹 배포 처리기에 배포 하는 경우 원격 에이전트 서비스 및 <strong>Basic</strong> 에 배포 하는 경우 <strong>NTLM</strong> 을 사용 합니다. 기본 인증을 사용 하는 경우 배포를 수행 하기 위해 IIS 웹 배포 도구 (웹 배포)에서 가장할 사용자 이름 및 암호도 지정 해야 합니다. 이 예제에서 이러한 값은 <strong>MSDeployUsername</strong> 및 <strong>MSDeployPassword</strong> 속성을 통해 제공 됩니다. NTLM 인증을 사용 하는 경우 이러한 속성을 생략 하거나 비워 둘 수 있습니다.                                                                                                                                                                                                                          |
| <strong>MSDeployUsername</strong> 기본 인증을 사용 하는 경우 웹 배포은 원격 컴퓨터에서이 계정을 사용 합니다.  |                                                                                                                                                                                                                                                                                                                                                                                                                       <em>도메인</em>\*사용자 이름 * 형식으로 지정 해야 합니다 (예: <strong>FABRIKAM\matt</strong>). 이 값은 기본 인증을 지정 하는 경우에만 사용 됩니다. NTLM 인증을 사용 하는 경우 속성을 생략할 수 있습니다. 값을 제공 하면 무시 됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                        |
| <strong>MSDeployPassword</strong> 기본 인증을 사용 하는 경우 웹 배포은 원격 컴퓨터에서이 암호를 사용 합니다. |                                                                                                                                                                                                                                                                                                                                                                                                                    <strong>MSDeployUsername</strong> 속성에 지정한 사용자 계정의 암호입니다. 이 값은 기본 인증을 지정 하는 경우에만 사용 됩니다. NTLM 인증을 사용 하는 경우 속성을 생략할 수 있습니다. 값을 제공 하면 무시 됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                    |
|     <strong>ContactManagerIisPath</strong> Contact Manager MVC 응용 프로그램을 배포 하려는 IIS 경로입니다.     |                                                                                                                                                                                                                                                                                                                                                                        IIS 관리자에 표시 되는 경로는 [<em>iis 웹 사이트 이름</em>]/[<em>웹</em><em>응용 프로그램 이름</em>] 형식으로 지정 해야 합니다. 응용 프로그램을 배포 하기 전에 IIS 웹 사이트가 있어야 합니다. 예를 들어 DemoSite 라는 IIS 웹 사이트를 만든 경우 MVC 응용 프로그램에 대 한 IIS 경로를 DemoSite/연락처 관리자로 지정할 수 있습니다.                                                                                                                                                                                                                                                                                                                                                                        |
|   <strong>ContactManagerServiceIisPath</strong> Contact Manager WCF 서비스를 배포 하려는 IIS 경로입니다.    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                          예를 들어 DemoSite 라는 IIS 웹 사이트를 만든 경우 WCF 서비스에 대 한 IIS 경로를 <strong>demosite/ContactManagerService</strong>으로 지정할 수 있습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                  <strong>ContactManagerTargetUrl</strong> WCF 서비스에 연결할 수 있는 URL입니다.                   |                                                                                                                                                     그러면 [<em>IIS 웹 사이트 루트 URL</em>]/[<em>서비스 응용 프로그램 이름</em>]/[<em>서비스 끝점</em>] 형식이 사용 됩니다. 예를 들어 85 포트에서 IIS 웹 사이트를 만든 경우 URL은 `http://localhost:85/ContactManagerService/ContactService.svc`형식을 사용 합니다. MVC 응용 프로그램 및 WCF 서비스는 동일한 서버에 배포 됩니다. 결과적으로이 URL은 해당 데이터베이스가 설치 된 컴퓨터 에서만 액세스 됩니다. 따라서 URL에는 컴퓨터 이름이 나 호스트 헤더가 아닌 localhost 또는 IP 주소를 사용 하는 것이 좋습니다. 컴퓨터 이름이 나 호스트 헤더를 사용 하는 경우 IIS의 [루프백](https://go.microsoft.com/?linkid=9805131) 보안 기능에서 URL을 차단 하 고 <strong>HTTP 401.1-권한이 없음</strong> 오류를 반환할 수 있습니다.                                                                                                                                                     |
|                  <strong>CmDatabaseConnectionString</strong> 데이터베이스 서버에 대 한 연결 문자열입니다.                  | 연결 문자열은 VSDBCMD가 데이터베이스 서버에 연결 하는 데 사용할 자격 증명과 웹 서버 응용 프로그램 풀에서 데이터베이스 서버에 연결 하 고 데이터베이스와 상호 작용 하는 데 사용할 자격 증명을 모두 결정 합니다. 기본적으로 두 가지 옵션을 선택할 수 있습니다. Integrated <strong>security = true</strong>를 지정할 수 있습니다 .이 경우 Windows 통합 인증이 사용 됩니다 .이 경우에는 <strong>DATA Source = 배치한; integrated security = true</strong> 입니다 .이 경우에는 VSDBCMD 실행 파일을 실행 하는 사용자의 자격 증명을 사용 하 여 데이터베이스가 생성 되 고 응용 프로그램은 웹 서버 컴퓨터 계정의 id를 사용 하 여 데이터베이스에 액세스 합니다. 또는 SQL Server 계정의 사용자 이름 및 암호를 지정할 수 있습니다. 이 경우 SQL Server 자격 증명을 사용 하 여 데이터베이스를 만들고 응용 프로그램 풀을 사용 하 여 데이터베이스와 상호 작용 합니다. <strong>Data Source = 배치한; 사용자 Id = ASqlUser; Password = Pa $ $w 0rd</strong> 이 항목의 연습에서는 Windows 통합 인증을 사용 한다고 가정 합니다. |
|        <strong>Cmtargetdatabase</strong> 데이터베이스 서버에서 만들 데이터베이스를 지정 하는 데 사용할 이름입니다.        |                                                                                                                                                                                                                                                                                                                                                                                                                                                     여기에서 제공 하는 값은 VSDBCMD 명령에 매개 변수로 추가 됩니다. 웹 서버의 응용 프로그램 풀에서 데이터베이스와 상호 작용 하는 데 사용할 수 있는 전체 연결 문자열을 작성 하는 데도 사용 됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

이러한 예제에서는 특정 배포 시나리오에 대해 이러한 속성을 구성 하는 방법을 보여 줍니다.

### <a name="example-1x2014deployment-to-the-remote-agent-service"></a>원격 에이전트&#x2014;서비스에 대 한 예제 1 배포

이 예제에서:

- TESTWEB1의 원격 에이전트 서비스에 배포 하는 중입니다.
- NTLM 인증을 사용 하도록 웹 배포에 지시 하 고 있습니다. 웹 배포 Microsoft Build Engine (MSBuild)를 호출 하는 데 사용한 자격 증명을 사용 하 여 실행 됩니다.
- 통합 인증을 사용 하 여 배치한에 데이터 **관리자** 데이터베이스를 배포 하 고 있습니다. MSBuild를 호출 하는 데 사용한 자격 증명을 사용 하 여 데이터베이스를 배포 합니다.

[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample1.xml)]

### <a name="example-2x2014deployment-to-the-web-deploy-handler-endpoint"></a>예 2&#x2014;웹 배포 처리기 끝점에 배포

이 예제에서:

- STAGEWEB1의 웹 배포 Handler 서비스 끝점에 배포 하는 중입니다.
- 웹 배포 기본 인증을 사용 하도록 지시 하 고 있습니다.
- 웹 배포 원격 컴퓨터에서 FABRIKAM\stagingdeployer 계정을 가장 하도록 지정 하는 것입니다.
- SQL Server 인증을 사용 하 여 STAGEDB1에 데이터 **관리자** 데이터베이스를 배포 합니다.

[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample2.xml)]

## <a name="conclusion"></a>결론

이 시점에서 프로젝트 파일은 하나 이상의 대상 환경에 대해 Contact Manager 솔루션을 빌드하고 배포 하도록 완전히 구성 됩니다.

이 프로젝트 파일을 단일 단계의 반복 가능한 배포 프로세스의 일부로 사용 하려면 MSBuild를 사용 하 여 *게시 proj* 파일을 실행 하 고 환경 관련 프로젝트 파일의 위치를 매개 변수로 전달 해야 합니다. 다음과 같은 다양 한 방법으로이 작업을 수행할 수 있습니다.

- MSBuild의 개요와 사용자 지정 프로젝트 파일에 대 한 소개는 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)를 참조 하세요.
- 사용자 지정 프로젝트 파일을 실행 하는 MSBuild 명령을 작성 하는 방법에 대 한 자세한 내용은 [웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)를 참조 하세요.
- 단일 단계의 반복 가능한 배포를 위해 명령 파일에 MSBuild 명령을 통합 하는 방법에 대 한 자세한 내용은 [배포 명령 파일 만들기 및 실행](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)을 참조 하세요.
- 팀 빌드에서 사용자 지정 프로젝트 파일을 실행 하는 방법에 대 한 자세한 내용은 [배포를 지 원하는 빌드 정의 만들기](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](creating-a-server-farm-with-the-web-farm-framework.md)
