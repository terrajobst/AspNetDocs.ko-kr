---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: 배포에서 파일 및 폴더 제외 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 응용 프로그램 프로젝트를 빌드하고 패키지할 때 웹 배포 패키지에서 파일 및 폴더를 제외할 수 있는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438419"
---
# <a name="excluding-files-and-folders-from-deployment"></a>배포에서 파일 및 폴더 제외

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 웹 응용 프로그램 프로젝트를 빌드하고 패키지할 때 웹 배포 패키지에서 파일 및 폴더를 제외할 수 있는 방법에 대해 설명 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="overview"></a>개요

Visual Studio 2010에서 웹 응용 프로그램 프로젝트를 빌드하면 WPP (웹 게시 파이프라인)를 사용 하 여 컴파일된 웹 응용 프로그램을 배포 가능한 웹 패키지에 패키징하 여이 빌드 프로세스를 확장할 수 있습니다. 그런 다음 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여이 웹 패키지를 원격 IIS 웹 서버에 배포 하거나 IIS 관리자를 통해 수동으로 웹 패키지를 가져올 수 있습니다. 이 패키징 프로세스는 [웹 응용 프로그램 프로젝트 빌드 및 패키징](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)에 설명 되어 있습니다.

웹 패키지에 포함 되는 항목을 제어 하려면 어떻게 해야 하나요? 기본 프로젝트 파일을 통해 Visual Studio의 프로젝트 설정은 많은 시나리오에 대 한 충분 한 제어를 제공 합니다. 그러나 경우에 따라 특정 대상 환경에 맞게 웹 패키지의 콘텐츠를 조정 해야 할 수도 있습니다. 예를 들어 응용 프로그램을 테스트 환경에 배포할 때 로그 파일에 대 한 폴더를 포함 하 고 스테이징 또는 프로덕션 환경에 응용 프로그램을 배포할 때 해당 폴더를 제외 하려고 할 수 있습니다. 이 항목에서는이 작업을 수행 하는 방법을 보여 줍니다.

## <a name="what-gets-included-by-default"></a>기본적으로 포함 되는 항목

Visual Studio에서 웹 응용 프로그램 프로젝트 속성을 구성 하는 경우 **패키지/게시 웹** 페이지의 **배포할 항목** 목록에서 웹 배포 패키지에 포함할 항목을 지정할 수 있습니다. 기본적으로이 **응용 프로그램을 실행 하는 데 필요한 파일만**으로 설정 됩니다.

![](excluding-files-and-folders-from-deployment/_static/image1.png)

**이 응용 프로그램을 실행 하는 데 필요한 파일만**선택 하는 경우 WPP는 웹 패키지에 추가 해야 하는 파일을 확인 하려고 합니다. 다음 내용이 포함됩니다.

- 프로젝트에 대 한 모든 빌드 출력입니다.
- **콘텐츠**빌드 작업으로 표시 된 모든 파일

> [!NOTE]
> 포함할 파일을 결정 하는 논리는 다음 파일에 포함 되어 있습니다.   
> *%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\. OnlyFilesToRunTheApp.*

## <a name="excluding-specific-files-and-folders"></a>특정 파일 및 폴더 제외

어떤 경우에는 배포 되는 파일 및 폴더에 대해 보다 세분화 된 제어를 원할 수 있습니다. 미리 제외 하려는 파일을 확인 하 고 제외를 모든 대상 환경에 적용 하는 경우 각 파일의 **빌드 작업** 을 **None**으로 간단히 설정할 수 있습니다.

**배포에서 특정 파일을 제외 하려면**

1. **솔루션 탐색기** 창에서 파일을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.
2. **속성** 창의 **빌드 작업** 행에서 **없음**을 선택 합니다.

그러나이 방법은 항상 편리 하지는 않습니다. 예를 들어 대상 환경에 따라 그리고 Visual Studio 외부에서 포함 되는 파일 및 폴더를 변경 하는 것이 좋습니다. 예를 들어 Contact manager 샘플 솔루션에서 다음을 수행 합니다. Mvc 프로젝트의 내용을 확인 합니다.

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- 내부 폴더에는 개발자가 개발 목적으로 로컬 데이터베이스를 만들고, 삭제 하 고, 채우기 위해 사용 하는 몇 가지 SQL 스크립트가 포함 되어 있습니다. 이 폴더에는 스테이징 또는 프로덕션 환경에 배포할 내용이 없습니다.
- Scripts 폴더에는 여러 JavaScript 파일이 포함 되어 있습니다. 이러한 파일은 대부분 Visual Studio에서 디버깅을 지원 하거나 IntelliSense를 제공 하기 위해서만 포함 됩니다. 이러한 파일 중 일부는 스테이징 또는 프로덕션 환경에 배포 하면 안 됩니다. 그러나 문제 해결을 용이 하 게 하기 위해 개발자 테스트 환경에 배포 하는 것이 좋습니다.

프로젝트 파일을 조작 하 여 특정 파일 및 폴더를 제외할 수는 있지만 더 쉬운 방법이 있습니다. WPP에는 **ExcludeFromPackageFolders** 및 **ExcludeFromPackageFiles**라는 항목 목록을 작성 하 여 파일과 폴더를 제외 하는 메커니즘이 포함 되어 있습니다. 이러한 목록에 사용자 고유의 항목을 추가 하 여이 메커니즘을 확장할 수 있습니다. 이렇게 하려면 다음과 같은 개략적인 단계를 완료 해야 합니다.

1. 프로젝트 파일과 동일한 폴더에 *[project name]. wpp. .targets* 라는 사용자 지정 프로젝트 파일을 만듭니다.

    > [!NOTE]
    > 웹 응용 프로그램 프로젝트&#x2014;파일과 동일한 *폴더 (예*&#x2014;: 빌드 및 배포 프로세스를 제어 하는 데 사용 하는 사용자 지정 프로젝트 파일)와 동일한 폴더에 있어야 *합니다.*
2. *Wpp* 파일에서 **ItemGroup** 요소를 추가 합니다.
3. **ItemGroup** 요소에서 **ExcludeFromPackageFolders** 및 **ExcludeFromPackageFiles** 항목을 추가 하 여 필요에 따라 특정 파일 및 폴더를 제외 합니다.

*이 파일의* 기본 구조는 다음과 같습니다.

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

각 항목에는 **Fromtarget**이라는 항목 메타 데이터 요소가 포함 됩니다. 이는 빌드 프로세스에 영향을 주지 않는 선택적 값입니다. 사용자가 빌드 로그를 검토 하는 경우 특정 파일이 나 폴더가 생략 된 이유를 나타내는 역할만 합니다.

## <a name="excluding-files-and-folders-from-a-web-package"></a>웹 패키지에서 파일 및 폴더 제외

다음 절차에서는 웹 응용 프로그램 프로젝트에. n e t *.targets* 파일을 추가 하는 방법 및 프로젝트를 빌드할 때 파일을 사용 하 여 웹 패키지에서 특정 파일 및 폴더를 제외 하는 방법을 보여 줍니다.

**웹 배포 패키지에서 파일 및 폴더를 제외 하려면**

1. Visual Studio 2010에서 솔루션을 엽니다.
2. **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 (예 **:),** **추가**를 가리킨 다음 **새 항목**을 클릭 합니다.
3. **새 항목 추가** 대화 상자에서 **XML 파일** 템플릿을 선택 합니다.
4. **이름** 상자에 *[project Name] * * * *..* t a g e * (예: **의사**(...))를 입력 한 다음 **추가**를 클릭 합니다.

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > 프로젝트의 루트 노드에 새 항목을 추가 하는 경우 해당 파일은 프로젝트 파일과 동일한 폴더에 만들어집니다. Windows 탐색기에서 폴더를 열어이를 확인할 수 있습니다.
5. 파일에서 **프로젝트** 요소와 **ItemGroup** 요소를 추가 합니다.

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. 웹 패키지에서 폴더를 제외 하려면 **ItemGroup** 요소에 **ExcludeFromPackageFolders** 요소를 추가 합니다.

   1. **Include** 특성에서 제외 하려는 폴더를 세미콜론으로 구분한 목록을 제공 합니다.
   2. **Fromtarget** metadata 요소에서 폴더를 제외 하는 이유 (예: *wpp* 파일의 이름)를 나타내는 의미 있는 값을 제공 합니다.

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. 웹 패키지에서 파일을 제외 하려면 **ExcludeFromPackageFiles** 요소를 **ItemGroup** 요소에 추가 합니다.

   1. **Include** 특성에서 제외 하려는 파일의 세미콜론으로 구분 된 목록을 제공 합니다.
   2. **Fromtarget** metadata 요소에서 파일을 제외 하는 이유 (예: *wpp* 파일의 이름)를 나타내는 의미 있는 값을 제공 합니다.

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. 이제 *[project name]. wpp* 파일은 다음과 유사 합니다.

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. *[Project name] .targets .targets* 파일을 저장 한 후 닫습니다.

다음 번에 웹 응용 프로그램 프로젝트를 빌드하고 패키지할 때 WPP는 *wpp 파일을* 자동으로 검색 합니다. 지정한 모든 파일 및 폴더는 웹 패키지에 포함 되지 않습니다.

## <a name="conclusion"></a>결론

이 항목에서는 웹 응용 프로그램 프로젝트 파일과 동일한 폴더에 사용자 지정. n e t *.targets* 파일을 만들어 웹 패키지를 빌드할 때 특정 파일 및 폴더를 제외 하는 방법에 대해 설명 했습니다.

## <a name="further-reading"></a>추가 참고 자료

사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 방법에 대 한 자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)를 참조 하세요. 패키징 및 배포 프로세스에 대 한 자세한 내용은 [웹 응용 프로그램 프로젝트 빌드 및 패키징](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [웹 패키지 배포에 대 한 매개 변수 구성](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)및 [웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](deploying-membership-databases-to-enterprise-environments.md)
> [다음](taking-web-applications-offline-with-web-deploy.md)
