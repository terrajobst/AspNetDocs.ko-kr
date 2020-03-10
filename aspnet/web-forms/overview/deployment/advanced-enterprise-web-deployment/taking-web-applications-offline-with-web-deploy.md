---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
title: 웹 배포를 사용 하 여 웹 응용 프로그램을 오프 라인 상태로 만들기 Microsoft Docs
author: jrjlee
description: 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 Depl를 사용 하 여 자동화 된 배포 기간 동안 웹 응용 프로그램을 오프 라인으로 전환 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3e9f6e7d-8967-4586-94d5-d3a122f12529
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
msc.type: authoredcontent
ms.openlocfilehash: ba60664a0c3daa0650cd7e7cfc4ab9da08df3440
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422213"
---
# <a name="taking-web-applications-offline-with-web-deploy"></a>웹 배포를 통해 웹 애플리케이션을 오프라인으로 전환

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 자동화 된 배포 기간 동안 웹 응용 프로그램을 오프 라인으로 전환 하는 방법을 설명 합니다. 웹 응용 프로그램을 검색 하는 사용자는 배포가 완료 될 때까지 *오프 라인 .htm 파일\_응용* 프로그램으로 리디렉션됩니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="task-overview"></a>작업 개요

여러 시나리오에서 데이터베이스 또는 웹 서비스와 같은 관련 구성 요소를 변경 하는 동안 웹 응용 프로그램을 오프 라인 상태로 만들 수 있습니다. 일반적으로 IIS 및 ASP.NET에서는 IIS 웹 사이트 또는 웹 응용 프로그램의 루트 폴더에 라는\_이름의 파일을 배치 하 여이를 수행 합니다 *.* *앱\_오프 라인 .htm* 파일은 표준 HTML 파일 이며 일반적으로 유지 관리로 인해 사이트를 일시적으로 사용할 수 없음을 사용자에 게 알리는 간단한 메시지를 포함 합니다. *앱\_오프 라인 .htm* 파일이 웹 사이트의 루트 폴더에 있는 동안 IIS는 모든 요청을 파일에 자동으로 리디렉션합니다. 업데이트를 완료 한 후에는 *오프 라인 .htm 파일\_앱* 을 제거 하 고 웹 사이트에서 평소와 같은 요청 처리를 다시 시작 합니다.

웹 배포를 사용 하 여 대상 환경에 대 한 자동 또는 단일 단계 배포를 수행 하는 경우에는 앱을 추가 및 제거 하 고 *오프 라인 .htm 파일\_* 배포 프로세스에 통합 하는 것이 좋습니다. 이렇게 하려면 다음과 같은 개략적인 작업을 완료 해야 합니다.

- 배포 프로세스를 제어 하는 데 사용 하는 Microsoft Build Engine (MSBuild) 프로젝트 파일에서 배포 작업을 시작 하기 전에 응용 프로그램을 *오프 라인 .htm 파일\_* 대상 서버에 복사 하는 msbuild 대상을 만듭니다.
- 모든 배포 작업이 완료 되 면 대상 서버에서 *오프 라인 .htm 파일\_앱* 을 제거 하는 또 다른 MSBuild 대상을 추가 합니다.
- 웹 응용 프로그램 프로젝트에서 웹 배포 호출 될 때 *앱\_오프 라인 .htm* 파일이 배포 패키지에 추가 되도록 하는 *..* n e t 파일을 만듭니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 보여 줍니다. 이 항목의 작업 및 연습에서는 웹 응용 프로그램 프로젝트가 하나 이상 포함 된 솔루션을 이미 만들었고 사용자 지정 프로젝트 파일을 사용 하 여 [엔터프라이즈의 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)에 설명 된 대로 배포 프로세스를 제어 하는 것으로 가정 합니다. 또는 [연락처 관리자](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션을 사용 하 여 항목의 예제를 따를 수 있습니다.

## <a name="adding-an-app_offline-file-to-a-web-application-project"></a>웹 응용 프로그램 프로젝트에 앱\_오프 라인 파일 추가

완료 해야 하는 첫 번째 작업은 웹 응용 프로그램 프로젝트에 *앱\_오프 라인* 파일을 추가 하는 것입니다.

- 파일이 개발 프로세스를 방해 하지 않도록 방지 하려면 (응용 프로그램을 영구적으로 오프 라인으로 설정 하지 않음), *앱\_오프 라인*으로 설정 해야 합니다. 예를 들어 파일 앱의 이름을 *offline-template\_* 로 설정할 수 있습니다.
- 파일이 있는 그대로 배포 되지 않도록 하려면 빌드 작업을 **None**으로 설정 해야 합니다.

**웹 응용 프로그램 프로젝트에 앱\_오프 라인 파일을 추가 하려면**

1. Visual Studio 2010에서 솔루션을 엽니다.
2. **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 가리킨 다음 **새 항목**을 클릭 합니다.
3. **새 항목 추가** 대화 상자에서 **HTML 페이지**를 선택 합니다.
4. **이름** 상자에 **App\_offline-template**를 입력 한 다음 **추가**를 클릭 합니다.

    ![](taking-web-applications-offline-with-web-deploy/_static/image1.png)
5. 몇 가지 간단한 HTML을 추가 하 여 응용 프로그램을 사용할 수 없음을 사용자에 게 알리고 파일을 저장 합니다. 서버 쪽 태그 (예: "asp:" 접두사가 붙은 태그)는 포함 하지 마십시오. 

    ![](taking-web-applications-offline-with-web-deploy/_static/image2.png)
6. **솔루션 탐색기** 창에서 새 파일을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.
7. **속성** 창의 **빌드 작업** 행에서 **없음**을 선택 합니다.

    ![](taking-web-applications-offline-with-web-deploy/_static/image3.png)

## <a name="deploying-and-deleting-an-app_offline-file"></a>오프 라인 파일\_앱 배포 및 삭제

다음 단계는 배포 프로세스를 시작할 때 대상 서버에 파일을 복사 하 고 끝에 제거 하는 배포 논리를 수정 하는 것입니다.

> [!NOTE]
> 다음 절차에서는 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 대로 사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 것으로 가정 합니다. Visual Studio에서 직접 배포 하는 경우에는 다른 방법을 사용 해야 합니다. Sayed Ibrahim Hashimi [는 게시 하는 동안 웹 앱을 오프 라인으로 전환 하는 방법에 대](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)한 이러한 접근 방식을 설명 합니다.

*앱\_오프 라인* 파일을 대상 IIS 웹 사이트에 배포 하려면 [웹 배포 **contentpath** 공급자](https://technet.microsoft.com/library/dd569034(WS.10).aspx)를 사용 하 여 msdeploy.exe를 호출 해야 합니다. **Contentpath** 공급자는 실제 디렉터리 경로와 iis 웹 사이트 또는 응용 프로그램 경로를 지원 합니다. 그러면 Visual Studio 프로젝트 폴더와 iis 웹 응용 프로그램 간에 파일을 동기화 하는 데 이상적인 선택이 됩니다. 파일을 배포 하려면 다음과 같이 Msdeploy.exe 명령을 지정 해야 합니다.

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample1.cmd)]

배포 프로세스가 끝날 때 대상 사이트에서 파일을 제거 하려면 다음 명령을 명령과 같이 지정 합니다.

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample2.cmd)]

빌드 및 배포 프로세스의 일부로 이러한 명령을 자동화 하려면 사용자 지정 MSBuild 프로젝트 파일에 통합 해야 합니다. 다음 절차에서는이 작업을 수행 하는 방법을 설명 합니다.

**앱\_오프 라인 파일을 배포 및 삭제 하려면**

1. Visual Studio 2010에서 배포 프로세스를 제어 하는 MSBuild 프로젝트 파일을 엽니다. [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션에서이는 *게시 proj* 파일입니다.
2. 루트 **프로젝트** 요소에서 새 **PropertyGroup** 요소를 만들어 *앱\_오프 라인* 배포에 대 한 변수를 저장 합니다.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample3.xml)]
3. **SourceRoot** 속성은 *Publish. proj* 파일의 다른 위치에 정의 됩니다. 이는&#x2014; *게시 proj* 파일의 위치를 기준으로 하 여 현재 경로를 기준으로 하는 소스 콘텐츠에 대 한 루트 폴더의 위치를 나타냅니다.
4. **Contentpath** 공급자는 상대 파일 경로를 허용 하지 않으므로 배포할 수 있으려면 먼저 원본 파일의 절대 경로를 가져와야 합니다. [ConvertToAbsolutePath](https://msdn.microsoft.com/library/bb882668.aspx) 작업을 사용 하 여이 작업을 수행할 수 있습니다.
5. **GetAppOfflineAbsolutePath**라는 새 **Target** 요소를 추가 합니다. 이 대상 내에서 **ConvertToAbsolutePath** 작업을 사용 하 여 프로젝트 폴더에 있는 *앱\_오프 라인 템플릿* 파일의 절대 경로를 가져옵니다.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample4.xml)]
6. 이 대상은 프로젝트 폴더에서 *앱\_오프 라인 템플릿* 파일에 대 한 상대 경로를 사용 하 여 새 속성에 절대 파일 경로로 저장 합니다. **BeforeTargets** 특성은이 대상이 다음 단계에서 만들 **Deployappoffline** 대상 보다 먼저 실행 되도록 지정 합니다.
7. **Deployappoffline**이라는 새 대상을 추가 합니다. 이 대상 내에서 *앱\_오프 라인* 파일을 대상 웹 서버에 배포 하는 msdeploy.exe 명령을 호출 합니다.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample5.xml)]
8. 이 예제에서 **ContactManagerIisPath** 속성은 프로젝트 파일의 다른 위치에 정의 됩니다. 이는 단순히 *[Iis 웹 사이트 이름]/[응용 프로그램 이름]* 형식의 IIS 응용 프로그램 경로입니다. 사용자는 대상에 조건을 포함 하 여 속성 값을 변경 하거나 명령줄 매개 변수를 제공 하 여 *오프 라인 배포를\_오프 라인* 으로 전환할 수 있습니다.
9. **Deleteappoffline**이라는 새 대상을 추가 합니다. 이 대상 내에서 대상 웹 서버에서 *앱\_오프 라인* 파일을 제거 하는 msdeploy.exe 명령을 호출 합니다.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample6.xml)]
10. 최종 작업은 프로젝트 파일을 실행 하는 동안 적절 한 지점에서 이러한 새 대상을 호출 하는 것입니다. 다양 한 방법으로이 작업을 수행할 수 있습니다. 예를 들어, *Publish. proj* 파일에서 **FullPublishDependsOn** 속성은 **fullpublish** 기본 대상이 호출 될 때 순서 대로 실행 해야 하는 대상 목록을 지정 합니다.
11. 게시 프로세스의 적절 한 지점에서 **deployappoffline** 및 **deleteappoffline** 대상을 호출 하도록 MSBuild 프로젝트 파일을 수정 합니다.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample7.xml)]

사용자 지정 MSBuild 프로젝트 파일을 실행 하면 성공적으로 빌드한 후 *응용 프로그램\_오프 라인* 파일이 서버에 즉시 배포 됩니다. 모든 배포 작업이 완료 되 면 서버에서 삭제 됩니다.

## <a name="adding-an-app_offline-file-to-deployment-packages"></a>배포 패키지에 앱\_오프 라인 파일 추가

배포를 구성 하는 방법에 따라 대상에 웹 패키지를 배포할 때 *앱\_* 와 같은 대상 IIS 웹 응용 프로그램&#x2014;&#x2014;의 모든 기존 콘텐츠를 자동으로 삭제할 수 있습니다. *응용 프로그램\_오프 라인 .htm* 파일이 배포 기간 동안 그대로 유지 되도록 하려면 배포 프로세스를 시작할 때 직접 파일을 배포 하는 것 외에도 웹 배포 패키지 자체 내에 파일을 포함 해야 합니다.

- 이 항목의 이전 작업을 수행한 후에는 *앱\_오프 라인 .htm* 파일을 다른 파일 이름으로 ( *앱\_offline-template*) 사용 하 여 웹 응용 프로그램 프로젝트에 추가 하 고 빌드 작업을 **없음**으로 설정 합니다. 이러한 변경은 파일이 개발 및 디버깅을 방해 하지 않도록 방지 하기 위해 필요 합니다. 따라서 *앱\_오프 라인 .htm* 파일이 웹 배포 패키지에 포함 되도록 패키징 프로세스를 사용자 지정 해야 합니다.

웹 게시 파이프라인 (WPP)은 **FilesForPackagingFromProject** 라는 항목 목록을 사용 하 여 웹 배포 패키지에 포함 되어야 하는 파일 목록을 작성 합니다. 이 목록에 사용자 고유의 항목을 추가 하 여 웹 패키지의 콘텐츠를 사용자 지정할 수 있습니다. 이렇게 하려면 다음과 같은 개략적인 단계를 완료 해야 합니다.

1. 프로젝트 파일과 동일한 폴더에 *[project name]. wpp. .targets* 라는 사용자 지정 프로젝트 파일을 만듭니다.

    > [!NOTE]
    > 웹 응용 프로그램 프로젝트&#x2014;파일과 동일한 *폴더 (예*&#x2014;: 빌드 및 배포 프로세스를 제어 하는 데 사용 하는 사용자 지정 프로젝트 파일)와 동일한 폴더에 있어야 *합니다.*
2. **CopyAllFilesToSingleFolderForPackage** 파일 *에서* *실행 되는 새* MSBuild 대상을 만듭니다. 패키지에 포함할 항목의 목록을 작성 하는 WPP 대상입니다.
3. 새 대상에서 **ItemGroup** 요소를 만듭니다.
4. **ItemGroup** 요소에서 **FilesForPackagingFromProject** 항목을 추가 하 고 *오프 라인 .htm 파일\_앱* 을 지정 합니다.

이 *파일은* 다음과 유사 합니다.

[!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample8.xml)]

다음은이 예의 핵심 사항입니다.

- **BeforeTargets** 특성은 **CopyAllFilesToSingleFolderForPackage** 대상 바로 앞에서 실행 되도록 지정 하 여이 대상을 WPP에 삽입 합니다.
- **FilesForPackagingFromProject** 항목은 **DestinationRelativePath** 메타 데이터 값을 사용 하 여 목록에 추가 된 파일의 이름을 *app\_offline-template* 에서 *app\_오프 라인* 으로 바꿉니다.

다음 절차에서는 웹 응용 프로그램 프로젝트에이 *.* n e t .targets 파일을 추가 하는 방법을 보여 줍니다.

**웹 배포 패키지에. n e t .targets 파일을 추가 하려면**

1. Visual Studio 2010에서 솔루션을 엽니다.
2. **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 (예 **:),** **추가**를 가리킨 다음 **새 항목**을 클릭 합니다.
3. **새 항목 추가** 대화 상자에서 **XML 파일** 템플릿을 선택 합니다.
4. **이름** 상자에 *[project Name] * * * *..* t a g e * (예: **의사**(...))를 입력 한 다음 **추가**를 클릭 합니다.

    ![](taking-web-applications-offline-with-web-deploy/_static/image4.png)

    > [!NOTE]
    > 프로젝트의 루트 노드에 새 항목을 추가 하는 경우 해당 파일은 프로젝트 파일과 동일한 폴더에 만들어집니다. Windows 탐색기에서 폴더를 열어이를 확인할 수 있습니다.
5. 파일에서 앞에서 설명한 MSBuild 태그를 추가 합니다.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample9.xml)]
6. *[Project name] .targets .targets* 파일을 저장 한 후 닫습니다.

다음 번에 웹 응용 프로그램 프로젝트를 빌드하고 패키지할 때 WPP는 *wpp 파일을* 자동으로 검색 합니다. *앱\_offline-template* 파일은 결과 웹 배포 패키지에 *앱\_오프 라인 .htm*으로 포함 됩니다.

> [!NOTE]
> 배포가 실패 하면 *앱\_오프 라인 .htm* 파일이 그대로 유지 되 고 응용 프로그램이 오프 라인 상태로 유지 됩니다. 이는 일반적으로 원하는 동작입니다. 응용 프로그램을 다시 온라인 상태로 전환 하려면 웹 서버에서 *오프 라인 .htm 파일\_앱* 을 삭제할 수 있습니다. 또는 오류를 수정 하 고 성공적인 배포를 실행 하는 경우 *앱\_오프 라인 .htm* 파일이 제거 됩니다.

## <a name="conclusion"></a>결론

이 항목에서는 배포 하는\_동안 응용 프로그램을 오프 라인으로 전환 하는 방법에 대해 설명 했습니다 *.* 배포 프로세스 시작 시 대상 서버에 응용 프로그램을 오프 라인으로 설정 하 고 끝에 해당 파일을 제거 하는 방법을 설명 합니다. 또한 웹 배포 패키지에 *\_응용 프로그램을 오프 라인 .htm* 파일에 포함 하는 방법도 살펴보았습니다.

## <a name="further-reading"></a>추가 참고 자료

패키징 및 배포 프로세스에 대 한 자세한 내용은 [웹 응용 프로그램 프로젝트 빌드 및 패키징](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [웹 패키지 배포에 대 한 매개 변수 구성](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)및 [웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)를 참조 하세요.

이러한 자습서에서 설명 하는 사용자 지정 MSBuild 프로젝트 파일 방법을 사용 하지 않고 Visual Studio에서 직접 웹 응용 프로그램을 게시 하는 경우 게시 하는 동안 약간 다른 방법을 사용 하 여 응용 프로그램을 오프 라인으로 전환 해야 합니다. 프로세스.

> [!div class="step-by-step"]
> [이전](excluding-files-and-folders-from-deployment.md)
> [다음](running-windows-powershell-scripts-from-msbuild-project-files.md)
