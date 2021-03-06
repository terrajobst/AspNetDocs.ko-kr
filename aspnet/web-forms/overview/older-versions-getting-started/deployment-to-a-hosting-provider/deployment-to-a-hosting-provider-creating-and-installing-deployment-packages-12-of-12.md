---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 문제 해결 (12/12) | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: db8f58e3679e6dea865dadb6f64916032dd9f38c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424037"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a>Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 문제 해결 (12/12)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다. 시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여주고, Windows Azure 웹 사이트에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 웹 배포 ASP.NET](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.

이 페이지에서는 Visual Studio를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포할 때 발생할 수 있는 몇 가지 일반적인 문제에 대해 설명 합니다. 각각에 대해 하나 이상의 가능한 원인과 해당 솔루션이 제공 됩니다.

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a>'/' 응용 프로그램에 서버 오류가 있습니다.-현재 사용자 지정 오류 설정으로 인해 오류에 대 한 세부 정보가 원격으로 표시 되지 않습니다.

### <a name="scenario"></a>시나리오

원격 호스트에 사이트를 배포한 후 web.config 파일의 customErrors 설정이 표시 되는 오류 메시지가 표시 되지만 오류의 실제 원인을 나타내는 것은 아닙니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

기본적으로 ASP.NET는 웹 응용 프로그램이 로컬 컴퓨터에서 실행 중인 경우에만 자세한 오류 정보를 표시 합니다. 일반적으로 해커는이 정보를 사용 하 여 응용 프로그램의 취약성을 찾을 수 있기 때문에 웹 응용 프로그램을 인터넷을 통해 공개적으로 사용할 수 있는 경우 자세한 오류 정보를 표시 하지 않으려고 합니다. 그러나 사이트 또는 업데이트를 사이트에 배포 하는 경우 어떤 경우에도 오류가 발생 하 여 실제 오류 메시지를 받아야 합니다.

응용 프로그램이 원격 호스트에서 실행 될 때 자세한 오류 메시지를 표시 하도록 설정 하려면 Web.config 파일을 편집 하 여 `customErrors` 모드를 해제 하 고 응용 프로그램을 다시 배포한 후 응용 프로그램을 다시 실행 합니다.

1. 응용 프로그램 Web.config 파일의 `system.web` 요소에 `customErrors` 요소가 있으면 `mode` 특성을 "off"로 변경 합니다. 그렇지 않은 경우 다음 예제와 같이 `mode` 특성이 "off"로 설정 된 상태에서 `system.web` 요소에 `customErrors` 요소를 추가 합니다.

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. 애플리케이션을 배포합니다.
3. 응용 프로그램을 실행 하 고 이전에 발생 한 오류를 발생 시킨 모든 항목을 반복 합니다. 이제 실제 오류 메시지를 확인할 수 있습니다.
4. 오류를 해결 한 경우 원래 `customErrors` 설정을 복원 하 고 응용 프로그램을 다시 배포 합니다.

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a>SQL Server Compact를 사용 하는 웹 페이지에서 액세스가 거부 되었습니다.

### <a name="scenario"></a>시나리오

SQL Server Compact를 사용 하는 사이트를 배포 하 고 데이터베이스에 액세스 하는 배포 된 사이트에서 페이지를 실행 하는 경우 다음 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

서버의 네트워크 서비스 계정에서 *bin\amd64* 또는 *bin\x86* 폴더에 있는 SQL SERVICE Compact 네이티브 이진 파일을 읽을 수 있어야 하지만 해당 폴더에 대 한 읽기 권한이 없습니다. *Bin* 폴더에서 네트워크 서비스에 대 한 읽기 권한을 설정 하 고 하위 폴더에 대 한 사용 권한을 확장 합니다.

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a>권한 부족으로 인해 구성 파일을 읽을 수 없습니다.

### <a name="scenario"></a>시나리오

Visual Studio 게시 단추를 클릭 하 여 로컬 컴퓨터의 IIS에 응용 프로그램을 배포 하면 게시가 실패 하 고 **출력** 창에 다음과 유사한 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

로컬 컴퓨터에서 한 번 클릭으로 IIS에 게시를 사용 하려면 관리자 권한으로 Visual Studio를 실행 해야 합니다. Visual Studio를 닫고 관리자 권한으로 다시 시작 합니다.

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a>대상 컴퓨터에 연결할 수 없습니다. 지정 된 프로세스 사용

### <a name="scenario"></a>시나리오

Visual Studio 게시 단추를 클릭 하 여 응용 프로그램을 배포 하면 게시가 실패 하 고 **출력** 창에 다음과 유사한 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

프록시 서버에서 대상 서버와의 통신을 중단 하 고 있습니다. Windows 제어판 또는 Internet Explorer에서 **인터넷 옵션** 을 선택 하 고 **연결** 탭을 선택 합니다. **인터넷 속성** 대화 상자에서 **LAN 설정**을 클릭 합니다. **Lan (Local Area Network) 설정** 대화 상자에서 **자동으로 설정 검색** 확인란의 선택을 취소 합니다. 그런 다음 게시 단추를 다시 클릭 합니다.

문제가 지속 되 면 시스템 관리자에 게 문의 하 여 프록시 또는 방화벽 설정으로 수행할 수 있는 작업을 확인 하십시오. 웹 배포는 웹 관리 서비스 배포 (8172)에 비표준 포트를 사용 하기 때문에 문제가 발생 합니다. 다른 연결의 경우 웹 배포는 포트 80를 사용 합니다. 타사 호스팅 공급자에 배포 하는 경우 일반적으로 웹 관리 서비스를 사용 합니다.

## <a name="default-net-40-application-pool-does-not-exist"></a>기본 .NET 4.0 응용 프로그램 풀이 없습니다.

### <a name="scenario"></a>시나리오

.NET Framework 4가 필요한 응용 프로그램을 배포 하는 경우 다음 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

ASP.NET 4가 IIS에 설치 되어 있지 않습니다. 배포 하는 서버가 개발 컴퓨터 이며 Visual Studio 2010가 설치 되어 있는 경우에는 ASP.NET 4가 컴퓨터에 설치 되어 있지만 IIS에 설치 되어 있지 않을 수 있습니다. 배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에 ASP.NET 4를 설치 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

기본 응용 프로그램 풀의 .NET Framework 버전을 수동으로 설정 해야 할 수도 있습니다. 자세한 내용은 [테스트 환경으로 IIS에 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서를 참조 하세요.

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a>초기화 문자열의 형식이 인덱스 0부터 시작 하는 사양과 일치 하지 않습니다.

### <a name="scenario"></a>시나리오

한 번 클릭 게시를 사용 하 여 응용 프로그램을 배포한 후 데이터베이스에 액세스 하는 페이지를 실행 하면 다음과 같은 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

배포 된 사이트에서 web.config 파일을 열고 다음 예제와 같이 연결 문자열 값이 `$(ReplaceableToken_`로 시작 하는지 *확인 합니다.*

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

연결 문자열이이 예제와 같이 보이는 경우 프로젝트 파일을 편집 하 고 모든 빌드 구성에 대 한 `PropertyGroup` 요소에 다음 속성을 추가 합니다.

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

그런 다음 응용 프로그램을 다시 배포 합니다.

## <a name="http-500-internal-server-error"></a>HTTP 500 내부 서버 오류

### <a name="scenario"></a>시나리오

배포 된 사이트를 실행 하는 경우 오류의 원인을 나타내는 특정 정보가 없는 다음 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

500 오류가 발생 하는 원인은 여러 가지가 있지만, 이러한 자습서를 수행 하는 경우 xml 변환 파일 중 하나에서 XML 요소를 잘못 된 위치에 배치 하는 것이 가능한 원인 중 하나입니다. 예를 들어 `<configuration>`바로 아래에 있는 대신 `<system.web>`에 `<location>` 요소를 삽입 하는 변환을 배치 하는 경우이 오류가 발생 합니다. 이 경우의 해결 방법은 XML 변환 파일을 수정 하 고 다시 배포 하는 것입니다.

## <a name="http-50021-internal-server-error"></a>HTTP 500.21 내부 서버 오류

### <a name="scenario"></a>시나리오

배포 된 사이트를 실행 하는 경우 다음 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

배포한 사이트는 ASP.NET 4 이지만 ASP.NET 4는 서버의 IIS에 등록 되어 있지 않습니다. 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 ASP.NET 4를 등록 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

기본 응용 프로그램 풀의 .NET Framework 버전을 수동으로 설정 해야 할 수도 있습니다. 자세한 내용은 [테스트 환경으로 IIS에 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서를 참조 하세요.

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a>앱\_데이터에서 SQL Server Express 데이터베이스를 여는 데 실패 했습니다.

### <a name="scenario"></a>시나리오

응용 프로그램 *\_Data* 폴더의 .mdf 파일로 SQL Server Express 데이터베이스를 가리키도록 *web.config* 파일 연결 문자열을 업데이트 하 고 응용 프로그램을 처음 실행할 때 다음과 같은 오류 메시지가 표시 *됩니다* .

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

이전에 기존 데이터베이스의 *.mdf* 파일을 삭제 한 경우에도 *.mdf* 파일의 이름은 컴퓨터에 있었던 SQL Server Express 데이터베이스의 이름과 일치할 수 없습니다. *.Mdf* 파일의 이름을 데이터베이스 이름으로 사용 된 적이 없는 이름으로 변경 하 고 *web.config* 파일을 변경 하 여 새 이름을 사용 합니다. 또는 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) 를 사용 하 여 이전에 기존 SQL Server Express 데이터베이스를 삭제할 수 있습니다.

## <a name="model-compatibility-cannot-be-checked"></a>모델 호환성을 확인할 수 없습니다.

### <a name="scenario"></a>시나리오

새 SQL Server Express 데이터베이스를 가리키도록 *web.config* 파일 연결 문자열을 업데이트 하 고 응용 프로그램을 처음 실행할 때 다음과 같은 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

컴퓨터에서 web.config 파일에 저장 한 데이터베이스 이름이 이미 사용 된 경우 데이터베이스에 일부 테이블이 이미 있을 수 있습니다. 이전에 컴퓨터에서 사용 되지 않은 새 이름을 선택 하 고이 새 데이터베이스 이름을 사용 하도록 *web.config 파일을 변경 합니다.* 또는 [SQL Server Express 유틸리티](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) 또는 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) 를 사용 하 여 기존 데이터베이스를 삭제할 수 있습니다.

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a>스크립트에서 사용자 또는 역할을 만들려고 할 때 SQL 오류가 발생 합니다.

### <a name="scenario"></a>시나리오

**Sql 패키지 및 게시** 탭에서 구성 된 데이터베이스 배포를 사용 하 고 있습니다. 배포 중에 실행 되는 sql 스크립트에는 사용자 만들기 또는 역할 만들기 명령이 포함 되며, 이러한 명령이 실행 되 면 스크립트 실행이 실패 합니다. 다음과 같이 보다 자세한 메시지가 표시 될 수 있습니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

**SQL 패키지 및 게시** 탭이 아니라 **웹 게시** 마법사에서 데이터베이스 배포를 구성 했을 때이 오류가 발생 하는 경우 [구성 및 배포](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) 포럼에서 스레드를 만들면이 문제 해결 페이지에 솔루션이 추가 됩니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

배포를 수행 하는 데 사용 하는 사용자 계정에 사용자 또는 역할을 만들 수 있는 권한이 없습니다. 예를 들어 호스팅 회사는 `db_datareader`, `db_datawriter`및 `db_ddladmin` 역할을 설정 하는 사용자 계정에 할당할 수 있습니다. 이러한 데이터는 대부분의 데이터베이스 개체를 만드는 데 충분 하지만 사용자 또는 역할을 만드는 데에는 충분 하지 않습니다. 이 오류를 방지 하는 한 가지 방법은 데이터베이스 배포에서 사용자와 역할을 제외 하는 것입니다. 이렇게 하려면 데이터베이스에서 자동으로 생성 된 스크립트에 대 한 `PreSource` 요소를 편집 하 여 다음 특성을 포함 하도록 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

프로젝트 파일에서 `PreSource` 요소를 편집 하는 방법에 대 한 자세한 내용은 [방법: 프로젝트 파일의 배포 설정 편집](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)을 참조 하세요. 개발 데이터베이스의 사용자 또는 역할이 대상 데이터베이스에 있어야 하는 경우 호스팅 공급자에 게 문의 하십시오.

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a>배포 하는 동안 사용자 지정 스크립트를 실행 하는 동안 SQL Server 시간 초과 오류 발생

### <a name="scenario"></a>시나리오

배포 하는 동안 실행할 사용자 지정 SQL 스크립트를 지정 하 고 웹 배포 실행 하면 시간 초과 됩니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

다른 트랜잭션 모드를 포함 하는 여러 스크립트를 실행 하면 시간 초과 오류가 발생할 수 있습니다. 기본적으로 자동으로 생성 된 스크립트는 트랜잭션에서 실행 되지만 사용자 지정 스크립트는 그렇지 않습니다. **Sql 패키지 및 게시** 탭에서 **기존 데이터베이스에서 데이터 및/또는 스키마 가져오기** 옵션을 선택 하 고 사용자 지정 sql 스크립트를 추가 하는 경우 모든 스크립트가 동일한 트랜잭션 설정을 사용 하도록 일부 스크립트의 트랜잭션 설정을 변경 해야 합니다. 자세한 내용은 [방법: 웹 응용 프로그램 프로젝트를 사용 하 여 데이터베이스 배포](https://msdn.microsoft.com/library/dd465343.aspx)를 참조 하세요.

모든 것이 동일 하지만이 오류가 발생 하지 않도록 트랜잭션 설정을 구성한 경우 스크립트를 별도로 실행 하는 것이 가능한 해결 방법입니다. SQL **패키지 및 게시** 탭의 **데이터베이스 스크립트** 표에서 제한 시간 오류를 발생 시키는 스크립트에 대 한 **포함** 확인란의 선택을 취소 한 다음 프로젝트를 게시 합니다. 그런 다음 **데이터베이스 스크립트** 그리드로 돌아가서 해당 스크립트의 **포함** 확인란을 선택 하 고 다른 스크립트에 대 한 **포함** 확인란의 선택을 취소 합니다. 그런 다음 프로젝트를 다시 게시 합니다. 이번에는 게시할 때 선택한 사용자 지정 스크립트만 실행 됩니다.

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a>사이트 매니페스트의 스트림 데이터를 아직 사용할 수 없습니다.

### <a name="scenario"></a>시나리오

`t` (테스트) 옵션을 사용 하 여 *배포 .cmd* 파일을 사용 하 여 패키지를 설치 하는 경우 다음 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

오류 메시지는 명령이 테스트 보고서를 생성할 수 없음을 의미 합니다. 그러나 `y` (실제 설치) 옵션을 사용 하는 경우 명령이 실행 될 수 있습니다. 이 메시지는 테스트 모드에서 명령을 실행 하는 데 문제가 있음을 나타냅니다.

## <a name="this-application-requires-managedruntimeversion-v40"></a>이 응용 프로그램에는 ManagedRuntimeVersion v 4.0이 필요 합니다.

### <a name="scenario"></a>시나리오

배포 하려고 하면 다음과 같은 오류 메시지가 표시 됩니다.

 오류: ' sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlScript '의 스트림 데이터를 아직 사용할 수 없습니다. 사용 하려는 응용 프로그램 풀의 ' managedRuntimeVersion ' 속성이 ' v 2.0 '으로 설정 되어 있습니다. 이 응용 프로그램에는 ' v 4.0 '이 필요 합니다. 

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

ASP.NET 4가 IIS에 설치 되어 있지 않습니다. 배포 하는 서버가 개발 컴퓨터 이며 Visual Studio 2010가 설치 되어 있는 경우에는 ASP.NET 4가 컴퓨터에 설치 되어 있지만 IIS에 설치 되어 있지 않을 수 있습니다. 배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에 ASP.NET 4를 설치 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a>Microsoft. Deployment. DeploymentProviderOptions를 캐스팅할 수 없습니다.

### <a name="scenario"></a>시나리오

패키지를 배포 하는 경우 다음 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

웹 배포 1.1 UI를 사용 하 여 IIS 관리자에서 웹 배포 2.0이 설치 된 서버에 배포 하려고 합니다. 패키지를 가져와서 IIS 원격 관리 도구를 사용 하 여 배포 하는 경우 연결을 설정할 때 **사용 가능한 새 기능** 대화 상자를 선택 합니다. 이 대화 상자는 연결이 처음 설정 될 때 한 번만 표시 될 수 있습니다. 연결을 지우고 다시 시작 하려면 IIS 관리자를 닫고 명령 프롬프트에서 `inetmgr /reset`를 입력 하 여 다시 시작 합니다.) 나열 된 기능 중 하나가 **UI 웹 배포**이 고 8 보다 낮은 버전의 버전을 포함 하는 경우 배포 하는 서버에 1.1 및 2.0 버전의 웹 배포 설치 되어 있을 수 있습니다. 2\.0가 설치 된 클라이언트에서 배포 하려면 서버에 웹 배포 2.0만 설치 되어 있어야 합니다. 이 문제를 해결 하려면 호스팅 공급자에 게 문의 해야 합니다.

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a>SQL Server Compact의 네이티브 구성 요소를 로드할 수 없습니다.

### <a name="scenario"></a>시나리오

배포 된 사이트를 실행 하는 경우 다음 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

배포 된 사이트에는 응용 프로그램의 *bin* 폴더 아래에 네이티브 어셈블리가 있는 *amd64* 및 *x86* 하위 폴더가 없습니다. SQL Server Compact 설치 된 컴퓨터에서 네이티브 어셈블리는 *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*에 있습니다. Visual Studio 프로젝트에서 올바른 폴더에 올바른 파일을 가져오는 가장 좋은 방법은 NuGet SqlServerCompact 패키지를 설치 하는 것입니다. 패키지 설치는 네이티브 어셈블리를 *amd64* 및 *x 86*으로 복사 하는 빌드 후 스크립트를 추가 합니다. 그러나 이러한 배포를 배포 하려면 프로젝트에 수동으로 포함 해야 합니다. 자세한 내용은 [SQL Server Compact 배포](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) 자습서를 참조 하세요.

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a>Entity Framework Code First 응용 프로그램을 배포한 후 "경로가 잘못 되었습니다." 오류

### <a name="scenario"></a>시나리오

Entity Framework Code First 마이그레이션를 사용 하는 응용 프로그램을 배포 하 고 SQL Server Compact와 같은 DBMS를 앱\_데이터 폴더의 파일에 저장 합니다. 첫 번째 배포 후에 데이터베이스를 만들도록 Code First 마이그레이션 구성 되어 있습니다. 응용 프로그램을 실행 하면 다음 예제와 같은 오류 메시지가 표시 됩니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

Code First에서 데이터베이스를 만들려고 하지만 응용 프로그램\_데이터 폴더가 없습니다. 배포할 때 *앱\_data* 폴더에 파일이 없거나 **프로젝트 속성** 창의 **패키지/게시 웹** 탭에서 **앱\_데이터 제외** 를 선택 했습니다. 서버에 복사할 폴더에 파일이 없는 경우 배포 프로세스에서 서버에 폴더를 만들지 않습니다. 사이트에서 데이터베이스를 이미 설정한 경우에는 게시 프로필의 **대상에서 추가 파일 제거** 를 선택한 경우 배포 프로세스에서 파일 및 *앱\_데이터* 폴더 자체를 삭제 합니다. 이 문제를 해결 하려면 *응용 프로그램\_data* 폴더에 .txt 파일과 같은 자리 표시자 파일을 배치 하 고, **앱 제외\_데이터** 를 선택 하 고 다시 배포 하지 않았는지 확인 합니다. 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a>"내부 RCW에서 분리 된 COM 개체를 사용할 수 없습니다."

### <a name="scenario"></a>시나리오

한 번의 클릭으로 게시를 사용 하 여 응용 프로그램을 배포한 후이 오류가 발생 하기 시작 했습니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

일반적으로이 오류를 해결 하려면 Visual Studio를 닫고 다시 시작 해야 합니다.

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a>게시에 사용 된 사용자 자격 증명에 setACL 기관이 없으므로 배포가 실패 함

### <a name="scenario"></a>시나리오

폴더 사용 권한을 설정할 권한이 없다는 것을 나타내는 오류로 인해 게시에 실패 합니다. 사용 중인 사용자 계정에는 setACL 기관이 없습니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

기본적으로 Visual Studio는 사이트의 루트 폴더에 대 한 읽기 권한과 앱\_데이터 폴더에 대 한 쓰기 권한을 설정 합니다. 사이트 폴더에 대 한 기본 사용 권한이 정확 하 고 설정 하지 않아도 되는 경우이 동작을 사용 하지 않도록 설정 합니다 .이 동작을 사용 하지 않도록 설정 **&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 을 게시 프로필 파일 (단일 프로필에 영향을 줌) 또는 wpp .targets 파일 (모든 프로필에 영향을 줌)에&lt;추가 합니다. 이러한 파일을 편집 하는 방법에 대 한 자세한 내용은 [방법: 프로필 (pubxml) 파일의 배포 설정 편집](https://msdn.microsoft.com/library/ff398069.aspx)을 참조 하세요. 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a>응용 프로그램이 응용 프로그램 폴더에 쓰려고 할 때 액세스 거부 오류

### <a name="scenario"></a>시나리오

응용 프로그램 폴더에 대 한 쓰기 권한이 없기 때문에 응용 프로그램 폴더 중 하나에서 파일을 만들거나 편집 하려고 할 때 응용 프로그램 오류가 발생 합니다.

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

기본적으로 Visual Studio는 사이트의 루트 폴더에 대 한 읽기 권한과 앱\_데이터 폴더에 대 한 쓰기 권한을 설정 합니다. 하위 폴더에 대 한 쓰기 권한이 응용 프로그램에 필요한 경우 [폴더 권한 설정](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md) 및 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에 표시 된 대로 해당 폴더에 대 한 권한을 설정할 수 있습니다. 응용 프로그램에 사이트의 루트 폴더에 대 한 쓰기 액세스 권한이 필요한 경우에는 해당 응용 프로그램에서 **includesetacl&gt;&lt;&gt;provider&lt;** 을 추가 하 여 루트 폴더에 대 한 읽기 전용 액세스를 설정 하는 것을 방지 해야 합니다 .이 경우에는 게시 프로필 파일 (단일 프로필에 영향을 주는) 또는 wpp .targets 파일 (모든 프로필에 영향을 줌 이러한 파일을 편집 하는 방법에 대 한 자세한 내용은 [방법: 프로필 (pubxml) 파일의 배포 설정 편집](https://msdn.microsoft.com/library/ff398069.aspx)을 참조 하세요. <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a>구성 오류-targetFramework 특성이 설치 된 버전 보다 최신 버전을 참조 .NET Framework

### <a name="scenario"></a>시나리오

ASP.NET 4.5를 대상으로 하는 웹 프로젝트를 성공적으로 게시 했지만, web.config 파일에서 `customErrors` 모드가 "off"로 설정 된 상태에서 응용 프로그램을 실행 하면 다음과 같은 오류가 발생 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

오류 페이지의 원본 오류 상자는 Web.config의 다음 줄을 오류의 원인으로 강조 표시 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a>가능한 원인 및 해결 방법

서버에서 ASP.NET 4.5를 지원 하지 않습니다. 호스팅 공급자에 게 문의 하 여 ASP.NET 4.5에 대 한 지원을 추가할 수 있는 시기 및 시기를 확인 합니다. 서버를 업그레이드할 수 없는 경우 대신 ASP.NET 4 또는 이전 버전을 대상으로 하는 웹 프로젝트를 배포 해야 합니다. ASP.NET 4 또는 이전 웹 프로젝트를 동일한 대상에 배포 하는 경우 **웹 게시** 마법사의 **설정** 탭에서 **대상에서 추가 파일 제거** 확인란을 선택 합니다. **대상에서 추가 파일 제거**를 선택 하지 않으면 계속 해 서 구성 오류 페이지가 표시 됩니다.

프로젝트 **속성** 창에는 대상 프레임 워크 드롭다운 목록이 포함 되어 있지만 **.NET Framework 4.5** 에서 **.NET Framework 4**로 변경 하면이 문제를 해결할 수 없습니다. 대상 프레임 워크를 이전 프레임 워크 버전으로 변경 하는 경우 프로젝트는 이후 프레임 워크 버전의 어셈블리에 대 한 참조를 계속 가지 며 실행 되지 않습니다. 이러한 참조를 수동으로 변경 하거나 .NET Framework 4 또는 이전 버전을 대상으로 하는 새 프로젝트를 만들어야 합니다. 자세한 내용은 [.NET Framework 대상 웹 사이트](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
