---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: 패키징 프로세스 문제 해결 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 EnablePackageProcessLoggingAndAssert 속성을 사용 하 여 패키징 프로세스에 대 한 자세한 정보를 수집 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509753"
---
# <a name="troubleshooting-the-packaging-process"></a>패키징 프로세스 문제 해결

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 Microsoft Build Engine (MSBuild)에서 **EnablePackageProcessLoggingAndAssert** 속성을 사용 하 여 패키징 프로세스에 대 한 자세한 정보를 수집 하는 방법에 대해 설명 합니다.
> 
> **EnablePackageProcessLoggingAndAssert** 속성을 **true**로 설정 하면 MSBuild에서 다음을 수행 합니다.
> 
> - 패키징 프로세스에 대 한 추가 정보를 빌드 로그에 추가 합니다.
> - 특정 조건에 따라 오류를 기록 합니다. 예를 들어 패키지 목록에서 중복 된 파일을 찾을 수 있습니다.
> - *ProjectName*\_패키지 폴더에 로그 디렉터리를 만들고이를 사용 하 여 패키지 중인 파일에 대 한 정보를 기록 합니다.
> 
> 패키징 프로세스가 실패 하거나 웹 배포 패키지에 원하는 파일이 포함 되지 않은 경우이 정보를 사용 하 여 프로세스 문제를 해결 하 고 문제가 발생 한 위치를 파악할 수 있습니다.
> 
> > [!NOTE]
> > **EnablePackageProcessLoggingAndAssert** 속성은 **디버그** 구성을 사용 하 여 프로젝트를 빌드하는 경우에만 작동 합니다. 다른 구성에서는 속성이 무시 됩니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a>EnablePackageProcessLoggingAndAssert 속성 이해

웹 [응용 프로그램 프로젝트 빌드 및 패키징을](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) 통해 웹 게시 파이프라인 (WPP)에서 msbuild의 기능을 확장 하 고 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)와 통합할 수 있는 msbuild 대상 집합을 제공 하는 방법에 대해 설명 했습니다. 웹 응용 프로그램 프로젝트를 패키지할 때 WPP 대상을 호출 하 게 됩니다.

이러한 많은 WPP 대상에는 **EnablePackageProcessLoggingAndAssert** 속성이 **true**로 설정 된 경우 추가 정보를 기록 하는 조건부 논리가 포함 됩니다. 예를 들어 **패키지** 대상을 검토 하는 경우 추가 로그 디렉터리를 만들고 **EnablePackageProcessLoggingAndAssert** 가 **true**인 경우 텍스트 파일에 파일 목록을 기록 하는 것을 볼 수 있습니다.

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> WPP 대상은% PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더에 있는 *Microsoft .targets* 파일에 정의 되어 있습니다. 이 파일을 열고 Visual Studio 2010 또는 모든 XML 편집기에서 대상을 검토할 수 있습니다. 파일의 내용을 수정 하지 않도록 주의 하십시오.

## <a name="enabling-the-additional-logging"></a>추가 로깅 사용

프로젝트를 빌드하는 방법에 따라 다양 한 방법으로 **EnablePackageProcessLoggingAndAssert** 속성에 대 한 값을 제공할 수 있습니다.

명령줄에서 프로젝트를 빌드하는 경우 명령줄 인수로 **EnablePackageProcessLoggingAndAssert** 속성에 대 한 값을 제공할 수 있습니다.

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

사용자 지정 프로젝트 파일을 사용 하 여 프로젝트를 빌드하는 경우 **MSBuild** 작업의 **Properties** 특성에 **EnablePackageProcessLoggingAndAssert** 값을 포함할 수 있습니다.

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

Team Foundation Server (TFS) 빌드 정의를 사용 하 여 프로젝트를 빌드하는 경우 **MSBuild 인수** 행에서 **EnablePackageProcessLoggingAndAssert** 속성에 대 한 값을 제공할 수 있습니다.![](troubleshooting-the-packaging-process/_static/image1.png)

> [!NOTE]
> 빌드 정의를 만들고 구성 하는 방법에 대 한 자세한 내용은 [배포를 지 원하는 빌드 정의 만들기](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)를 참조 하세요.

또는 모든 빌드에서 패키지를 포함 하려는 경우 웹 응용 프로그램 프로젝트에 대 한 프로젝트 파일을 수정 하 여 **EnablePackageProcessLoggingAndAssert** 속성을 **true**로 설정할 수 있습니다. .Csproj 또는 .vbproj 파일 내의 첫 번째 **PropertyGroup** 요소에 속성을 추가 해야 합니다.

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a>로그 파일 검토

**EnablePackageProcessLoggingAndAssert** 가 **true**로 설정 된 웹 응용 프로그램 프로젝트를 빌드하고 패키지할 경우 MSBuild는 *ProjectName*\_package 폴더에 Log 라는 추가 폴더를 만듭니다. 로그 폴더는 다음과 같은 다양 한 파일을 포함 합니다.

![](troubleshooting-the-packaging-process/_static/image2.png)

표시 되는 파일 목록은 프로젝트의 항목 및 빌드 프로세스에 따라 달라 집니다. 그러나 이러한 파일은 일반적으로 프로세스의 다양 한 단계에서, WPP가 패키징을 위해 수집 하는 파일 목록을 기록 하는 데 사용 됩니다.

- *PreExcludePipelineCollectFilesPhaseFileList* 파일은 제외에 지정 된 파일이 제거 되기 전에 MSBuild가 패키징을 수집 하는 파일을 나열 합니다.
- *AfterExcludeFilesFilesList* 파일에는 제외 하도록 지정 된 파일이 제거 된 후 수정 된 파일 목록이 포함 되어 있습니다.

    > [!NOTE]
    > 패키징 프로세스에서 파일 및 폴더를 제외 하는 방법에 대 한 자세한 내용은 [배포에서 파일 및 폴더 제외](excluding-files-and-folders-from-deployment.md)를 참조 하세요.
- *AfterTransformWebConfig* 파일에는 *web.config* 변환이 수행 된 후 패키징을 위해 수집 된 파일이 나열 됩니다. 이 목록에서 *web.config* 및 *web.config*와 같은 구성 관련 *web.config* 변환 파일은 패키징을 위해 파일 목록에서 제외 됩니다 (예: *변환 된 단일 web.config가* 해당 자리에 포함 됩니다.
- *PostAutoParameterizationWebConfigConnectionStrings* *파일에는 web.config 파일의* 연결 문자열이 매개 변수화 된 후의 파일 목록이 포함 되어 있습니다. 이 프로세스를 통해 패키지를 배포할 때 대상 환경에 대 한 적절 한 설정으로 연결 문자열을 바꿀 수 있습니다.
- *Prepackage* 파일에는 패키지에 포함할 완성 된 빌드 전 파일 목록이 포함 되어 있습니다.

> [!NOTE]
> 추가 로그 파일의 이름은 일반적으로 WPP 대상에 해당 합니다. % PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더에 있는 *Microsoft* .targets 파일을 검사 하 여 이러한 대상을 검토할 수 있습니다.

웹 패키지의 내용이 예상과 다른 경우에는 이러한 파일을 검토 하 여 어떤 상황이 발생 했는지 확인 하는 것이 유용할 수 있습니다.

## <a name="conclusion"></a>결론

이 항목에서는 MSBuild에서 **EnablePackageProcessLoggingAndAssert** 속성을 사용 하 여 패키징 프로세스의 문제를 해결 하는 방법에 대해 설명 했습니다. 빌드 프로세스에 속성 값을 제공할 수 있는 다양 한 방법과 속성을 **true**로 설정할 때 기록 되는 추가 정보에 대해 설명 했습니다.

## <a name="further-reading"></a>추가 참고 자료

사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 방법에 대 한 자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)를 참조 하세요. WPP 및 패키징 프로세스를 관리 하는 방법에 대 한 자세한 내용은 [웹 응용 프로그램 프로젝트 빌드 및 패키징](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)을 참조 하세요. 웹 배포 패키지에서 특정 파일 및 폴더를 제외 하는 방법에 대 한 지침은 [배포에서 파일 및 폴더 제외](excluding-files-and-folders-from-deployment.md)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](running-windows-powershell-scripts-from-msbuild-project-files.md)
