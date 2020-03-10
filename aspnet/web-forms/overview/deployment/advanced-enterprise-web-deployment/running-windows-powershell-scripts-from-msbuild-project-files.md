---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트 실행 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 빌드 및 배포 프로세스의 일부로 Windows PowerShell 스크립트를 실행 하는 방법에 대해 설명 합니다. 스크립트를 로컬로 실행할 수 있습니다. 즉,
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441449"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a>MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트 실행

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 빌드 및 배포 프로세스의 일부로 Windows PowerShell 스크립트를 실행 하는 방법에 대해 설명 합니다. 대상 웹 서버 또는 데이터베이스 서버와 같이 로컬에서 (즉, 빌드 서버에서) 또는 원격으로 스크립트를 실행할 수 있습니다.
> 
> 배포 후 Windows PowerShell 스크립트를 실행 하려는 많은 이유가 있습니다. 예를 들면 다음과 같습니다.
> 
> - 레지스트리에 사용자 지정 이벤트 소스를 추가 합니다.
> - 업로드할 파일 시스템 디렉터리를 생성 합니다.
> - 빌드 디렉터리를 정리 합니다.
> - 사용자 지정 로그 파일에 항목을 씁니다.
> - 새로 프로 비전 된 웹 응용 프로그램에 사용자를 초대 하는 전자 메일을 보냅니다.
> - 적절 한 권한이 있는 사용자 계정을 만듭니다.
> - SQL Server 인스턴스 간에 복제를 구성 합니다.
> 
> 이 항목에서는 MSBuild (Microsoft Build Engine) 프로젝트 파일의 사용자 지정 대상에서 로컬 및 원격으로 Windows PowerShell 스크립트를 실행 하는 방법을 보여 줍니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="task-overview"></a>작업 개요

자동 또는 단일 단계 배포 프로세스의 일부로 Windows PowerShell 스크립트를 실행 하려면 다음과 같은 개략적인 작업을 완료 해야 합니다.

- Windows PowerShell 스크립트를 솔루션에 추가 하 고 소스 제어에 추가 합니다.
- Windows PowerShell 스크립트를 호출 하는 명령을 만듭니다.
- 명령에서 모든 예약 된 XML 문자를 이스케이프 합니다.
- 사용자 지정 MSBuild 프로젝트 파일에서 대상을 만들고 **Exec** 작업을 사용 하 여 명령을 실행 합니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 보여 줍니다. 이 항목의 작업 및 연습에서는 이미 MSBuild 대상과 속성을 잘 알고 있고 사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 빌드 및 배포 프로세스를 구동 하는 방법을 이해 하 고 있다고 가정 합니다. 자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)를 참조 하세요.

## <a name="creating-and-adding-windows-powershell-scripts"></a>Windows PowerShell 스크립트 만들기 및 추가

이 항목의 태스크에서는 MSBuild에서 스크립트를 실행 하는 방법을 보여 주기 위해 **Logdeploy. ps1** 이라는 샘플 Windows PowerShell 스크립트를 사용 합니다. **Logdeploy. ps1** 스크립트에는 로그 파일에 한 줄 항목을 기록 하는 간단한 함수가 포함 되어 있습니다.

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

**Logdeploy. ps1** 스크립트는 두 개의 매개 변수를 허용 합니다. 첫 번째 매개 변수는 항목을 추가할 로그 파일의 전체 경로를 나타내고, 두 번째 매개 변수는 로그 파일에 기록 하려는 배포 대상을 나타냅니다. 스크립트를 실행 하면 로그 파일에 다음 형식으로 줄이 추가 됩니다.

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

MSBuild에서 **Logdeploy. ps1** 스크립트를 사용할 수 있도록 하려면 다음을 수행 해야 합니다.

- 소스 제어에 스크립트를 추가 합니다.
- Visual Studio 2010에서 솔루션에 스크립트를 추가 합니다.

빌드 서버 또는 원격 컴퓨터에서 스크립트를 실행할 계획 인지 여부에 관계 없이 솔루션 콘텐츠와 함께 스크립트를 배포할 필요가 없습니다. 한 가지 옵션은 솔루션 폴더에 스크립트를 추가 하는 것입니다. Contact Manager 예제에서 배포 프로세스의 일부로 Windows PowerShell 스크립트를 사용 하려는 경우 게시 솔루션 폴더에 스크립트를 추가 하는 것이 좋습니다.

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

솔루션 폴더의 콘텐츠는 빌드 서버에 원본 자료로 복사 됩니다. 그러나 프로젝트 출력의 일부는 구성 되지 않습니다.

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a>빌드 서버에서 Windows PowerShell 스크립트 실행

일부 시나리오에서는 프로젝트를 빌드하는 컴퓨터에서 Windows PowerShell 스크립트를 실행 하는 것이 좋습니다. 예를 들어 Windows PowerShell 스크립트를 사용 하 여 빌드 폴더를 정리 하거나 사용자 지정 로그 파일에 항목을 쓸 수 있습니다.

구문 측면에서 MSBuild 프로젝트 파일을 사용 하 여 Windows PowerShell 스크립트를 실행 하는 것은 일반 명령 프롬프트에서 Windows PowerShell 스크립트를 실행 하는 것과 같습니다. Powershell .exe 실행 파일을 호출 하 고 **– command** 스위치를 사용 하 여 Windows powershell을 실행 하려는 명령을 제공 해야 합니다. Windows PowerShell v2에서는 **– file** 스위치를 사용할 수도 있습니다. 이 명령은 다음 형식을 사용 해야 합니다.

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

다음은 그 예입니다.

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

스크립트의 경로에 공백이 포함 된 경우 파일 경로를 앰퍼샌드 앞에 오는 작은따옴표로 묶어야 합니다. 사용자가 이미 명령을 묶는 데 사용 했기 때문에 큰따옴표를 사용할 수 없습니다.

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

MSBuild에서이 명령을 호출 하는 경우 몇 가지 사항을 추가로 고려해 야 합니다. 먼저 **-비 대화형** 플래그를 포함 하 여 스크립트가 자동으로 실행 되도록 해야 합니다. 다음으로 적절 한 인수 값을 사용 하 여 **– set-executionpolicy** 플래그를 포함 해야 합니다. 이는 Windows PowerShell이 스크립트에 적용 되는 실행 정책을 지정 하며, 스크립트 실행을 방해할 수 있는 기본 실행 정책을 재정의할 수 있도록 합니다. 다음 인수 값 중에서 선택할 수 있습니다.

- **제한** 값을 사용 하면 스크립트가 서명 되었는지 여부에 관계 없이 Windows PowerShell에서 스크립트를 실행할 수 있습니다.
- **RemoteSigned** 값을 사용 하면 Windows PowerShell에서 로컬 컴퓨터에 생성 된 서명 되지 않은 스크립트를 실행할 수 있습니다. 그러나 다른 곳에서 만든 스크립트는 서명 해야 합니다. 실제로는 빌드 서버에서 로컬로 Windows PowerShell 스크립트를 만들 가능성이 거의 없습니다.
- **AllSigned** 값을 사용 하면 Windows PowerShell에서 서명 된 스크립트만 실행할 수 있습니다.

기본 실행 정책은 Windows PowerShell에서 스크립트 파일을 실행할 수 없도록 **제한**됩니다.

마지막으로, Windows PowerShell 명령에서 발생 하는 모든 예약 된 XML 문자를 이스케이프 해야 합니다.

- 작은따옴표를 **&amp;apos;** 로 바꿉니다.
- 큰따옴표를 **&amp;q;** 로 바꿉니다.
- 앰퍼샌드를 **&amp;amp** 로 바꾸기

- 이러한 변경을 수행 하는 경우 명령은 다음과 같습니다.

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

사용자 지정 MSBuild 프로젝트 파일 내에서 새 대상을 만들고 **Exec** 작업을 사용 하 여 다음 명령을 실행할 수 있습니다.

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

이 예제에서는 다음을 확인 합니다.

- 매개 변수 값 및 Windows PowerShell 실행 파일의 위치와 같은 모든 변수는 MSBuild 속성으로 선언 됩니다.
- 사용자가 명령줄에서 이러한 값을 재정의할 수 있도록 하는 조건이 포함 됩니다.
- **MSDeployComputerName** 속성은 프로젝트 파일의 다른 위치에 선언 됩니다.

빌드 프로세스의 일부로이 대상을 실행 하면 Windows PowerShell에서 명령을 실행 하 고 지정한 파일에 로그 항목을 기록 합니다.

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a>원격 컴퓨터에서 Windows PowerShell 스크립트 실행

Windows PowerShell은 WinRM ( [Windows 원격 관리](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) )을 통해 원격 컴퓨터에서 스크립트를 실행할 수 있습니다. 이렇게 하려면 [Invoke Command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet을 사용 해야 합니다. 이를 통해 원격 컴퓨터에 스크립트를 복사 하지 않고 하나 이상의 원격 컴퓨터에 대해 스크립트를 실행할 수 있습니다. 모든 결과는 스크립트를 실행 한 로컬 컴퓨터로 반환 됩니다.

> [!NOTE]
> **호출 명령** cmdlet을 사용 하 여 원격 컴퓨터에서 Windows PowerShell 스크립트를 실행 하기 전에 원격 메시지를 수락 하도록 WinRM 수신기를 구성 해야 합니다. 원격 컴퓨터에서 **winrm quickconfig** 명령을 실행 하 여이 작업을 수행할 수 있습니다. 자세한 내용은 [Windows 원격 관리 설치 및 구성](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)을 참조 하세요.

Windows PowerShell 창에서이 구문을 사용 하 여 원격 컴퓨터에서 **Logdeploy.** p s 1 스크립트를 실행 합니다.

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> **Invoke 명령을** 사용 하 여 스크립트 파일을 실행 하는 다른 여러 가지 방법이 있지만이 방법은 매개 변수 값을 제공 하 고 공백을 사용 하 여 경로를 관리 해야 하는 경우에 가장 간단 합니다.

명령 프롬프트에서이 명령을 실행 하는 경우 Windows PowerShell 실행 파일을 호출 하 고 **– command** 매개 변수를 사용 하 여 지침을 제공 해야 합니다.

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

이전과 마찬가지로 MSBuild에서 명령을 실행할 때 몇 가지 추가 스위치를 제공 하 고 예약 된 XML 문자를 이스케이프 해야 합니다.

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

마지막으로, 이전과 같이 사용자 지정 MSBuild 대상 내에서 **Exec** 작업을 사용 하 여 명령을 실행할 수 있습니다.

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

빌드 프로세스의 일부로이 대상을 실행 하는 경우 Windows PowerShell은 **– computername** 인수에 지정 된 컴퓨터에서 스크립트를 실행 합니다.

## <a name="conclusion"></a>결론

이 항목에서는 MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트를 실행 하는 방법에 대해 설명 했습니다. 이 방법을 사용 하 여 자동 또는 단일 단계 빌드 및 배포 프로세스의 일부로 Windows PowerShell 스크립트를 로컬 또는 원격 컴퓨터에서 실행할 수 있습니다.

## <a name="further-reading"></a>추가 참고 자료

Windows PowerShell 스크립트에 서명 하 고 실행 정책을 관리 하는 방법에 대 한 지침은 [Windows Powershell 스크립트 실행](https://technet.microsoft.com/library/ee176949.aspx)을 참조 하세요. 원격 컴퓨터에서 Windows PowerShell 명령을 실행 하는 방법에 대 한 지침은 [원격 명령 실행](https://technet.microsoft.com/library/dd819505.aspx)을 참조 하세요.

사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 방법에 대 한 자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](taking-web-applications-offline-with-web-deploy.md)
> [다음](troubleshooting-the-packaging-process.md)
