---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
title: 웹 패키지 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포 도구)를 사용 하 여 원격 서버에 웹 배포 패키지를 게시 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a5c5eed2-8683-40a5-a2e1-35c9f8d17c29
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 91b99e6e250342851aea6860164b6f6af54818d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464969"
---
# <a name="deploying-web-packages"></a>웹 패키지 배포

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0를 사용 하 여 원격 서버에 웹 배포 패키지를 게시할 수 있는 방법에 대해 설명 합니다.
> 
> 웹 패키지를 원격 서버에 배포할 수 있는 두 가지 주요 방법이 있습니다.
> 
> - Msdeploy.exe 명령줄 유틸리티를 직접 사용할 수 있습니다.
> - 빌드 프로세스에서 생성 하는 *[project name]. .deploy* 파일을 실행할 수 있습니다.
> 
> 최종 결과는 사용 하는 방법에 관계 없이 동일 합니다. 기본적으로 모든 *. .deploy* 파일은 미리 정의 된 값으로 msdeploy.exe를 실행 하 여 패키지를 배포 하기 위해 많은 정보를 제공할 필요가 없도록 합니다. 이렇게 하면 배포 프로세스가 간단해 집니다. 반면, Msdeploy.exe를 직접 사용 하면 패키지를 배포 하는 방법에 비해 훨씬 더 많은 유연성을 제공 합니다.
> 
> 사용 하는 방법은 배포 프로세스에 대해 필요한 제어 양과 웹 배포 원격 에이전트 서비스를 대상으로 하는지 아니면 웹 배포 처리기를 대상으로 하는지 여부를 비롯 한 다양 한 요인에 따라 달라 집니다. 이 항목에서는 각 접근 방법을 사용 하는 방법에 대해 설명 하 고 각 방법이 적절 한 경우를 식별 합니다.
> 
> 이 항목의 작업 및 연습에서는 다음을 가정 합니다.
> 
> - [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)에 설명 된 대로 웹 응용 프로그램을 빌드 및 패키지화 했습니다.
> - [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)에 설명 된 대로 *setparameters .xml* 파일을 수정 하 여 대상 환경에 적합 한 매개 변수 값을 제공 했습니다.

웹 패키지를 배포 하는 가장 간단한 방법은 [*project name*] *. .deploy* 파일을 실행 하는 것입니다. 특히 *. deploy .cmd* 파일을 사용 하면 msdeploy.exe를 직접 사용 하는 것 보다 다음과 같은 이점이 제공 됩니다.

- 웹 배포 패키지&#x2014;의 위치를 지정 하지 않아도 됩니다 *. .deploy* 파일은 이미 있는 위치를 알고 있습니다.
- *Setparameters .xml* 파일&#x2014;의 위치를 지정 하지 않아도 됩니다. *.deploy* 파일은 이미 있는 위치를 알고 있습니다.
- 원본 및 대상 Msdeploy.exe 공급자&#x2014;를 지정할 필요가 없습니다 *. .deploy* 파일은 사용할 값을 이미 알고 있습니다.
- Msdeploy.exe 작업 설정을&#x2014;지정할 필요가 없습니다 *. .deploy* 파일에 일반적으로 필요한 값이 msdeploy.exe 명령에 자동으로 추가 됩니다.

*.Deploy* 파일을 사용 하 여 웹 패키지를 배포 하기 전에 다음을 확인 해야 합니다.

- *.Deploy* 파일 ([*프로젝트 이름*])을 입력 합니다. *Setparameters .xml* 파일 및 웹 패키지 ([*프로젝트 이름*] *) zip*)는 동일한 폴더에 있습니다.
- 웹 배포 (Msdeploy.exe)는 ..exe 파일을 실행 하는 컴퓨터에 설치 *됩니다.*

*.Deploy. .cmd* 파일은 다양 한 명령줄 옵션을 지원 합니다. 명령 프롬프트에서 파일을 실행 하는 경우 기본 구문은 다음과 같습니다.

[!code-console[Main](deploying-web-packages/samples/sample1.cmd)]

평가판 실행 또는 라이브 배포를 각각 수행할지 여부를 지정 하려면 **/t** 플래그 또는 **/y** 플래그를 지정 해야 합니다 (동일한 명령에서 두 플래그를 모두 사용 하지 않음). 다음 표에서는 이러한 각 플래그의 용도에 대해 설명 합니다.

| 플래그 | Description |
| --- | --- |
| **/T** | 평가판 실행을 나타내는 **– whatif** 플래그를 사용 하 여 msdeploy.exe를 호출 합니다. 패키지를 배포 하는 대신 패키지를 배포 하는 경우 발생 하는 상황에 대 한 보고서가 생성 됩니다. |
| **/Y** | **– Whatif** 플래그 없이 msdeploy.exe를 호출 합니다. 이렇게 하면 패키지가 로컬 컴퓨터 또는 지정 된 대상 서버에 배포 됩니다. |
| **연속** | 대상 서버 이름 또는 서비스 URL을 지정 합니다. 여기에서 제공할 수 있는 값에 대 한 자세한 내용은이 항목의 **끝점 고려 사항** 섹션을 참조 하세요. **/M** 플래그를 생략 하면 패키지가 로컬 컴퓨터에 배포 됩니다. |
| **없음을** | Msdeploy.exe에서 배포를 수행 하는 데 사용 해야 하는 인증 유형을 지정 합니다. 가능한 값은 **NTLM** 및 **기본**입니다. **/A** 플래그를 생략 하면 인증 유형은 웹 배포 원격 에이전트 서비스에 배포 하는 경우 **NTLM** 으로 설정 되 고 웹 배포 처리기에 배포할 때 **기본** 으로 설정 됩니다. |
| **/U** | 사용자 이름을 지정합니다. 이는 기본 인증을 사용 하는 경우에만 적용 됩니다. |
| **/P** | 암호를 지정합니다. 이는 기본 인증을 사용 하는 경우에만 적용 됩니다. |
| **/L** | 패키지가 로컬 IIS Express 인스턴스에 배포 되어야 함을 나타냅니다. |
| **/G** | [Tempagent 공급자 설정을](https://technet.microsoft.com/library/ee517345(WS.10).aspx)사용 하 여 패키지를 배포 하도록 지정 합니다. **/G** 플래그를 생략 하면 값의 기본값은 **false**입니다. |

> [!NOTE]
> 빌드 프로세스에서 웹 패키지를 만들 때마다 이러한 배포 옵션을 설명 하는 *[project name]. deploy-readme* 라는 파일도 만들어집니다.

이러한 플래그 외에도 웹 배포 작업 설정을 추가 *.* s t a s 매개 변수로 지정할 수 있습니다. 지정 하는 모든 추가 설정은 단순히 Msdeploy.exe 명령으로 전달 됩니다. 이러한 설정에 대 한 자세한 내용은 [웹 배포 작업 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)을 참조 하세요.

*.Deploy. .cmd* 파일을 실행 하 여 테스트 환경에 지 수의 웹 응용 프로그램 프로젝트를 배포 하려는 경우를 가정 합니다. 테스트 환경은 [웹 배포 게시를 위한 웹 서버 구성 (원격 에이전트)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)에 설명 된 대로 웹 배포 원격 에이전트 서비스를 사용 하도록 구성 됩니다. 웹 응용 프로그램을 배포 하려면 다음 단계를 완료 해야 합니다.

**.Deploy. .cmd 파일을 사용 하 여 웹 응용 프로그램을 배포 하려면**

1. [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)에 설명 된 대로 웹 응용 프로그램 프로젝트를 빌드하고 패키지 합니다.
2. [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)에 설명 된 대로 테스트 환경에 대 한 올바른 매개 변수 값을 포함 *하도록 파일을 수정 합니다.*
3. 명령 프롬프트 창을 열고. c. c. c. c *파일의* 위치로 이동 합니다.
4. 다음 명령을 입력 하 고 Enter 키를 누릅니다.

    [!code-console[Main](deploying-web-packages/samples/sample2.cmd)]

이 예제에서:

- **/Y** 플래그는 평가판 실행을 수행 하는 대신 실제로 패키지를 배포 하려는 경우를 나타냅니다.
- **/M** 플래그는 TESTWEB1 라는 서버에 패키지를 배포 하려는 경우를 나타냅니다. 이 값에서 Msdeploy.exe는 http://TESTWEB1/MSDeployAgentService에서 웹 배포 원격 에이전트 서비스에 패키지를 배포 하려고 합니다.
- **/A** 플래그는 NTLM 인증을 사용 하고자 함을 나타냅니다. 따라서 사용자 이름과 암호를 지정할 필요가 없습니다.

*.Deploy* 파일을 사용 하 여 배포 프로세스를 간소화 하는 방법을 보여 주기 위해 위에 표시 된 옵션 *을 사용 하* 여 생성 되 고 실행 될 때 생성 되 고 실행 되는 msdeploy.exe 명령을 살펴보세요.

[!code-console[Main](deploying-web-packages/samples/sample3.cmd)]

*. .Deploy* 파일을 사용 하 여 웹 패키지를 배포 하는 방법에 대 한 자세한 내용은 [방법: 배포 파일을 사용 하 여 배포 패키지 설치](https://msdn.microsoft.com/library/ff356104.aspx)를 참조 하세요.

## <a name="using-msdeployexe"></a>Msdeploy.exe 사용

일반적으로 *.deploy* 파일을 사용 하 여 배포 프로세스를 간소화 하지만 msdeploy.exe를 직접 사용 하는 것이 좋습니다. 다음은 그 예입니다.

- 관리자가 아닌 사용자로 웹 배포 처리기에 배포 하려는 경우에는 *.deploy .cmd* 파일을 사용할 수 없습니다. 이 문제는 **끝점 고려 사항**에 설명 된 대로 웹 배포 2.0의 버그로 인해 발생 합니다.
- 다른 위치에 있는 다른 *Setparameters .xml* 파일 간에 수동으로 전환 하려면 msdeploy.exe를 직접 사용 하는 것이 좋습니다.
- 여러 Msdeploy.exe 명령줄 인수를 재정의 하려는 경우 Msdeploy.exe를 직접 사용 하는 것이 좋습니다.

Msdeploy.exe를 사용 하는 경우 세 가지 주요 정보를 제공 해야 합니다.

- 데이터의 출처를 나타내는 **-source** 매개 변수입니다.
- 데이터의 이동 위치를 나타내는 **-dest** 매개 변수입니다.
- A **–** 수행 하려는 [작업](https://technet.microsoft.com/library/dd568989(WS.10).aspx) 을 나타내는 verb 매개 변수입니다.

Msdeploy.exe는 [웹 배포 공급자](https://technet.microsoft.com/library/dd569040(WS.10).aspx) 를 사용 하 여 소스 및 대상 데이터를 처리 합니다. 웹 배포에는 사용할&#x2014;수 있는 응용 프로그램 및 데이터 원본에 대 한 공급자가 포함 되어 있습니다. 예를 들어 SQL Server 데이터베이스, IIS 웹 서버, 인증서, GAC (전역 어셈블리 캐시) 어셈블리, 다양 한 구성 파일 및 기타 많은 형식의 데이터에 대 한 공급자가 있습니다. – **Source** 매개 변수와 **– dest** 매개 변수 모두 **– source**: [*providerName*] = [*location*] 형식의 공급자를 지정 해야 합니다. 웹 패키지를 IIS 웹 사이트에 배포 하는 경우 다음 값을 사용 해야 합니다.

- **– 소스** 공급자는 항상 [패키지](https://technet.microsoft.com/library/dd569019(WS.10).aspx)입니다. 다음은 그 예입니다.

    [!code-console[Main](deploying-web-packages/samples/sample4.cmd)]
- **– Dest** 공급자는 항상 [자동](https://technet.microsoft.com/library/dd569016(WS.10).aspx)입니다. 예를 들어:

    [!code-console[Main](deploying-web-packages/samples/sample5.cmd)]
- **– 동사** 는 항상 **동기화**됩니다.

    [!code-console[Main](deploying-web-packages/samples/sample6.cmd)]

또한 다양 한 [공급자별 설정](https://technet.microsoft.com/library/dd569001(WS.10).aspx) 및 일반 [작업 설정을](https://technet.microsoft.com/library/dd569089(WS.10).aspx)지정 해야 합니다. 예를 들어, 스테이징 환경에 연락처 관리자. Mvc 웹 응용 프로그램을 배포 하려고 한다고 가정 합니다. 배포는 웹 배포 처리기를 대상으로 하며 기본 인증을 사용 해야 합니다. 웹 응용 프로그램을 배포 하려면 다음 단계를 완료 해야 합니다.

**Msdeploy.exe를 사용 하 여 웹 응용 프로그램을 배포 하려면**

1. [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)에 설명 된 대로 웹 응용 프로그램 프로젝트를 빌드하고 패키지 합니다.
2. [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)에 설명 된 대로 스테이징 환경에 대 한 올바른 매개 변수 값을 포함 *하도록 파일을 수정 합니다.*
3. 명령 프롬프트 창을 열고 Msdeploy.exe의 위치로 이동 합니다. 일반적 으로%PROGRAMFILES%\IIS\Microsoft 웹 배포 V2\msdeploy.exe.에 있습니다.
4. 다음 명령을 입력 하 고 Enter 키를 누릅니다 (줄 바꿈 무시).

    [!code-console[Main](deploying-web-packages/samples/sample7.cmd)]

이 예제에서:

- **– Source** 매개 변수는 **패키지** 공급자를 지정 하 고 웹 패키지의 위치를 나타냅니다.
- **– Dest** 매개 변수는 **자동** 공급자를 지정 합니다. **ComputerName** 설정은 대상 서버에서 웹 배포 처리기의 서비스 URL을 제공 합니다. **Authtype** 설정은 기본 인증을 사용 하 고 **사용자 이름과** **암호**를 제공 해야 함을 나타냅니다. 마지막으로 **includeacls = "False"** 설정은 원본 웹 응용 프로그램의 파일에 대 한 acl (액세스 제어 목록)을 대상 서버로 복사 하지 않음을 나타냅니다.
- **– Verb: sync** 인수는 대상 서버에서 원본 콘텐츠를 복제 하려고 함을 나타냅니다.
- **– DisableLink** 인수는 대상 서버에서 응용 프로그램 풀, 가상 디렉터리 구성 또는 SSL(SECURE SOCKETS LAYER) (SSL) 인증서를 복제 하지 않음을 의미 합니다. 자세한 내용은 [웹 배포 링크 확장명](https://technet.microsoft.com/library/dd569028(WS.10).aspx)을 참조 하세요.
- **– Setparamfile** 매개 변수는 *setparameters .xml* 파일의 위치를 제공 합니다.
- **– Allowuntrusted** 스위치는 웹 배포 신뢰할 수 있는 인증 기관에서 발급 하지 않은 SSL 인증서를 허용 해야 함을 나타냅니다. 웹 배포 처리기에 배포 하는 경우 자체 서명 된 인증서를 사용 하 여 서비스 URL을 보호 한 경우에는이 스위치를 포함 해야 합니다.

## <a name="automating-web-package-deployment"></a>웹 패키지 배포 자동화

많은 엔터프라이즈 시나리오에서 대규모의 단일 단계 또는 자동 배포의 일부로 웹 패키지를 배포 하는 것이 좋습니다. *.Deploy* 파일을 실행 하거나 msdeploy.exe를 직접 사용 하 여 웹 패키지를 배포 하도록 선택 했는지에 관계 없이 명령을 매개 변수화 하 고 MSBuild (Microsoft Build Engine) 프로젝트 파일의 대상에서 호출할 수 있습니다.

Contact Manager 샘플 솔루션에서 *Publish. proj* 파일의 **웹 패키지** 대상을 살펴보세요. 이 **대상은 이름이 있는**항목 목록으로 식별 되는 *배포 .cmd* 파일에 대해 한 번씩 실행 됩니다. 대상은 속성 및 항목 메타 데이터를 사용 하 여 각 *. .cmd* 파일의 전체 인수 값 집합을 작성 한 다음 **Exec** 작업을 사용 하 여 명령을 실행 합니다.

[!code-xml[Main](deploying-web-packages/samples/sample8.xml)]

> [!NOTE]
> 샘플 솔루션의 프로젝트 파일 모델에 대 한 광범위 한 개요와 일반적으로 사용자 지정 프로젝트 파일에 대 한 소개는 [프로젝트 파일 이해](understanding-the-project-file.md) 및 [빌드 프로세스 이해](understanding-the-build-process.md)를 참조 하세요.

## <a name="endpoint-considerations"></a>끝점 고려 사항

*.Deploy* 파일을 실행 하거나 msdeploy.exe를 직접 사용 하 여 웹 패키지를 배포 하는지에 관계 없이 배포에 대 한 컴퓨터 이름이 나 서비스 끝점을 지정 해야 합니다.

웹 배포 원격 에이전트 서비스를 사용 하 여 배포 하도록 대상 웹 서버를 구성 하는 경우 대상 서비스 URL을 대상으로 지정 합니다.

[!code-console[Main](deploying-web-packages/samples/sample9.cmd)]

또는 서버 이름만 대상으로 지정할 수 있으며, 웹 배포 원격 에이전트 서비스 URL을 유추 합니다.

[!code-console[Main](deploying-web-packages/samples/sample10.cmd)]

웹 배포 처리기를 사용 하 여 배포 하도록 대상 웹 서버를 구성 하는 경우 IIS 웹 관리 서비스 (WMSvc)의 끝점 주소를 대상으로 지정 해야 합니다. 기본적으로 다음과 같은 형식이 사용 됩니다.

[!code-console[Main](deploying-web-packages/samples/sample11.cmd)]

*.Deploy* 파일 또는 msdeploy.exe를 직접 사용 하 여 이러한 끝점을 대상으로 지정할 수 있습니다. 그러나 [웹 배포 게시용 웹 서버 구성 (웹 배포 처리기)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)에 설명 된 대로 웹 배포 처리기에 관리자가 아닌 사용자로 배포 하려는 경우 서비스 끝점 주소에 쿼리 문자열을 추가 해야 합니다.

[!code-console[Main](deploying-web-packages/samples/sample12.cmd)]

관리자가 아닌 사용자에 게 IIS에 대 한 서버 수준 액세스 권한이 없기 때문입니다. 특정 IIS 웹 사이트에만 액세스할 수 있습니다. 작성 당시에는 웹 게시 파이프라인 (WPP)의 버그로 인해 쿼리 문자열이 포함 된 끝점 주소를 사용 하 여 *.deploy* 파일을 실행할 수 없습니다. 이 시나리오에서는 Msdeploy.exe를 직접 사용 하 여 웹 패키지를 배포 해야 합니다.

> [!NOTE]
> 웹 배포 원격 에이전트 서비스 및 웹 배포 처리기에 대 한 자세한 내용은 [웹 배포에 대 한 올바른 방법 선택](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)을 참조 하세요. 이러한 끝점에 배포할 환경 관련 프로젝트 파일을 구성 하는 방법에 대 한 지침은 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)을 참조 하세요.

## <a name="authentication-considerations"></a>인증 고려 사항

*.Deploy* 파일을 실행 하거나 msdeploy.exe를 직접 사용 하 여 웹 패키지를 배포 하는지에 관계 없이 인증 유형을 지정 해야 합니다. 웹 배포는 **NTLM** 또는 **기본**의 두 가지 가능한 값을 허용 합니다. 기본 인증을 지정 하는 경우 사용자 이름 및 암호도 제공 해야 합니다. 인증 유형을 선택 하는 경우 주의 해야 하는 다양 한 요인이 있습니다.

- 웹 배포 원격 에이전트 서비스에 배포 하는 경우 NTLM 인증을 사용 해야 합니다. 원격 에이전트 서비스는 기본 인증 자격 증명을 허용 하지 않습니다.
- 웹 배포 처리기에 배포 하는 경우 NTLM 또는 기본 인증을 사용할 수 있습니다. 기본 설정은 기본 인증입니다. 기본 인증에는 일반 텍스트로 전송 되는 사용자 이름과 암호를 사용 하지만 웹 배포 처리기에서 항상 SSL 암호화를 사용 하므로 자격 증명이 보호 됩니다.
- 웹 패키지에 데이터베이스가 포함 되어 있고 웹 서버와 데이터베이스 서버가 서로 다른 컴퓨터에 있는 경우 [ntlm "이중 홉" 제한](https://go.microsoft.com/?linkid=9805120)으로 인해 ntlm 인증을 사용 하 여 데이터베이스를 배포할 수 없습니다. 배포 연결 문자열에 SQL Server 자격 증명을 사용 하거나 웹 배포 하려면 기본 인증 자격 증명을 제공 해야 합니다. 이 문제는 [엔터프라이즈 환경에 멤버 자격 데이터베이스 배포](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)에 자세히 설명 되어 있습니다.

## <a name="conclusion"></a>결론

이 항목에서는 *.* n e c 파일을 실행 하거나 msdeploy.exe를 직접 사용 하 여 웹 패키지를 배포 하는 방법에 대해 설명 했습니다. 각 방법이 적합할 수 있는 경우에 대해 설명 하 고, 대규모 단일 단계 또는 자동화 된 빌드 프로세스의 일부로 배포 명령을 매개 변수화 하 고 실행 하는 방법을 설명 했습니다.

## <a name="further-reading"></a>추가 참고 자료

웹 배포 패키지를 만들고 매개 변수화 하는 방법에 대 한 지침은 웹 [응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md) 및 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)을 참조 하세요. TFS (Team Foundation Server) 인스턴스에서 웹 패키지를 빌드 및 배포 하는 방법에 대 한 지침은 [자동화 된 웹 배포에 대 한 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)을 참조 하세요. 배포 프로세스를 사용자 지정 하 고 문제를 해결 하는 방법에 대 한 자세한 내용은 [배포에서 파일 및 폴더 제외](../advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment.md)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](configuring-parameters-for-web-package-deployment.md)
> [다음](deploying-database-projects.md)
