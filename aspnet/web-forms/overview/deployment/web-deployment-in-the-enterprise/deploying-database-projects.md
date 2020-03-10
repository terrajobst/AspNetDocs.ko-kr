---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
title: 데이터베이스 프로젝트 배포 | Microsoft Docs
author: jrjlee
description: '참고: 많은 엔터프라이즈 배포 시나리오에서 배포 된 데이터베이스에 증분 업데이트를 게시 하는 기능이 필요 합니다. 다른 방법으로 다시 만들 수 있습니다 ...'
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 832f226a-1aa3-4093-8c29-ce4196793259
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
msc.type: authoredcontent
ms.openlocfilehash: 221808758492aedb8e8329364e511df28fd11105
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514943"
---
# <a name="deploying-database-projects"></a>데이터베이스 프로젝트 배포

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> [!NOTE]
> 많은 엔터프라이즈 배포 시나리오에서 배포 된 데이터베이스에 증분 업데이트를 게시 하는 기능이 필요 합니다. 다른 방법은 모든 배포에서 데이터베이스를 다시 만드는 것입니다. 즉, 기존 데이터베이스의 모든 데이터가 손실 됩니다. Visual Studio 2010을 사용 하는 경우 증분 데이터베이스 게시에 대 한 권장 접근 방법은 VSDBCMD를 사용 하는 것입니다. 그러나 다음 버전의 Visual Studio 및 WPP (웹 게시 파이프라인)에는 증분 게시를 직접 지 원하는 도구가 포함 됩니다.

Visual Studio 2010에서 Contact Manager 샘플 솔루션을 여는 경우 데이터베이스 프로젝트에 4 개의 파일이 포함 된 속성 폴더가 포함 되어 있는 것을 볼 수 있습니다.

![](deploying-database-projects/_static/image1.png)

이러한 파일은 프로젝트 파일 (이 경우에는 프로젝트 파일)과 함께 빌드 및 배포 프로세스의 다양 한 측면을*제어 합니다.*

- *Sqlcmdvars* 파일은 프로젝트를 배포할 때 사용 하는 SQLCMD 변수에 대 한 값을 제공 합니다. 각 솔루션 구성 (예: 디버그 및 릴리스)은 다른 sqlcmdvars 파일을 지정할 수 있습니다.
- *Sqldeployment* 파일은 프로젝트에 정의 된 데이터 정렬 또는 대상 서버의 데이터 정렬 중 어떤 것을 사용할지와 같은 배포 관련 설정을 제공 합니다. 즉, 항상 대상 데이터베이스를 다시 만들지 아니면 기존 데이터베이스를 최신으로 가져오도록 수정할 수 있습니다. 각 솔루션 구성에서는 다른 sqldeployment 파일을 지정할 수 있습니다.
- *Database. sqlpermissions* 파일은 대상 데이터베이스에 추가 하려는 사용 권한을 정의 하는 데 사용할 수 있는 XML 문서입니다. 모든 솔루션 구성은 동일한. sqlpermissions 파일을 공유 합니다.
- 데이터베이스를 만들 때 사용할 데이터 정렬, 비교 연산자의 동작 등 데이터베이스를 만들 때 사용할 데이터베이스 수준 속성을 지정 하는 *sqlsettings* 파일을 지정 합니다. 모든 솔루션 구성은 동일한. sqlsettings 파일을 공유 합니다.

잠시 시간을 내어 Visual Studio에서 파일을 열고 내용을 숙지 합니다.

데이터베이스 프로젝트를 빌드하면 빌드 프로세스에서 다음 두 개의 파일을 만듭니다.

- *데이터베이스 스키마* (.dbschema 파일) XML 형식으로 만들려는 데이터베이스의 스키마에 대해 설명 합니다.
- *배포 매니페스트* (deploymanifest 파일). 여기에는 데이터베이스를 만들고 배포 하는 데 필요한 모든 정보가 포함 됩니다. 배포 지침 (sqldeployment 파일) 및 배포 전 또는 배포 후 SQL 스크립트와 같은 다른 리소스와 함께 .dbschema 파일을 참조 합니다.

다음은 이러한 리소스 간의 관계를 보여 줍니다.

![](deploying-database-projects/_static/image2.png)

여기에서 볼 수 있듯이. sqlsettings 파일 및 sqlsettings 파일은 빌드 프로세스에 대 한 입력입니다. 데이터베이스 프로젝트 파일과 함께 이러한 파일은 데이터베이스 스키마 파일을 만드는 데 사용 됩니다. Sqldeployment 파일과 sqlcmdvars 파일은 빌드 프로세스를 변경 되지 않은 상태로 전달 합니다. 배포 매니페스트는 데이터베이스 스키마, sqldeployment 파일, sqlcmdvars 파일 및 배포 전 또는 배포 후 SQL 스크립트의 위치를 나타냅니다.

## <a name="why-use-vsdbcmd-to-deploy-a-database-project"></a>VSDBCMD를 사용 하 여 데이터베이스 프로젝트를 배포 하는 이유

여러 가지 방법으로 데이터베이스 프로젝트를 배포할 수 있습니다. 그러나이 중 일부는 엔터프라이즈 환경의 원격 서버에 데이터베이스 프로젝트를 배포 하는 데 적합 하지 않습니다. 데이터베이스 프로젝트 배포에서 원하는 내용을 고려 합니다. 엔터프라이즈 배포 시나리오에서 다음과 같은 작업을 할 수 있습니다.

- 원격 위치에서 데이터베이스 프로젝트를 배포할 수 있습니다.
- 기존 데이터베이스에 대해 증분 업데이트를 수행 하는 기능입니다.
- 배포 전 스크립트 또는 배포 후 스크립트를 포함 하는 기능입니다.
- 여러 대상 환경에 배포를 조정할 수 있습니다.
- 데이터베이스 프로젝트를 더 크고 일반적으로 스크립팅된 단일 단계 솔루션 배포의 일부로 배포할 수 있습니다.

데이터베이스 프로젝트를 배포 하는 데 사용할 수 있는 세 가지 주요 방법은 다음과 같습니다.

- Visual Studio 2010의 데이터베이스 프로젝트 형식에서 배포 기능을 사용할 수 있습니다. Visual Studio 2010에서 데이터베이스 프로젝트를 빌드 및 배포 하는 경우 배포 프로세스는 배포 매니페스트를 사용 하 여 빌드 구성과 관련 된 SQL 기반 배포 파일을 생성 합니다. 데이터베이스가 이미 존재 하지 않는 경우 데이터베이스를 만들고 데이터베이스에 필요한 변경 내용을 적용 합니다 (이미 존재 하는 경우). SQLCMD를 사용 하 여 대상 서버에서이 파일을 실행 하거나 Visual Studio를 설정 하 여 파일을 만들고 실행할 수 있습니다. 이 방법의 단점은 배포 설정에 대 한 제어 권한만 제한 한다는 것입니다. 환경 특정 변수 값을 제공 하도록 SQL 배포 파일을 수정 해야 할 수도 있습니다. 이 방법은 Visual Studio 2010가 설치 된 컴퓨터 에서만 사용할 수 있으며, 개발자는 모든 대상 환경에 대 한 연결 문자열 및 자격 증명을 알고 제공 해야 합니다.
- 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 [웹 응용 프로그램 프로젝트의 일부로 데이터베이스를 배포할](https://msdn.microsoft.com/library/dd465343.aspx)수 있습니다. 그러나이 방법은 단순히 대상 서버에 있는 기존 로컬 데이터베이스를 복제 하는 것이 아니라 데이터베이스 프로젝트를 배포 하려는 경우 훨씬 더 복잡 합니다. 데이터베이스 프로젝트가 생성 하는 SQL 배포 스크립트를 실행 하도록 웹 배포를 구성할 수 있지만이를 위해 웹 응용 프로그램 프로젝트에 대 한 사용자 지정 WPP 대상 파일을 만들어야 합니다. 이렇게 하면 배포 프로세스에 상당한 양의 복잡성이 추가 됩니다. 또한 웹 배포는 기존 데이터베이스에 대 한 증분 업데이트를 직접 지원 하지 않습니다. 이 방법에 대 한 자세한 내용은 [패키지 데이터베이스 프로젝트 배포 SQL 파일에 웹 게시 파이프라인 확장](https://go.microsoft.com/?linkid=9805121)을 참조 하세요.
- VSDBCMD 유틸리티를 사용 하 여 데이터베이스 스키마 또는 배포 매니페스트를 사용 하 여 데이터베이스를 배포할 수 있습니다. MSBuild 대상에서 VSDBCMD를 호출 하 여 데이터베이스를 더 크고 스크립팅된 배포 프로세스의 일부로 게시할 수 있습니다. Sqlcmdvars 파일의 변수와 많은 다른 데이터베이스 속성을 VSDBCMD 명령에서 재정의할 수 있습니다 .이를 통해 여러 빌드 구성을 만들지 않고도 다른 환경에 대 한 배포를 사용자 지정할 수 있습니다. VSDBCMD는 차별화 기능을 제공 하며,이는 대상 데이터베이스를 데이터베이스 스키마와 맞추기 위해 필요한 변경만 수행 하는 것을 의미 합니다. 또한 VSDBCMD는 배포 프로세스를 세부적으로 제어할 수 있게 해 주는 다양 한 명령줄 옵션을 제공 합니다.

이 개요에서 MSBuild와 함께 VSDBCMD를 사용 하는 것이 일반적인 엔터프라이즈 배포 시나리오에 가장 적합 한 방법 임을 확인할 수 있습니다.

|  | Visual Studio 2010 | 웹 배포 2.0 | VSDBCMD.exe |
| --- | --- | --- | --- |
| 원격 배포를 지원 하나요? | yes | yes | yes |
| 증분 업데이트를 지원 하나요? | yes | 예 | yes |
| 배포 전/배포 후 스크립트를 지원 하나요? | yes | yes | yes |
| 다중 환경 배포를 지원 하나요? | 제한적 | 제한적 | yes |
| 스크립팅된 배포를 지원 하나요? | 제한적 | yes | yes |

이 항목의 나머지 부분에서는 MSBuild에서 VSDBCMD를 사용 하 여 데이터베이스 프로젝트를 배포 하는 방법을 설명 합니다.

## <a name="understanding-the-deployment-process"></a>배포 프로세스 이해

VSDBCMD 유틸리티를 사용 하면 데이터베이스 스키마 (.dbschema 파일) 또는 배포 매니페스트 (deploymanifest 파일)를 사용 하 여 데이터베이스를 배포할 수 있습니다. 실제로 배포 매니페스트를 사용 하면 다양 한 배포 속성에 기본값을 제공 하 고 실행 하려는 배포 전 또는 배포 후 SQL 스크립트를 식별할 수 있으므로 실제로 배포 매니페스트를 사용 합니다. 예를 들어이 VSDBCMD 명령은 테스트 환경의 데이터베이스 서버에 배포 된 데이터베이스 **관리자** 데이터베이스를 배포 하는 데 사용 됩니다.

[!code-console[Main](deploying-database-projects/samples/sample1.cmd)]

이 경우 다음과 같습니다.

- **/A** (또는 **/Action**) 스위치는 VSDBCMD에서 수행할 작업을 지정 합니다. **가져오거나** **배포**하도록 설정할 수 있습니다. **가져오기** 옵션은 기존 데이터베이스에서 .dbschema 파일을 생성 하는 데 사용 되 고 **배포** 옵션은 .dbschema 파일을 대상 데이터베이스에 배포 하는 데 사용 됩니다.
- **/Sb** (또는 **/ManifestFile**) 스위치는 배포 하려는 .deploy 매니페스트 파일을 식별 합니다. 대신 .dbschema 파일을 사용 하려는 경우 **/promodel** (또는 **/modelfile**) 스위치를 사용 합니다.
- **/Cs** (또는 **/ConnectionString**) 스위치는 대상 데이터베이스 서버에 대 한 연결 문자열을 제공 합니다. 여기에는 데이터베이스를 만들기 위해 서버에 연결&#x2014;하는 데 필요한 데이터베이스 VSDBCMD 이름이 포함 되지 않습니다. 개별 데이터베이스에 연결 하지 않아도 됩니다. Deploymanifest 파일에 연결 문자열이 포함 된 경우이 스위치를 생략할 수 있습니다. 스위치를 사용 하는 경우 스위치 값이. deploymanifest 값을 재정의 합니다.
- <strong>/P: targetdatabase</strong> 속성은 만들어질 때 대상 데이터베이스에 할당 하려는 이름을 제공 합니다. 이렇게 하면 deploymanifest 파일의 <strong>Targetdatabase</strong> 속성 값이 재정의 됩니다. <strong>/P:</strong> <em>[property name]</em>구문을 사용 하 여 다양 한 배포 속성을 설정 하 고 sqlcmdvars 파일에 선언 된 SQLCMD 변수를 재정의할 수 있습니다.
- **/Dd +** (또는 **/sttodatabase +** ) 스위치는 배포를 만들어 대상 환경에 배포 하려는 경우를 나타냅니다. **/Dd-** 를 지정 하거나 스위치를 생략 하면 VSDBCMD는 배포 스크립트를 생성 하지만 대상 환경에는 배포 하지 않습니다. 이 스위치는 혼동의 원인이 되는 경우가 많으며 다음 섹션에서 자세히 설명 합니다.
- **/Sscript** (또는 **/DeploymentScriptFile**) 스위치는 배포 스크립트를 생성 하려는 위치를 지정 합니다. 이 값은 배포 프로세스에 영향을 주지 않습니다.

VSDBCMD에 대 한 자세한 내용은 [vsdbcmd에 대 한 명령줄 참조를 참조 하세요. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx) 및 [방법: VSDBCMD를 사용 하 여 명령 프롬프트에서 배포용 데이터베이스 준비 EXE](https://msdn.microsoft.com/library/dd193258.aspx).

MSBuild 프로젝트 파일에서 VSDBCMD를 사용 하는 방법에 대 한 예제는 [빌드 프로세스 이해](understanding-the-build-process.md)를 참조 하세요. 여러 환경에 대 한 데이터베이스 배포 설정을 구성 하는 방법에 대 한 예는 [여러 환경에 대 한 데이터베이스 배포 사용자 지정](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)을 참조 하세요.

## <a name="understanding-the-deploytodatabase-switch"></a>DeployToDatabase 스위치 이해

**/Dd** 또는 **/hidatabase** 스위치의 동작은 .dbschema 파일이 있는 VSDBCMD를 사용 하는지 또는 deploymanifest 파일을 사용 하는지에 따라 달라 집니다. .Dbschema 파일을 사용 하는 경우 다음과 같은 동작을 수행 하는 것이 매우 간단 합니다.

- **/Dd +** 또는 **/dd**을 지정 하는 경우 VSDBCMD는 배포 스크립트를 생성 하 고 데이터베이스를 배포 합니다.
- **/Dd-** 를 지정 하거나 스위치를 생략 하면 VSDBCMD는 배포 스크립트만 생성 합니다.

Deploymanifest 파일을 사용 하는 경우 동작이 훨씬 더 복잡해 집니다. 이는 데이터베이스를 배포할지 여부를 결정 하는 속성 이름 **Deploytodatabase** 가 포함 되어 있기 때문입니다.

[!code-xml[Main](deploying-database-projects/samples/sample2.xml)]

이 속성의 값은 데이터베이스 프로젝트의 속성에 따라 설정 됩니다. 배포 **작업** 을 설정 하 여 **배포 스크립트 (.Sql)를 만드는**경우 값은 **False**가 됩니다. 배포 **작업** 을 설정 하 여 **배포 스크립트 (.Sql)를 만들고 데이터베이스에 배포**하는 경우 값이 **True**가 됩니다.

> [!NOTE]
> 이러한 설정은 특정 빌드 구성 및 플랫폼과 연결 됩니다. 예를 들어 **디버그** 구성에 대 한 설정을 구성 하 고 **릴리스** 구성을 사용 하 여 게시 하는 경우 설정이 사용 되지 않습니다.

![](deploying-database-projects/_static/image3.png)

> [!NOTE]
> 이 시나리오에서는 Visual Studio 2010에서 데이터베이스를 배포 하지 않으려는 경우 배포 **작업** 은 항상 **배포 스크립트 (.Sql)를 만들도록**설정 해야 합니다. 즉, **Deploytodatabase** 속성은 항상 **False**여야 합니다.

**Deploytodatabase** 속성이 지정 된 경우 속성 값이 **false**인 경우에만 **/dd** 스위치가 속성을 재정의 합니다.

- **Deploytodatabase** 속성이 **False**이 고 **/dd +** 또는 **/dd**을 지정 하는 경우 VSDBCMD는 **deploytodatabase** 속성을 재정의 하 고 데이터베이스를 배포 합니다.
- **Deploytodatabase** 속성이 **False**이 고 **/dd-** 를 지정 하거나 스위치를 생략 하면 VSDBCMD는 데이터베이스를 배포 하지 않습니다.
- **Deploytodatabase** 속성이 **True**이면 VSDBCMD는 스위치를 무시 하 고 데이터베이스를 배포 합니다.
- 배포 스크립트는 데이터베이스 배포 여부와 관계 없이 각 경우에 생성 됩니다.

## <a name="conclusion"></a>결론

이 항목에서는 Visual Studio 2010의 데이터베이스 프로젝트에 대 한 빌드 및 배포 프로세스의 개요를 제공 했습니다. 또한 MSBuild에서 VSDBCMD를 사용 하 여 엔터프라이즈급 데이터베이스 배포를 지 원하는 방법도 설명 했습니다.

실제로이 작업을 수행 하는 방법에 대 한 자세한 내용은 [여러 환경에 대 한 데이터베이스 배포 사용자 지정](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)을 참조 하세요.

## <a name="further-reading"></a>추가 참고 자료

각 환경에 대 한 별도의 배포 구성 파일을 만들어 데이터베이스 배포를 사용자 지정 하는 방법에 대 한 자세한 내용은 [여러 환경에 대 한 데이터베이스 배포 사용자 지정](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)을 참조 하세요. 배포 후 스크립트를 실행 하 여 데이터베이스 역할 멤버 자격을 구성 하는 방법에 대 한 지침은 [데이터베이스 역할 멤버 자격을 테스트 환경에 배포](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)를 참조 하세요. 멤버 자격 데이터베이스에서 적용 하는 고유한 문제 중 일부를 관리 하는 방법에 대 한 지침은 [엔터프라이즈 환경에 멤버 자격 데이터베이스 배포](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)를 참조 하세요.

MSDN의 이러한 항목에서는 Visual Studio 데이터베이스 프로젝트 및 데이터베이스 배포 프로세스에 대 한 광범위 한 지침과 배경 정보를 제공 합니다.

- [Visual Studio 2010 SQL Server 데이터베이스 프로젝트](https://msdn.microsoft.com/library/ff678491.aspx)
- [데이터베이스 변경 관리](https://msdn.microsoft.com/library/aa833404.aspx)
- [방법: VSDBCMD를 사용 하 여 명령 프롬프트에서 배포용 데이터베이스 준비 CONVERT.EXE](https://msdn.microsoft.com/library/dd193258.aspx)
- [데이터베이스 빌드 및 배포 개요](https://msdn.microsoft.com/library/aa833165.aspx)

> [!div class="step-by-step"]
> [이전](deploying-web-packages.md)
> [다음](creating-and-running-a-deployment-command-file.md)
