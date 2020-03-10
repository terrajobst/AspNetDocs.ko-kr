---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: 웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 WFF (웹 팜 프레임 워크) 2.0를 사용 하 여 서버 컬렉션에서 웹 서버 팜을 만들고 구성 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: 204996514bed336e60ab77f184a923f04e7e2bba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517499"
---
# <a name="creating-a-server-farm-with-the-web-farm-framework"></a>웹 팜 프레임워크를 사용하여 서버 팜 만들기

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 WFF (웹 팜 프레임 워크) 2.0를 사용 하 여 서버 컬렉션에서 웹 서버 팜을 만들고 구성 하는 방법에 대해 설명 합니다.

WFF를 사용 하면 부하 분산 된 여러 웹 서버에서 웹 플랫폼 제품과 구성 요소, 웹 응용 프로그램, 웹 사이트 및 구성 설정을 동기화 할 수 있습니다. 스테이징 및 프로덕션 환경과 같은 웹 서버가 두 개 이상 필요한 시나리오에서는 배포 및 구성 프로세스를 크게 간소화할 수 있습니다. 단일 서버&#x2014;에 *기본 서버*&#x2014;에 웹 응용 프로그램을 배포할 수 있으며, wff는 서버 팜의 다른 모든 웹 서버에서 해당 웹 응용 프로그램을 자동으로 복제 합니다.

## <a name="understanding-the-web-farm-framework"></a>웹 팜 프레임 워크 이해

WFF 2.0을 사용 하 여 웹 서버 그룹에 콘텐츠를 프로 비전, 관리 및 배포할 수 있습니다. WFF 배포는 다음 세 가지 주요 서버 역할로 구성 됩니다.

- *컨트롤러 서버*입니다. 이 서버를 사용 하 여 WFF 서버 팜을 만들고 구성 합니다. 컨트롤러 서버는 웹 플랫폼 구성 요소, 구성 설정 및 서버 팜의 웹 서버 간 응용 프로그램의 동기화를 관리 합니다. 컨트롤러 서버에 WFF 2.0을 설치 하면 컨트롤러 서버는 서버 팜의 각 서버에 WFF 에이전트를 설치 합니다. 컨트롤러 서버는 개념적으로 모든 WFF 서버 팜에 속하며 단일 컨트롤러 서버는 여러 서버 팜을 관리할 수 있습니다. 이 시나리오에서는 단일 WFF 컨트롤러 서버를 사용 하 여 준비 서버 팜과 프로덕션 서버 팜을 만들고 관리 합니다.
- *주 서버*입니다. 각 WFF 서버 팜은 단일 주 서버를 포함 합니다. 웹 플랫폼 구성 요소를 설치 하거나 주 서버에 응용 프로그램을 배포 하는 경우 WFF는 서버 팜의 다른 모든 서버에 변경 내용을 동기화 합니다.
- *보조 서버*입니다. 각 WFF 서버 팜은 하나 이상의 보조 서버를 포함 합니다. 주 서버에서 수행 하는 모든 변경 내용은 서버 팜 내의 모든 보조 서버에 복제 됩니다.

이러한 서버 역할이 Fabrikam, Inc. 스테이징 및 프로덕션 환경과 어떻게 관련 되는지를 보여 줍니다.

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

이 시나리오에서 스테이징 환경 및 프로덕션 환경은 둘 다 WFF 서버 팜으로 구성 됩니다. 단일 WFF 컨트롤러 서버는 두 팜을 모두 관리 합니다. 각 서버 팜 내에서 주 서버에 대 한 모든 변경 내용은 모든 보조 서버에 복제 됩니다.

스테이징 및 프로덕션 환경 구성을 시작 하기 전에 다음 문서를 참조 하 여 WFF 2.0의 주요 개념을 숙지 하는 것이 좋습니다.

- [IIS 7 용 웹 팜 프레임 워크 2.0 개요](https://go.microsoft.com/?linkid=9805126)
- [IIS 7 용 웹 팜 프레임 워크 2.0를 사용 하 여 서버 팜 설정](https://go.microsoft.com/?linkid=9805127)
- [IIS 7 용 웹 팜 프레임 워크 2.0에 대 한 시스템 및 플랫폼 요구 사항](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a>작업 개요

이 항목의 작업 및 연습을 완료 하려면 하나 이상의 서버&#x2014;에 wff 컨트롤러 1 개, 서버 팜의 기본 웹 서버 하나, 서버 팜에 대 한 하나 이상의 보조 웹 서버가 필요 합니다. 언제 든 지 WFF 서버 팜에 보조 서버를 더 추가할 수 있습니다. 개략적인 수준에서 스테이징 또는 프로덕션 환경에 대 한 WFF 서버 팜을 만들고 구성 하려면 다음을 수행 해야 합니다.

- 인터넷 정보 서비스 (IIS) 7.5 및 WFF 2.0를 설치 하 여 컨트롤러 서버를 만듭니다.
- 일반 관리자 계정을 만들고 방화벽 예외를 구성 하 여 주 서버와 보조 서버를 준비 합니다.
- 컨트롤러 서버에서 IIS 관리자를 사용 하 여 서버 팜을 구성 합니다.
- IIS ARR (응용 프로그램 요청 라우팅) 또는 대체 부하 분산 기술을 사용 하 여 부하 분산을 구성 합니다.

이 항목의 작업 및 연습에서는 Windows Server 2008 r 2를 실행 하는 클린 서버 빌드를 시작 한다고 가정 합니다. 시작 하기 전에 각 서버에 대해 다음을 확인 합니다.

- Windows Server 2008 R2 서비스 팩 1 및 사용 가능한 모든 업데이트가 설치 되어 있습니다.
- 서버가 도메인에 가입 되어 있습니다.
- 서버에 고정 IP 주소가 있습니다.

> [!NOTE]
> 컴퓨터를 도메인에 가입 하는 방법에 대 한 자세한 내용은 [도메인에 컴퓨터 가입 및 로그온](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)을 참조 하세요. 고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 [고정 Ip 주소 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)을 참조 하세요.

## <a name="create-the-wff-controller-server"></a>WFF 컨트롤러 서버 만들기

WFF 컨트롤러 서버를 만들려면 IIS 7 이상 및 WFF 2.0 이상을 설치 해야 합니다. 내부적으로 WFF는 IIS 웹 배포 도구 (웹 배포) 2.x를 사용 하 여 팜의 서버를 동기화 합니다. 웹 플랫폼 설치 관리자를 사용 하 여 WFF를 설치 하는 경우 설치 관리자에서 자동으로 웹 배포를 다운로드 하 여 설치 합니다.

**WFF 컨트롤러 서버를 만들려면**

1. [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9739157)를 다운로드 하 여 설치 합니다.
2. **웹 플랫폼 설치 관리자 3.0** 창의 위쪽에서 **제품**을 클릭 합니다.
3. 창의 왼쪽에 있는 탐색 창에서 **서버**를 클릭 합니다.
4. **IIS 7 권장 구성** 행에서 **추가**를 클릭 합니다.
5. <strong>웹 팜 프레임 워크 2에서.</strong> <em>x</em> 행에서 <strong>추가</strong>를 클릭 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. **Install**을 클릭합니다. 웹 플랫폼 설치 관리자는 다양 한 다른 종속성과 함께 웹 배포 도구를 설치 목록에 추가 했습니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. 사용 약관을 검토 하 고 약관에 동의 하는 경우 동의 **함**을 클릭 합니다.
8. 설치가 완료 되 면 **마침**을 클릭 하 고 **웹 플랫폼 설치 관리자 3.0** 창을 닫습니다.

## <a name="configure-the-primary-and-secondary-servers"></a>주 서버 및 보조 서버 구성

WFF 서버 팜을 만들기 전에 팜을 구성 하는 웹 서버에서 몇 가지 준비 작업을 완료 해야 합니다.

- 방화벽 예외를 추가 하 여 **핵심 네트워킹**, **원격 관리**및 **파일 및 프린터 공유** 기능이 wff 컨트롤러 서버와 통신할 수 있도록 합니다.
- Active Directory에서 도메인 계정 (예: **FABRIKAM\stagingfarm**)을 만들고 각 서버의 로컬 관리자 그룹에 추가 합니다. 서버 팜을 만들 때이 계정을 서버 팜 관리자 계정으로 사용 합니다.

Windows 방화벽에서 이러한 방화벽 예외를 구성 하는 방법에 대 한 자세한 내용은 [IIS 7 용 웹 팜 프레임 워크 2.0에 대 한 시스템 및 플랫폼 요구 사항](https://go.microsoft.com/?linkid=9805128)을 참조 하세요. 다른 방화벽 시스템은 제품 설명서를 참조 하십시오.

Windows Server 2008 r 2의 로컬 관리자 그룹에 도메인 계정을 추가 하려면 다음 절차를 사용할 수 있습니다. 즉, 서버 팜에&#x2014;추가 하려는 모든 서버에서이 절차를 수행 해야 합니다. 즉, 주 서버와 각 보조 서버의 로컬 관리자 그룹에 동일한 도메인 계정을 추가 합니다.

**로컬 관리자 그룹에 도메인 계정을 추가 하려면**

1. **시작** 메뉴에서 **관리 도구**를 가리킨 다음 **서버 관리자**를 클릭 합니다.
2. **서버 관리자** 창의 트리 뷰 창에서 **구성**, **로컬 사용자 및 그룹**을 차례로 확장 한 다음 **그룹**을 클릭 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. **그룹** 창에서 **관리자**를 두 번 클릭 합니다.
4. **관리자 속성** 대화 상자에서 **추가**를 클릭 합니다.
5. **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에서 도메인 계정 (예: **FABRIKAM\stagingfarm**)을 입력 하거나 검색 한 다음 **확인**을 클릭 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. **관리자 속성** 대화 상자에서 **확인**을 클릭 합니다.

서버를 서버 팜에 추가할 준비가 되었습니다. 주 서버의 경우 두 경우 모두 서버 팜을&#x2014;만들기 전이나 후에 응용 프로그램 요구 사항을 충족 하도록 서버를 구성할 수 있습니다. wff는 동일한 제품, 구성 요소 또는 구성을 보조 서버에 배포 하 여 서버를 동기화 합니다. 간단히 하기 위해이 자습서에서는 서버 팜 만들기를 완료할 때 주 서버를 구성 한다고 가정 합니다.

## <a name="create-the-wff-server-farm"></a>WFF 서버 팜 만들기

이 시점에서 모든 서버가 WFF 서버 팜에 추가 될 준비가 되었습니다.

- 컨트롤러 서버에 WFF를 설치 했습니다.
- 기본 및 보조 웹 서버에서 방화벽 예외를 구성 했습니다.
- 기본 및 보조 웹 서버의 로컬 관리자 그룹에 도메인 계정을 추가 했습니다.

다음 단계는 WFF에서 서버 팜을 만드는 것입니다. 이 작업은 WFF 컨트롤러 서버의 IIS 관리자에서 수행할 수 있습니다.

**WFF 서버 팜을 만들려면**

1. WFF 컨트롤러 서버의 **시작** 메뉴에서 **관리 도구**를 가리킨 다음 **인터넷 정보 서비스 (IIS) 관리자**를 클릭 합니다.
2. **연결** 창에서 로컬 서버 노드를 확장 하 고 **서버 팜**을 마우스 오른쪽 단추로 클릭 한 다음 **서버 팜 만들기**를 클릭 합니다.
3. **서버 팜 만들기** 대화 상자에서 서버 팜 (예: **스테이징 팜**)에 대 한 의미 있는 이름을 입력 한 다음 **서버 팜 프로 비전**을 선택 합니다.
4. 각 서버의 로컬 관리자 그룹에 추가한 도메인 계정의 사용자 이름 및 암호를 입력 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. **다음**을 클릭합니다.
6. **서버 추가** 페이지에서 주 서버의 FQDN (정규화 된 도메인 이름)을 입력 하 고 **주 서버**를 선택한 다음 **추가**를 클릭 합니다.
7. 이 시점에서 WFF는 제공한 자격 증명을 사용 하 여 주 서버에 연결을 시도 합니다. 연결에 성공 하면 주 서버가 **서버 추가** 페이지의 테이블에 추가 됩니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > **부하 분산에 서버를 사용할 수** 있다는 것이 기본적으로 선택 되어 있는 것을 알 수 있습니다. WFF는 IIS ARR 모듈을 사용 하 여 부하 분산을 구현 하 고 서버 팜의 웹 서버에서 요청을 분산 합니다. 대부분의 시나리오에서는 타사 부하 분산 솔루션을 대신 사용 하려는 경우 **부하 분산에 서버를 사용할 수 있음** 옵션을 선택 취소 해야 합니다.
8. **서버 추가** 페이지에서 첫 번째 보조 서버의 FQDN을 입력 한 다음 **추가**를 클릭 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. 팜의 추가 보조 서버에 대해 7 단계를 반복 하 고 **마침**을 클릭 합니다.

이제 WFF 서버 팜이 실행 중입니다. 주 서버에 설치한 모든 웹 플랫폼 제품 또는 구성 요소와 주 서버에 배포 하는 웹 응용 프로그램이 나 콘텐츠가 모든 보조 서버에 자동으로 프로 비전 됩니다.

WFF는 광범위 하 고 복잡 한 항목이 며 [IIS 7 웹 사이트 용 Microsoft 웹 팜 프레임 워크 2.0](https://go.microsoft.com/?linkid=9805129) 웹 사이트에서 자세히 알아볼 수 있습니다. 그러나이 시점에서 알아야 하는 두 가지 기능 영역은 다음과 같습니다.

- *응용 프로그램 프로 비전은* 서버 팜의 모든 보조 서버에서 웹 응용 프로그램 및 구성 설정과 같은 주 서버에서 콘텐츠를 복제 하는 프로세스입니다. 예를 들어 기본 스테이징 서버에 Contact Manager 샘플 솔루션을 배포 하는 경우 WFF 응용 프로그램 프로 비전 프로세스는이 솔루션을 모든 보조 스테이징 서버에 배포 합니다. 기본적으로 응용 프로그램 프로 비전 프로세스는 30 초 마다 실행 됩니다.
- *플랫폼 프로 비전은* 주 서버에서 서버 팜의 모든 보조 서버에 웹 플랫폼 제품 및 구성 요소를 동기화 하는 프로세스입니다. 예를 들어 기본 준비 서버에 ASP.NET MVC 3을 설치 하는 경우 플랫폼 프로 비전 프로세스는 웹 플랫폼 설치 관리자를 사용 하 여 모든 보조 스테이징 서버에 ASP.NET MVC 3을 설치 합니다. 기본적으로 플랫폼 프로 비전 프로세스는 5 분 마다 실행 됩니다.

WFF 컨트롤러 서버의 IIS 관리자에서 기본 응용 프로그램 및 플랫폼 프로 비전 설정을 관리할 수 있습니다.

**응용 프로그램 및 플랫폼 프로 비전 설정 살펴보기**

1. IIS 관리자의 **연결** 창에서 서버 팜을 선택 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. **서버 팜** 창에서 **응용 프로그램 프로 비전**을 두 번 클릭 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. 여기에서 볼 수 있듯이 서버 팜은 현재 주 서버와 보조 서버 간의 웹 콘텐츠 및 구성 설정을 30 초 마다 동기화 하도록 구성 되어 있습니다.
4. **뒤로**를 클릭 한 다음 **플랫폼 프로 비전**을 두 번 클릭 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. 여기에서 볼 수 있듯이 서버 팜은 현재 주 서버와 보조 서버 간의 웹 플랫폼 제품과 구성 요소를 5 분 마다 동기화 하도록 구성 되어 있습니다.
6. **뒤로**를 클릭합니다.
7. 서버 팜이 웹 플랫폼 제품을 즉시 동기화 하도록 강제 하려면 **작업** 창에서 **플랫폼 프로 비전**을 클릭 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > 플랫폼 프로 비전은 다소 시간이 걸릴 수 있습니다. 설치 관리자 프로세스는 서버 팜의 보조 서버에서 백그라운드로 실행 됩니다.
8. 프로 비전 프로세스가 완료 될 때까지 충분 한 시간을 허용 하면 주 서버에 추가한 제품 및 구성 요소가 보조 서버에 복제 되었는지 확인할 수 있습니다. 예를 들어 보조 서버에 로그온 하 고 **서버 관리자** 창을 사용 하 여 웹 서버 역할이 설치 되어 있는지 확인할 수 있습니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. 설치 된 프로그램 목록을 확인 하 여 다양 한 웹 플랫폼 구성 요소가 추가 되었는지 확인할 수도 있습니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a>부하 분산 구성

웹 팜을 만들 때 웹 서버 간에 HTTP 요청을 배포 하기 위해 일종의 부하 분산을 설정 해야 합니다. 이는 Windows Server 2008 네트워크 부하 분산, IIS ARR 또는 타사 소프트웨어 기반 또는 하드웨어 기반 부하 분산 솔루션 일 수 있습니다.

WFF는 IIS ARR과 긴밀 하 게 통합 되도록 설계 되었습니다. 이 통합 기능을 활용 하려면 WFF 컨트롤러 서버에 ARR 모듈을 설치 해야 합니다. 그런 다음 일반적으로 DNS (Domain Name System) 레코드를 구성 하 여 모든 웹 트래픽을 컨트롤러 서버로 보냅니다. 그러면 컨트롤러 서버는 서버 가용성 및 기타 다양 한 조건에 따라 팜의 서버 간에 들어오는 요청을 분산 합니다.

> [!NOTE]
> WFF;에 ARR을 사용할 필요가 없습니다. WFF를 구성 하 여 타사 부하 분산 솔루션을 사용할 수 있습니다. 자세한 내용은 [IIS 7 용 웹 팜 프레임 워크 2.0 개요](https://go.microsoft.com/?linkid=9805126)를 참조 하세요.

ARR을 사용한 부하 분산은이 자습서에서 다루지 않는 복잡 한 항목입니다. 그러나 다음 절차를 사용 하 여 ARR 모듈을 설치 하 고 부하 분산을 시작할 수 있습니다.

**WFF 컨트롤러 서버에서 부하 분산을 설정 하려면**

1. WFF 컨트롤러 서버에서 웹 플랫폼 설치 관리자를 시작 합니다.
2. **웹 플랫폼 설치 관리자 3.0** 창의 위쪽에서 **제품**을 클릭 합니다.
3. 창의 왼쪽에 있는 탐색 창에서 **서버**를 클릭 합니다.
4. **응용 프로그램 요청 라우팅 2.5** 행에서 **추가**를 클릭 합니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. **설치**를 클릭 하 고 **웹 플랫폼 설치** 창의 지시를 따릅니다.
6. 설치가 완료 되 면 IIS 관리자를 시작 하 고 **연결** 창에서 서버 팜 노드를 클릭 합니다. **서버 팜** 창에는 여러 개의 새 아이콘이 추가 되었습니다.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. **서버 팜** 창에서 **부하 분산**을 두 번 클릭 합니다.
8. **부하 분산** 창에서 부하 분산 알고리즘 (예: **최소 현재 요청**)을 선택 합니다.

    > [!NOTE]
    > 부하 분산 알고리즘 및 기타 구성 설정에 대 한 자세한 내용은 [응용 프로그램 요청 라우팅 모듈](https://go.microsoft.com/?linkid=9805130)을 참조 하세요.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. **작업** 창에서 **적용**을 클릭 합니다.

이제 서버 팜의 서버에 대 한 기본 부하 분산을 구성 했습니다. 모든 웹 팜 트래픽을 컨트롤러 서버로 전달 하는 경우 요청은 가용성 및 선택한 부하 분산 알고리즘에 따라 팜의 서버 간에 배포 됩니다.

ARR을 사용 하 여 부하 분산을 구성 하는 방법에 대 한 자세한 내용은 [응용 프로그램 요청 라우팅 모듈](https://go.microsoft.com/?linkid=9805130)을 참조 하세요.

## <a name="monitor-the-server-farm"></a>서버 팜 모니터링

컨트롤러 서버에서 IIS 관리자를 통해 언제 든 지 서버 팜의 상태를 모니터링할 수 있습니다. **연결** 창에서 서버 팜을 확장 한 다음 **서버**를 클릭 합니다. 가운데 창에는 팜의 각 서버에 대 한 요약이 최근 작업의 추적 로그와 함께 표시 됩니다.

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a>결론

이제 WFF 서버 팜이 실행 중 이어야 합니다. 원하는&#x2014;배포 방법을 지원 하도록 주 서버를 구성할 수 있습니다. 자세한 내용은 추가 정보&#x2014;섹션을 참조 하십시오. 그러면 구성이 서버 팜의 각 보조 서버에서 복제 됩니다.

## <a name="further-reading"></a>추가 참고 자료

WFF 구성 및 사용의 모든 측면에 대 한 자세한 지침은 [Microsoft 웹 팜 프레임 워크 2.0 FOR IIS 7](https://go.microsoft.com/?linkid=9805129) 웹 사이트를 참조 하세요.

> [!div class="step-by-step"]
> [이전](configuring-a-database-server-for-web-deploy-publishing.md)
> [다음](configuring-deployment-properties-for-a-target-environment.md)
