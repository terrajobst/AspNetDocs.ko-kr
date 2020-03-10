---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: What If 배포 수행 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 및 V ...를 사용 하 여 ' what if ' (또는 시뮬레이션 된) 배포를 수행 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510335"
---
# <a name="performing-a-what-if-deployment"></a>“가상 시나리오” 배포 수행

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 및 VSDBCMD를 사용 하 여 "가상으로" (또는 시뮬레이션 된) 배포를 수행 하는 방법을 설명 합니다. 이렇게 하면 응용 프로그램을 실제로 배포 하기 전에 특정 대상 환경에서 배포 논리의 영향을 확인할 수 있습니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다. 프로젝트 파일에 대 한 빌드 및 배포 프로세스는 모든&#x2014;대상 환경에 적용 되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 합니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="performing-a-what-if-deployment-for-web-packages"></a>웹 패키지에 대 한 "What If" 배포 수행

웹 배포에는 "what if" (또는 평가판) 모드에서 배포를 수행할 수 있는 기능이 포함 되어 있습니다. "What if" 모드로 아티팩트를 배포 하는 경우 웹 배포는 배포를 수행 하는 것 처럼 로그 파일을 생성 하지만 실제로 대상 서버에서 아무것도 변경 하지는 않습니다. 로그 파일을 검토 하면 특히 대상 서버에 대 한 배포의 영향을 이해 하는 데 도움이 됩니다.

- 추가 될 것입니다.
- 업데이트 됩니다.
- 삭제 될 항목입니다.

"What if" 배포는 실제로 대상 서버에서 어떤 것도 변경 하지 않기 때문에 항상 배포 성공 여부를 예측 하는 것은 아닙니다.

[웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)에 설명 된 대로, msdeploy.exe 명령줄 유틸리티를 직접 사용 하거나 빌드 프로세스&#x2014;에서 생성 하는 *.deploy .cmd* 파일을 실행 하 여 두 가지 방법으로 웹 배포를 사용 하 여 웹 패키지를 배포할 수 있습니다.

Msdeploy.exe를 직접 사용 하는 경우 명령에 **– whatif** 플래그를 추가 하 여 "what if" 배포를 실행할 수 있습니다. 예를 들어 스테이징 환경에 배포 하는 경우에 발생 하는 결과를 평가 하기 위해 다음과 유사 하 게 Msdeploy.exe 명령이 있습니다.

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

"What if" 배포 결과가 만족 스 러 우면 **– whatif** 플래그를 제거 하 여 라이브 배포를 실행할 수 있습니다.

> [!NOTE]
> Msdeploy.exe의 명령줄 옵션에 대 한 자세한 내용은 [웹 배포 작업 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)을 참조 하세요.

*. Deploy .cmd* 파일을 사용 하는 경우 명령에 **/y** 플래그 ("yes" 또는 업데이트 모드) 대신 **/t** 플래그 (평가판 모드) 플래그를 포함 하 여 "what if" 배포를 실행할 수 있습니다. 예를 들어 .deploy 파일을 실행 하 여 *.* c a p. c a c .zip .zip 패키지를 배포한 경우 발생 하는 동작을 평가 하려면 명령이 다음과 유사 해야 합니다.

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

"평가 모드" 배포 결과에 만족 하는 경우 **/t** 플래그를 **/y** 플래그로 바꿔 라이브 배포를 실행할 수 있습니다.

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> *. .Cmd* 파일을 사용 하는 명령줄 옵션에 대 한 자세한 내용은 [방법: 배포 파일을 사용 하 여 배포 패키지 설치](https://msdn.microsoft.com/library/ff356104.aspx)를 참조 하세요. 플래그를 지정 하지 않고 *.deploy* 파일을 실행 하는 경우 명령 프롬프트에 사용 가능한 플래그의 목록이 표시 됩니다.

## <a name="performing-a-what-if-deployment-for-databases"></a>데이터베이스에 대 한 "What If" 배포 수행

이 섹션에서는 VSDBCMD 유틸리티를 사용 하 여 증분 스키마 기반 데이터베이스 배포를 수행 하는 것으로 가정 합니다. 이 방법은 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)에 자세히 설명 되어 있습니다. 여기에 설명 된 개념을 적용 하기 전에이 항목을 숙지 하는 것이 좋습니다.

**배포** 모드에서 vsdbcmd를 사용 하는 경우 **/Dd** (또는 **/deploytodatabase**) 플래그를 사용 하 여 vsdbcmd에서 실제로 데이터베이스를 배포할지 아니면 배포 스크립트만 생성할지를 제어할 수 있습니다. .Dbschema 파일을 배포 하는 경우 다음과 같은 동작이 발생 합니다.

- **/Dd +** 또는 **/dd**을 지정 하는 경우 VSDBCMD는 배포 스크립트를 생성 하 고 데이터베이스를 배포 합니다.
- **/Dd-** 를 지정 하거나 스위치를 생략 하면 VSDBCMD는 배포 스크립트만 생성 합니다.

> [!NOTE]
> .Dbschema 파일이 아닌 deploymanifest 파일을 배포 하는 경우 **/dd** 스위치의 동작은 훨씬 더 복잡 합니다. 기본적으로 deploymanifest 파일에는 값이 **True**인 **deploytodatabase** 요소가 포함 된 경우 **/dd** 스위치의 값을 무시 합니다. [데이터베이스 프로젝트를 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md) 하면이 동작이 전체적으로 설명 됩니다.

예를 들어 데이터베이스를 실제로 배포 하지 않고 동료 **관리자** 데이터베이스에 대 한 배포 스크립트를 생성 하려면 VSDBCMD 명령이 다음과 유사 해야 합니다.

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

VSDBCMD는 차등 데이터베이스 배포 도구 이며, 현재 데이터베이스를 업데이트 하는 데 필요한 모든 SQL 명령 (있는 경우)을 지정 된 스키마에 포함 하기 위해 배포 스크립트가 동적으로 생성 됩니다. 배포 스크립트를 검토 하면 현재 데이터베이스와 해당 데이터베이스에 포함 된 데이터에 대 한 배포의 영향을 확인 하는 데 도움이 됩니다. 예를 들어 다음을 확인할 수 있습니다.

- 기존 테이블을 제거할지 여부와이로 인해 데이터가 손실 될 수 있는지 여부입니다.
- 예를 들어 테이블을 분할 하거나 병합 하는 등의 작업 순서에서 데이터 손실 위험을 초래할 수 있는지 여부를 나타냅니다.

배포 스크립트에 만족 하는 경우 **/dd +** 플래그로 VSDBCMD를 반복 하 여 변경 작업을 수행할 수 있습니다. 또는 요구 사항에 맞게 배포 스크립트를 편집한 다음 데이터베이스 서버에서 수동으로 실행할 수 있습니다.

## <a name="integrating-what-if-functionality-into-custom-project-files"></a>"What If" 기능을 사용자 지정 프로젝트 파일에 통합

더 복잡 한 배포 시나리오에서는 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 대로 사용자 지정 MSBuild (Microsoft Build Engine) 프로젝트 파일을 사용 하 여 빌드 및 배포 논리를 캡슐화 할 수 있습니다. 예를 들어 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션에서 proj 파일을 *게시* 합니다.

- 솔루션을 빌드합니다.
- 에서는 웹 배포를 사용 하 여 배포 된 응용 프로그램을 패키지 하 고 배포 합니다.
- 에서는 웹 배포를 사용 하 여 서비스 응용 프로그램을 패키지 하 고 배포 합니다.
- 는 **연락처 관리자** 데이터베이스를 배포 합니다.

이러한 방식으로 여러 웹 패키지 및/또는 데이터베이스의 배포를 단일 단계 프로세스에 통합 하는 경우 "what if" 모드로 전체 배포를 수행 하는 옵션을 사용할 수도 있습니다.

*Publish. proj* 파일은이 작업을 수행 하는 방법을 보여 줍니다. 먼저 "what if" 값을 저장할 속성을 만들어야 합니다.

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

이 경우 기본값 **false**로 **WhatIf** 라는 속성을 만들었습니다. 사용자는 명령줄 매개 변수에서 속성을 **true** 로 설정 하 여이 값을 재정의할 수 있습니다. 잠시 후에 표시 됩니다.

다음 단계는 플래그에 **WhatIf** 속성 값이 반영 되도록 모든 웹 배포 및 VSDBCMD 명령을 매개 변수화 하는 것입니다. 예를 들어, 다음 대상 ( *Publish. proj* 파일 및 간소화)은 *. .deploy* 파일을 실행 하 여 웹 패키지를 배포 합니다. 기본적으로이 명령은 **/y** 스위치 ("예" 또는 업데이트 모드)를 포함 합니다. **WhatIf** 를 **true**로 설정 하면 **/t** 스위치 (평가판 또는 "what if" 모드)로 대체 됩니다.

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

마찬가지로 다음 대상은 VSDBCMD 유틸리티를 사용 하 여 데이터베이스를 배포 합니다. 기본적으로 **/dd** 스위치는 포함 되지 않습니다. 즉, VSDBCMD는 배포 스크립트를 생성 하지만 데이터베이스&#x2014;를 배포 하지 않습니다. 즉, "what if" 시나리오를 사용 합니다. **WhatIf** 속성이 **true**로 설정 되어 있지 않으면 **/DD** 스위치가 추가 되 고 VSDBCMD가 데이터베이스를 배포 합니다.

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

동일한 방법을 사용 하 여 프로젝트 파일의 모든 관련 명령을 매개 변수화 할 수 있습니다. "What if" 배포를 실행 하려는 경우 명령줄에서 **WhatIf** 속성 값을 제공 하면 됩니다.

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

이러한 방식으로 모든 프로젝트 구성 요소에 대 한 "가상의 경우" 배포를 한 번에 실행할 수 있습니다.

## <a name="conclusion"></a>결론

이 항목에서는 웹 배포, VSDBCMD 및 MSBuild를 사용 하 여 "what if" 배포를 실행 하는 방법에 대해 설명 했습니다. "어떻게 할까요?" 배포를 사용 하면 대상 환경을 변경 하기 전에 제안 된 배포의 영향을 평가할 수 있습니다.

## <a name="further-reading"></a>추가 참고 자료

웹 배포 명령줄 구문에 대 한 자세한 내용은 [웹 배포 작업 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)을 참조 하세요. *. Deploy .cmd* 파일을 사용 하는 경우 명령줄 옵션에 대 한 지침은 [방법: 배포 파일을 사용 하 여 배포 패키지 설치](https://msdn.microsoft.com/library/ff356104.aspx)를 참조 하세요. VSDBCMD 명령줄 구문에 대 한 지침은 [vsdbcmd에 대 한 명령줄 참조를 참조 하세요. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx)

> [!div class="step-by-step"]
> [이전](advanced-enterprise-web-deployment.md)
> [다음](customizing-database-deployments-for-multiple-environments.md)
