---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: ASP.NET 및 Azure App Service에 암호 및 기타 중요 한 데이터 배포-ASP.NET 4.x
author: Rick-Anderson
description: 이 자습서에서는 코드가 안전 하 게 보안 정보를 저장 하 고 액세스 하는 방법을 보여 줍니다. 가장 중요 한 점은 암호 또는 다른 send를 저장 하지 않는 것입니다.
ms.author: riande
ms.date: 05/21/2015
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 8356a90611f791779cc4ff4730038d82cd76242f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457052"
---
# <a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a>ASP.NET 및 Azure App Service에 암호와 기타 중요한 데이터를 배포하는 방법에 대한 모범 사례

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 코드가 안전 하 게 보안 정보를 저장 하 고 액세스 하는 방법을 보여 줍니다. 무엇보다 중요한 점은 절대로 소스 코드에 암호나 기타 중요한 데이터를 저장하면 안 될 뿐만 아니라, 프로덕션 환경의 보안 정보를 개발 및 테스트 모드에서 사용해서는 안 된다는 것입니다
> 
> 샘플 코드는 간단한 WebJob 콘솔 앱 및 데이터베이스 연결 문자열 password, Twilio, Google 및 SendGrid secure 키에 대 한 액세스 권한이 필요한 ASP.NET MVC 앱입니다.
> 
> 온-프레미스 설정 및 PHP도 설명 되어 있습니다.

- [개발 환경에서 암호 작업](#pwd)
- [개발 환경에서 연결 문자열 작업](#con)
- [WebJobs 콘솔 앱](#wj)
- [Azure에 비밀 배포](#da)
- [온-프레미스 및 PHP에 대 한 참고 사항](#not)
- [추가 리소스](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a>개발 환경에서 암호 작업

자습서는 중요 한 데이터를 소스 코드에 자주 표시 하 고, 중요 한 데이터를 소스 코드에 저장 하지 않는 것이 좋습니다. 예를 들어 [SMS 및 전자 메일 2FA 자습서를 사용 하는 ASP.NET MVC 5 앱](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) 은 web.config *파일에* 다음을 보여 줍니다.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

Web.config *파일은* 소스 코드 이므로 이러한 암호는 해당 파일에 저장 되지 않아야 합니다. 다행히 `<appSettings>` 요소에는 중요 한 앱 구성 설정이 포함 된 외부 파일을 지정할 수 있는 `file` 특성이 있습니다. 외부 파일이 원본 트리에 체크 인 되지 않은 경우 모든 비밀을 외부 파일로 이동할 수 있습니다. 예를 들어 다음 태그에서 *Appsettingssecrets* 파일은 모든 앱 암호를 포함 합니다.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

외부 파일 (이 샘플의 경우*Appsettingssecrets* )의 태그는 *web.config 파일에* 있는 것과 동일한 태그입니다.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

ASP.NET 런타임은 외부 파일의 내용을 &lt;appSettings&gt; 요소의 태그와 병합 합니다. 지정된 파일을 찾을 수 없는 경우 런타임에서 파일 특성을 무시합니다.

> [!WARNING]
> 보안-프로젝트에 *암호 .config* 파일을 추가 하거나 소스 제어에 체크 인 하지 않습니다. 기본적으로 Visual Studio는 `Build Action`를 `Content`로 설정 합니다. 즉, 파일이 배포 됩니다. 자세한 내용은 [내 프로젝트 폴더의 모든 파일을 배포 하지 않는 이유](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment) 를 참조 하세요. 구성 파일이 IIS에서 제공 되지 않으므로이 *파일에* 대 한 모든 확장을 사용할 수는 있지만 구성 파일을 보관 하는 것이 좋습니다 *.* 또한 *Appsettingssecrets* *파일은 web.config 파일의* 두 디렉터리 수준 이므로 솔루션 디렉터리에서 완전히 제외 됩니다. 솔루션 디렉터리에서 파일을 이동 하 여 &quot;git 추가 \*&quot; 리포지토리에 추가 하지 않습니다.

<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a>개발 환경에서 연결 문자열 작업

Visual Studio는 [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)를 사용 하는 새 ASP.NET 프로젝트를 만듭니다. LocalDB는 개발 환경 전용으로 만들어졌습니다. 암호는 필요 하지 않으므로 소스 코드에서 비밀을 체크 인하지 못하도록 하기 위해 아무것도 수행할 필요가 없습니다. 일부 개발 팀에서는 암호를 요구 하는 SQL Server (또는 기타 DBMS)의 전체 버전을 사용 합니다.

`configSource` 특성을 사용 하 여 전체 `<connectionStrings>` 태그를 바꿀 수 있습니다. 태그를 병합 하는 `<appSettings>` `file` 특성과 달리 `configSource` 특성은 태그를 대체 합니다. 다음 태그는 *web.config 파일의* `configSource` 특성을 보여 줍니다.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> 위에 표시 된 것 처럼 `configSource` 특성을 사용 하 여 연결 문자열을 외부 파일로 이동 하 고 Visual Studio에서 새 웹 사이트를 만들도록 하는 경우 데이터베이스를 사용 하 고 있는지 여부를 확인할 수 없으며 Visual Studio에서 Azure에 게시할 때 데이터베이스를 구성 하는 옵션을 사용할 수 없습니다. `configSource` 특성을 사용 하는 경우 PowerShell을 사용 하 여 웹 사이트 및 데이터베이스를 만들고 배포할 수 있습니다. 또는 게시 하기 전에 포털에서 웹 사이트 및 데이터베이스를 만들 수 있습니다. [New-AzureWebsitewithDB](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 스크립트는 새 웹 사이트 및 데이터베이스를 만듭니다.

> [!WARNING]
> 보안- *Appsettingssecrets* 파일의 경우와 달리, 외부 연결 문자열 파일 *은 루트 web.config* 파일과 동일한 디렉터리에 있어야 하므로 원본 리포지토리에 체크 인 하지 않도록 주의 해야 합니다.

> [!NOTE]
> **비밀 파일의 보안 경고:** 테스트 및 개발에서 프로덕션 암호를 사용 하지 않는 것이 가장 좋습니다. 테스트 또는 개발에서 프로덕션 암호를 사용 하면 이러한 비밀을 누출 합니다.

<a id="wj"></a>
## <a name="webjobs-console-apps"></a>WebJobs 콘솔 앱

콘솔 앱에서 사용 하는 *app.config* 파일은 상대 경로를 지원 하지 않지만 절대 경로를 지원 합니다. 절대 경로를 사용 하 여 프로젝트 디렉터리에서 비밀을 이동할 수 있습니다. 다음 태그는 *app.config* 파일에 있는 *C:\secrets\AppSettingsSecrets.config* 파일 및 중요 하지 않은 데이터의 비밀을 보여 줍니다.

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a>Azure에 비밀 배포

Azure에 웹 앱을 배포 하는 경우 *Appsettingssecrets .config* 파일이 배포 되지 않습니다 (원하는 항목). [Azure 관리 포털](https://azure.microsoft.com/services/management-portal/) 로 이동 하 고 수동으로 설정 하 여 다음과 같은 작업을 수행할 수 있습니다.

1. [https://portal.azure.com](https://portal.azure.com)로 이동 하 고 Azure 자격 증명을 사용 하 여 로그인 합니다.
2. **찾아보기 &gt; Web Apps**를 클릭 한 다음 웹 앱의 이름을 클릭 합니다.
3. **모든 설정 &gt; 응용 프로그램 설정**을 클릭 합니다.

**앱 설정** 및 **연결 문자열** 값이 *web.config 파일의* 동일한 설정을 재정의 합니다. 이 예제에서는 Azure에 이러한 설정을 배포 하지 않았지만 이러한 *키가 web.config 파일에* 있는 경우 포털에 표시 되는 설정이 우선 적용 됩니다.

[Devops 워크플로](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md) 를 따르고 [Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) (또는 [Chef](http://www.opscode.com/chef/) 또는 [퍼핏](http://puppetlabs.com/puppet/what-is-puppet)와 같은 다른 프레임 워크)를 사용 하 여 Azure에서 이러한 값을 자동으로 설정 하는 것이 가장 좋습니다. 다음 PowerShell 스크립트는 [export-clixml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk) 를 사용 하 여 암호화 된 암호를 디스크로 내보냅니다.

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

위의 스크립트에서 ' n a m e '은 '&quot;FB\_AppSecret&quot; 또는 "TwitterSecret"와 같은 비밀 키의 이름입니다. 브라우저에서 스크립트를 통해 만든 "credential" 파일을 볼 수 있습니다. 아래 코드 조각은 각 자격 증명 파일을 테스트 하 고 명명 된 웹 앱에 대 한 암호를 설정 합니다.

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> 보안-PowerShell 스크립트에 암호 또는 기타 암호를 포함 하지 마십시오. 이렇게 하면 PowerShell 스크립트를 사용 하 여 중요 한 데이터를 배포 하는 목적이 무효화 됩니다. [자격 증명 가져오기](https://technet.microsoft.com/library/hh849815.aspx) cmdlet은 암호를 얻기 위한 보안 메커니즘을 제공 합니다. UI 프롬프트를 사용 하면 암호 누수가 발생 하지 않을 수 있습니다.

### <a name="deploying-db-connection-strings"></a>DB 연결 문자열 배포

DB 연결 문자열은 앱 설정과 유사 하 게 처리 됩니다. Visual Studio에서 웹 앱을 배포 하는 경우 연결 문자열이 구성 됩니다. 포털에서이를 확인할 수 있습니다. 연결 문자열을 설정 하는 권장 방법은 PowerShell을 사용 하는 것입니다. PowerShell 스크립트의 예를 보려면에서 웹 사이트 및 데이터베이스를 만들고 [Azure 스크립트 라이브러리](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)에서 [New-AzureWebsitewithDB](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 를 다운로드 하 여 웹 사이트의 연결 문자열을 설정 합니다.

<a id="not"></a>
## <a name="notes-for-php"></a>PHP에 대 한 참고 사항

**앱 설정** 및 **연결 문자열** 의 키-값 쌍은 Azure App Service의 환경 변수에 저장 되므로 PHP와 같은 웹 앱 프레임 워크를 사용 하는 개발자는 이러한 값을 쉽게 검색할 수 있습니다. Stefan Schackow 's [Microsoft Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) 블로그 게시물에서 앱 설정 및 연결 문자열을 읽는 PHP 코드 조각을 보여 줍니다.

## <a name="notes-for-on-premises-servers"></a>온-프레미스 서버에 대 한 참고 사항

온-프레미스 웹 서버에 배포 하는 경우 [구성 파일의 구성 섹션을 암호화](https://msdn.microsoft.com/library/ff647398.aspx)하 여 비밀을 보호할 수 있습니다. 또는 Azure Websites에 권장 되는 동일한 방법을 사용할 수 있습니다. 구성 파일에서 개발 설정을 유지 하 고 프로덕션 설정에 환경 변수 값을 사용 합니다. 그러나이 경우에는 Azure Websites에서 자동 인 기능의 응용 프로그램 코드를 작성 해야 합니다. 환경 변수에서 설정을 검색 하 고 구성 파일 설정 대신 해당 값을 사용 하거나 구성 파일 설정을 사용 합니다. 환경 변수를 찾을 수 없습니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

웹 앱 + 데이터베이스를 만드는 PowerShell 스크립트의 예를 보려면 [Azure 스크립트 라이브러리](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)에서 연결 문자열 + 앱 설정, [New-AzureWebsitewithDB](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 다운로드를 설정 합니다. 

Stefan Schackow 's [Microsoft Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식을](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) 참조 하세요.

검토를 위해 [@blowdart](https://twitter.com/blowdart) (Barry Dorrans) 및 Carlos Farre에 대해 특별히 감사 합니다.
