---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: 소스 제어에 콘텐츠 추가 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 TFS (Team Foundation Server) 2010에서 소스 제어에 콘텐츠를 추가 하는 방법에 대해 설명 합니다. 팀 프로젝트에 솔루션 및 프로젝트를 추가 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515111"
---
# <a name="adding-content-to-source-control"></a>소스 제어에 콘텐츠 추가

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 TFS (Team Foundation Server) 2010에서 소스 제어에 콘텐츠를 추가 하는 방법에 대해 설명 합니다. 또한 TFS에서 팀 프로젝트에 솔루션 및 프로젝트를 추가 하는 방법에 대해 설명 하 고 프레임 워크 또는 어셈블리와 같은 외부 종속성을 소스 제어에 추가 하는 방법을 설명 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

## <a name="task-overview"></a>작업 개요

대부분의 경우 개발자 팀의 모든 멤버는 소스 제어에 콘텐츠를 추가할 수 있어야 합니다. TFS에서 소스 제어에 솔루션을 추가 하려면 다음과 같은 개략적인 단계를 완료 해야 합니다.

- 팀 프로젝트에 연결 합니다.
- 서버의 팀 프로젝트 폴더 구조를 로컬 컴퓨터의 폴더 구조에 매핑합니다.
- 솔루션과 해당 콘텐츠를 소스 제어에 추가 합니다.
- 소스 제어에 외부 종속성을 추가 합니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 보여 줍니다.

이 항목의 작업 및 연습에서는 콘텐츠를 관리 하는 새 TFS 팀 프로젝트를 이미 만들었다고 가정 합니다. 새 팀 프로젝트를 만드는 방법에 대 한 자세한 내용은 [TFS에서 팀 프로젝트 만들기](creating-a-team-project-in-tfs.md)를 참조 하세요.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람은 누구 인가요?

대부분의 경우 개발자 팀의 모든 멤버는 특정 팀 프로젝트 내에서 콘텐츠를 추가 하 고 수정할 수 있어야 합니다.

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a>팀 프로젝트에 연결 하 고 폴더 매핑을 만듭니다.

소스 제어에 콘텐츠를 추가 하기 전에 팀 프로젝트에 연결 하 고 서버의 폴더 구조와 로컬 컴퓨터의 파일 시스템 간에 매핑을 만들어야 합니다.

**팀 프로젝트에 연결 하 고 로컬 경로를 매핑하려면**

1. 개발자 워크스테이션에서 Visual Studio 2010을 엽니다.
2. Visual Studio의 **팀** 메뉴에서 **Team Foundation Server에 연결**을 클릭 합니다.

    > [!NOTE]
    > TFS 서버에 대 한 연결을 이미 구성한 경우에는 3-6 단계를 생략할 수 있습니다.
3. **팀 프로젝트에 연결** 대화 상자에서 **서버**를 클릭 합니다.
4. **Team Foundation Server 추가/제거** 대화 상자에서 **추가**를 클릭 합니다.
5. **Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 입력 한 다음 **확인**을 클릭 합니다.

    ![](adding-content-to-source-control/_static/image1.png)
6. **Team Foundation Server 추가/제거** 대화 상자에서 **닫기**를 클릭 합니다.
7. **팀 프로젝트에 연결** 대화 상자에서 연결할 TFS 인스턴스를 선택 하 고 팀 프로젝트 컬렉션을 선택한 다음 추가 하려는 팀 프로젝트를 선택 하 고 **연결**을 클릭 합니다.

    ![](adding-content-to-source-control/_static/image2.png)
8. **팀 탐색기** 창에서 팀 프로젝트를 확장 한 다음 **소스 제어**를 두 번 클릭 합니다.

    ![](adding-content-to-source-control/_static/image3.png)
9. **소스 제어 탐색기** 탭에서 **매핑 안 함**을 클릭 합니다.

    ![](adding-content-to-source-control/_static/image4.png)
10. **맵** 대화 상자의 **로컬 폴더** 상자에서 팀 프로젝트에 대 한 루트 폴더로 사용할 로컬 폴더를 찾아보거나 만든 다음 **지도**를 클릭 합니다.

    ![](adding-content-to-source-control/_static/image5.png)
11. 원본 파일을 다운로드 하 라는 메시지가 표시 되 면 **예**를 클릭 합니다.

    ![](adding-content-to-source-control/_static/image6.png)

이 시점에서 팀 프로젝트에 대 한 서버 쪽 폴더를 개발자 워크스테이션의 로컬 폴더에 매핑 했습니다. 또한 팀 프로젝트에서 로컬 폴더 구조로 기존 콘텐츠를 다운로드 했습니다. 이제 소스 제어에 자신의 콘텐츠를 추가 하기 시작할 수 있습니다.

## <a name="add-projects-and-solutions-to-source-control"></a>프로젝트 및 솔루션을 소스 제어에 추가

프로젝트 및 솔루션을 소스 제어에 추가 하려면 먼저 로컬 컴퓨터의 팀 프로젝트에 대 한 매핑된 폴더로 이동 해야 합니다. 그런 다음 콘텐츠를 체크 인하고 서버와의 추가 내용을 동기화 할 수 있습니다.

**소스 제어에 프로젝트를 추가 하려면**

1. 개발자 워크스테이션에서 프로젝트와 솔루션을 팀 프로젝트에 대 한 매핑된 폴더 구조 내의 적절 한 위치로 이동 합니다.

    > [!NOTE]
    > 많은 조직에는 소스 제어에서 프로젝트와 솔루션을 구성 하는 방법에 대 한 기본 방법이 있습니다. 폴더 구조를 구성 하는 방법에 대 한 지침은 [방법: Team Foundation Server에서 소스 제어 폴더 구조](https://msdn.microsoft.com/library/bb668992.aspx)를 참조 하세요.
2. Visual Studio 2010에서 솔루션을 엽니다.
3. **솔루션 탐색기** 창에서 솔루션을 마우스 오른쪽 단추로 클릭 한 다음 **소스 제어에 솔루션 추가**를 클릭 합니다.

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > 일부 경우에는 조직이 TFS에서 콘텐츠를 구조화 하는 방법에 따라 소스 제어에 프로젝트를 개별적으로 추가 하 여 소스 코드를 구성 하는 방법을 보다 세밀 하 게 제어 해야 할 수 있습니다.
4. **소스 제어 탐색기** 탭에 팀 프로젝트의 서버 폴더 구조 내에 추가한 내용이 표시 되는지 확인 합니다.

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > 로컬 파일 시스템의 매핑된 폴더에 솔루션을 추가 했으므로 **소스 제어 탐색기** 탭에는 추가 메시지를 표시 하지 않고 콘텐츠가 표시 됩니다. 솔루션이 매핑되지 않은 위치에 있는 경우 TFS와 로컬 파일 시스템 모두에서 폴더 위치를 지정 하 라는 메시지가 표시 됩니다.
5. **소스 제어 탐색기** 탭의 **폴더** 창에서 팀 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 (예: **연락처 관리자**) **보류 중인 변경 내용 체크 인**을 클릭 합니다.
6. 체크 인 **– 소스 파일** 대화 상자에 설명을 입력 한 다음 **체크**인을 클릭 합니다.

    ![](adding-content-to-source-control/_static/image9.png)

이 시점에서 TFS의 소스 제어에 솔루션을 추가 했습니다.

## <a name="add-external-dependencies-to-source-control"></a>소스 제어에 외부 종속성 추가

프로젝트 또는 솔루션을 소스 제어에 추가 하면 프로젝트 또는 솔루션 내의 모든 파일 및 폴더도 추가 됩니다. 그러나 많은 경우에 프로젝트와 솔루션은 로컬 어셈블리와 같은 외부 종속성을 사용 하 여 제대로 작동 합니다. 팀 빌드와 개발자 팀의 다른 멤버가 코드를 성공적으로 빌드할 수 있도록 소스 제어에 이러한 리소스를 추가 해야 합니다.

예를 들어 Contact Manager 샘플 솔루션의 폴더 구조에는 패키지 라는 폴더가 포함 됩니다. 여기에는 ADO.NET Entity Framework 4.1에 대 한 어셈블리와 다양 한 지원 리소스가 포함 되어 있습니다. 패키지 폴더는 Contact Manager 솔루션에 포함 되지 않지만 솔루션은이 솔루션을 사용 하지 않고 제대로 빌드되지 않습니다. 팀 빌드에서 솔루션을 빌드할 수 있도록 하려면 패키지 폴더를 소스 제어에 추가 해야 합니다.

> [!NOTE]
> 패키지 폴더는 Visual Studio 2010에 대 한 NuGet 확장을 사용 하 여 솔루션에 Entity Framework 또는 유사한 리소스를 추가할 때 일반적으로 발생 합니다.

**비 프로젝트 콘텐츠를 소스 제어에 추가 하려면**

1. 추가 하려는 항목 (예: 패키지 폴더)이 로컬 파일 시스템의 매핑된 폴더 내에서 적절 한 위치에 있는지 확인 합니다.
2. Visual Studio 2010의 **팀 탐색기** 창에서 팀 프로젝트를 확장 한 다음 **소스 제어**를 두 번 클릭 합니다.

    ![](adding-content-to-source-control/_static/image10.png)
3. **소스 제어 탐색기** 탭의 **폴더** 창에서 추가 하려는 항목이 포함 된 폴더를 선택 합니다.
4. **폴더에 항목 추가** 단추를 클릭 합니다.

    ![](adding-content-to-source-control/_static/image11.png)
5. **소스 제어에 추가** 대화 상자에서 추가 하려는 폴더를 선택 하 고 **다음**을 클릭 합니다.

    ![](adding-content-to-source-control/_static/image12.png)
6. 제외 된 **항목** 탭에서 자동으로 제외 된 필수 항목 (예: 어셈블리)을 선택 하 고 **항목 포함**을 클릭 합니다.

    ![](adding-content-to-source-control/_static/image13.png)
7. **추가할 항목** 탭에서 포함 하려는 모든 파일이 나열 되는지 확인 한 다음 **마침**을 클릭 합니다.

    ![](adding-content-to-source-control/_static/image14.png)
8. **소스 제어 탐색기** 창에서 **체크** 인 단추를 클릭 합니다.

    ![](adding-content-to-source-control/_static/image15.png)
9. 체크 인 **– 소스 파일** 대화 상자에 설명을 입력 한 다음 **체크**인을 클릭 합니다.

이 시점에서 솔루션에 대 한 외부 종속성을 소스 제어에 추가 했습니다.

## <a name="conclusion"></a>결론

이 항목에서는 팀 프로젝트에 연결 하 고, 폴더 구조를 매핑하고, 소스 제어에 콘텐츠를 추가 하는 방법에 대해 설명 했습니다. 소스 제어에서 항목으로 작업 하는 방법에 대 한 자세한 내용은 [버전 제어 사용](https://msdn.microsoft.com/library/ms181368.aspx)을 참조 하세요.

다음 항목인 [Tfs 빌드 서버를 웹 배포용으로 구성](configuring-a-tfs-build-server-for-web-deployment.md)에서는 솔루션을 빌드 및 배포 하기 위해 Tfs 팀 빌드 서버를 준비 하는 방법을 설명 합니다.

## <a name="further-reading"></a>추가 참고 자료

TFS에서 원본 제어 작업에 대 한 자세한 내용은 [버전 제어 사용](https://msdn.microsoft.com/library/ms181368.aspx)을 참조 하세요.

> [!div class="step-by-step"]
> [이전](creating-a-team-project-in-tfs.md)
> [다음](configuring-a-tfs-build-server-for-web-deployment.md)
