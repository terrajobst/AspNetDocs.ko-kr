---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: 웹 배포 게시용 데이터베이스 서버 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 배포 및 게시를 지원 하도록 SQL Server 2008 R2 데이터베이스 서버를 구성 하는 방법에 대해 설명 합니다. 이 항목에서 설명 하는 작업은 공동 작업입니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: ade3c1ba1c470092f512436f39b8831458408c2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515243"
---
# <a name="configuring-a-database-server-for-web-deploy-publishing"></a>웹 배포 게시용 데이터베이스 서버 구성

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 웹 배포 및 게시를 지원 하도록 SQL Server 2008 R2 데이터베이스 서버를 구성 하는 방법에 대해 설명 합니다.
> 
> 이 항목에서 설명 하는 작업은 웹 서버가 IIS 웹&#x2014;배포 도구 (웹 배포) 원격 에이전트 서비스, 웹 배포 처리기 또는 오프 라인 배포를 사용 하도록 구성 되어 있는지, 아니면 응용 프로그램이 단일 웹 서버 또는 서버 팜에서 실행 되 고 있는지에 관계 없이 모든 배포 시나리오에 공통적으로 적용 됩니다. 데이터베이스를 배포 하는 방법은 보안 요구 사항 및 기타 고려 사항에 따라 달라질 수 있습니다. 예를 들어 예제 데이터를 포함 하거나 포함 하지 않고 데이터베이스를 배포 하 고 배포 후 사용자 역할 매핑을 배포 하거나 수동으로 구성할 수 있습니다. 그러나 데이터베이스 서버를 구성 하는 방식은 동일 하 게 유지 됩니다.

웹 배포를 지원 하도록 데이터베이스 서버를 구성 하기 위해 추가 제품 또는 도구를 설치할 필요가 없습니다. 데이터베이스 서버와 웹 서버가 서로 다른 컴퓨터에서 실행 되는 경우 다음을 수행 해야 합니다.

- TCP/IP를 사용 하 여 SQL Server 통신 하도록 허용 합니다.
- 모든 방화벽을 통해 SQL Server 트래픽을 허용 합니다.
- 웹 서버 컴퓨터 계정에 SQL Server 로그인을 제공 합니다.
- 필요한 데이터베이스 역할에 컴퓨터 계정 로그인을 매핑합니다.
- 배포를 실행 하는 계정에 SQL Server 로그인 및 데이터베이스 작성자 권한을 부여 합니다.
- 반복 배포를 지원 하려면 배포 계정 로그인을 **db\_소유자** 데이터베이스 역할에 매핑합니다.

이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여 줍니다. 이 항목의 작업 및 연습에서는 Windows Server 2008 r 2에서 실행 되는 SQL Server 2008 R2의 기본 인스턴스로 시작 한다고 가정 합니다. 계속 하기 전에 다음을 확인 하십시오.

- Windows Server 2008 R2 서비스 팩 1 및 사용 가능한 모든 업데이트가 설치 되어 있습니다.
- 서버가 도메인에 가입 되어 있습니다.
- 서버에 고정 IP 주소가 있습니다.
- SQL Server 2008 R2 서비스 팩 1 및 사용 가능한 모든 업데이트가 설치 되어 있습니다.

SQL Server 인스턴스는 SQL Server 설치에 자동으로 포함 되는 **데이터베이스 엔진 Services** 역할만 포함 하면 됩니다. 그러나 쉽게 구성 및 유지 관리를 위해 **관리 도구-기본** 및 **관리 도구-전체** 서버 역할을 포함 하는 것이 좋습니다.

> [!NOTE]
> 컴퓨터를 도메인에 가입 하는 방법에 대 한 자세한 내용은 [도메인에 컴퓨터 가입 및 로그온](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)을 참조 하세요. 고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 [고정 Ip 주소 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)을 참조 하세요. SQL Server 설치에 대 한 자세한 내용은 [SQL Server 2008 R2 설치](https://technet.microsoft.com/library/bb500395.aspx)를 참조 하세요.

## <a name="enable-remote-access-to-sql-server"></a>SQL Server에 대 한 원격 액세스 사용

SQL Server은 TCP/IP를 사용 하 여 원격 컴퓨터와 통신 합니다. 데이터베이스 서버와 웹 서버가 서로 다른 컴퓨터에 있는 경우 다음을 수행 해야 합니다.

- TCP/IP를 통한 통신을 허용 하도록 SQL Server 네트워킹 설정을 구성 합니다.
- SQL Server 인스턴스가 사용 하는 포트에서 TCP 트래픽 (일부 경우에는 UDP (사용자 데이터 그램 프로토콜) 트래픽)을 허용 하도록 하드웨어 또는 소프트웨어 방화벽을 구성 합니다.

SQL Server TCP/IP를 통해 통신할 수 있도록 설정 하려면 SQL Server 구성 관리자를 사용 하 여 SQL Server 인스턴스에 대 한 네트워크 구성을 변경 하십시오.

**TCP/IP를 사용 하 여 SQL Server 통신할 수 있도록 설정 하려면**

1. **시작** 메뉴에서 **모든 프로그램**을 가리키고 **Microsoft SQL Server 2008 R2**, **구성 도구**를 차례로 클릭 한 다음 **SQL Server 구성 관리자**을 클릭 합니다.
2. 트리 뷰 창에서 **SQL Server 네트워크 구성**을 확장 한 다음 **MSSQLSERVER에 대 한 프로토콜**을 클릭 합니다.

   > [!NOTE]
   > SQL Server의 인스턴스를 여러 개 설치한 경우 각 인스턴스에 대 한<em>[instance name]</em> 항목 <strong>에 대 한 프로토콜이</strong>표시 됩니다. 인스턴스 단위로 네트워크 설정을 구성 해야 합니다.
3. 세부 정보 창에서 **tcp/ip** 행을 마우스 오른쪽 단추로 클릭 한 다음 **사용**을 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. **경고** 대화 상자에서 **확인**을 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. 새 네트워크 구성이 적용 되려면 먼저 MSSQLSERVER 서비스를 다시 시작 해야 합니다. 명령 프롬프트, 서비스 콘솔 또는 SQL Server Management Studio에서 수행할 수 있습니다. 이 절차에서는 SQL Server Management Studio을 사용 합니다.
6. SQL Server 구성 관리자를 닫습니다.
7. **시작** 메뉴에서 **모든 프로그램**을 가리키고 **Microsoft SQL Server 2008 R2**를 클릭 한 다음 **SQL Server Management Studio**를 클릭 합니다.
8. **서버에 연결** 대화 상자의 **서버 이름** 상자에 데이터베이스 서버의 이름을 입력 한 다음 **연결**을 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. **개체 탐색기** 창에서 부모 서버 노드 (예: **배치한**)를 마우스 오른쪽 단추로 클릭 한 다음 **다시 시작**을 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. **Microsoft SQL Server Management Studio** 대화 상자에서 **예**를 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. 서비스가 다시 시작 되 면 SQL Server Management Studio를 닫습니다.

방화벽을 통해 SQL Server 트래픽을 허용 하려면 먼저 SQL Server 인스턴스가 사용 하는 포트를 알고 있어야 합니다. SQL Server 인스턴스를 만들고 구성 하는 방법에 따라 달라 집니다.

- SQL Server의 *기본 인스턴스* 는 TCP 포트 1433에서 요청을 수신 하 고 요청에 응답 합니다.
- SQL Server의 *명명 된 인스턴스* 는 동적으로 할당 된 TCP 포트에서 요청을 수신 하 고 요청에 응답 합니다.
- SQL Server Browser 서비스를 사용 하는 경우 클라이언트는 UDP 포트 1434에서 서비스를 쿼리하여 특정 SQL Server 인스턴스에 사용할 TCP 포트를 찾을 수 있습니다. 그러나이 서비스는 보안상의 이유로 사용 하지 않는 경우가 많습니다.

SQL Server의 기본 인스턴스를 사용 하 고 있다고 가정 하 고 트래픽을 허용 하도록 방화벽을 구성 해야 합니다.

| Direction | 보낸 포트 | 포트에 | 포트 유형 |
| --- | --- | --- | --- |
| 인바운드 | 모두 | 1433 | TCP |
| 아웃바운드 | 1433 | 모두 | TCP |

> [!NOTE]
> 기술적으로 클라이언트 컴퓨터는 1024과 5000 사이의 임의로 할당 된 TCP 포트를 사용 하 여 SQL Server와 통신 하 고 그에 따라 방화벽 규칙을 제한할 수 있습니다. SQL Server 포트 및 방화벽에 대 한 자세한 내용은 [방화벽을 통해 SQL과 통신 하는 데 필요한 tcp/ip 포트 번호](https://go.microsoft.com/?linkid=9805125) 및 [방법: 특정 Tcp 포트에서 수신 하도록 서버 구성 (SQL Server 구성 관리자)](https://msdn.microsoft.com/library/ms177440.aspx)을 참조 하세요.

대부분의 Windows Server 환경에서는 데이터베이스 서버에서 Windows 방화벽을 구성 해야 할 가능성이 높습니다. 기본적으로 Windows 방화벽은 규칙에서 특별히 금지 하지 않는 한 모든 아웃 바운드 트래픽을 허용 합니다. 웹 서버에서 데이터베이스에 연결할 수 있도록 하려면 SQL Server 인스턴스에서 사용 하는 포트 번호에 TCP 트래픽을 허용 하는 인바운드 규칙을 구성 해야 합니다. SQL Server의 기본 인스턴스를 사용 하는 경우 다음 절차를 사용 하 여이 규칙을 구성할 수 있습니다.

**기본 SQL Server 인스턴스와의 통신을 허용 하도록 Windows 방화벽을 구성 하려면**

1. 데이터베이스 서버의 **시작** 메뉴에서 **관리 도구**를 가리킨 다음 **고급 보안이 포함 된 Windows 방화벽**을 클릭 합니다.
2. 트리 뷰 창에서 **인바운드 규칙**을 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. **작업** 창의 **인바운드 규칙**에서 **새 규칙**을 클릭 합니다.
4. 새 인바운드 규칙 마법사의 **규칙 유형** 페이지에서 **포트**를 선택 하 고 **다음**을 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. **프로토콜 및 포트** 페이지에서 **TCP** 가 선택 되어 있는지 확인 하 고, **특정 로컬 포트** 상자에 **1433**을 입력 한 후 **다음**을 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. **작업** 페이지에서 **연결 허용** 을 선택한 상태로 두고 **다음**을 클릭 합니다.
7. **프로필** 페이지에서 **도메인** 을 선택 된 채로 두고 **개인** 및 **공용** 확인란의 선택을 취소 한 후 **다음**을 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. **이름** 페이지에서 규칙에 적절 한 설명이 포함 된 이름 (SQL Server 예: **기본 인스턴스 – 네트워크 액세스**)을 지정한 다음 **마침**을 클릭 합니다.

SQL Server에 대 한 Windows 방화벽 구성에 대 한 자세한 내용은 특히 비표준 또는 동적 포트를 통해 SQL Server와 통신 해야 하 [는 경우 방법: 데이터베이스 엔진 액세스를 위해 Windows 방화벽 구성](https://technet.microsoft.com/library/ms175043.aspx)을 참조 하세요.

## <a name="configure-logins-and-database-permissions"></a>로그인 및 데이터베이스 권한 구성

웹 응용 프로그램을 인터넷 정보 서비스 (IIS)에 배포 하는 경우 응용 프로그램은 응용 프로그램 풀의 id를 사용 하 여 실행 됩니다. 도메인 환경에서 응용 프로그램 풀 id는 네트워크 리소스에 액세스 하기 위해 실행 되는 서버의 컴퓨터 계정을 사용 합니다. 컴퓨터 계정은 <em>[도메인 이름]</em><strong>\</strong ><em>[컴퓨터 이름]</em> <strong>$</strong> &#x2014;를 사용 합니다 (예: <strong>FABRIKAM\TESTWEB1 $</strong>). 웹 응용 프로그램이 네트워크를 통해 데이터베이스에 액세스할 수 있게 하려면 다음을 수행 해야 합니다.

- 웹 서버 컴퓨터 계정에 대 한 로그인을 SQL Server 인스턴스에 추가 합니다.
- 필요한 데이터베이스 역할 (일반적으로 **db\_datareader** 및 **db\_datawriter 여부**)에 컴퓨터 계정 로그인을 매핑합니다.

웹 응용 프로그램이 단일 서버가 아닌 서버 팜에서 실행 되는 경우 서버 팜의 모든 웹 서버에 대해 이러한 절차를 반복 해야 합니다.

> [!NOTE]
> 응용 프로그램 풀 id 및 네트워크 리소스에 액세스 하는 방법에 대 한 자세한 내용은 [응용 프로그램 풀 id](https://go.microsoft.com/?linkid=9805123)를 참조 하세요.

이러한 작업은 다양 한 방법으로 사용할 수 있습니다. 로그인을 만들려면 다음 중 하나를 수행할 수 있습니다.

- Transact-sql 또는 SQL Server Management Studio를 사용 하 여 데이터베이스 서버에서 수동으로 로그인을 만듭니다.
- Visual Studio에서 SQL Server 2008 서버 프로젝트를 사용 하 여 로그인을 만들고 배포 합니다.

SQL Server 로그인은 데이터베이스 수준 개체가 아닌 서버 수준 개체 이므로 배포 하려는 데이터베이스에 종속 되지 않습니다. 따라서 언제 든 지 로그인을 만들 수 있으며 데이터베이스 배포를 시작 하기 전에 데이터베이스 서버에서 수동으로 로그인을 만드는 것이 가장 쉬운 방법입니다. 다음 절차를 사용 하 여 SQL Server Management Studio에서 로그인을 만들 수 있습니다.

**웹 서버 컴퓨터 계정에 대 한 SQL Server 로그인을 만들려면**

1. 데이터베이스 서버의 **시작** 메뉴에서 **모든 프로그램**을 가리키고 **Microsoft SQL Server 2008 R2**를 클릭 한 다음 **SQL Server Management Studio**를 클릭 합니다.
2. **서버에 연결** 대화 상자의 **서버 이름** 상자에 데이터베이스 서버의 이름을 입력 한 다음 **연결**을 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. **개체 탐색기** 창에서 **보안**을 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 가리킨 다음 **로그인**을 클릭 합니다.
4. **로그인-새로 만들기** 대화 상자의 **로그인 이름** 상자에 웹 서버 컴퓨터 계정 (예: **FABRIKAM\TESTWEB1 $** )의 이름을 입력 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. **확인**을 클릭합니다.

이 시점에서 데이터베이스 서버는 웹 배포 게시할 준비가 된 것입니다. 그러나 배포 하는 모든 솔루션은 필요한 데이터베이스 역할에 컴퓨터 계정 로그인을 매핑할 때까지 작동 하지 않습니다. 데이터베이스 역할에 로그인을 매핑하면 데이터베이스를 배포한 후에도 역할을 매핑할 수 없으므로 훨씬 더 고려해 야 합니다. 컴퓨터 계정 로그인을 필요한 데이터베이스 역할에 매핑하려면 다음 중 하나를 수행할 수 있습니다.

- 처음으로 데이터베이스를 배포한 후 데이터베이스 역할을 로그인에 수동으로 할당 합니다.
- 배포 후 스크립트를 사용 하 여 데이터베이스 역할을 로그인에 할당 합니다.

로그인 및 데이터베이스 역할 매핑을 자동화 하는 방법에 대 한 자세한 내용은 [테스트 환경에 데이터베이스 역할 멤버 자격 배포](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)를 참조 하세요. 또는 다음 절차를 사용 하 여 필요한 데이터베이스 역할에 컴퓨터 계정 로그인을 수동으로 매핑할 수 있습니다. 데이터베이스를 배포한 *후에* 는이 절차를 수행할 수 없습니다.

**데이터베이스 역할을 웹 서버 컴퓨터 계정 로그인에 매핑하려면**

1. 이전 처럼 SQL Server Management Studio를 엽니다.
2. **개체 탐색기** 창에서 **보안** 노드를 확장 하 고 **로그인** 노드를 확장 한 다음 컴퓨터 계정 로그인 (예: **FABRIKAM\TESTWEB1 $** )을 두 번 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. **로그인 속성** 대화 상자에서 **사용자 매핑**을 클릭 합니다.
4. **이 로그인으로 매핑된 사용자** 테이블에서 데이터베이스 이름 (예: **연락처 관리자**)을 선택 합니다.
5. **데이터베이스 역할 멤버 자격:** *[데이터베이스 이름]* 목록에서 필요한 사용 권한을 선택 합니다. Contact Manager 샘플 솔루션의 경우 **db\_datareader** 및 **db\_datawriter 여부** 역할을 선택 해야 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. **확인**을 클릭합니다.

데이터베이스 역할을 수동으로 매핑하는 것이 테스트 환경에 적합 한 경우를 제외 하 고는 스테이징 또는 프로덕션 환경에 대 한 자동화 되거나 한 번 클릭으로 배포 하는 것이 더 바람직하지 않습니다. 이러한 종류의 작업 자동화에 대 한 자세한 내용은 배포 후 스크립트를 사용 하 여 [데이터베이스 역할 멤버 자격을 테스트 환경에 배포](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)에서 확인할 수 있습니다.

> [!NOTE]
> 서버 프로젝트 및 데이터베이스 프로젝트에 대 한 자세한 내용은 [Visual Studio 2010 SQL Server 데이터베이스 프로젝트](https://msdn.microsoft.com/library/ff678491.aspx)를 참조 하세요.

## <a name="configure-permissions-for-the-deployment-account"></a>배포 계정에 대 한 사용 권한 구성

배포를 실행 하는 데 사용 하는 계정이 SQL Server 관리자가 아닌 경우이 계정에 대 한 로그인도 만들어야 합니다. 데이터베이스를 만들려면 계정이 **dbcreator** 서버 역할의 멤버 이거나 이와 동등한 권한이 있어야 합니다.

> [!NOTE]
> 웹 배포 또는 VSDBCMD를 사용 하 여 데이터베이스를 배포 하는 경우 Windows 자격 증명 또는 SQL Server 자격 증명을 사용할 수 있습니다 (SQL Server 인스턴스가 혼합 모드 인증을 지원 하도록 구성 된 경우). 다음 절차에서는 Windows 자격 증명을 사용 하려는 경우를 가정 하지만 배포를 구성할 때 연결 문자열에 SQL Server 사용자 이름 및 암호를 지정 하는 것을 중지 하지 않습니다.

**배포 계정에 대 한 사용 권한을 설정 하려면**

1. 이전 처럼 SQL Server Management Studio를 엽니다.
2. **개체 탐색기** 창에서 **보안**을 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 가리킨 다음 **로그인**을 클릭 합니다.
3. **로그인-새로 만들기** 대화 상자의 **로그인 이름** 상자에 배포 계정의 이름 (예: **FABRIKAM\matt**)을 입력 합니다.
4. **페이지 선택** 창에서 **서버 역할**을 클릭 합니다.
5. **Dbcreator**을 선택 하 고 **확인**을 클릭 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

후속 배포를 지원 하려면 첫 번째 배포 후 데이터베이스의 **db\_owner** 역할에 배포 계정을 추가 해야 합니다. 이후 배포에서는 새 데이터베이스를 만드는 대신 기존 데이터베이스의 스키마를 수정 하는 것입니다. 이전 섹션에서 설명한 것 처럼 데이터베이스를 만들 때까지 데이터베이스 역할에 사용자를 추가할 수 없습니다.

**배포 계정 로그인을 db\_소유자 데이터베이스 역할에 매핑하려면**

1. 이전 처럼 SQL Server Management Studio를 엽니다.
2. **개체 탐색기** 창에서 **보안** 노드를 확장 하 고 **로그인** 노드를 확장 한 다음 컴퓨터 계정 로그인 (예: **FABRIKAM\matt**)을 두 번 클릭 합니다.
3. **로그인 속성** 대화 상자에서 **사용자 매핑**을 클릭 합니다.
4. **이 로그인으로 매핑된 사용자** 테이블에서 데이터베이스 이름 (예: **연락처 관리자**)을 선택 합니다.
5. **데이터베이스 역할 멤버 자격:** *[데이터베이스 이름]* 목록에서 **db\_소유자** 역할을 선택 합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. **확인**을 클릭합니다.

## <a name="conclusion"></a>결론

이제 데이터베이스 서버에서 원격 데이터베이스 배포를 수락 하 고 원격 IIS 웹 서버에서 데이터베이스에 액세스할 수 있도록 준비 해야 합니다. 데이터베이스를 배포 하 고 사용 하기 전에 다음과 같은 주요 사항을 확인 해야 할 수 있습니다.

- 원격 TCP/IP 연결을 허용 하도록 SQL Server를 구성 했습니까?
- SQL Server 트래픽을 허용 하도록 방화벽을 구성 했습니까?
- SQL Server에 액세스 하는 모든 웹 서버에 대 한 컴퓨터 계정 로그인을 만들었는지 여부
- 데이터베이스 배포에 사용자 역할 매핑을 만들기 위한 스크립트가 포함 되어 있습니까? 아니면 데이터베이스를 처음 배포한 후 수동으로 만들어야 하나요?
- 배포 계정에 대 한 로그인을 만들고 **dbcreator** 서버 역할에 추가 했습니까?

## <a name="further-reading"></a>추가 참고 자료

데이터베이스 프로젝트 배포에 대 한 지침은 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)를 참조 하세요. 배포 후 스크립트를 실행 하 여 데이터베이스 역할 멤버 자격을 만드는 방법에 대 한 지침은 [데이터베이스 역할 멤버 자격을 테스트 환경에 배포](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)를 참조 하세요. 멤버 자격 데이터베이스가 야기 하는 고유한 배포 문제를 충족 하는 방법에 대 한 지침은 [엔터프라이즈 환경에 멤버 자격 데이터베이스 배포](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [다음](creating-a-server-farm-with-the-web-farm-framework.md)
