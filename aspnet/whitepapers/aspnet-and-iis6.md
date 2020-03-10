---
uid: whitepapers/aspnet-and-iis6
title: IIS 6.0를 사용 하 여 ASP.NET 1.1 실행 | Microsoft Docs
author: rick-anderson
description: Windows Server 2003에는 IIS 6.0과 ASP.NET 1.1가 모두 포함 되어 있지만 이러한 구성 요소는 기본적으로 사용 하지 않도록 설정 되어 있습니다. 이 백서에서는 IIS 6.0를 사용 하도록 설정 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419849"
---
# <a name="running-aspnet-11-with-iis-60"></a>IIS 6.0에서 ASP.NET 1.1 실행

> Windows Server 2003에는 IIS 6.0과 ASP.NET 1.1가 모두 포함 되어 있지만 이러한 구성 요소는 기본적으로 사용 하지 않도록 설정 되어 있습니다. 이 백서에서는 IIS 6.0 및 ASP.NET 1.1를 사용 하도록 설정 하는 방법을 설명 하 고, IIS 및 ASP.NET에서 최적의 성능을 얻기 위해 몇 가지 구성 설정을 권장 합니다.
> 
> ASP.NET 1.1 및 IIS 6.0에 적용 됩니다.

ASP.NET 1.1은 최신 버전의 인터넷 정보 서버 (IIS) 버전 6.0도 포함 하는 Windows Server 2003과 함께 제공 됩니다. IIS 6.0 및 ASP.NET 1.1은 기본적으로 새 IIS 6.0 작업자 프로세스 모델에 자연스럽 게 통합 되도록 설계 되었습니다.

## <a name="aspnet-11-is-not-installed-by-default"></a>ASP.NET 1.1는 기본적으로 설치 되지 않습니다.

이전 버전의 Microsoft 서버 운영 체제와 달리 인터넷 정보 서버 (IIS)는 기본적으로 사용 하도록 설정 되어 있지 않습니다. 또는는 ASP.NET 1.1입니다. IIS를 사용 하도록 설정 하는 방법에는 다음 두 가지가 있습니다.

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a>IIS 사용, 옵션 #1-서버 구성 마법사

Windows Server 2003에는 원하는 모드에서 서버를 올바르게 구성 하는 데 도움이 되는 새로운 ' 서버 구성 마법사 '가 제공 됩니다.

마법사를 시작 하려면 마법사를 실행 하려면 관리자 권한으로 로그인 해야 합니다. 시작 | 프로그램 | 관리 도구를 선택 하 고 ' 서버 구성 '을 선택 합니다.

선택 하면 ' 서버 구성 마법사 ' 열기 화면이 표시 됩니다.

![](aspnet-and-iis6/_static/image1.jpg)

' 다음 &gt;'을 클릭 합니다.

![](aspnet-and-iis6/_static/image2.jpg)

' 다음 &gt;' 클릭

![](aspnet-and-iis6/_static/image3.jpg)

이 화면에서 구성할 옵션으로 ' 응용 프로그램 서버 (IIS, ASP.NET)를 선택 해야 합니다.

' 다음 &gt;'을 클릭 합니다.

![](aspnet-and-iis6/_static/image4.jpg)

서버를 응용 프로그램 서버로 구성 하도록 선택한 후에는 추가 기능을 설치할 것인지 묻는 메시지가이 화면에 표시 됩니다. 옵션은 기본적으로 선택 되어 있지 않습니다. ASP.NET를 자동으로 사용 하도록 설정 하려면 ' ASP 사용을 선택 해야 합니다. NET '.

' 다음 &gt;'을 클릭 합니다.

![](aspnet-and-iis6/_static/image5.jpg)

이 화면에는 설치할 옵션이 표시 됩니다.

' 다음 &gt;'을 클릭 합니다.

![](aspnet-and-iis6/_static/image6.jpg)

선택한 옵션을 설치 하는 동안이 화면이 표시 됩니다. 서비스가 설치 되는 동안 다른 대화 상자를 표시 하는 것이 일반적입니다. Windows 2003 서버 설치 CD의 위치를 묻는 메시지가 추가로 표시 될 수도 있습니다.

완료 되 면 ' 다음 &gt;'을 클릭 합니다.

![](aspnet-and-iis6/_static/image7.jpg)

' 마침 '을 클릭 합니다. 이제 Windows Server 2003는 IIS 6.0 및 ASP.NET 1.1을 지원 하도록 구성 됩니다.

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a>IIS 사용, 옵션 #2-수동으로 IIS 및 ASP.NET 구성

' 서버 구성 마법사 '를 사용 하지 않으려면 제어판에서 ' 프로그램 추가/제거 '를 사용 하 여 IIS 6.0 및 ASP.NET 1.1를 선택적으로 설치할 수 있습니다.

먼저 제어판을 엽니다.

![](aspnet-and-iis6/_static/image8.jpg)

' Windows 구성 요소 추가/제거 '를 클릭 하면 ' Windows 구성 요소 마법사 '가 열립니다.

![](aspnet-and-iis6/_static/image9.jpg)

' 응용 프로그램 서버 '를 강조 표시 하 고 확인 한 다음 ' 세부 정보? '를 클릭 합니다. 단추만

![](aspnet-and-iis6/_static/image10.jpg)

ASP.NET를 설치 하려면 ' ASP '를 확인 하세요. NET '.

' 확인 '을 클릭 하 여 Windows 구성 요소 마법사로 돌아갑니다. Windows 구성 요소 마법사에서 ' 다음 &gt;'을 클릭 하 여 설치를 시작 합니다.

![](aspnet-and-iis6/_static/image11.jpg)

서비스가 설치 되는 동안 다른 대화 상자를 표시 하는 것이 일반적입니다. Windows 2003 서버 설치 CD의 위치를 묻는 메시지가 추가로 표시 될 수도 있습니다.

설치가 완료 되 면 Windows 구성 요소 마법사의 마지막 화면이 표시 됩니다.

![](aspnet-and-iis6/_static/image12.jpg)

이제 IIS 6.0 및 ASP.NET 1.1이 구성 되 고 사용 가능 합니다.

## <a name="recommended-settings"></a>권장 설정

IIS 6.0에서 ASP.NET 1.1를 실행 하는 경우 ASP.NET에서 최적의 성능을 얻기 위해 권장 되는 몇 가지 구성 설정이 있습니다.

- 작업자 프로세스 메모리 제한 구성
- 작업자 프로세스 재활용 구성

### <a name="configuring-worker-process-memory-limits"></a>작업자 프로세스 메모리 제한 구성

기본적으로 IIS 6.0는 IIS에서 사용할 수 있는 메모리 양에 대 한 제한을 설정 하지 않습니다. ASP. 네트워크의 캐시 기능은 메모리의 제한에 의존 하므로 캐시가 메모리에서 사용 하지 않는 항목을 사전에 제거할 수 있습니다.

IIS 6.0의 메모리 재활용 기능을 구성 하는 것이 좋습니다. 이 열린 인터넷 정보 서비스 관리자를 구성 하려면 (시작 | 프로그램 | 관리 도구 | 인터넷 정보 서비스). 열린 후 ' 응용 프로그램 풀 ' 폴더를 확장 합니다.

각 응용 프로그램 풀에 대해 다음을 수행 합니다.

![](aspnet-and-iis6/_static/image13.jpg)

1. 응용 프로그램 풀을 마우스 오른쪽 단추로 클릭 하 고 (예: ' DefaultAppPool ') ' 속성 '을 선택 합니다.

![](aspnet-and-iis6/_static/image14.jpg)

2. 다음으로 ' 사용 된 최대 메모리 (메가바이트): '를 클릭 하 여 메모리 재활용을 사용 하도록 설정 합니다. 값은 서버에 있는 물리적 (가상이 아닌) 메모리의 양 보다 커야 하며, 실제 메모리의 60%입니다. 예를 들어, 512MB의 실제 메모리를 사용 하는 서버의 경우 310를 선택 합니다. 또한 2GB 주소 공간을 사용 하는 경우 최대 800MB를 초과 하지 않는 것이 좋습니다. 서버의 메모리 주소 공간이 3GB 인 경우 작업자 프로세스에 대 한 최대 메모리 제한은 1, 800MB입니다.

![](aspnet-and-iis6/_static/image15.jpg)

' 적용 '을 클릭 하 고 ' 확인 '을 클릭 하 여 속성 대화 상자를 종료 합니다. 사용 가능한 모든 응용 프로그램 풀에 대해이를 반복 합니다.

### <a name="configuring-worker-recycling"></a>작업자 재활용 구성

기본적으로 IIS 6.0는 29 시간 마다 작업자 프로세스를 재활용 하도록 구성 되어 있습니다. 이는 ASP.NET를 실행 하는 응용 프로그램의 다소 적극적 이며, 자동 작업자 프로세스 재활용을 사용 하지 않도록 설정 하는 것이 좋습니다.

자동 작업자 프로세스 재활용을 사용 하지 않도록 설정 하려면 먼저 인터넷 정보 서비스 Manager를 엽니다 (시작 | 프로그램 | 관리 도구 | 인터넷 정보 서비스). 열린 후 ' 응용 프로그램 풀 ' 폴더를 확장 합니다.

![](aspnet-and-iis6/_static/image16.jpg)

각 응용 프로그램 풀에 대해 다음을 수행 합니다.

1. 응용 프로그램 풀을 마우스 오른쪽 단추로 클릭 하 고 (예: ' DefaultAppPool ') ' 속성 '을 선택 합니다.

![](aspnet-and-iis6/_static/image17.jpg)

2. ' 작업자 프로세스 재생 (분): ': '을 선택 취소 합니다.

![](aspnet-and-iis6/_static/image18.jpg)

' 적용 '을 클릭 하 고 ' 확인 '을 클릭 하 여 속성 대화 상자를 종료 합니다. 사용 가능한 모든 응용 프로그램 풀에 대해이를 반복 합니다.

## <a name="granting-write-access-to-the-file-system"></a>파일 시스템에 대 한 쓰기 권한 부여

응용 프로그램에 파일 시스템에 대 한 쓰기 권한이 필요 하 고 NTFS를 사용 하는 경우 ASP.NET에 액세스 권한을 부여 하려면 폴더나 파일에서 ACL (Access Control 목록)을 수정 해야 합니다.

예를 들어 c:\inetpub\wwwroot의 첫 번째 열린 탐색기에 ASP.NET 쓰기 액세스 권한을 부여 하 고 디렉터리로 이동 합니다.

![](aspnet-and-iis6/_static/image19.jpg)

그런 다음 디렉터리 (예: ' wwwroot ')를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다. 속성 대화 상자가 열리면 ' 보안 ' 탭을 선택 합니다.

![](aspnet-and-iis6/_static/image20.jpg)

C:\inetpub\wwwroot\ 디렉터리는 특수 한 IIS 6.0 그룹 ' IIS\_WPG '에 이미 읽기 &amp; 실행, 폴더 내용 보기 및 읽기 권한이 부여 된 특수 한 디렉터리입니다. 그러나 쓰기 권한을 부여 하려면 쓰기에 대 한 허용 확인란을 클릭 해야 합니다.

![](aspnet-and-iis6/_static/image21.jpg)

이제 IIS 6.0에이 폴더에 대 한 쓰기 권한이 있습니다. 다른 폴더에 대 한 쓰기 권한을 부여 하려면 다음 단계를 따르세요. IIS\_WPG 그룹이 아직 없는 경우 추가 해야 할 수 있습니다.

> [!CAUTION]
> IIS\_WPG에 대 한 쓰기 권한을 부여 하면 모든 ASP.NET 응용 프로그램에서이 디렉터리에 쓸 수 있습니다.

## <a name="supporting-integrated-authentication-with-sql-server"></a>SQL Server 통합 인증 지원

통합 인증을 사용 하면 SQL Server Windows NT 인증을 활용 하 여 SQL Server 로그온 계정의 유효성을 검사할 수 있습니다. 이를 통해 사용자는 표준 SQL Server 로그온 프로세스를 무시할 수 있습니다. 이 접근 방식을 사용 하면 Windows NT 네트워크 보안 프로세스에서 사용자 및 암호 정보를 가져오기 때문 SQL Server에 네트워크 사용자가 별도의 로그온 id 또는 암호를 제공 하지 않고 SQL Server 데이터베이스에 액세스할 수 있습니다.

응용 프로그램에 대 한 연결 문자열 내에 자격 증명을 저장 하지 않기 때문에 ASP.NET 응용 프로그램에 대 한 통합 인증을 선택 하는 것이 좋습니다. 대신 SQL에 연결 하는 데 사용 되는 연결 문자열은 다음과 같습니다.

`"server=localhost; database=Northwind;Trusted_Connection=true"`

이 연결 문자열은 SQL Server 액세스를 시도 하는 응용 프로그램의 Windows 자격 증명을 사용 SQL Server를 알려 줍니다. ASP.NET/IIS 6의 경우 IIS\_WPG 그룹의 계정입니다.

SQL Server과 ASP.NET 간에 통합 인증을 사용 하도록 설정 하려면 먼저 통합 인증에 대 한 SQL Server 구성 되어 있는지 확인 하 고 DBA를 사용 하 여이를 확인 하도록 구성 해야 합니다. SQL Server이 두 모드 중 하나에 있는 경우 통합 인증을 사용할 수 있습니다.

SQL Server Enterprise 관리자 열기 (시작 | 프로그램 | Microsoft SQL Server | 엔터프라이즈 관리자)에서 적절 한 서버를 선택 하 고 보안 폴더를 확장 합니다.

![](aspnet-and-iis6/_static/image22.jpg)

' BUILTINT\IIS\_WPG ' 그룹이 목록에 없으면 로그인을 마우스 오른쪽 단추로 클릭 하 고 ' New 로그인 ':

![](aspnet-and-iis6/_static/image23.jpg)

' 이름: ' 텍스트 상자에 ' [Server/Domain Name] \IIS\_WPG '를 입력 하거나 줄임표 단추를 클릭 하 여 Windows NT 사용자/그룹 선택기를 엽니다.

![](aspnet-and-iis6/_static/image24.jpg)

현재 컴퓨터의 IIS\_WPG 그룹을 선택 하 고 ' 추가 '를 클릭 한 다음 확인을 클릭 하 여 선택을 닫습니다.

그런 다음 데이터베이스에 액세스할 수 있는 기본 데이터베이스 및 권한도 설정 해야 합니다. 기본 데이터베이스를 설정 하려면 드롭다운 목록에서 선택 합니다. 예를 들어 Northwind 아래에서 선택 합니다.

![](aspnet-and-iis6/_static/image25.jpg)

그런 다음 데이터베이스 액세스 탭을 클릭 합니다.

![](aspnet-and-iis6/_static/image26.jpg)

액세스를 허용 하려는 모든 데이터베이스에 대해 허용 확인란을 클릭 합니다. 데이터베이스 역할을 선택 해야 합니다. db\_소유자를 선택 하면 선택한 데이터베이스를 관리 하 고 사용 하는 데 필요한 모든 권한이 로그인에 있는지 확인 합니다.

확인을 클릭 하 여 속성 대화 상자를 종료 합니다. 이제 ASP.NET 응용 프로그램이 통합 SQL Server 인증을 지원 하도록 구성 되었습니다.

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a>IIS 6.0 기본 모드에서 ASP.NET 1.0 실행 안 함

IIS 6.0의 ASP.NET 1.0은 IIS 5 호환성 모드 에서만 지원 됩니다.

ASP.NET 1.0를 IIS 5.0 호환성 모드로 실행 하도록 구성 하려면 인터넷 서비스 관리자을 열고 웹 사이트를 마우스 오른쪽 단추로 클릭 한 다음 속성을 선택 합니다.

![](aspnet-and-iis6/_static/image27.jpg)

서비스 탭으로 전환 하 고 확인 합니다. IIS 5.0 격리 모드에서 WWW 서비스를 실행 하 시겠습니까?:

![](aspnet-and-iis6/_static/image28.jpg)
