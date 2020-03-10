---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
title: 여러 환경에 대 한 데이터베이스 배포 사용자 지정 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 배포 프로세스의 일부로 데이터베이스의 속성을 특정 대상 환경에 맞게 조정 하는 방법에 대해 설명 합니다. 참고:이 항목은 ...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a172979a-1318-4318-a9c6-4f9560d26267
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
msc.type: authoredcontent
ms.openlocfilehash: 8ae8cb1a322afb95c5d2e8d5e73c7825c7b2fe5a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78489035"
---
# <a name="customizing-database-deployments-for-multiple-environments"></a>다중 환경을 위한 데이터베이스 배포 사용자 지정

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 배포 프로세스의 일부로 데이터베이스의 속성을 특정 대상 환경에 맞게 조정 하는 방법에 대해 설명 합니다.
> 
> > [!NOTE]
> > 이 항목에서는 Msbuild.exe 및 nuget.exe를 사용 하 여 Visual Studio 2010 데이터베이스 프로젝트를 배포 한다고 가정 합니다. 이 방법을 선택할 수 있는 이유에 대 한 자세한 내용은 [엔터프라이즈의 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md) 및 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)를 참조 하세요.
> 
> 
> 데이터베이스 프로젝트를 여러 대상에 배포 하는 경우 각 대상 환경에 대 한 데이터베이스 배포 속성을 사용자 지정 하는 것이 좋습니다. 예를 들어 테스트 환경에서는 일반적으로 모든 배포에서 데이터베이스를 다시 만드는 반면 스테이징 또는 프로덕션 환경에서는 데이터를 보존 하기 위해 증분 업데이트를 수행 하는 것이 훨씬 더 많을 것입니다.
> 
> Visual Studio 2010 데이터베이스 프로젝트에서 배포 설정은 배포 구성 파일 (. sqldeployment)에 포함 됩니다. 이 항목에서는 환경 특정 배포 구성 파일을 만들고 VSDBCMD 매개 변수로 사용할 파일을 지정 하는 방법을 보여 줍니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="task-overview"></a>작업 개요

이 항목에서는 다음과 같이 가정합니다.

- [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 대로 프로젝트 파일 분할 방식을 솔루션 배포에 사용 합니다.
- [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)의 설명에 따라 프로젝트 파일에서 VSDBCMD를 호출 하 여 데이터베이스 프로젝트를 배포 합니다.

대상 환경 간의 다양 한 데이터베이스 배포 속성을 지 원하는 배포 시스템을 만들려면 다음을 수행 해야 합니다.

- 각 대상 환경에 대 한 배포 구성 (. sqldeployment) 파일을 만듭니다.
- 명령줄 스위치로 배포 구성 파일을 지정 하는 VSDBCMD 명령을 만듭니다.
- VSDBCMD 옵션이 대상 환경에 적합 하도록 Microsoft Build Engine (MSBuild) 프로젝트 파일에서 VSDBCMD 명령을 매개 변수화 합니다.

이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여 줍니다.

## <a name="creating-environment-specific-deployment-configuration-files"></a>환경 특정 배포 구성 파일 만들기

기본적으로 데이터베이스 프로젝트에는 *sqldeployment*라는 단일 배포 구성 파일이 포함 되어 있습니다. Visual Studio 2010에서이 파일을 열면 사용할 수 있는 다양 한 배포 옵션을 확인할 수 있습니다.

- **배포 비교 데이터 정렬**입니다. 이를 통해 프로젝트의 데이터베이스 데이터 정렬 ( *원본* 데이터 정렬) 또는 대상 서버의 데이터베이스 데이터 정렬 ( *대상* 데이터 정렬) 중 어떤 것을 사용할지 선택할 수 있습니다. 대부분의 경우 개발 또는 테스트 환경에 배포 하는 경우 원본 데이터 정렬을 사용 하는 것이 좋습니다. 스테이징 또는 프로덕션 환경에 배포 하는 경우에는 일반적으로 상호 운용성 문제를 방지 하기 위해 대상 데이터 정렬을 변경 하지 않는 것이 좋습니다.
- **데이터베이스 속성을 배포**합니다. 이를 통해 데이터베이스 속성을 적용할지 여부를 선택할 수 있습니다. *sqlsettings* 파일에 정의 되어 있습니다. 처음으로 데이터베이스를 배포 하는 경우 데이터베이스 속성을 배포 해야 합니다. 기존 데이터베이스를 업데이트 하는 경우 속성이 이미 준비 되어 있어야 하 고, 다시 배포할 필요가 없습니다.
- **항상 데이터베이스를 다시 만듭니다**. 이렇게 하면 스키마를 사용 하 여 대상 데이터베이스를 최신 상태로 만들기 위해 배포 하거나 증분 변경 작업을 수행할 때마다 대상 데이터베이스를 다시 만들지 여부를 선택할 수 있습니다. 데이터베이스를 다시 만들면 기존 데이터베이스의 모든 데이터가 손실 됩니다. 따라서 스테이징 또는 프로덕션 환경에 대 한 배포의 경우 일반적으로 **false** 로 설정 해야 합니다.
- **데이터 손실이 발생할 수 있는 경우 증분 배포를 차단**합니다. 이를 통해 데이터베이스 스키마를 변경 하면 데이터가 손실 될 경우 배포를 중지할지 여부를 선택할 수 있습니다. 일반적으로 프로덕션 환경에 배포 하는 경우이를 **true** 로 설정 하 여 중요 한 데이터를 개입 하 고 보호할 수 있는 기회를 제공 합니다. **항상 데이터베이스 다시 만들기** 를 **false**로 설정한 경우에는이 설정이 적용 되지 않습니다.
- **단일 사용자 모드로 배포를 실행**합니다. 이는 일반적으로 개발 또는 테스트 환경에서 문제가 되지 않습니다. 그러나 스테이징 또는 프로덕션 환경에 대 한 배포의 경우 일반적으로이를 **true** 로 설정 해야 합니다. 이렇게 하면 배포가 진행 되는 동안 사용자가 데이터베이스를 변경할 수 없습니다.
- **배포 전에 데이터베이스를 백업**합니다. 일반적으로 데이터 손실을 예방 하기 위해 프로덕션 환경에 배포할 때이를 **true** 로 설정 합니다. 스테이징 데이터베이스에 많은 데이터가 포함 된 경우 스테이징 환경에 배포 하는 경우이를 **true** 로 설정 해야 할 수도 있습니다.
- **대상 데이터베이스에 있지만 데이터베이스 프로젝트에 없는 개체에 대 한 DROP 문을 생성**합니다. 대부분의 경우 데이터베이스에 대 한 증분 변경을 수행 하는 데 필수적인 부분입니다. **항상 데이터베이스 다시 만들기** 를 **false**로 설정한 경우에는이 설정이 적용 되지 않습니다.
- **ALTER ASSEMBLY 문을 사용 하 여 CLR 유형을 업데이트 하지 마십시오**. 이 설정은 SQL Server CLR (공용 언어 런타임) 형식을 최신 어셈블리 버전으로 업데이트 하는 방법을 결정 합니다. 대부분의 시나리오에서이는 **false** 로 설정 해야 합니다.

다음 표에서는 다양 한 대상 환경에 대 한 일반적인 배포 설정을 보여 줍니다. 그러나 정확한 요구 사항에 따라 설정이 달라질 수 있습니다.

|  | 개발자/테스트 | 스테이징/통합 | 프로덕션 |
| --- | --- | --- | --- |
| **배포 비교 데이터 정렬** | 원본 | 대상 | 대상 |
| **데이터베이스 속성 배포** | True | 첫 번째 시간만 | 첫 번째 시간만 |
| **항상 데이터베이스 다시 만들기** | True | False | False |
| **데이터 손실이 발생할 수 있는 경우 증분 배포 차단** | False | 가능할 수도 있음 | True |
| **단일 사용자 모드에서 배포 스크립트 실행** | False | True | True |
| **배포 전 데이터베이스 백업** | False | 가능할 수도 있음 | True |
| **대상 데이터베이스에 있지만 데이터베이스 프로젝트에 없는 개체에 대 한 DROP 문을 생성 합니다.** | False | True | True |
| **ALTER ASSEMBLY 문을 사용 하 여 CLR 형식 업데이트 안 함** | False | False | False |

> [!NOTE]
> 데이터베이스 배포 속성 및 환경 고려 사항에 대 한 자세한 내용은 [데이터베이스 프로젝트 설정 개요](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx), [방법: 배포 정보에 대 한 속성 구성](https://msdn.microsoft.com/library/dd172125.aspx), [격리 된 개발 환경에 데이터베이스 빌드 및 배포](https://msdn.microsoft.com/library/dd193409.aspx), [스테이징 또는 프로덕션 환경에 데이터베이스 빌드 및 배포](https://msdn.microsoft.com/library/dd193413.aspx)를 참조 하세요.

여러 대상에 대 한 데이터베이스 프로젝트 배포를 지원 하려면 각 대상 환경에 대 한 배포 구성 파일을 만들어야 합니다.

**환경 관련 구성 파일을 만들려면**

1. Visual Studio 2010의 **솔루션 탐색기** 창에서 데이터베이스 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.
2. 데이터베이스 프로젝트 속성 페이지의 **배포 탭에** 있는 **배포 구성 파일** 행에서 **새로 만들기**를 클릭 합니다.

    ![](customizing-database-deployments-for-multiple-environments/_static/image1.png)
3. **새 배포 구성 파일** 대화 상자에서 파일에 의미 있는 이름 (예: **testenvironment**)을 지정한 다음 **저장**을 클릭 합니다.
4. *[Filename] * * *. sqldeployment** 페이지에서 대상 환경의 요구 사항과 일치 하도록 배포 속성을 설정한 후 파일을 저장 합니다.

    ![](customizing-database-deployments-for-multiple-environments/_static/image2.png)
5. 새 파일이 데이터베이스 프로젝트의 속성 폴더에 추가 됩니다.

    ![](customizing-database-deployments-for-multiple-environments/_static/image3.png)

## <a name="specifying-the-deployment-configuration-file-in-vsdbcmd"></a>VSDBCMD에서 배포 구성 파일 지정

Visual Studio 2010 내에서 솔루션 구성 (예: 디버그 및 릴리스)을 사용 하는 경우 배포 구성 파일을 각 구성과 연결할 수 있습니다. 특정 구성을 빌드할 때 빌드 프로세스는 구성 별 배포 구성 파일을 가리키는 구성 특정 배포 매니페스트 파일을 생성 합니다. 그러나 이러한 자습서에서 설명 하는 배포 방법의 주요 목표 중 하나는 Visual Studio 2010 및 솔루션 구성을 사용 하지 않고 배포 프로세스를 제어 하는 기능을 사용자에 게 제공 하는 것입니다. 이 방법에서는 대상 배포 환경에 관계 없이 솔루션 구성이 동일 합니다. 데이터베이스 배포를 특정 대상 환경에 맞게 조정 하려면 VSDBCMD 명령줄 옵션을 사용 하 여 배포 구성 파일을 지정할 수 있습니다.

VSDBCMD에서 배포 구성 파일을 지정 하려면 **p:/DeploymentConfigurationFile** 스위치를 사용 하 고 파일의 전체 경로를 제공 합니다. 이렇게 하면 배포 매니페스트에서 식별 하는 배포 구성 파일이 재정의 됩니다. 예를 들어이 VSDBCMD 명령을 사용 하 여 테스트 환경에 배포 **하는 데** 사용할 수 있습니다.

[!code-console[Main](customizing-database-deployments-for-multiple-environments/samples/sample1.cmd)]

> [!NOTE]
> 빌드 프로세스는 파일을 출력 디렉터리에 복사할 때 sqldeployment 파일의 이름을 바꿀 수 있습니다.

배포 전 또는 배포 후 SQL 스크립트에서 SQL 명령 변수를 사용 하는 경우 유사한 방법을 사용 하 여 배포에 sqlcmdvars 파일을 연결할 수 있습니다. 이 경우에는 **p:/SqlCommandVariablesFile** 스위치를 사용 하 여 sqlcmdvars 파일을 식별 합니다.

## <a name="running-the-vsdbcmd-command-from-an-msbuild-project-file"></a>MSBuild 프로젝트 파일에서 VSDBCMD 명령 실행

Msbuild 대상 내에서 **Exec** 작업을 사용 하 여 msbuild 프로젝트 파일에서 VSDBCMD 명령을 호출할 수 있습니다. 가장 간단한 형태는 다음과 같습니다.

[!code-xml[Main](customizing-database-deployments-for-multiple-environments/samples/sample2.xml)]

- 실제로 프로젝트 파일을 쉽게 읽고 다시 사용할 수 있도록 하려면 다양 한 명령줄 매개 변수를 저장 하는 속성을 만들어야 합니다. 이렇게 하면 사용자가 환경 관련 프로젝트 파일에서 속성 값을 보다 쉽게 제공 하거나 MSBuild 명령줄에서 기본값을 재정의할 수 있습니다. [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 분할 프로젝트 파일 방법을 사용 하는 경우 두 파일 간에 빌드 지침과 속성을 적절 하 게 나누어야 합니다.
- 배포 구성 파일 이름, 데이터베이스 연결 문자열 및 대상 데이터베이스 이름과 같은 환경 관련 설정은 환경 관련 프로젝트 파일에 있어야 합니다.
- Vsdbcmd 명령을 실행 하는 MSBuild 대상과 VSDBCMD 실행 파일의 위치와 같은 범용 속성은 모두 유니버설 프로젝트 파일에 있어야 합니다.

또한 VSDBCMD를 호출 하기 전에 데이터베이스 프로젝트를 빌드하여 deploymanifest 파일을 만들고 사용할 수 있도록 준비 해야 합니다. [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)항목에서이 방법의 전체 예제를 볼 수 있으며,이는 [Contact Manager 샘플 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)의 프로젝트 파일을 안내 합니다.

## <a name="conclusion"></a>결론

이 항목에서는 MSBuild 및 VSDBCMD를 사용 하 여 데이터베이스 프로젝트를 배포할 때 데이터베이스 속성을 다른 대상 환경에 맞게 조정 하는 방법에 대해 설명 했습니다. 이 방법은 대규모의 엔터프라이즈급 솔루션의 일부로 데이터베이스 프로젝트를 배포 해야 하는 경우에 유용 합니다. 이러한 솔루션은 샌드박스가 적용 된 개발 또는 테스트 환경, 스테이징 또는 통합 플랫폼, 프로덕션 또는 라이브 환경과 같은 여러 대상에 배포 되는 경우가 많습니다. 이러한 각 대상 환경에는 일반적으로 고유한 데이터베이스 배포 속성 집합이 필요 합니다.

## <a name="further-reading"></a>추가 참고 자료

VSDBCMD를 사용 하 여 데이터베이스 프로젝트를 배포 하는 방법에 대 한 자세한 내용은 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)를 참조 하세요. 사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 방법에 대 한 자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)를 참조 하세요.

MSDN의 이러한 문서에서는 데이터베이스 배포에 대 한 일반적인 지침을 제공 합니다.

- [데이터베이스 프로젝트 설정 개요](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)
- [방법: 배포 정보에 대 한 속성 구성](https://msdn.microsoft.com/library/dd172125.aspx)
- [격리 된 개발 환경에 데이터베이스 빌드 및 배포](https://msdn.microsoft.com/library/dd193409.aspx)
- [스테이징 또는 프로덕션 환경에 데이터베이스 빌드 및 배포](https://msdn.microsoft.com/library/dd193413.aspx)

> [!div class="step-by-step"]
> [이전](performing-a-what-if-deployment.md)
> [다음](deploying-database-role-memberships-to-test-environments.md)
