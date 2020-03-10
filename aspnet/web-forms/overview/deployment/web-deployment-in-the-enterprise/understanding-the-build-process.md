---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
title: 빌드 프로세스 이해 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 엔터프라이즈급 빌드 및 배포 프로세스에 대 한 연습을 제공 합니다. 이 항목에서 설명 하는 방법은 사용자 지정 Microsoft 빌드 Engin를 사용 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5b982451-547b-4a2f-a5dc-79bc64d84d40
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
msc.type: authoredcontent
ms.openlocfilehash: 802d93f7ca987d018967275bae68b8c56d883a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520835"
---
# <a name="understanding-the-build-process"></a>빌드 프로세스 이해

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 엔터프라이즈급 빌드 및 배포 프로세스에 대 한 연습을 제공 합니다. 이 항목에서 설명 하는 방법은 사용자 지정 MSBuild (Microsoft Build Engine) 프로젝트 파일을 사용 하 여 프로세스의 모든 측면에 대 한 세분화 된 제어를 제공 합니다. 프로젝트 파일 내에서 사용자 지정 MSBuild 대상은 인터넷 정보 서비스 (IIS) 웹 배포 도구 (Msdeploy.exe) 및 데이터베이스 배포 유틸리티 nuget.exe와 같은 배포 유틸리티를 실행 하는 데 사용 됩니다.
> 
> > [!NOTE]
> > 이전 항목인 [프로젝트 파일 이해](understanding-the-project-file.md)에서는 MSBuild 프로젝트 파일의 주요 구성 요소에 대해 설명 하 고 여러 대상 환경에 대 한 배포를 지원 하기 위해 분할 프로젝트 파일의 개념을 소개 했습니다. 이러한 개념에 대해 잘 모르는 경우이 항목을 진행 하기 전에 [프로젝트 파일 이해](understanding-the-project-file.md) 를 검토 해야 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="build-and-deployment-overview"></a>빌드 및 배포 개요

[Contact Manager 솔루션](the-contact-manager-solution.md)에서 다음과 같은 세 개의 파일이 빌드 및 배포 프로세스를 제어 합니다.

- *유니버설 프로젝트 파일* (*Publish. proj*) 여기에는 대상 환경 간에 변경 되지 않는 빌드 및 배포 지침이 포함 됩니다.
- *환경 관련 프로젝트 파일* (*Env-Dev. proj*) 여기에는 특정 대상 환경에 특정 한 빌드 및 배포 설정이 포함 됩니다. 예를 들어, *env-Dev. proj* 파일을 사용 하 여 개발자 또는 테스트 환경에 대 한 설정을 제공 하 고, 스테이징 환경에 대 한 설정을 제공 하는 *env Stage* 라는 대체 파일을 만들 수 있습니다.
- *명령 파일* (*Publish-Dev*). 여기에는 실행할 프로젝트 파일을 지정 하는 Msbuild.exe 명령이 포함 됩니다. 모든 대상 환경에 대해 명령 파일을 만들 수 있습니다. 여기에는 각 파일에 다른 환경 관련 프로젝트 파일을 지정 하는 Msbuild.exe 명령이 있습니다. 이렇게 하면 개발자가 적절 한 명령 파일을 실행 하 여 다른 환경에 배포할 수 있습니다.

샘플 솔루션의 솔루션 게시 폴더에서 이러한 세 개의 파일을 찾을 수 있습니다.

![](understanding-the-build-process/_static/image1.png)

이러한 파일을 좀 더 자세히 살펴보기 전에이 방법을 사용할 때 전체 빌드 프로세스의 작동 방식을 살펴보겠습니다. 개략적인 수준에서 빌드 및 배포 프로세스는 다음과 같습니다.

![](understanding-the-build-process/_static/image2.png)

첫 번째는 두 프로젝트 파일이 유니버설 빌드 및 배포 명령을&#x2014;포함 하 고 환경 관련 설정이&#x2014;포함 된 파일을 단일 프로젝트 파일에 병합 하는 것입니다. 그런 다음 MSBuild는 프로젝트 파일의 지침을 따릅니다. 각 프로젝트에 대 한 프로젝트 파일을 사용 하 여 솔루션의 각 프로젝트를 빌드합니다. 그런 다음 웹 배포 (Msdeploy.exe)와 같은 다른 도구를 호출 하 고, VSDBCMD 유틸리티를 호출 하 여 웹 콘텐츠 및 데이터베이스를 대상 환경에 배포 합니다.

시작부터 완료까지 빌드 및 배포 프로세스는 다음 작업을 수행 합니다.

1. 새 빌드를 준비 하면서 출력 디렉터리의 내용을 삭제 합니다.
2. 솔루션의 각 프로젝트를 빌드합니다.

    1. 이 경우 웹&#x2014;프로젝트의 경우 ASP.NET MVC 웹 응용 프로그램 및 WCF 웹 서비스&#x2014;빌드 프로세스에서 각 프로젝트에 대 한 웹 배포 패키지를 만듭니다.
    2. 데이터베이스 프로젝트의 경우 빌드 프로세스에서 각 프로젝트에 대 한 배포 매니페스트 (deploymanifest 파일)를 만듭니다.
3. 이 메서드는 VSDBCMD 유틸리티를 사용 하 여 솔루션의 각 데이터베이스 프로젝트를 배포 합니다. 프로젝트&#x2014;의 다양 한 속성을 사용 하 여 대상 연결 문자열 및&#x2014;데이터베이스 이름과 .deploy 매니페스트 파일을 함께 사용 합니다.
4. 이 클래스는 Msdeploy.exe 유틸리티를 사용 하 여 솔루션의 각 웹 프로젝트를 배포 하 고 프로젝트 파일의 다양 한 속성을 사용 하 여 배포 프로세스를 제어 합니다.

샘플 솔루션을 사용 하 여이 프로세스를 보다 자세히 추적할 수 있습니다.

> [!NOTE]
> 사용자의 서버 환경에 맞는 환경 관련 프로젝트 파일을 사용자 지정 하는 방법에 대 한 지침은 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)을 참조 하세요.

## <a name="invoking-the-build-and-deployment-process"></a>빌드 및 배포 프로세스 호출

개발자 테스트 환경에 Contact Manager 솔루션을 배포 하려면 개발자가 *Publish-Dev* 명령 파일을 실행 합니다. 이렇게 하면 Msbuild.exe를 호출 하 고, 실행할 프로젝트 파일로 *proj* 를 지정 하 고,를 매개 변수 값으로 *Env* 를 지정 합니다.

[!code-console[Main](understanding-the-build-process/samples/sample1.cmd)]

> [!NOTE]
> **/Sfl** 스위치 (short **/file로거에서**short)는 현재 디렉터리에 있는 *msbuild .log* 파일에 빌드 출력을 기록 합니다. 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)를 참조 하세요.

이 시점에서 MSBuild는 실행을 시작 하 고, *Publish. proj* 파일을 로드 하 고, 그 안에 있는 명령 처리를 시작 합니다. 첫 번째 명령은 **TargetEnvPropsFile** 매개 변수가 지정 하는 프로젝트 파일을 가져오도록 MSBuild에 지시 합니다.

[!code-xml[Main](understanding-the-build-process/samples/sample2.xml)]

**TargetEnvPropsFile** 매개 변수는 *env-dev. proj* 파일을 지정 합니다. 따라서 MSBuild는 *Env* 파일의 콘텐츠를 *Publish.* proj 파일에 병합 합니다.

MSBuild가 병합 된 프로젝트 파일에서 발견 하는 다음 요소는 속성 그룹입니다. 속성은 파일에 표시 되는 순서 대로 처리 됩니다. MSBuild는 지정 된 조건을 충족 하는 각 속성에 대 한 키-값 쌍을 만듭니다. 파일에서 나중에 정의 된 속성은 파일에서 이전에 정의 된 동일한 이름의 속성을 덮어씁니다. 예를 들어 **Outputroot** 속성을 고려 합니다.

[!code-xml[Main](understanding-the-build-process/samples/sample3.xml)]

MSBuild에서 첫 번째 **outputroot** 요소를 처리할 때 비슷한 이름의 매개 변수를 제공 하지 않으면 **outputroot** 속성의 값 **을로 설정 합니다. \** . 두 번째 **outputroot** 요소가 발견 되 면 조건이 **true**로 평가 되 면 **Outputroot** 속성의 값을 **OutDir** 매개 변수 값으로 덮어씁니다.

MSBuild에서 발견 하는 다음 요소는 단일 항목 그룹 이며 **ProjectsToBuild**이라는 항목이 포함 되어 있습니다.

[!code-xml[Main](understanding-the-build-process/samples/sample4.xml)]

MSBuild는 이름이 **ProjectsToBuild**인 항목 목록을 빌드하여이 명령을 처리 합니다. 이 경우 항목 목록에는 솔루션 파일의 경로와&#x2014;파일 이름을 포함 하는 단일 값이 포함 됩니다.

이 시점에서 나머지 요소는 대상입니다. 대상은 기본적으로 속성 및 항목과&#x2014;다르게 처리 되지만, 사용자가 명시적으로 지정 하거나 프로젝트 파일 내의 다른 구문에서 호출 하지 않는 한 대상은 처리 되지 않습니다. 열기 **프로젝트** 태그에 **defaulttargets** 특성이 포함 되어 있다는 것을 기억 하세요.

[!code-xml[Main](understanding-the-build-process/samples/sample5.xml)]

이렇게 하면 Msbuild.exe가 호출 될 때 대상이 지정 되지 않은 경우 **Fullpublish** 대상을 호출 하도록 msbuild에 지시 합니다. **Fullpublish** 대상에는 작업이 포함 되지 않습니다. 대신 종속성 목록을 지정 하기만 하면 됩니다.

[!code-xml[Main](understanding-the-build-process/samples/sample6.xml)]

이 종속성은 **Fullpublish** 대상을 실행 하기 위해 제공 된 순서 대로이 대상 목록을 호출 해야 함을 MSBuild에 지시 합니다.

1. **정리** 대상을 호출 해야 합니다.
2. **Buildprojects** 대상을 호출 해야 합니다.
3. **GatherPackagesForPublishing** 대상을 호출 해야 합니다.
4. 이는 파일을 대상으로 호출 **해야 합니다.**
5. 이 클래스는 **웹 패키지** 대상을 호출 해야 합니다.

### <a name="the-clean-target"></a>정리 대상

**Clean** 대상은 새로운 빌드에 대 한 준비로 출력 디렉터리와 모든 콘텐츠를 기본적으로 삭제 합니다.

[!code-xml[Main](understanding-the-build-process/samples/sample7.xml)]

대상이 **ItemGroup** 요소를 포함 하 고 있습니다. **대상** 요소 내에서 속성 또는 항목을 정의 하는 경우 *동적* 속성 및 항목을 만듭니다. 즉, 속성이 나 항목은 대상이 실행 될 때까지 처리 되지 않습니다. 빌드 프로세스가 시작 될 때까지 출력 디렉터리가 존재 하지 않거나 파일을 포함 하지 않을 수 있으므로 **\_FilesToDelete** 목록을 정적 항목으로 빌드할 수 없습니다. 실행이 진행 될 때까지 기다려야 합니다. 따라서 목록을 대상 내의 동적 항목으로 빌드합니다.

> [!NOTE]
> 이 경우 **정리** 대상이 가장 먼저 실행 되기 때문에 동적 항목 그룹을 사용할 필요가 없습니다. 그러나 특정 시점에서 다른 순서로 대상을 실행할 수 있으므로 이러한 유형의 시나리오에서 동적 속성 및 항목을 사용 하는 것이 좋습니다.  
> 또한 사용 하지 않을 항목을 선언 하지 않아야 합니다. 특정 대상에만 사용 되는 항목이 있는 경우 대상에 배치 하 여 빌드 프로세스에서 불필요 한 오버 헤드를 제거 하는 것이 좋습니다.

동적 항목을 제거 하 고, **정리** 대상은 매우 간단 하며, 기본 제공 **Message**, **Delete**및 **RemoveDir** 작업을 다음과 같이 사용 합니다.

1. 로 거로 메시지를 보냅니다.
2. 삭제할 파일 목록을 작성 합니다.
3. 파일을 삭제 합니다.
4. 출력 디렉터리를 제거 합니다.

### <a name="the-buildprojects-target"></a>BuildProjects 대상

**Buildprojects** 대상은 기본적으로 샘플 솔루션의 모든 프로젝트를 빌드합니다.

[!code-xml[Main](understanding-the-build-process/samples/sample8.xml)]

이 대상은 이전 항목인 [프로젝트 파일 이해](understanding-the-project-file.md)에서 작업 및 대상이 속성 및 항목을 참조 하는 방법을 설명 하는 세부 정보에 설명 되어 있습니다. 이 시점에서 주로 **MSBuild** 작업에 관심이 있습니다. 이 작업을 사용 하 여 여러 프로젝트를 빌드할 수 있습니다. 태스크가 Msbuild.exe의 새 인스턴스를 만들지 않습니다. 현재 실행 중인 인스턴스를 사용 하 여 각 프로젝트를 빌드합니다. 이 예제에서 중요 한 점은 배포 속성입니다.

- **Deployonbuild** 속성은 각 프로젝트의 빌드가 완료 되 면 프로젝트 설정에서 배포 명령을 실행 하도록 MSBuild에 지시 합니다.
- **Deploytarget** 속성은 프로젝트가 빌드된 후에 호출 하려는 대상을 식별 합니다. 이 경우 **패키지** 대상은 배포 가능한 웹 패키지에 프로젝트 출력을 빌드합니다.

> [!NOTE]
> **패키지** 대상은 웹 게시 파이프라인 (WPP)을 호출 합니다 .이를 통해 MSBuild와 웹 배포 간의 통합을 제공 합니다. WPP에서 제공 하는 기본 제공 대상을 살펴보려면% PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더에 있는 *Microsoft* .targets 파일을 검토 하십시오.

### <a name="the-gatherpackagesforpublishing-target"></a>GatherPackagesForPublishing 대상

**GatherPackagesForPublishing** 대상을 연구 하면 실제로 어떤 작업도 포함 되지 않는다는 것을 알 수 있습니다. 대신 세 개의 동적 항목을 정의 하는 단일 항목 그룹을 포함 합니다.

[!code-xml[Main](understanding-the-build-process/samples/sample9.xml)]

이러한 항목은 **Buildprojects** 대상이 실행 될 때 생성 된 배포 패키지를 참조 합니다. 항목이 참조 하는 파일이 **Buildprojects** 대상이 실행 될 때까지 존재 하지 않기 때문에 프로젝트 파일에서 이러한 항목을 정적으로 정의할 수 없습니다. 대신 **Buildprojects** 대상이 실행 될 때까지 호출 되지 않는 대상 내에서 항목을 동적으로 정의 해야 합니다.

항목이이 대상&#x2014;내에서 사용 되지 않습니다 .이 대상은 각 항목 값과 연결 된 항목 및 메타 데이터를 간단 하 게 빌드합니다. 이러한 요소를 처리 한 후에는 지 수 **패키지** 항목에 두 개의 값, 즉 *valmanager* . c a c. p a c. .cmd 파일의 경로 *와 파일에* 대 한 경로가 포함 됩니다. 웹 배포는 각 프로젝트에 대 한 웹 패키지의 일부로 이러한 파일을 만들며, 패키지를 배포 하기 위해 대상 서버에서 호출 해야 하는 파일입니다. 이러한 파일 중 하나를 여는 경우에는 기본적으로 다양 한 빌드 관련 매개 변수 값을 사용 하는 Msdeploy.exe 명령이 표시 됩니다.

**Dbpublishpackages** 항목에는 단일 값, 즉 *연락처 관리자. 데이터베이스. deploymanifest* 파일의 경로가 포함 됩니다.

> [!NOTE]
> 데이터베이스 프로젝트를 빌드할 때 deploymanifest 파일이 생성 되 고 MSBuild 프로젝트 파일과 동일한 스키마를 사용 합니다. 데이터베이스 스키마 (.dbschema)의 위치와 배포 전 및 배포 후 스크립트의 세부 정보를 포함 하 여 데이터베이스를 배포 하는 데 필요한 모든 정보를 포함 합니다. 자세한 내용은 [데이터베이스 빌드 및 배포 개요](https://msdn.microsoft.com/library/aa833165.aspx)를 참조 하세요.

배포 패키지 및 데이터베이스 배포 매니페스트를 만들고 사용 하 여 [웹 응용 프로그램 프로젝트를 빌드하고 패키지](building-and-packaging-web-application-projects.md) 하 고 [데이터베이스 프로젝트를 배포](deploying-database-projects.md)하는 방법에 대해 자세히 알아봅니다.

### <a name="the-publishdbpackages-target"></a>패키지 대상

잠시 후에는 대상 환경에 배포 **하는 대상** 환경에 배포 하는 VSDBCMD **DB패키지** 대상이 VSDBCMD 유틸리티를 호출 합니다. 데이터베이스 배포를 구성 하려면 많은 의사 결정 및 미묘한 차이이 필요 하며, [데이터베이스 프로젝트 배포](deploying-database-projects.md) 및 [여러 환경에 대 한 데이터베이스 배포 사용자 지정](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)에서이에 대해 자세히 알아보세요. 이 항목에서는이 대상이 실제로 작동 하는 방식에 대해 집중적으로 설명 합니다.

먼저, 여는 태그에 **Outputs** 특성이 포함 되어 있는지 확인 합니다.

[!code-xml[Main](understanding-the-build-process/samples/sample10.xml)]

*대상 일괄 처리*의 예입니다. MSBuild 프로젝트 파일에서 일괄 처리는 컬렉션을 반복 하는 기술입니다. **Outputs** 특성의 값 "% (Db\\\doud\\\\\\\\\doudid **)"** 는 **Dbpublishpackages** 항목 목록의 **Identity** metadata 속성을 참조 합니다. **Outputs =% * * * (Itemlist)* 표기법은 다음과 같이 변환 됩니다.

- **Dbpublishpackages** 의 항목을 동일한 **id** 메타 데이터 값을 포함 하는 항목의 일괄 처리로 분할 합니다.
- 일괄 처리당 대상을 한 번 실행 합니다.

> [!NOTE]
> **Id** 는 만들 때 모든 항목에 할당 되는 [기본 제공 메타 데이터 값](https://msdn.microsoft.com/library/ms164313.aspx) 중 하나입니다. **항목 요소의** &#x2014; **Include** 특성 값, 즉 항목의 경로와 파일 이름을 나타냅니다.

이 경우 경로와 파일 이름이 같은 항목이 두 개 이상 이어야 하기 때문에 기본적으로 일괄 처리 크기를 사용 하 게 됩니다. 대상은 모든 데이터베이스 패키지에 대해 한 번 실행 됩니다.

**\_Cmd** 속성에서 비슷한 표기법을 확인할 수 있습니다 .이 속성은 적절 한 스위치를 사용 하 여 VSDBCMD 명령을 작성 합니다.

[!code-xml[Main](understanding-the-build-process/samples/sample11.xml)]

이 경우 **% (DbDatabaseConnectionString)** , **% (dbFullPath**) 및 **% (Db)** 는 모두 **dbpublishpackages** 항목 컬렉션의 메타 데이터 값을 참조 합니다. **\_Cmd** 속성은 명령을 호출 하는 **Exec** 작업에서 사용 됩니다.

[!code-xml[Main](understanding-the-build-process/samples/sample12.xml)]

이 표기법의 결과로 **Exec** 작업은 **DatabaseConnectionString**, **targetdatabase**및 **FullPath** 메타 데이터 값의 고유한 조합을 기반으로 일괄 처리를 만들며 각 일괄 처리에 대해 작업이 한 번씩 실행 됩니다. *작업 일괄 처리*의 예입니다. 그러나 대상 수준 일괄 처리가 항목 컬렉션을 단일 항목 일괄 처리로 이미 분할 했으므로 **Exec** 태스크는 대상의 각 반복에 대해 한 번만 실행 됩니다. 즉,이 작업은 솔루션의 각 데이터베이스 패키지에 대해 VSDBCMD 유틸리티를 한 번씩 호출 합니다.

> [!NOTE]
> 대상 및 작업 일괄 처리에 대 한 자세한 내용은 MSBuild [일괄 처리](https://msdn.microsoft.com/library/ms171473.aspx), [대상 일괄 처리의 항목 메타 데이터](https://msdn.microsoft.com/library/ms228229.aspx)및 [작업 일괄 처리의 항목 메타 데이터](https://msdn.microsoft.com/library/ms171474.aspx)를 참조 하세요.

### <a name="the-publishwebpackages-target"></a>대상 웹 패키지 대상

이 시점에서는 샘플 솔루션의 각 프로젝트에 대해 웹 배포 패키지를 생성 하는 **Buildprojects** 대상을 호출 했습니다. 각 패키지는 패키지를 대상 환경에 배포 하는 데 필요한 Msdeploy.exe 명령이 포함 된 *배포 .cmd* 파일이 며, 대상 환경에 필요한 세부 정보를 지정 하는 *setparameters .xml* 파일이 있습니다. 또한 관심 있는 *배포 .cmd* 파일이 포함 된 항목 컬렉션을 생성 하는 **GatherPackagesForPublishing** 대상을 호출 했습니다. 기본적으로, 대상 **웹 패키지** 대상은 다음 함수를 수행 합니다.

- **XmlPoke** 작업을 사용 하 여 대상 환경에 대 한 올바른 세부 정보를 포함 하도록 각 패키지에 대 한 *setparameters .xml* 파일을 조작 합니다.
- 적절 한 스위치를 사용 하 여 각 패키지에 대 한 *배포 .cmd* 파일을 호출 합니다.

지 수 **dbpackage** 대상과 마찬가지로, 대상 일괄 **처리 대상은 대상** 일괄 처리를 사용 하 여 각 웹 패키지에 대해 한 번씩 대상이 실행 되도록 합니다.

[!code-xml[Main](understanding-the-build-process/samples/sample13.xml)]

대상 내에서 **Exec** 작업은 각 웹 패키지에 대 한 *배포 .cmd* 파일을 실행 하는 데 사용 됩니다.

[!code-xml[Main](understanding-the-build-process/samples/sample14.xml)]

웹 패키지 배포를 구성 하는 방법에 대 한 자세한 내용은 [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)을 참조 하세요.

## <a name="conclusion"></a>결론

이 항목에서는 연락처 관리자 샘플 솔루션에 대 한 시작부터 끝까지 프로젝트 파일 분할을 사용 하 여 빌드 및 배포 프로세스를 제어 하는 방법에 대 한 연습을 제공 했습니다. 이 방법을 사용 하면 특정 환경 전용 명령 파일을 실행 하 여 반복 가능한 단일 단계로 복잡 한 엔터프라이즈급 배포를 실행할 수 있습니다.

## <a name="further-reading"></a>추가 참고 자료

프로젝트 파일 및 WPP에 대 한 자세한 소개는 Microsoft Build Engine 내부: Sayed Ibrahim Hashimi에서 [MSBuild 및 Team Foundation Build 사용](http://amzn.com/0735645248) 및 WILLIAM, ISBN: 978-0-7356-4524-0을 참조 하세요.

> [!div class="step-by-step"]
> [이전](understanding-the-project-file.md)
> [다음](building-and-packaging-web-application-projects.md)
