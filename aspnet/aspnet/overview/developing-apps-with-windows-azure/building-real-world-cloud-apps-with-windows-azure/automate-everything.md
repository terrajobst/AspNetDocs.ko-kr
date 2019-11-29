---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: 모든 항목 자동화 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: d5c8190d0b0c91bf9e42f6ef03adc5b07a65359a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582884"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a>모든 항목 자동화 (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 소개는 [첫 번째 챕터](introduction.md)를 참조 하세요.

처음에는 소프트웨어 개발 프로젝트에 실제로 적용 되는 세 가지 패턴이 있습니다. 특히 클라우드 프로젝트에도 적용 됩니다. 이 패턴은 개발 작업 자동화에 대 한 것입니다. 수동 프로세스가 느리고 오류가 발생 하기 쉬우므로 중요 한 항목입니다. 최대한 많은 항목을 최대한으로 자동화 하면 빠르고 안정적 이며 민첩 한 워크플로를 설정 하는 데 도움이 됩니다. 온-프레미스 환경에서 자동화 하기가 어렵거나 불가능 한 많은 작업을 쉽게 자동화할 수 있으므로 클라우드 개발에는 고유 하 게 중요 합니다. 예를 들어 새 웹 서버와 백 엔드 Vm, 데이터베이스, blob 저장소 (파일 저장소), 큐 등을 비롯 한 전체 테스트 환경을 설정할 수 있습니다.

## <a name="devops-workflow"></a>DevOps 워크플로

"DevOps" 라는 용어가 점점 늘어나고 있습니다. 소프트웨어를 효율적으로 개발 하기 위해 개발 및 운영 작업을 통합 해야 한다는 인식을 통해 개발 된 용어입니다. 사용 하도록 설정할 워크플로의 종류는 앱을 개발 하 고, 배포 하 고, 프로덕션 환경에서 학습 하 고, 학습 한 내용에 대 한 응답으로 변경 하 고, 빠르고 안정적으로 주기를 반복 하는 것입니다.

일부 성공적인 클라우드 개발 팀은 하루에 여러 번 라이브 환경에 배포 합니다. Azure 팀은 2-3 개월 마다 주요 업데이트를 배포 하는 데 사용 되지만, 이제 2-3 일 마다 및 주 2-3 릴리스 마다 몇 분 마다 업데이트를 릴리스 합니다. 이러한 흐름을 가져오면 고객 피드백에 응답 하는 데 도움이 됩니다.

이렇게 하려면 반복 가능 하 고 안정적 이며 예측 가능 하며 주기 시간이 낮은 개발 및 배포 주기를 사용 하도록 설정 해야 합니다.

![DevOps 워크플로](automate-everything/_static/image1.png)

즉, 기능에 대해 아이디어를 사용 하 고 고객을 사용 하 고 피드백을 제공 하는 시간 사이의 기간은 가능한 한 짧아야 합니다. 처음 세 가지 패턴 (모든 것, 소스 제어 및 연속 통합 및 배달 자동화)은 이러한 종류의 프로세스를 사용 하기 위해 권장 되는 모범 사례에 대 한 것입니다.

## <a name="azure-management-scripts"></a>Azure 관리 스크립트

[이 e-learning 소개](introduction.md)에서는 웹 기반 콘솔 인 Azure 관리 포털를 살펴보았습니다. 관리 포털을 사용 하면 Azure에 배포한 모든 리소스를 모니터링 하 고 관리할 수 있습니다. 웹 앱 및 Vm과 같은 서비스를 만들고 삭제 하 고, 서비스를 구성 하 고, 서비스 작업을 모니터링 하는 등의 작업을 수행 하는 쉬운 방법입니다. 훌륭한 도구 이지만이를 사용 하는 것은 수동 프로세스입니다. 팀 환경에서 모든 규모의 프로덕션 응용 프로그램을 개발 하려는 경우에는 Azure를 학습 하 고 탐색 한 다음 반복적으로 수행 하는 프로세스를 자동화 하기 위해 포털 UI를 진행 하는 것이 좋습니다.

관리 포털 또는 Visual Studio에서 수동으로 수행할 수 있는 거의 모든 작업은 REST 관리 API를 호출 하 여 수행할 수도 있습니다. [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)을 사용 하 여 스크립트를 작성 하거나 [Chef](http://www.opscode.com/chef/) 또는 [퍼핏](http://puppetlabs.com/puppet/what-is-puppet)와 같은 오픈 소스 프레임 워크를 사용할 수 있습니다. Mac 또는 Linux 환경에서 Bash 명령줄 도구를 사용할 수도 있습니다. Azure는 이러한 다양 한 환경에 대 한 스크립팅 Api를 포함 하 고 있으며 스크립트 대신 코드를 작성 하려는 경우에 [.net 관리 api](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) 를 포함 합니다.

Fix It 앱의 경우 테스트 환경을 만들고 해당 환경에 프로젝트를 배포 하는 프로세스를 자동화 하는 Windows PowerShell 스크립트를 만들었습니다. 이러한 스크립트의 내용 중 일부를 검토해 보겠습니다.

## <a name="environment-creation-script"></a>환경 만들기 스크립트

여기서 살펴볼 첫 번째 스크립트의 이름은 *New-AzureWebsiteEnv*입니다. 테스트를 위해 Fix It 앱을 배포할 수 있는 Azure 환경을 만듭니다. 이 스크립트에서 수행 하는 주요 작업은 다음과 같습니다.

- 웹앱 만들기
- 저장소 계정을 만듭니다. (Blob 및 큐에 필요 합니다. 이후 단원에서 볼 수 있습니다.)
- SQL Database 서버와 두 개의 데이터베이스 (응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스)를 만듭니다.
- 앱이 저장소 계정 및 데이터베이스에 액세스 하는 데 사용할 수 있는 설정을 Azure에 저장 합니다.
- 배포를 자동화 하는 데 사용 되는 설정 파일을 만듭니다.

### <a name="run-the-script"></a>스크립트 실행

> [!NOTE]
> 이 장에서는 스크립트 및 스크립트 실행을 위해 입력 하는 명령에 대 한 예제를 보여 줍니다. 이 데모에서는 스크립트를 실행 하기 위해 알아야 할 모든 사항을 제공 하지 않습니다. 단계별 방법에 대 한 지침은 [부록: Fix It 샘플 응용 프로그램](the-fix-it-sample-application.md#deploybase)을 참조 하세요.

Azure 서비스를 관리 하는 PowerShell 스크립트를 실행 하려면 Azure PowerShell 콘솔을 설치 하 고 Azure 구독을 사용 하도록 구성 해야 합니다. 설정이 완료 되 면 다음과 같은 명령을 사용 하 여 It 환경 생성 수정 스크립트를 실행할 수 있습니다.

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

`Name` 매개 변수는 데이터베이스 및 저장소 계정을 만들 때 사용할 이름을 지정 하 고, `SqlDatabasePassword` 매개 변수는 SQL Database에 대해 생성 되는 관리자 계정의 암호를 지정 합니다. 나중에 살펴볼 수 있는 다른 매개 변수를 사용할 수 있습니다.

![PowerShell 창](automate-everything/_static/image2.png)

스크립트가 완료 되 면 관리 포털에서 만들어진 항목을 볼 수 있습니다. 두 개의 데이터베이스를 찾을 수 있습니다.

![데이터베이스](automate-everything/_static/image3.png)

저장소 계정:

![저장소 계정](automate-everything/_static/image4.png)

웹 앱:

![웹 사이트](automate-everything/_static/image5.png)

웹 앱에 대 한 **구성** 탭에서 저장소 계정 설정 및 Fix it 앱에 대 한 SQL database 연결 문자열을 설정 하는 것을 볼 수 있습니다.

![appSettings 및 connectionStrings](automate-everything/_static/image6.png)

이제 *Automation* 폴더에 *&lt;websitename&gt;pubxml* 파일이 포함 되어 있습니다. 이 파일에는 MSBuild에서 방금 만든 Azure 환경에 응용 프로그램을 배포 하는 데 사용 하는 설정이 저장 됩니다. 예를 들면 다음과 같습니다.:

[!code-xml[Main](automate-everything/samples/sample1.xml)]

여기에서 볼 수 있듯이 스크립트는 전체 테스트 환경을 만들었으며 전체 프로세스는 약 90 초 내에 수행 됩니다.

팀의 다른 사용자가 테스트 환경을 만들려는 경우 스크립트를 실행 하기만 하면 됩니다. 뿐만 아니라 사용 중인 환경과 동일한 환경을 사용 하는 것을 확신할 수 있습니다. 관리 포털 UI를 사용 하 여 모든 사용자가 수동으로 설정 하는 경우에는 확실 하지 않을 수 있습니다.

### <a name="a-look-at-the-scripts"></a>스크립트 살펴보기

실제로이 작업을 수행 하는 세 가지 스크립트가 있습니다. 명령줄에서 하나를 호출 하 고 다른 두 항목을 자동으로 사용 하 여 일부 작업을 수행 합니다.

- *New-AzureWebSiteEnv* 는 기본 스크립트입니다.

    - *New-AzureStorage* 저장소 계정을 만듭니다.
    - *New-AzureSql* 는 데이터베이스를 만듭니다.

### <a name="parameters-in-the-main-script"></a>주 스크립트의 매개 변수

주 스크립트 *New-AzureWebSiteEnv*은 몇 가지 매개 변수를 정의 합니다.

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

두 매개 변수가 필요 합니다.

- 스크립트에서 만드는 웹 앱의 이름입니다. URL: `<name>.azurewebsites.net`에도 사용 됩니다.
- 스크립트에서 만드는 데이터베이스 서버의 새 관리자에 대 한 암호입니다.

선택적 매개 변수를 사용 하 여 데이터 센터 위치 (기본값은 "미국 서 부"), 데이터베이스 서버 관리자 이름 (기본값은 "dbuser"), 데이터베이스 서버에 대 한 방화벽 규칙을 지정할 수 있습니다.

### <a name="create-the-web-app"></a>웹 앱 만들기

스크립트는 `New-AzureWebsite` cmdlet을 호출 하 여 웹 앱을 만들고 웹 앱 이름 및 위치 매개 변수 값으로 전달 하 여 웹 앱을 만드는 것이 가장 좋습니다.

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a>저장소 계정 만들기

그런 다음 주 스크립트는 *New-AzureStorage* 스크립트를 실행 하 여 저장소 계정 이름에 대해 " *&lt;websitename&gt;* 저장소"를 지정 하 고 웹 앱과 동일한 데이터 센터 위치를 지정 합니다.

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

*New-AzureStorage* 는 `New-AzureStorageAccount` cmdlet을 호출 하 여 저장소 계정을 만들고 계정 이름과 액세스 키 값을 반환 합니다. 저장소 계정의 blob 및 큐에 액세스 하려면 응용 프로그램에 이러한 값이 필요 합니다.

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

항상 새 저장소 계정을 만들 필요는 없습니다. 필요에 따라 기존 저장소 계정을 사용 하도록 지시 하는 매개 변수를 추가 하 여 스크립트를 향상 시킬 수 있습니다.

### <a name="create-the-databases"></a>데이터베이스 만들기

기본 스크립트는 기본 데이터베이스 및 방화벽 규칙 이름을 설정한 후 데이터베이스 생성 스크립트 *New-AzureSql.* p s 1을 실행 합니다.

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

데이터베이스 생성 스크립트는 개발 컴퓨터의 IP 주소를 검색 하 고, 개발 컴퓨터에서 서버에 연결 하 고 관리할 수 있도록 방화벽 규칙을 설정 합니다. 그런 다음 데이터베이스 생성 스크립트는 데이터베이스를 설정 하는 몇 가지 단계를 거칩니다.

- `New-AzureSqlDatabaseServer` cmdlet을 사용 하 여 서버를 만듭니다.

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- 개발 컴퓨터에서 서버를 관리 하 고 웹 앱이 서버에 연결할 수 있도록 하는 방화벽 규칙을 만듭니다. 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- `New-AzureSqlDatabaseServerContext` cmdlet을 사용 하 여 서버 이름과 자격 증명을 포함 하는 데이터베이스 컨텍스트를 만듭니다.

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    `New-PSCredentialFromPlainText`은 `ConvertTo-SecureString` cmdlet을 호출 하 여 암호를 암호화 하 고 `Get-Credential` cmdlet이 반환 하는 것과 동일한 형식의 `PSCredential` 개체를 반환 하는 스크립트의 함수입니다.
- `New-AzureSqlDatabase` cmdlet을 사용 하 여 응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스를 만듭니다.

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- 는 로컬로 정의 된 함수를 호출 하 여 각 데이터베이스에 대 한 연결 문자열을 만듭니다. 응용 프로그램에서는 이러한 연결 문자열을 사용 하 여 데이터베이스에 액세스 합니다. 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    SQLAzureDatabaseConnectionString는 제공 된 매개 변수 값에서 연결 문자열을 만드는 스크립트에 정의 된 함수입니다.

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- 데이터베이스 서버 이름 및 연결 문자열을 사용 하 여 해시 테이블을 반환 합니다.

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

Fix It 앱은 별도의 멤버 자격과 응용 프로그램 데이터베이스를 사용 합니다. 또한 멤버 자격 및 응용 프로그램 데이터를 모두 단일 데이터베이스에 둘 수 있습니다.

### <a name="store-app-settings-and-connection-strings"></a>앱 설정 및 연결 문자열 저장

Azure에는 Web.config 파일에서 `appSettings` 또는 `connectionStrings` 컬렉션을 읽으려고 할 때 응용 프로그램에 반환 되는 내용을 자동으로 재정의 하는 설정 및 연결 문자열을 저장할 수 있는 기능이 있습니다. 배포할 때 [web.config 변환을](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) 적용 하는 대신 사용할 수 있습니다. 자세한 내용은이 설명서의 뒷부분에 나오는 [Azure에 중요 한 데이터 저장](source-control.md#appsettings) 을 참조 하세요.

환경 만들기 스크립트는 azure에서 실행 될 때 응용 프로그램이 저장소 계정 및 데이터베이스에 액세스 하는 데 필요한 모든 `appSettings` 및 `connectionStrings` 값을 Azure에 저장 합니다.

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

[새 유물](http://newrelic.com/) 은 [모니터링 및 원격 분석](monitoring-and-telemetry.md) 챕터에서 설명 하는 원격 분석 프레임 워크입니다. 또한 환경 생성 스크립트는 웹 앱을 다시 시작 하 여 새 유물 설정을 선택 합니다.

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a>배포 준비

프로세스가 끝나면 환경 만들기 스크립트에서 두 함수를 호출 하 여 배포 스크립트에서 사용 되는 파일을 만듭니다.

이러한 함수 중 하나는 게시 프로필 *(&lt;websitename&gt;* 파일)을 만듭니다. 이 코드는 Azure REST API를 호출 하 여 게시 설정을 가져오고 정보를 *publishsettings* 파일에 저장 합니다. 그런 다음 템플릿 파일 (*pubxml*)과 함께 해당 파일의 정보를 사용 하 여 게시 프로필을 포함 하는 *pubxml* 파일을 만듭니다. 이 2 단계 프로세스는 Visual Studio에서 수행 하는 작업을 시뮬레이션 *합니다. publishsettings* 파일을 다운로드 하 고 가져와서 게시 프로필을 만듭니다.

다른 함수는 다른 템플릿 파일 (website-environment)을 사용 하 여 배포 스크립트에서 *pubxml* 파일과 함께 사용할 설정을 포함 하는 파일을 만듭니다.

### <a name="troubleshooting-and-error-handling"></a>문제 해결 및 오류 처리

스크립트는 프로그램과 유사 합니다. 실패할 수 있으며, 오류 및 발생 원인에 대 한 정보를 파악 하고자 할 수 있습니다. 이러한 이유로 환경 만들기 스크립트는 `VerbosePreference` 변수의 값을 `SilentlyContinue`에서 `Continue`으로 변경 하 여 모든 자세한 정보 메시지가 표시 되도록 합니다. 또한 `ErrorActionPreference` 변수의 값을 `Continue`에서 `Stop`으로 변경 하 여 종료 되지 않는 오류가 발생 해도 스크립트가 중지 되도록 합니다.

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

작업을 수행 하기 전에 스크립트는 시작 시간을 저장 하 여 경과 된 시간을 계산할 수 있도록 합니다.

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

작업이 완료 되 면 스크립트는 경과 된 시간을 표시 합니다.

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

그리고 모든 키 작업에 대해 스크립트는 다음과 같은 자세한 정보 메시지를 작성 합니다.

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a>배포 스크립트

*New-AzureWebsiteEnv* 스크립트는 환경을 만들기 위해 수행 하는 작업, *Publish-AzureWebsite* 스크립트는 응용 프로그램 배포를 위한 것입니다.

배포 스크립트는 환경 생성 스크립트에서 만든 *website-environment* 파일에서 웹 앱의 이름을 가져옵니다.

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

*Publishsettings* 파일에서 배포 사용자 암호를 가져옵니다.

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

프로젝트를 빌드하고 배포 하는 [MSBuild](http://msbuildbook.com/) 명령을 실행 합니다.

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

명령줄에서 `Launch` 매개 변수를 지정한 경우 `Show-AzureWebsite` cmdlet을 호출 하 여 웹 사이트 URL에 대 한 기본 브라우저를 엽니다.

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

다음과 같은 명령을 사용 하 여 배포 스크립트를 실행할 수 있습니다.

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

완료 되 면 브라우저는 클라우드에서 실행 중인 사이트가 `<websitename>.azurewebsites.net` URL에 열립니다.

![Windows Azure에 배포 된 It 앱 수정](automate-everything/_static/image7.png)

## <a name="summary"></a>요약

이러한 스크립트를 사용 하면 동일한 옵션을 사용 하 여 동일한 단계가 항상 동일한 순서로 실행 되도록 확신할 수 있습니다. 이렇게 하면 팀의 각 개발자가 다른 팀 멤버의 환경 또는 프로덕션 환경에서 실제로 동일한 방식으로 작동 하지 않는 특정 컴퓨터에서 무언가를 누락 하거나 사용자 지정 항목을 배포할 수 없습니다.

이와 비슷한 방식으로 Linux 또는 Mac에서 실행할 수 있는 REST API, Windows PowerShell 스크립트, .NET 언어 API 또는 Bash 유틸리티를 사용 하 여 관리 포털에서 수행할 수 있는 대부분의 Azure 관리 기능을 자동화할 수 있습니다.

[다음 장에서](source-control.md) 는 소스 코드를 살펴보고 소스 코드 리포지토리에 스크립트를 포함 하는 것이 중요 한 이유를 설명 합니다.

## <a name="resources"></a>자료

- [Azure 용 Windows PowerShell을 설치 하 고 구성](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)합니다. Azure PowerShell cmdlet을 설치 하는 방법 및 Azure 계정을 관리 하기 위해 컴퓨터에 필요한 인증서를 설치 하는 방법에 대해 설명 합니다. PowerShell 자체를 학습 하기 위한 리소스 링크도 있으므로이 작업을 시작 하는 것이 좋습니다.
- [Azure 스크립트 센터](https://docs.microsoft.com/azure/automation/automation-runbook-gallery). WindowsAzure.com 포털을 사용 하 여 Azure 서비스를 관리 하는 스크립트를 개발 하기 위한 링크, 시작 자습서에 대 한 링크, cmdlet 참조 설명서와 소스 코드 및 샘플 스크립트를 제공 합니다.
- [주말 스크립터: Azure 및 PowerShell 시작](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx) Windows PowerShell 전용 블로그에서이 게시물은 Azure 관리 기능에 PowerShell을 사용 하는 것에 대 한 유용한 소개를 제공 합니다.
- [Azure 플랫폼 간 명령줄 인터페이스를 설치 하 고 구성](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)합니다. Mac 및 Linux 및 Windows 시스템에서 작동 하는 Azure scripting framework에 대 한 시작 자습서입니다.
- [Azure sdk 및 도구 다운로드 항목의 명령줄 도구 섹션을 참조](https://azure.microsoft.com/downloads/)하세요. Azure에 대 한 명령줄 도구와 관련 된 설명서 및 다운로드를 위한 포털 페이지입니다.
- [Azure 관리 라이브러리 및 .net을 사용 하 여 모든 것을 자동화](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)합니다. Scott Hanselman는 Azure 용 .NET 관리 API를 소개 합니다.
- [Windows PowerShell 스크립트를 사용 하 여 개발 및 테스트 환경에 게시](https://msdn.microsoft.com/library/azure/dn642480.aspx) Visual Studio에서 웹 프로젝트에 대해 자동으로 생성 하는 게시 스크립트를 사용 하는 방법을 설명 하는 MSDN 설명서입니다.
- [PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597). Visual studio에서 Windows PowerShell에 대 한 언어 지원을 추가 하는 visual Studio 확장입니다.

> [!div class="step-by-step"]
> [이전](introduction.md)
> [다음](source-control.md)
