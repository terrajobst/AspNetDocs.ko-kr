---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: 특정 빌드 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 특정 이전 빌드의 웹 패키지 및 데이터베이스 스크립트를 스테이징 또는 프로덕션 enviro 같은 새 대상에 배포 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 6bede6b36c24ade928ab052e14daec1e017bd0b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519575"
---
# <a name="deploying-a-specific-build"></a>특정 빌드 배포

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 특정 이전 빌드의 웹 패키지 및 데이터베이스 스크립트를 스테이징 또는 프로덕션 환경과 같은 새 대상에 배포 하는 방법에 대해 설명 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다. 프로젝트 파일에 대 한 빌드 및 배포 프로세스는 모든&#x2014;대상 환경에 적용 되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 합니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="task-overview"></a>작업 개요

지금까지이 자습서의 항목은 단일 단계 또는 자동화 된 프로세스의 일부로 웹 응용 프로그램 및 데이터베이스를 빌드, 패키징 및 배포 하는 방법에 중점을 두었습니다. 그러나 몇 가지 일반적인 시나리오에서는 저장 폴더의 빌드 목록에서 배포 하는 리소스를 선택 하는 것이 좋습니다. 즉, 최신 빌드는 배포 하려는 빌드가 아닐 수 있습니다.

이전 항목에서 설명한 CI (지속적인 통합) 시나리오를 고려 하 여 [배포를 지 원하는 빌드 정의를 만듭니다](creating-a-build-definition-that-supports-deployment.md). Team Foundation Server (TFS) 2010에서 빌드 정의를 만들었습니다. 개발자가 코드를 TFS에 체크 인할 때마다 팀 빌드는 코드를 빌드하고, 웹 패키지와 데이터베이스 스크립트를 빌드 프로세스의 일부로 만들고, 단위 테스트를 실행 하 고, 리소스를 테스트 환경에 배포 합니다. 빌드 정의를 만들 때 구성한 보존 정책에 따라 TFS는 특정 개수의 이전 빌드를 유지 합니다.

![](deploying-a-specific-build/_static/image1.png)

이제 테스트 환경에서 이러한 빌드 중 하나에 대해 확인 및 유효성 검사 테스트를 수행 했으며 스테이징 환경에 응용 프로그램을 배포할 준비가 되었다고 가정 합니다. 한편 개발자는 새 코드를 체크 인할 수 있습니다. 솔루션을 다시 빌드하고 스테이징 환경에 배포 하지 않고 최신 빌드를 스테이징 환경에 배포 하지 않으려는 경우 대신 테스트 서버에서 확인 하 고 유효성을 검사 한 특정 빌드를 배포 하려고 합니다.

이를 위해서는 특정 빌드에서 생성 된 웹 패키지 및 데이터베이스 스크립트를 찾을 수 있는 위치 (MSBuild)를 Microsoft Build Engine (MSBuild)에 알려야 합니다.

## <a name="overriding-the-outputroot-property"></a>OutputRoot 속성 재정의

[샘플 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)에서 *게시 Proj* 파일은 **outputroot**라는 속성을 선언 합니다. 이름에서 알 수 있듯이이 폴더는 빌드 프로세스에서 생성 하는 모든 항목을 포함 하는 루트 폴더입니다. *Publish. proj* 파일에서 **outputroot** 속성은 모든 배포 리소스의 루트 위치를 참조 하는 것을 볼 수 있습니다.

> [!NOTE]
> **Outputroot** 는 일반적으로 사용 되는 속성 이름입니다. 시각적 C# 개체 및 Visual Basic 프로젝트 파일은이 속성을 선언 하 여 모든 빌드 출력의 루트 위치를 저장 합니다.

[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]

프로젝트 파일에서 이전 TFS 빌드의&#x2014;&#x2014;출력과 같은 다른 위치에서 웹 패키지 및 데이터베이스 스크립트를 배포 하려는 경우에는 **outputroot** 속성을 재정의 하기만 하면 됩니다. 속성 값을 팀 빌드 서버의 관련 빌드 폴더로 설정 해야 합니다. 명령줄에서 MSBuild를 실행 하는 경우 명령줄 인수로 **Outputroot** 의 값을 지정할 수 있습니다.

[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]

그러나 실제로 빌드 출력을 사용 하지 않으려는 경우에는 솔루션 을 빌드하&#x2014;는 시점이 없는 빌드 대상을 건너뛸 수도 있습니다. 이렇게 하려면 명령줄에서 실행할 대상을 지정 합니다.

[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]

그러나 대부분의 경우에는 배포 논리를 TFS 빌드 정의로 빌드해야 합니다. 이렇게 하면 **큐 빌드** 권한이 있는 사용자가 TFS 서버에 대 한 연결을 사용 하 여 Visual Studio 설치에서 배포를 트리거할 수 있습니다.

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a>특정 빌드를 배포 하기 위한 빌드 정의 만들기

다음 절차에서는 사용자가 단일 명령을 사용 하 여 스테이징 환경에 대 한 배포를 트리거할 수 있도록 하는 빌드 정의를 만드는 방법을 설명 합니다.

이 경우 빌드 정의에서 사용자 지정 프로젝트 파일의 배포 논리를 실행&#x2014;하는 데 필요한 모든 항목을 실제로 빌드하지는 않습니다. *Publish. proj* 파일에는 팀 빌드에서 파일이 실행 중인 경우 **빌드** 대상을 건너뛰는 조건부 논리가 포함 됩니다. 팀 빌드에서 프로젝트 파일을 실행 하는 경우 자동으로 **true** 로 설정 되는 기본 제공 **BuildingInTeamBuild** 속성을 평가 하 여이를 수행 합니다. 따라서 빌드 프로세스를 건너뛰고 단순히 프로젝트 파일을 실행 하 여 기존 빌드를 배포할 수 있습니다.

**배포를 수동으로 트리거하는 빌드 정의를 만들려면**

1. Visual Studio 2010의 **팀 탐색기** 창에서 팀 프로젝트 노드를 확장 하 고 **빌드**를 마우스 오른쪽 단추로 클릭 한 다음 **새 빌드 정의**를 클릭 합니다.

    ![](deploying-a-specific-build/_static/image2.png)
2. **일반** 탭에서 빌드 정의 이름 (예: **deploytostaging**) 및 설명 (선택 사항)을 지정 합니다.
3. **트리거** 탭에서 **수동-체크 인이 새 빌드를 트리거하지 않습니다**.를 선택 합니다.
4. **빌드 기본값** 탭의 **다음 저장 폴더에 빌드 출력 복사** 상자에 저장 폴더의 UNC (범용 명명 규칙) 경로를 입력 합니다 (예: **\\TFSBUILD\Drops**).

    ![](deploying-a-specific-build/_static/image3.png)
5. **프로세스** 탭의 **빌드 프로세스 파일** 드롭다운 목록에서 **defaulttemplate .xaml** 을 선택 된 채로 둡니다. 모든 새 팀 프로젝트에 추가 되는 기본 빌드 프로세스 템플릿 중 하나입니다.
6. **빌드 프로세스 매개 변수** 테이블에서 **빌드할 항목** 행을 클릭 한 다음 **줄임표** 단추를 클릭 합니다.

    ![](deploying-a-specific-build/_static/image4.png)
7. **빌드할 항목** 대화 상자에서 **추가**를 클릭 합니다.
8. 다음 **형식의 항목** 드롭다운 목록에서 **MSBuild 프로젝트 파일**을 선택 합니다.
9. 배포 프로세스를 제어 하는 사용자 지정 프로젝트 파일의 위치로 이동 하 여 파일을 선택한 다음 **확인**을 클릭 합니다.

    ![](deploying-a-specific-build/_static/image5.png)
10. **빌드할 항목** 대화 상자에서 **확인**을 클릭 합니다.
11. **빌드 프로세스 매개 변수** 테이블에서 **고급** 섹션을 확장 합니다.
12. **MSBuild Arguments** 행에서 환경 관련 프로젝트 파일의 위치를 지정 하 고 빌드 폴더의 위치에 대 한 자리 표시자를 추가 합니다.

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > 빌드를 큐에 대기 시킬 때마다 **Outputroot** 값을 재정의 해야 합니다. 이에 대해서는 다음 절차에서 설명 합니다.
13. **저장**을 클릭합니다.

빌드를 트리거할 때 배포 하려는 빌드를 가리키도록 **Outputroot** 속성을 업데이트 해야 합니다.

**빌드 정의에서 특정 빌드를 배포 하려면**

1. **팀 탐색기** 창에서 빌드 정의를 마우스 오른쪽 단추로 클릭 한 다음 **새 빌드 큐 대기**를 클릭 합니다.

    ![](deploying-a-specific-build/_static/image7.png)
2. **큐 빌드** 대화 상자의 **매개 변수** 탭에서 **고급** 섹션을 확장 합니다.
3. **MSBuild Arguments** 행에서 **outputroot** 속성의 값을 빌드 폴더의 위치로 바꿉니다. 다음은 그 예입니다.

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > 빌드 폴더 경로 끝에 후행 슬래시를 포함 해야 합니다.
4. **큐**를 클릭 합니다.

빌드를 큐에 대기 시 프로젝트 파일은 **Outputroot** 속성에 지정한 빌드 저장 폴더에서 데이터베이스 스크립트와 웹 패키지를 배포 합니다.

## <a name="conclusion"></a>결론

이 항목에서는 분할 프로젝트 파일 배포 모델을 사용 하 여 특정 이전 빌드에서 웹 패키지 및 데이터베이스 스크립트와 같은 배포 리소스를 게시 하는 방법에 대해 설명 했습니다. **Outputroot** 속성을 재정의 하는 방법 및 배포 논리를 TFS 빌드 정의에 통합 하는 방법에 대해 설명 했습니다.

## <a name="further-reading"></a>추가 참고 자료

빌드 정의를 만드는 방법에 대 한 자세한 내용은 [기본 빌드 정의 만들기](https://msdn.microsoft.com/library/ms181716.aspx) 및 [빌드 프로세스 정의](https://msdn.microsoft.com/library/ms181715.aspx)를 참조 하세요. 빌드를 큐에 추가 하는 방법에 대 한 자세한 지침은 [빌드 큐 대기](https://msdn.microsoft.com/library/ms181722.aspx)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](creating-a-build-definition-that-supports-deployment.md)
> [다음](configuring-permissions-for-team-build-deployment.md)
