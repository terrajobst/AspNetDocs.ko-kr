---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: 웹 배포용 TFS 빌드 서버 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 팀 빌드와 인터넷 형식 ...을 사용 하 여 솔루션을 빌드 및 배포 하기 위해 TFS (Team Foundation Server) 빌드 서버를 준비 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: b3aaf7234706d149a3c784347528923f662c3511
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512225"
---
# <a name="configuring-a-tfs-build-server-for-web-deployment"></a>웹 배포용 TFS Build Server 구성

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 Team Build 및 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 솔루션을 빌드 및 배포 하기 위해 TFS (Team Foundation Server) 빌드 서버를 준비 하는 방법에 대해 설명 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="task-overview"></a>작업 개요

솔루션을 빌드 및 배포 하기 위해 빌드 서버를 준비 하려면 다음을 수행 해야 합니다.

- TFS 빌드 서비스를 설치 및 구성 합니다.
- Visual Studio 2010을 설치 합니다.
- .NET Framework 또는 ASP.NET MVC와 같은 솔루션을 빌드하는 데 필요한 모든 제품이 나 구성 요소를 설치 합니다.
- 웹 배포 2.0 이상 버전을 설치 합니다.

이 항목에서는 이러한 절차를 수행 하거나 해당 절차를 수행 하는 다른 리소스를 가리키는 방법을 보여 줍니다. 이 항목의 작업 및 연습에서는 다음을 가정 합니다.

- Windows Server 2008 R2 서비스 팩 1을 실행 하는 클린 서버 빌드를 시작 합니다.
- 서버는 고정 IP 주소를 사용 하 여 도메인에 가입 됩니다.
- [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)에 설명 된 대로 TFS 응용 프로그램 계층을 별도의 서버에 설치 했습니다.

### <a name="who-performs-these-procedures"></a>이러한 절차를 수행 하는 사람은 누구 인가요?

대부분의 경우 TFS 관리자는 빌드 서버를 구성 해야 합니다. 일부 경우에 개발자 팀은 특정 빌드 서버에 대 한 소유권을 가질 수 있습니다.

## <a name="install-and-configure-the-tfs-build-service"></a>TFS 빌드 서비스 설치 및 구성

빌드 서버를 구성 하는 경우 첫 번째 작업은 TFS 빌드 서비스를 설치 하 고 구성 하는 것입니다. 이 프로세스의 일부로 다음을 수행 해야 합니다.

- TFS 빌드 서비스를 설치 하 고 서비스 계정을 구성 합니다. 배포를 비롯 한 모든 빌드 작업은 빌드 서비스 계정의 id를 사용 하 여 실행 됩니다.
- *빌드 컨트롤러* 와 하나 이상의 *빌드 에이전트*를 만듭니다. 각 빌드 컨트롤러는 빌드 에이전트 집합을 관리 합니다. 빌드를 큐에 대기 시킬 때 빌드 컨트롤러는 사용 가능한 빌드 에이전트에 빌드 작업을 할당 합니다. TFS의 각 팀 프로젝트 컬렉션은 단일 빌드 컨트롤러에 매핑됩니다.
- 빌드 출력에 대 한 저장 폴더를 구성 합니다. 네트워크 공유입니다. 웹 배포 패키지와 같은 모든 빌드 출력이 drop 폴더로 전송 됩니다.

MSDN의 [Team Foundation Build 관리](https://msdn.microsoft.com/library/ms252495.aspx) 챕터에는 다음 작업을 수행 하는 데 필요한 모든 리소스가 포함 되어 있습니다.

- 빌드 서비스, 빌드 컨트롤러 및 빌드 에이전트를 포함 하 여 Team Foundation Build에 대 한 개념적 개요는 [Team Foundation Build 시스템 이해](https://msdn.microsoft.com/library/dd793166.aspx)를 참조 하세요.
- 빌드 서비스를 설치 및 구성 하는 방법에 대 한 자세한 내용은 [빌드 컴퓨터 구성](https://msdn.microsoft.com/library/ms181712.aspx)을 참조 하세요.
- 빌드 컨트롤러를 만드는 방법에 대 한 자세한 내용은 [빌드 컨트롤러 만들기 및 사용](https://msdn.microsoft.com/library/ee330987.aspx)을 참조 하세요.
- 빌드 에이전트를 만드는 방법에 대 한 자세한 내용은 [빌드 에이전트 만들기 및 사용](https://msdn.microsoft.com/library/bb399135.aspx)을 참조 하세요.
- 저장 폴더를 만들고 구성 하는 방법에 대 한 자세한 내용은 [저장 폴더 설정](https://msdn.microsoft.com/library/bb778394.aspx)을 참조 하세요.

## <a name="install-required-products-and-components"></a>필수 제품 및 구성 요소 설치

빌드 서버에서 솔루션을 빌드할 수 있도록 하려면 솔루션에 필요한 모든 제품, 구성 요소 또는 어셈블리를 설치 해야 합니다. 웹 플랫폼 구성 요소를 설치 하기 전에 빌드 서버에 Visual Studio 2010 (모든 버전)을 설치 해야 합니다. 이렇게 하면 핵심 Microsoft Build Engine (MSBuild) 대상 파일 및 WPP (웹 게시 파이프라인) 대상 파일을 빌드 서비스에서 사용할 수 있습니다. 또한 Visual Studio 설치 관리자는 빌드 프로세스의 일부로 웹 패키지를 배포 하려는 경우 필요한 웹 배포를 설치 해야 합니다.

일반적인 웹 플랫폼 구성 요소를 설치 하는 가장 좋은 방법은 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)를 사용 하는 것입니다. 이렇게 하면 각 제품의 최신 버전을 설치 하 고 각 제품에 대 한 필수 구성 요소를 자동으로 검색 하 여 설치 합니다. [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 솔루션의 경우 웹 플랫폼 설치 관리자를 사용 하 여 다음 제품 및 구성 요소를 설치 해야 합니다.

- **.NET Framework 4.0**. 이는이 버전의 .NET Framework에서 빌드된 응용 프로그램을 실행 하는 데 필요 합니다.
- **웹 배포 도구 2.1**이상. 그러면 서버에 웹 배포 및 해당 기본 실행 파일 (Msdeploy.exe)이 설치 됩니다. 이 프로세스의 일부로 웹 Deployment Agent 서비스를 설치 하 고 시작 합니다. 이 서비스를 사용 하면 원격 컴퓨터에서 웹 패키지를 배포할 수 있습니다.
- **ASP.NET MVC 3**. ASP.NET MVC 3 응용 프로그램을 실행 하는 데 필요한 어셈블리를 설치 합니다.

**필요한 제품 및 구성 요소를 설치 하려면**

1. Visual Studio 2010을 설치 합니다. 설치할 기능을 선택 하 라는 메시지가 표시 되 면 다음을 포함 해야 합니다.

    1. 컴파일하는 데 필요한 모든 프로그래밍 언어
    2. Visual Web Developer. 이렇게 하면 WPP 대상이 빌드 서버에 추가 됩니다.

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. Visual Studio 2010 설치가 완료 되 면 [Visual studio 2010 서비스 팩 1](https://go.microsoft.com/?linkid=9805133) (설치 미디어에 아직 포함 되지 않은 경우)을 다운로드 하 여 설치 합니다.

    > [!NOTE]
    > Visual Studio 2010 서비스 팩 1에서는 MSBuild에서 Msdeploy.exe 실행 파일을 찾지 못할 수 있는 버그를 해결 합니다.
3. [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)를 다운로드 하 고 시작 합니다.
4. **웹 플랫폼 설치 관리자 3.0** 창의 위쪽에서 **제품**을 클릭 합니다.
5. 창의 왼쪽에 있는 탐색 창에서 **프레임 워크**를 클릭 합니다.
6. **Microsoft .NET Framework 4** 행에서 .NET Framework이 아직 설치 되지 않은 경우 **추가**를 클릭 합니다.

    > [!NOTE]
    > Windows 업데이트를 통해 .NET Framework 4.0를 이미 설치 했을 수 있습니다. 제품 또는 구성 요소가 이미 설치 되어 있는 경우 웹 플랫폼 설치 관리자는 **추가** 단추를 **설치**된 텍스트로 바꿔이를 표시 합니다.

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. **ASP.NET MVC 3 (Visual Studio 2010)** 행에서 **추가**를 클릭 합니다.
8. 탐색 창에서 **서버**를 클릭 합니다.
9. **웹 배포 도구 2.1** 행에서 **추가**를 클릭 합니다.
10. **Install**을 클릭합니다. 웹 플랫폼 설치 관리자에는 제품&#x2014;목록과 함께 설치 되는 연결 된 종속성&#x2014;이 표시 되며, 사용 조건에 동의 하 라는 메시지가 표시 됩니다.
11. 사용 약관을 검토 하 고 약관에 동의 하는 경우 동의 **함**을 클릭 합니다.
12. 설치가 완료 되 면 **마침**을 클릭 하 고 **웹 플랫폼 설치 관리자 3.0** 창을 닫습니다.

> [!NOTE]
> 배포 프로세스에 nuget.exe 또는 SQLCMD와 같은 도구를 사용 하는 경우 빌드 서버에 설치 되어 있는지 확인 해야 합니다. VSDBCMD는 Visual Studio 도구 이며 일반적으로 Team Foundation Build를 설치할 때 서버에 추가 됩니다. SQLCMD는 SQL Server 도구입니다. [Microsoft SQL Server 2008 R2 기능 팩](https://go.microsoft.com/?linkid=9805134) 페이지에서 독립 실행형 버전의 SQLCMD를 다운로드할 수 있습니다.

## <a name="conclusion"></a>결론

이 시점에서 빌드 서버는 웹 응용 프로그램 프로젝트 빌드 및 배포를 시작할 준비가 되었습니다. 다음 항목인 배포를 [지 원하는 빌드 정의 만들기](creating-a-build-definition-that-supports-deployment.md)에서는 빌드 정의를 만들고 구성 하 여 프로젝트를 빌드 및 배포 하는 시기와 방법을 제어 하는 방법을 설명 합니다.

## <a name="further-reading"></a>추가 참고 자료

팀 빌드 작업에 대 한 일반적인 지침은 [Team Foundation Build 관리](https://msdn.microsoft.com/library/ms252495.aspx)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](adding-content-to-source-control.md)
> [다음](creating-a-build-definition-that-supports-deployment.md)
