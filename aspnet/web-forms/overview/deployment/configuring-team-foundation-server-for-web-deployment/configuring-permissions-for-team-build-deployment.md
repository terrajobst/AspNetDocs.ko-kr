---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: 팀 빌드 배포에 대 한 사용 권한 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 빌드 서버에서 자동화 된 b ...의 일부로 웹 서버와 데이터베이스 서버에 콘텐츠를 배포할 수 있도록 사용 권한을 구성 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 5699f72af6b8d7f18d1a2c631dfdedd63c66e1e6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518507"
---
# <a name="configuring-permissions-for-team-build-deployment"></a>Team Build 배포를 위한 권한 구성

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 빌드 서버에서 자동화 된 빌드 프로세스의 일부로 콘텐츠를 웹 서버와 데이터베이스 서버에 배포할 수 있도록 사용 권한을 구성 하는 방법에 대해 설명 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="task-overview"></a>작업 개요

Team Foundation Server (TFS) 2010 빌드 서비스를 설치 하는 경우 서비스를 실행 하려는 id를 지정 합니다. 기본적으로이 계정은 네트워크 서비스 계정입니다. 또는 도메인 계정을 사용 하 여 실행 되도록 빌드 서비스를 구성할 수 있습니다.

Windows 인증을 필요로 하 고 팀 빌드를 사용 하 여 자동화할 계획인 모든 배포 작업은 빌드 서비스 id를 사용 하 여 실행 됩니다. 따라서 웹 서버 및 데이터베이스 서버에 대 한 필요한 권한을 빌드 서비스 id에 부여 해야 합니다.

> [!NOTE]
> 네트워크 서비스 계정은 컴퓨터 계정을 사용 하 여 다른 컴퓨터에 인증 합니다. 컴퓨터 계정은 * [도메인 이름]\[컴퓨터 이름] * **$** &#x2014;형식으로 사용 합니다 (예: **FABRIKAM\TFSBUILD $** ). 따라서 빌드 서비스가 네트워크 서비스 id를 사용 하 여 실행 되는 경우 빌드 서버에 대 한 컴퓨터 계정 id에 필요한 권한을 부여 해야 합니다.

## <a name="configuring-web-server-permissions"></a>웹 서버 권한 구성

[웹 배포에 대 한 적절 한 접근 방식 선택](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)에 설명 된 대로 원격 웹 서버에 웹 패키지를 배포 하려는 경우 두 가지 주요 방법으로 사용할 수 있습니다.

- 대상 서버에서 *웹 Deployment Agent 서비스* (원격 에이전트 라고도 함)를 대상으로 지정 하 여 원격 위치에서 응용 프로그램을 배포 합니다.
- 대상 서버에서 *인터넷 정보 서비스* (*IIS) 웹 배포 처리기* 를 대상으로 지정 하 여 원격 위치에서 응용 프로그램을 배포 합니다.

이 경우 원격 에이전트에는 두 가지 주요 제한 사항이 있습니다.

- 원격 에이전트는 NTLM 인증만 지원 합니다. 즉, 배포는 빌드 서비스 id&#x2014;를 사용 해야 하며 다른 계정을 가장할 수 없습니다.
- 원격 에이전트를 사용 하려면 배포를 수행 하는 계정이 대상 서버의 관리자 여야 합니다.

이러한 두 가지 제한 사항은 자동화 된 팀 빌드 배포에 대 한 원격 에이전트 접근 방식이 바람직하지 않도록 합니다. 이 접근 방식을 사용 하려면 모든 대상 웹 서버에서 빌드 서비스 계정을 관리자로 설정 해야 합니다.

이와 달리 웹 배포 처리기 방법은 다양 한 이점을 제공 합니다.

- 웹 배포 처리기는 HTTPS를 통한 기본 인증을 지원 하므로 대체 계정의 자격 증명을 IIS 웹 배포 도구 (웹 배포)에 전달할 수 있습니다.
- 관리자가 아닌 사용자가 웹 배포 처리기를 사용 하 여 특정 IIS 웹 사이트에 콘텐츠를 배포할 수 있도록 대상 웹 서버를 구성할 수 있습니다.

따라서 팀 빌드에서 웹 패키지 배포를 자동화 하는 경우 웹 배포 처리기를 대상으로 하는 것이 좋습니다. 다음은 권장 되는 프로세스입니다.

1. 배포에 사용할 권한이 낮은 도메인 계정을 만듭니다.
2. [웹 배포 게시용 웹 서버 구성 (웹 배포 처리기)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)에 설명 된 대로 웹 배포 처리기를 구성 하 고 특정 IIS 웹 사이트에 콘텐츠를 배포 하는 데 필요한 권한을 계정에 부여 합니다.
3. 웹 배포를 호출 하 웹 배포 고, 기본 인증을 사용 하 고 사용자가 만든 도메인 계정의 자격 증명을 제공 하 여 배포를 수행 합니다.

[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션에서는 환경 관련 프로젝트 파일에서 인증 유형 (기본 또는 NTLM), 웹 배포 자격 증명 및 끝점 주소 (원격 에이전트 또는 웹 배포 처리기)를 지정 합니다. 이러한 값은 프로젝트 파일이 실행 될 때 웹 배포 명령을 작성 하 고 실행 하는 데 사용 됩니다. 자세한 내용은 [웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)를 참조 하세요.

사용 권한을 구성 하는 방법을 비롯 하 여 웹 배포 처리기를 구성 하는 방법에 대 한 자세한 내용은 [웹 배포 게시용 웹 서버 구성 (웹 배포 처리기)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)을 참조 하세요. 원격 에이전트를 구성 하는 방법에 대 한 자세한 내용은 [웹 배포 게시용 웹 서버 구성 (원격 에이전트)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)을 참조 하세요.

## <a name="configuring-database-server-permissions"></a>데이터베이스 서버 사용 권한 구성

데이터베이스를 SQL Server에 배포 하려면 다음을 수행 해야 합니다.

- SQL Server 인스턴스에서 배포 계정에 대 한 로그인을 만듭니다.
- SQL Server 인스턴스에 대 한 로그인 **DBCreator** 권한을 부여 합니다.
- 초기 배포 후 로그인을 대상 데이터베이스의 **db\_owner** 역할에 추가 합니다. 후속 배포에서는 새 데이터베이스를 만드는 대신 기존 데이터베이스를 수정 하기 때문에이 작업이 필요 합니다.

NTLM 인증 또는 SQL Server 인증을 사용 하 여 SQL Server 인스턴스에 인증할 수 있습니다.

- NTLM 인증을 사용 하는 경우 위에 설명 된 사용 권한을 빌드 서비스 계정에 부여 해야 합니다.
- SQL Server 인증을 사용 하는 경우 위에 설명 된 사용 권한을 SQL Server 계정에 부여 해야 합니다. 또한 데이터베이스를 배포 하는 데 사용 하는 연결 문자열에 SQL Server 사용자 이름 및 암호를 포함 해야 합니다.

데이터베이스 배포에 대 한 사용 권한을 구성 하는 방법에 대 한 단계별 정보는 [웹 배포 게시용 데이터베이스 서버 구성](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)을 참조 하세요.

## <a name="conclusion"></a>결론

이 시점에서 팀 빌드에서 웹 응용 프로그램 및 데이터베이스 배포를 자동화 하는 경우 필요한 인증 옵션과 함께 필요한 사용 권한을 이해 해야 합니다. 또한 IIS 웹 서버 및 SQL Server 데이터베이스 서버에 필요한 권한을 구현할 수 있어야 합니다.

## <a name="further-reading"></a>추가 참고 자료

원격 배포를 지원 하도록 Windows server 환경을 구성 하는 방법에 대 한 자세한 내용은 [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)을 참조 하세요.

> [!div class="step-by-step"]
> [이전](deploying-a-specific-build.md)
