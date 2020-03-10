---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: TFS에서 팀 프로젝트 만들기 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 TFS (Team Foundation Server) 2010에서 새 팀 프로젝트를 만드는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519563"
---
# <a name="creating-a-team-project-in-tfs"></a>TFS에서 팀 프로젝트 만들기

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 TFS (Team Foundation Server) 2010에서 새 팀 프로젝트를 만드는 방법에 대해 설명 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

## <a name="task-overview"></a>작업 개요

TFS에서 새 팀 프로젝트를 프로 비전 하 고 사용 하려면 다음과 같은 개략적인 단계를 완료 해야 합니다.

- 새 팀 프로젝트를 만들 사용자에 게 사용 권한을 부여 합니다.
- 팀 프로젝트를 만듭니다.
- 프로젝트에 대 한 작업을 수행할 팀 멤버에 게 권한을 부여 합니다.
- 일부 콘텐츠를 체크 인 합니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 보여 주고 각 절차를 담당 하 게 될 가능성이 높은 사용자 및 작업 역할을 식별 합니다. 조직의 구조에 따라 이러한 각 작업은 다른 사용자의 책임 일 수 있습니다.

이 항목의 작업 및 연습에서는 TFS를 설치 및 구성 하 고 구성 프로세스의 일부로 팀 프로젝트 컬렉션을 만들었다고 가정 합니다. 이러한 가정에 대 한 자세한 내용 및 시나리오에 대 한 보다 일반적인 배경 정보는 [웹 배포용 TFS 빌드 서버 구성](configuring-a-tfs-build-server-for-web-deployment.md)을 참조 하세요.

## <a name="grant-permissions-to-the-team-project-creator"></a>팀 프로젝트 작성자에 게 권한 부여

새 팀 프로젝트를 만들려면 다음 권한이 필요 합니다.

- TFS 응용 프로그램 계층에 대 한 **새 프로젝트 만들기** 권한이 있어야 합니다. 일반적으로 **Project Collection Administrators** TFS 그룹에 사용자를 추가 하 여이 사용 권한을 부여 합니다. **Team Foundation Administrators** 글로벌 그룹에도이 권한이 포함 되어 있습니다.
- SharePoint 사이트 컬렉션 내에 TFS 팀 프로젝트 컬렉션에 해당 하는 새 팀 사이트를 만들 수 있는 권한이 있어야 합니다. 일반적으로 SharePoint 사이트 모음에 대 한 **모든** 권한이 있는 sharepoint 그룹에 사용자를 추가 하 여이 사용 권한을 부여 합니다.
- SQL Server Reporting Services 기능을 사용 하는 경우 Reporting Services에서 **Team Foundation Content Manager** 역할의 멤버 여야 합니다.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람은 누구 인가요?

일반적으로 TFS 배포를 관리 하는 개인 또는 그룹도 이러한 절차를 수행 합니다.

이는 권한이 높은 권한 집합 이기 때문에 일반적으로 TFS 배포 관리를 담당 하는 작은 사용자 하위 집합에서 새 팀 프로젝트를 만듭니다. 개발자에 게는 일반적으로 새 팀 프로젝트를 만드는 데 필요한 권한이 부여 되지 않습니다.

### <a name="grant-permissions-in-tfs"></a>TFS에서 권한 부여

사용자가 새 팀 프로젝트를 만들 수 있도록 하려는 경우 가장 높은 수준의 작업은 팀 프로젝트 컬렉션에 대 한 **Project Collection Administrators** 그룹에 사용자를 추가 하는 것입니다.

**Project Collection Administrators 그룹에 사용자를 추가 하려면**

1. TFS 서버의 **시작** 메뉴에서 **모든 프로그램**을 가리키고 **Microsoft Team Foundation Server 2010**를 클릭 한 다음 **Team Foundation 관리 콘솔**를 클릭 합니다.
2. 탐색 트리 보기에서 **응용 프로그램 계층**을 확장 한 다음 **팀 프로젝트 컬렉션**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. **팀 프로젝트 컬렉션** 창에서 관리 하려는 팀 프로젝트 컬렉션을 선택 합니다.

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. **일반** 탭에서 **그룹 멤버 자격**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. **전역 그룹** 대화 상자에서 **Project Collection Administrators** 그룹을 선택 하 고 **속성**을 클릭 합니다.
6. **Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**을 선택 하 고 **추가**를 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 새 팀 프로젝트를 만들 사용자의 이름을 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. **Team Foundation Server 그룹 속성** 대화 상자에서 **확인**을 클릭 합니다.
9. **전역 그룹** 대화 상자에서 **닫기**를 클릭 합니다.

### <a name="grant-permissions-in-sharepoint-services"></a>SharePoint Services에서 사용 권한 부여

다음으로 사용자에 게 TFS 팀 프로젝트 컬렉션에 해당 하는 SharePoint 사이트 모음에 새 팀 사이트를 만들 수 있는 권한을 부여 해야 합니다.

**SharePoint 사이트 모음에 대 한 모든 권한을 부여 하려면**

1. Team Foundation Server 관리 콘솔의 **팀 프로젝트 컬렉션** 페이지에서 관리 하려는 팀 프로젝트 컬렉션을 선택 합니다.
2. **SharePoint 사이트** 탭에서 **현재 기본 사이트 위치** URL의 값을 확인 합니다.

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. Internet Explorer를 열고 2 단계에서 적어둔 URL로 이동 합니다.

    > [!NOTE]
    > 팀 프로젝트 컬렉션을 만든 사용자로 Windows에 로그온 하지 않은 경우 계속 하려면 SharePoint에이 사용자로 로그인 해야 합니다.
4. **사이트 동작** 메뉴에서 **사이트 설정**을 클릭합니다.

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. **사이트 설정** 페이지의 **사용자 및 사용 권한**에서 **사용자 및 그룹**을 클릭 합니다.
6. 왼쪽 탐색 패널에서 **그룹**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. **사용자 및 그룹: 모든 그룹** 페이지에서 **이 사이트에 대 한 그룹 설정**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > 이중 HTTP 인코딩 버그로 인해 <strong>http 404 찾을</strong> 수 없음 오류가 표시 될 수 있습니다. 이 경우 URL을 다음과 같이 바꿉니다.   
   > `[site_collection_URL]/_layouts/permsetup.aspx` 예:  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. **이 사이트에 대 한 그룹 설정** 페이지에서 팀 프로젝트를 만들 사용자를 **소유자** 그룹에 추가한 다음 **확인**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image10.png)

사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만들 수 있도록 설정 하는 방법에 대 한 자세한 내용은 [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/library/dd547204.aspx)을 참조 하세요.

## <a name="create-a-new-team-project-and-add-users"></a>새 팀 프로젝트를 만들고 사용자 추가

필요한 권한이 있으면 Visual Studio 2010의 **팀 탐색기** 창을 사용 하 여 새 팀 프로젝트를 만들 수 있습니다. 이 방법은 필요한 모든 정보를 수집 하 고 TFS, SharePoint 및 SQL Server Reporting Services에서 필요한 작업을 수행 하는 마법사를 제공 합니다. 또한 개발자 팀의 멤버에 게 새 팀 프로젝트에 대 한 권한을 부여 하 여 콘텐츠를 추가 하 고 수정할 수 있도록 해야 합니다.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람은 누구 인가요?

일반적으로 TFS 관리자 또는 개발자 팀 리더는 이러한 절차를 수행 합니다.

### <a name="create-a-new-team-project"></a>새 팀 프로젝트 만들기

다음 절차에서는 TFS 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.

**새 팀 프로젝트를 만들려면**

1. **시작** 메뉴에서 **모든 프로그램**을 가리키고 **Microsoft Visual Studio 2010**를 클릭 한 다음 **Microsoft Visual Studio 2010**을 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 클릭 합니다.

    > [!NOTE]
    > Visual Studio 2010을 관리자 권한으로 실행 하지 않으면 새 팀 프로젝트 마법사가 마지막 단계에서 실패 합니다.
2. **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**를 클릭합니다.
3. Visual Studio의 **팀** 메뉴에서 **Team Foundation Server에 연결**을 클릭 합니다.

    > [!NOTE]
    > TFS 서버에 대 한 연결을 이미 구성한 경우에는 4-7 단계를 생략할 수 있습니다.
4. **팀 프로젝트에 연결** 대화 상자에서 **서버**를 클릭 합니다.
5. **Team Foundation Server 추가/제거** 대화 상자에서 **추가**를 클릭 합니다.
6. **Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 입력 한 다음 **확인**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. **Team Foundation Server 추가/제거** 대화 상자에서 **닫기**를 클릭 합니다.
8. **팀 프로젝트에 연결** 대화 상자에서 연결할 TFS 인스턴스를 선택 하 고 추가 하려는 팀 프로젝트 컬렉션을 선택한 다음 **연결**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. **팀 탐색기** 창에서 팀 프로젝트 컬렉션을 마우스 오른쪽 단추로 클릭 한 다음 **새 팀 프로젝트**를 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. **새 팀 프로젝트** 대화 상자에서 팀 프로젝트에 대 한 이름 및 설명을 입력 하 고 **다음**을 클릭 합니다.

    > [!NOTE]
    > 팀 프로젝트에 공백이 포함 된 경우 인터넷 정보 서비스 (IIS) 웹 배포 (웹 배포 도구)를 사용 하 여 출력 경로에서 패키지를 배포 하는 경우 몇 가지 문제가 발생할 수 있습니다. 경로에 공백이 있으면 명령 웹 배포 실행 하기가 훨씬 어려워집니다.

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. **프로세스 템플릿 선택** 페이지에서 개발 프로세스를 관리 하는 데 사용할 프로세스 템플릿을 선택 하 고 **다음**을 클릭 합니다.

    > [!NOTE]
    > TFS의 프로세스 템플릿에 대 한 자세한 내용은 [프로세스 템플릿 및 도구](https://msdn.microsoft.com/vstudio/aa718795)를 참조 하세요.
12. **팀 사이트 설정** 페이지에서 기본 설정을 변경 하지 않고 그대로 두고 **다음**을 클릭 합니다.
13. 이 설정은 TFS 팀 프로젝트와 연결 된 SharePoint 팀 사이트를 만들거나 식별 합니다. 개발 팀은이 사이트를 사용 하 여 설명서를 관리 하 고, 토론 스레드에 참여 하 고, wiki 페이지를 만들고, 코드와 관련 되지 않은 다양 한 기타 작업을 수행할 수 있습니다. 자세한 내용은 [SharePoint 제품 간의 상호 작용 및 Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx)을 참조 하세요.
14. **원본 제어 설정 지정** 페이지에서 기본 설정을 변경 하지 않고 그대로 **두고 다음을 클릭 합니다**.
15. 이 설정은 TFS 폴더 계층에서 콘텐츠에 대 한 루트 폴더 역할을 하는 위치를 식별 하거나 만듭니다.
16. **팀 프로젝트 설정 확인** 페이지에서 **마침**을 클릭 합니다.
17. 새 팀 프로젝트가 성공적으로 만들어지면 **팀 프로젝트를 만든** 페이지에서 **닫기**를 클릭 합니다.

### <a name="add-users-to-a-team-project"></a>팀 프로젝트에 사용자 추가

이제 새 팀 프로젝트를 만들었으므로 사용자에 게 콘텐츠를 추가 하 고 공동 작업을 시작할 수 있는 권한을 부여할 수 있습니다.

**팀 프로젝트에 사용자를 추가 하려면**

1. Visual Studio 2010의 **팀 탐색기** 창에서 팀 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **팀 프로젝트 설정**을 가리킨 다음 **그룹 멤버 자격**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. 사용자가 소스 제어에서 코드를 추가, 수정 및 제거할 수 있도록 하려면 해당 사용자를 **Contributors** 그룹에 추가 해야 합니다.
3. **프로젝트 그룹** 대화 상자에서 **Contributors** 그룹을 선택 하 고 **속성**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. **Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**을 선택 하 고 **추가**를 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 팀 프로젝트에 추가 하려는 사용자의 이름을 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. **Team Foundation Server 그룹 속성** 대화 상자에서 **확인**을 클릭 합니다.
7. **프로젝트 그룹** 대화 상자에서 **닫기**를 클릭 합니다.

## <a name="conclusion"></a>결론

이 시점에서 새로운 팀 프로젝트를 사용할 준비가 되 고 개발자 팀이 개발 프로세스에서 콘텐츠를 추가 하 고 공동 작업을 시작할 수 있습니다.

다음 항목인 [소스 제어에](adding-content-to-source-control.md)콘텐츠 추가에서는 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다.

## <a name="further-reading"></a>추가 참고 자료

TFS에서 팀 프로젝트를 만드는 방법에 대 한 광범위 한 지침은 [팀 프로젝트 만들기](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx)를 참조 하세요. 사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만들 수 있도록 설정 하는 방법에 대 한 자세한 내용은 [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/library/dd547204.aspx)을 참조 하세요. 팀 프로젝트에 사용자를 추가 하는 방법에 대 한 자세한 내용은 [팀 프로젝트에 사용자 추가](https://msdn.microsoft.com/library/bb558971.aspx)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](configuring-team-foundation-server-for-web-deployment.md)
> [다음](adding-content-to-source-control.md)
