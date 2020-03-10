---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: 테스트 환경에 데이터베이스 역할 멤버 자격 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 테스트 환경에 솔루션을 배포 하는 과정의 일부로 데이터베이스 역할에 사용자 계정을 추가 하는 방법에 대해 설명 합니다. 다음을 포함 하는 솔루션을 배포 하는 경우 ...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: a15f5bf5f659d151e91ef9e53c5ad55bcd8e2b01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474947"
---
# <a name="deploying-database-role-memberships-to-test-environments"></a>테스트 환경에 데이터베이스 역할 멤버 자격 배포

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 테스트 환경에 솔루션을 배포 하는 과정의 일부로 데이터베이스 역할에 사용자 계정을 추가 하는 방법에 대해 설명 합니다.
> 
> 데이터베이스 프로젝트를 포함 하는 솔루션을 스테이징 또는 프로덕션 환경에 배포 하는 경우 일반적으로 개발자가 데이터베이스 역할에 사용자 계정을 추가 하는 것을 원하지 않습니다. 대부분의 경우 개발자는 어떤 사용자 계정을 어떤 데이터베이스 역할에 추가 해야 할지 알 수 없으며, 이러한 요구 사항은 언제 든 지 변경 될 수 있습니다. 그러나 데이터베이스 프로젝트를 포함 하는 솔루션을 개발 또는 테스트 환경에 배포 하는 경우에는 일반적으로 다음과 같은 상황이 발생 합니다.
> 
> - 개발자는 일반적으로 하루에 몇 번 정기적으로 솔루션을 다시 배포 합니다.
> - 데이터베이스는 일반적으로 모든 배포에 다시 생성 됩니다. 즉, 모든 배포 후에 데이터베이스 사용자를 만들어 역할에 추가 해야 합니다.
> - 개발자는 일반적으로 대상 개발 또는 테스트 환경에 대 한 모든 권한을 가집니다.
> 
> 이 시나리오에서는 데이터베이스 사용자를 자동으로 만들고 배포 프로세스의 일부로 데이터베이스 역할 멤버 자격을 할당 하는 것이 유용한 경우가 많습니다.
> 
> 핵심 요소는이 작업이 대상 환경을 기반으로 해야 한다는 것입니다. 스테이징 또는 프로덕션 환경에 배포 하는 경우 작업을 건너뛰는 것이 좋습니다. 개발자 또는 테스트 환경에 배포 하는 경우 추가 개입 없이 역할 멤버 자격을 배포 하려고 합니다. 이 항목에서는 이러한 문제를 해결 하는 데 사용할 수 있는 방법에 대해 설명 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="task-overview"></a>작업 개요

이 항목에서는 다음과 같이 가정합니다.

- [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 대로 프로젝트 파일 분할 방식을 솔루션 배포에 사용 합니다.
- [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)의 설명에 따라 프로젝트 파일에서 VSDBCMD를 호출 하 여 데이터베이스 프로젝트를 배포 합니다.

데이터베이스 사용자를 만들고 테스트 환경에 데이터베이스 프로젝트를 배포할 때 역할 멤버 자격을 할당 하려면 다음을 수행 해야 합니다.

- 필요한 데이터베이스 변경을 수행 하는 Transact-sql (구조적 쿼리 언어 Transact-sql) 스크립트를 만듭니다.
- Sqlcmd 유틸리티를 사용 하 여 SQL 스크립트를 실행 하는 Microsoft Build Engine (MSBuild) 대상을 만듭니다.
- 테스트 환경에 솔루션을 배포 하는 경우 대상을 호출 하도록 프로젝트 파일을 구성 합니다.

이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여 줍니다.

## <a name="scripting-the-database-role-memberships"></a>데이터베이스 역할 멤버 자격 스크립팅

다양 한 방법 및 선택한 위치에서 Transact-sql 스크립트를 만들 수 있습니다. 가장 쉬운 방법은 Visual Studio 2010의 솔루션 내에서 스크립트를 만드는 것입니다.

**SQL 스크립트를 만들려면**

1. **솔루션 탐색기** 창에서 데이터베이스 프로젝트 노드를 확장 합니다.
2. **Scripts** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 가리킨 다음 **새 폴더**를 클릭 합니다.
3. 폴더 이름으로 **Test** 를 입력 한 다음 enter 키를 누릅니다.
4. **테스트** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 가리킨 다음 **스크립트**를 클릭 합니다.
5. **새 항목 추가** 대화 상자에서 스크립트에 의미 있는 이름 (예: **AddRoleMemberships**)을 지정한 다음 **추가**를 클릭 합니다.

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. AddRoleMemberships 파일에서 다음과 같은 Transact-sql 문을 추가 *합니다* .

    1. 데이터베이스에 액세스 하는 SQL Server 로그인에 대 한 데이터베이스 사용자를 만듭니다.
    2. 필요한 데이터베이스 역할에 데이터베이스 사용자를 추가 합니다.
7. 파일은 다음과 유사 합니다.

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. 파일을 저장합니다.

## <a name="executing-the-script-on-the-target-database"></a>대상 데이터베이스에서 스크립트 실행

데이터베이스 프로젝트를 배포할 때 배포 후 스크립트의 일부로 필요한 Transact-sql 스크립트를 실행 하는 것이 가장 좋습니다. 그러나 배포 후 스크립트를 사용 하면 솔루션 구성 또는 빌드 속성에 따라 조건부로 논리를 실행할 수 없습니다. 대신, sqlcmd 명령을 실행 하는 **대상** 요소를 만들어 MSBuild 프로젝트 파일에서 직접 SQL 스크립트를 실행 합니다. 이 명령을 사용 하 여 대상 데이터베이스에서 스크립트를 실행할 수 있습니다.

[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]

> [!NOTE]
> Sqlcmd 명령줄 옵션에 대 한 자세한 내용은 [Sqlcmd 유틸리티](https://msdn.microsoft.com/library/ms162773.aspx)를 참조 하세요.

이 명령을 MSBuild 대상에 포함 하기 전에 스크립트를 실행 하는 조건을 고려해 야 합니다.

- 대상 데이터베이스는 역할 멤버 자격을 변경 하기 전에 존재 해야 합니다. 따라서 데이터베이스 배포 *후* 이 스크립트를 실행 해야 합니다.
- 테스트 환경에 대해서만 스크립트가 실행 되도록 조건을 포함 해야 합니다.
- "What if" 배포&#x2014;를 실행 하는 경우 (즉, 배포 스크립트를 생성 하지만 실제로 실행&#x2014;하지 않는 경우) SQL 스크립트를 실행 해서는 안 됩니다.

Contact Manager 샘플 솔루션에 설명 된 것 처럼 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 분할 프로젝트 파일 방법을 사용 하는 경우 SQL 스크립트에 대 한 빌드 지침을 다음과 같이 분할할 수 있습니다.

- 사용 권한을 배포할지 여부를 결정 하는 속성과 함께 필수 환경 관련 속성은 환경 관련 프로젝트 파일 (예: *Env-Dev. proj*)에 있어야 합니다.
- 대상 환경 간에 변경 되지 않는 모든 속성과 함께 MSBuild 대상 자체도 유니버설 프로젝트 파일 (예: *Publish proj*)로 이동 해야 합니다.

환경 관련 프로젝트 파일에서 사용자가 역할 멤버 자격을 배포할지 여부를 지정할 수 있도록 데이터베이스 서버 이름, 대상 데이터베이스 이름 및 부울 속성을 정의 해야 합니다.

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]

유니버설 프로젝트 파일에서 sqlcmd 실행 파일의 위치와 실행 하려는 SQL 스크립트의 위치를 제공 해야 합니다. 이러한 속성은 대상 환경에 관계 없이 동일 하 게 유지 됩니다. Sqlcmd 명령을 실행 하려면 MSBuild 대상도 만들어야 합니다.

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]

Sqlcmd 실행 파일의 위치는 정적 속성으로 추가 합니다 .이는 다른 대상에 유용할 수 있습니다. 반면, 대상이 실행 되기 전에는 필요 하지 않으므로 SQL 스크립트의 위치와 sqlcmd 명령의 구문을 대상 내의 동적 속성으로 정의 합니다. 이 경우 **Deploytestdbpermissions** 대상은 다음 조건이 충족 되는 경우에만 실행 됩니다.

- **DeployTestDBRoleMemberships** 속성은 **true**로 설정 됩니다.
- 사용자가 **WhatIf = true** 플래그를 지정 하지 않았습니다.

마지막으로 대상을 호출 하는 것을 잊지 마세요. *Publish proj* 파일에서 기본 **fullpublish** 대상에 대 한 종속성 목록에 대상을 추가 하 여이 작업을 수행할 수 있습니다. **Deploydb패키지** 대상이 실행 될 때까지 **Deploytestdbpermissions** 대상이 실행 되지 않도록 해야 합니다.

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]

## <a name="conclusion"></a>결론

이 항목에서는 데이터베이스 프로젝트를 배포할 때 배포 후 작업으로 데이터베이스 사용자 및 역할 멤버 자격을 추가할 수 있는 한 가지 방법에 대해 설명 했습니다. 이는 일반적으로 테스트 환경에서 데이터베이스를 정기적으로 다시 만들 때 유용 하지만, 스테이징 또는 프로덕션 환경에 데이터베이스를 배포할 때는 일반적으로 피해 야 합니다. 따라서 데이터베이스 사용자 및 역할 멤버 자격이 적절 한 경우에만 만들어지도록 필요한 조건부 논리를 사용 해야 합니다.

## <a name="further-reading"></a>추가 참고 자료

VSDBCMD를 사용 하 여 데이터베이스 프로젝트를 배포 하는 방법에 대 한 자세한 내용은 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)를 참조 하세요. 여러 대상 환경의 데이터베이스 배포를 사용자 지정 하는 방법에 대 한 지침은 [여러 환경에 대 한 데이터베이스 배포 사용자 지정](customizing-database-deployments-for-multiple-environments.md)을 참조 하세요. 사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 방법에 대 한 자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)를 참조 하세요. Sqlcmd 명령줄 옵션에 대 한 자세한 내용은 [Sqlcmd 유틸리티](https://msdn.microsoft.com/library/ms162773.aspx)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](customizing-database-deployments-for-multiple-environments.md)
> [다음](deploying-membership-databases-to-enterprise-environments.md)
