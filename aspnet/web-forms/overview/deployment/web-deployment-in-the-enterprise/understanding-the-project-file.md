---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: 프로젝트 파일 이해 | Microsoft Docs
author: jrjlee
description: MSBuild (Microsoft Build Engine) 프로젝트 파일은 빌드 및 배포 프로세스의 핵심입니다. 이 항목에서는 MSBuild에 대 한 개념적인 개요부터 시작 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 419fe51aaf65bddcc2c50380f099f842a8d9439c
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445692"
---
# <a name="understanding-the-project-file"></a>프로젝트 파일 이해

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> MSBuild (Microsoft Build Engine) 프로젝트 파일은 빌드 및 배포 프로세스의 핵심입니다. 이 항목에서는 MSBuild 및 프로젝트 파일에 대 한 개념적인 개요부터 시작 합니다. 프로젝트 파일을 사용할 때 제공 되는 주요 구성 요소에 대해 설명 하 고, 프로젝트 파일을 사용 하 여 실제 응용 프로그램을 배포 하는 방법의 예제를 통해 작동 합니다.
> 
> 학습 내용:
> 
> - MSBuild에서 MSBuild 프로젝트 파일을 사용 하 여 프로젝트를 빌드하는 방법입니다.
> - MSBuild는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)와 같은 배포 기술과 통합 됩니다.
> - 프로젝트 파일의 주요 구성 요소를 이해 하는 방법
> - 프로젝트 파일을 사용 하 여 복잡 한 응용 프로그램을 빌드하고 배포 하는 방법을 설명 합니다.

## <a name="msbuild-and-the-project-file"></a>MSBuild 및 프로젝트 파일

Visual Studio에서 솔루션을 만들고 빌드할 때 Visual Studio는 MSBuild를 사용 하 여 솔루션의 각 프로젝트를 빌드합니다. 모든 Visual Studio 프로젝트에는 프로젝트 형식&#x2014;(예: C# 프로젝트 (.csproj), Visual Basic.NET 프로젝트 (.vbproj) 또는 데이터베이스 프로젝트 (.dbproj))을 반영 하는 파일 확장명을 포함 하는 MSBuild 프로젝트 파일이 포함 되어 있습니다. 프로젝트를 빌드하기 위해 MSBuild는 프로젝트와 연결 된 프로젝트 파일을 처리 해야 합니다. 프로젝트 파일은 포함할 내용, 플랫폼 요구 사항, 버전 관리 정보, 웹 서버 또는 데이터베이스 서버 설정, 프로젝트를 빌드하기 위해 MSBuild에 필요한 모든 정보 및 지침을 포함 하는 XML 문서입니다. 수행 해야 하는 작업입니다.

MSBuild 프로젝트 파일은 [MSBUILD XML 스키마](/visualstudio/msbuild/msbuild-project-file-schema-reference)를 기반으로 하며, 결과적으로 빌드 프로세스가 완전히 열리고 투명 합니다. 또한 msbuild 엔진&#x2014;을 사용 하기 위해 Visual Studio를 설치할 필요는 없습니다. msbuild.exe 실행 파일은 .NET Framework의 일부 이며 명령 프롬프트에서 실행할 수 있습니다. 개발자는 MSBuild XML 스키마를 사용 하 여 MSBuild 프로젝트 파일을 직접 만들어 프로젝트를 빌드하고 배포 하는 방법을 정교 하 고 세분화 된 방식으로 제어할 수 있습니다. 이러한 사용자 지정 프로젝트 파일은 Visual Studio에서 자동으로 생성 하는 프로젝트 파일과 정확히 동일한 방식으로 작동 합니다.

> [!NOTE]
> Team Foundation Server (TFS)의 팀 빌드 서비스에서 MSBuild 프로젝트 파일을 사용할 수도 있습니다. 예를 들어 CI (지속적인 통합) 시나리오에서 프로젝트 파일을 사용 하 여 새 코드를 체크 인할 때 테스트 환경에 대 한 배포를 자동화할 수 있습니다. 자세한 내용은 [자동화 된 웹 배포에 대 한 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)을 참조 하세요.

### <a name="project-file-naming-conventions"></a>프로젝트 파일 명명 규칙

프로젝트 파일을 직접 만들 때 원하는 파일 확장명을 사용할 수 있습니다. 그러나 솔루션을 다른 사용자가 쉽게 이해할 수 있도록 하려면 다음과 같은 일반적인 규칙을 사용 해야 합니다.

- 프로젝트를 빌드하는 프로젝트 파일을 만들 때 proj 확장명을 사용 합니다.
- 다른 프로젝트 파일로 가져올 재사용 가능한 프로젝트 파일을 만들 때 .targets 확장명을 사용 합니다. 확장명이 .targets 인 파일은 일반적으로 모든 항목을 빌드하지는 않지만, proj 파일에 가져올 수 있는 명령만 포함 됩니다.

### <a name="integration-with-deployment-technologies"></a>배포 기술과 통합

ASP.NET 웹 응용 프로그램 및 ASP.NET MVC 웹 응용 프로그램과 같이 Visual Studio 2010에서 웹 응용 프로그램 프로젝트를 사용 하 여 작업 하는 경우 이러한 프로젝트에는 웹 응용 프로그램을 패키지 하 고 대상 환경에 배포 하는 기능이 기본적으로 포함 되어 있다는 것을 알 수 있습니다. 이러한 프로젝트의 **속성** 페이지에는 응용 프로그램의 구성 요소를 패키지 하 고 배포 하는 방법을 구성 하는 데 사용할 수 있는 **웹 패키지/게시** 및 **SQL 패키지/게시** 탭이 포함 됩니다. 그러면 **웹 패키지 및 게시** 탭이 표시 됩니다.

![](understanding-the-project-file/_static/image1.png)

이러한 기능을 사용 하는 기본 기술은 웹 게시 파이프라인 (WPP) 이라고 합니다. 웹 응용 프로그램에 대 한 전체 빌드, 패키지 및 배포 프로세스를 제공 하기 위해 웹 응용 프로그램은 기본적으로 MSBuild 및 [웹 배포](https://go.microsoft.com/?linkid=9805122) 함께 제공 됩니다.

좋은 소식은 웹 프로젝트용 사용자 지정 프로젝트 파일을 만들 때 WPP에서 제공 하는 통합 요소를 활용할 수 있다는 것입니다. 프로젝트 파일에 배포 지침을 포함 하 여 프로젝트를 빌드하고, 웹 배포 패키지를 만들고, 단일 프로젝트 파일을 통해 원격 서버에 이러한 패키지를 설치 하 고, MSBuild에 대 한 단일 호출을 수행할 수 있습니다. 빌드 프로세스의 일부로 다른 실행 파일을 호출할 수도 있습니다. 예를 들어, VSDBCMD 명령줄 도구를 실행 하 여 스키마 파일에서 데이터베이스를 배포할 수 있습니다. 이 항목에서는 이러한 기능을 활용 하 여 엔터프라이즈 배포 시나리오의 요구 사항을 충족 하는 방법을 알아봅니다.

> [!NOTE]
> 웹 응용 프로그램 배포 프로세스의 작동 방식에 대 한 자세한 내용은 [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/library/dd394698.aspx)를 참조 하세요.

## <a name="the-anatomy-of-a-project-file"></a>프로젝트 파일의 분석

빌드 프로세스를 좀 더 자세히 살펴보기 전에 MSBuild 프로젝트 파일의 기본 구조를 이해 하는 데 몇 분 정도 걸릴 수 있습니다. 이 섹션에서는 프로젝트 파일을 검토, 편집 또는 만들 때 발생 하는 보다 일반적인 요소에 대 한 개요를 제공 합니다. 특히 다음에 대해 알아봅니다.

- *속성* 을 사용 하 여 빌드 프로세스에 대 한 변수를 관리 하는 방법입니다.
- *항목* 을 사용 하 여 코드 파일과 같은 빌드 프로세스에 대 한 입력을 식별 하는 방법입니다.
- 프로젝트 파일의 다른 곳에 정의 된 *속성* 및 *항목* 을 사용 하 여 MSBuild에 실행 명령을 제공 하기 위해 *대상과* *작업* 을 사용 하는 방법입니다.

MSBuild 프로젝트 파일의 키 요소 간 관계를 보여 줍니다.

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a>Project 요소

[Project](https://msdn.microsoft.com/library/bcxfsh87.aspx) 요소는 모든 프로젝트 파일의 루트 요소입니다. 프로젝트 파일에 대 한 XML 스키마를 식별 하는 것 외에도 **프로젝트** 요소에는 빌드 프로세스에 대 한 진입점을 지정 하는 특성이 포함 될 수 있습니다. 예를 들어 [Contact Manager 샘플 솔루션](the-contact-manager-solution.md)에서, *Publish. Proj* 파일은 **fullpublish**라는 대상을 호출 하 여 빌드를 시작 하도록 지정 합니다.

[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]

### <a name="properties-and-conditions"></a>속성 및 조건

프로젝트 파일은 프로젝트를 성공적으로 빌드하고 배포 하기 위해 일반적으로 다양 한 정보를 제공 해야 합니다. 이러한 정보에는 서버 이름, 연결 문자열, 자격 증명, 빌드 구성, 원본 및 대상 파일 경로, 사용자 지정을 지원 하기 위해 포함 하려는 기타 정보가 포함 될 수 있습니다. 프로젝트 파일에서 속성은 [PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx) 요소 내에서 정의 되어야 합니다. MSBuild 속성은 키-값 쌍으로 구성 됩니다. **PropertyGroup** 요소 내에서 요소 이름은 속성 키를 정의 하 고 요소 내용은 속성 값을 정의 합니다. 예를 들어 **ServerName** 및 **ConnectionString** 이라는 속성을 정의 하 여 정적 서버 이름과 연결 문자열을 저장할 수 있습니다.

[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]

속성 값을 검색 하려면 *$ (PropertyName)* 형식을 사용 합니다. 예를 들어 **ServerName** 속성의 값을 검색 하려면 다음을 입력 합니다.

[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]

> [!NOTE]
> 이 항목의 뒷부분에서 속성 값을 사용 하는 방법 및 시기에 대 한 예제가 나와 있습니다.

프로젝트 파일에 정적 속성으로 정보를 포함 하는 것은 빌드 프로세스를 관리 하는 데 적합 한 방식이 아닐 수 있습니다. 많은 시나리오에서 다른 원본의 정보를 얻거나 사용자가 명령 프롬프트에서 정보를 제공할 수 있도록 하는 것이 좋습니다. MSBuild를 사용 하 여 모든 속성 값을 명령줄 매개 변수로 지정할 수 있습니다. 예를 들어 사용자는 명령줄에서 Msbuild.exe를 실행할 때 **ServerName** 에 대 한 값을 제공할 수 있습니다.

[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]

> [!NOTE]
> Msbuild.exe와 함께 사용할 수 있는 인수 및 스위치에 대 한 자세한 내용은 [Msbuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)를 참조 하세요.

동일한 속성 구문을 사용 하 여 환경 변수 및 기본 제공 프로젝트 속성의 값을 가져올 수 있습니다. 일반적으로 사용 되는 많은 속성이 사용자에 대해 정의 되며 관련 매개 변수 이름을 포함 하 여 프로젝트 파일에서 사용할 수 있습니다. 예를&#x2014;들어 현재 프로젝트 플랫폼 (예: **x86** 또는 **AnyCpu**&#x2014;)을 검색 하려면 프로젝트 파일에 **$ (platform)** 속성 참조를 포함 하면 됩니다. 자세한 내용은 [빌드 명령 및 속성에 대 한 매크로](https://msdn.microsoft.com/library/c02as0cs.aspx), [공용 MSBuild 프로젝트 속성](https://msdn.microsoft.com/library/bb629394.aspx)및 예약 된 [속성](https://msdn.microsoft.com/library/ms164309.aspx)을 참조 하세요.

속성은 *조건과*함께 사용 되는 경우가 많습니다. 대부분의 MSBuild 요소는 **Condition** 특성을 지원 합니다 .이 특성을 사용 하면 msbuild에서 요소를 평가 하는 기준이 될 조건을 지정할 수 있습니다. 예를 들어 다음 속성 정의를 살펴보세요.

[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]

MSBuild는이 속성 정의를 처리할 때 먼저 **$ (Outputroot)** 속성 값을 사용할 수 있는지 여부를 확인 합니다. 다른 단어에서 속성 값이&#x2014;비어 있는 경우 사용자가이 속성&#x2014;에 대 한 값을 제공 하지 않았습니다. 조건이 **true** 로 평가 되 고 속성 값이 **로 설정 됩니다. \** . 사용자가이 속성에 대 한 값을 제공한 경우 조건이 **false** 로 평가 되 고 정적 속성 값이 사용 되지 않습니다.

조건을 지정할 수 있는 다양 한 방법에 대 한 자세한 내용은 [MSBuild 조건](https://msdn.microsoft.com/library/7szfhaft.aspx)을 참조 하세요.

### <a name="items-and-item-groups"></a>항목 및 항목 그룹

프로젝트 파일의 중요 한 역할 중 하나는 빌드 프로세스에 대 한 입력을 정의 하는 것입니다. 일반적으로 이러한 입력은 빌드&#x2014;프로세스의 일부로 처리 하거나 복사 해야 하는 파일 코드 파일, 구성 파일, 명령 파일 및 기타 파일입니다. MSBuild 프로젝트 스키마에서 이러한 입력은 [항목](https://msdn.microsoft.com/library/ms164283.aspx) 요소로 표시 됩니다. 프로젝트 파일에서 [ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx) 요소 내에 항목을 정의 해야 합니다. **속성** 요소와 마찬가지로 **항목** 요소의 이름을 원하는 대로 지정할 수 있습니다. 그러나 **Include** 특성을 지정 하 여 항목이 나타내는 파일 또는 와일드 카드를 식별 해야 합니다.

[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]

동일한 이름을 가진 여러 **항목** 요소를 지정 하면 리소스의 명명 된 목록을 효과적으로 만들 수 있습니다. 이 작업을 수행 하는 좋은 방법은 Visual Studio에서 만드는 프로젝트 파일 중 하나를 살펴보는 것입니다. 예를 들어 샘플 솔루션의 *연락처 관리자. Mvc .csproj* 파일에는 여러 개의 동일한 이름의 **항목** 요소가 포함 된 많은 항목 그룹이 포함 되어 있습니다.

[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]

이러한 방식으로 프로젝트 파일은 **참조** 목록에 성공적인 빌드를 위해 준비 해야 하는 어셈블리를 포함 하는 것과&#x2014;같은 방식으로 처리 해야 하는 파일 목록을 생성 하도록 MSBuild에 지시 합니다. **컴파일** 목록에는 코드가 포함 되어 있습니다. 컴파일해야 할 파일 및 **콘텐츠** 목록에는 변경 되지 않은 상태로 복사 해야 하는 리소스가 포함 되어 있습니다. 이 항목의 뒷부분에 나오는 빌드 프로세스에서 이러한 항목을 참조 하 고 사용 하는 방법을 살펴보겠습니다.

항목 요소에는 [Itemmetadata](https://msdn.microsoft.com/library/ms164284.aspx) 자식 요소가 포함 될 수도 있습니다. 이러한 값은 사용자 정의 키-값 쌍 이며 기본적으로 해당 항목과 관련 된 속성을 나타냅니다. 예를 들어 프로젝트 파일의 많은 **컴파일** 항목 요소는 **DependentUpon** 자식 요소를 포함 합니다.

[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]

> [!NOTE]
> 사용자가 만든 항목 메타 데이터 외에도 모든 항목에는 만들 때 다양 한 공통 메타 데이터가 할당 됩니다. 자세한 내용은 [잘 알려진 항목 메타데이터](https://msdn.microsoft.com/library/ms164313.aspx)를 참조하세요.

루트 수준 **프로젝트** 요소 또는 특정 **대상** 요소 내에서 **ItemGroup** 요소를 만들 수 있습니다. **ItemGroup** 요소는 또한 프로젝트 구성 또는 플랫폼과 같은 조건에 따라 빌드 프로세스에 대 한 입력을 조정할 수 있는 **조건** 특성도 지원 합니다.

### <a name="targets-and-tasks"></a>대상 및 작업

MSBuild 스키마에서 [task](https://msdn.microsoft.com/library/77f2hx1s.aspx) 요소는 개별 빌드 명령 (또는 작업)을 나타냅니다. MSBuild에는 미리 정의 된 여러 작업이 포함 되어 있습니다. 예를 들면,

- **복사** 작업은 파일을 새 위치에 복사 합니다.
- **Csc** 작업은 Visual C# 컴파일러를 호출 합니다.
- **Vbc** 작업은 Visual Basic 컴파일러를 호출 합니다.
- **Exec** 태스크가 지정 된 프로그램을 실행 합니다.
- **메시지** 태스크는로 거에 메시지를 씁니다.

> [!NOTE]
> 즉시 사용할 수 있는 작업에 대 한 자세한 내용은 [MSBuild 작업 참조](https://msdn.microsoft.com/library/7z253716.aspx)를 참조 하세요. 사용자 지정 작업을 만드는 방법을 비롯 하 여 작업에 대 한 자세한 내용은 [MSBuild 작업](https://msdn.microsoft.com/library/ms171466.aspx)을 참조 하세요.

작업은 항상 [대상](https://msdn.microsoft.com/library/t50z2hka.aspx) 요소 내에 포함 되어야 합니다. **대상** 요소는 순차적으로 실행 되는 하나 이상의 작업 집합으로, 프로젝트 파일에는 여러 대상이 포함 될 수 있습니다. 작업 또는 작업 집합을 실행 하려는 경우 해당 작업을 포함 하는 대상을 호출 합니다. 예를 들어 메시지를 기록 하는 간단한 프로젝트 파일이 있다고 가정 합니다.

[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]

**/T** 스위치를 사용 하 여 대상을 지정 하 여 명령줄에서 대상을 호출할 수 있습니다.

[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]

또는 **프로젝트** 요소에 **defaulttargets** 특성을 추가 하 여 호출 하려는 대상을 지정할 수 있습니다.

[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]

이 경우 명령줄에서 대상을 지정할 필요가 없습니다. 프로젝트 파일을 간단히 지정할 수 있으며 MSBuild는 **Fullpublish** 대상을 대신 호출 합니다.

[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]

대상과 태스크 모두 **조건** 특성을 포함할 수 있습니다. 따라서 특정 조건이 충족 되는 경우 전체 대상 또는 개별 작업을 생략 하도록 선택할 수 있습니다.

일반적으로 유용한 작업 및 대상을 만들 때 프로젝트 파일의 다른 위치에 정의 된 속성 및 항목을 참조 해야 합니다.

- 속성 값을 사용 하려면 **$ (***propertyname***)** 을 입력 합니다. 여기서 *PropertyName* 은 **속성** 요소의 이름 또는 매개 변수 이름입니다.
- 항목을 사용 하려면 **@ (***itemname***)** 을 입력 합니다. 여기서 *ItemName* 은 **item** 요소의 이름입니다.

> [!NOTE]
> 동일한 이름으로 여러 항목을 만드는 경우 목록을 작성 합니다. 이와 대조적으로 동일한 이름을 사용 하 여 여러 속성을 만드는 경우 사용자가 제공 하는 마지막 속성 값은 동일한 이름의&#x2014;모든 이전 속성을 덮어씁니다. 속성에는 단일 값만 포함 될 수 있습니다.

예를 들어 샘플 솔루션의 *게시 proj* 파일에서 **buildprojects** 대상을 살펴보세요.

[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]

이 샘플에서는 다음과 같은 주요 사항을 관찰할 수 있습니다.

- **BuildingInTeamBuild** 매개 변수를 지정 하 고 값이 **true**이면이 대상 내의 모든 작업이 실행 되지 않습니다.
- 대상은 [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx) 태스크의 단일 인스턴스를 포함 합니다. 이 작업을 통해 다른 MSBuild 프로젝트를 빌드할 수 있습니다.
- **ProjectsToBuild** 항목이 작업에 전달 됩니다. 이 항목은 항목 그룹 내의 **ProjectsToBuild** item 요소에 의해 정의 되는 프로젝트 또는 솔루션 파일 목록을 나타낼 수 있습니다. 이 경우 **ProjectsToBuild** 항목은 단일 솔루션 파일을 참조 합니다.

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- **MSBuild** 작업에 전달 된 속성 값은 **Outputroot** 및 **Configuration**이라는 매개 변수를 포함 합니다. 이러한 값은 매개 변수 값이 제공 된 경우 매개 변수 값으로 설정 되 고, 그렇지 않은 경우에는 정적 속성 값으로 설정 됩니다.

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

**MSBuild** 작업에서 **Build**라는 대상을 호출 하는 것도 확인할 수 있습니다. Visual Studio 프로젝트 파일에서 널리 사용 되 고 있으며 **빌드**, **정리**, **다시 빌드**및 **게시**와 같은 사용자 지정 프로젝트 파일에서 사용할 수 있는 몇 가지 기본 제공 대상 중 하나입니다. 대상 및 작업을 사용 하 여 빌드 프로세스를 제어 하는 방법과 특히이 항목의 뒷부분에 있는 **MSBuild** 작업에 대해 알아봅니다.

> [!NOTE]
> 대상에 대 한 자세한 내용은 [MSBuild 대상](https://msdn.microsoft.com/library/ms171462.aspx)을 참조 하세요.

## <a name="splitting-project-files-to-support-multiple-environments"></a>여러 환경을 지원 하도록 프로젝트 파일 분할

테스트 서버, 스테이징 플랫폼 및 프로덕션 환경과 같은 여러 환경에 솔루션을 배포할 수 있다고 가정 합니다. 이러한 환경&#x2014;에서는 서버 이름, 연결 문자열 등을 사용 하는 것이 아니라 자격 증명, 보안 설정 및 기타 많은 요인에 따라 구성이 크게 달라질 수 있습니다. 정기적으로이 작업을 수행 해야 하는 경우 대상 환경을 전환할 때마다 프로젝트 파일에서 여러 속성을 편집 하는 것은 정말 편리 하지 않습니다. 또한 빌드 프로세스에 제공 되는 다양 한 속성 값 목록을 필요로 하는 이상적인 솔루션은 아닙니다.

다행히 대안이 있습니다. MSBuild를 사용 하면 여러 프로젝트 파일에 빌드 구성을 분할할 수 있습니다. 이 기능이 어떻게 작동 하는지 확인 하기 위해 샘플 솔루션에는 두 개의 사용자 지정 프로젝트 파일이 있습니다.

- 모든 환경에 공통적인 속성, 항목 및 대상이 포함 된 *proj를 게시 합니다*.
- *Env-Dev.* 개발자 환경에 특정 한 속성이 포함 되어 있습니다.

이제 *Publish. proj* 파일은 열기 **프로젝트** 태그 바로 아래에 [Import](https://msdn.microsoft.com/library/92x05xfs.aspx) 요소를 포함 합니다.

[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]

**Import** 요소는 다른 msbuild 프로젝트 파일의 내용을 현재 msbuild 프로젝트 파일에 가져오는 데 사용 됩니다. 이 경우 **TargetEnvPropsFile** 매개 변수는 가져올 프로젝트 파일의 파일 이름을 제공 합니다. MSBuild를 실행할 때이 매개 변수에 대 한 값을 제공할 수 있습니다.

[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]

이렇게 하면 두 파일의 내용이 단일 프로젝트 파일에 효과적으로 병합 됩니다. 이 방법을 사용 하 여 범용 빌드 구성과 환경 관련 속성을 포함 하는 여러 보조 프로젝트 파일을 포함 하는 하나의 프로젝트 파일을 만들 수 있습니다. 따라서 다른 매개 변수 값을 사용 하 여 명령을 실행 하기만 하면 솔루션을 다른 환경에 배포할 수 있습니다.

![](understanding-the-project-file/_static/image3.png)

이러한 방식으로 프로젝트 파일을 분할 하는 것이 좋은 방법입니다. 이를 통해 개발자는 단일 명령을 실행 하 여 여러 환경에 배포할 수 있으며, 여러 프로젝트 파일에서 범용 빌드 속성의 중복을 방지할 수 있습니다.

> [!NOTE]
> 사용자의 서버 환경에 맞는 환경 관련 프로젝트 파일을 사용자 지정 하는 방법에 대 한 지침은 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)을 참조 하세요.

## <a name="conclusion"></a>결론

이 항목에서는 MSBuild 프로젝트 파일에 대 한 일반적인 소개를 제공 하 고 빌드 프로세스를 제어 하는 사용자 지정 프로젝트 파일을 만드는 방법을 설명 했습니다. 또한 프로젝트 파일을 여러 대상으로 쉽게 빌드하고 배포할 수 있도록 프로젝트 파일을 유니버설 빌드 지침 및 환경 관련 빌드 속성으로 분할 하는 개념을 소개 했습니다.

다음 항목인 [빌드 프로세스](understanding-the-build-process.md)에 대 한 자세한 내용은 프로젝트 파일을 사용 하 여 빌드 및 배포를 제어 하는 방법에 대 한 자세한 정보를 제공 합니다.

## <a name="further-reading"></a>추가 정보

프로젝트 파일 및 WPP에 대 한 자세한 소개는 Microsoft Build Engine 내부: Sayed Ibrahim Hashimi에서 [MSBuild 및 Team Foundation Build 사용](http://amzn.com/0735645248) 및 WILLIAM, ISBN: 978-0-7356-4524-0을 참조 하세요.

> [!div class="step-by-step"]
> [이전](setting-up-the-contact-manager-solution.md)
> [다음](understanding-the-build-process.md)
