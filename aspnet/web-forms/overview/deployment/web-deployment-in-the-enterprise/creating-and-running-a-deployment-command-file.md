---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 배포 명령 파일 만들기 및 실행 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 배포를 단일 단계로 실행 하는 데 사용할 수 있는 명령 파일을 빌드하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514979"
---
# <a name="creating-and-running-a-deployment-command-file"></a>배포 명령 파일 만들기 및 실행

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 반복 가능한 단일 프로세스로 배포를 실행할 수 있는 명령 파일을 빌드하는 방법에 대해 설명 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 [시리즈에서는 샘플](the-contact-manager-solution.md) 솔루션&#x2014;&#x2014;을 사용 하 여 ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 빌드&#x2014; [프로세스 이해](understanding-the-build-process.md)에서 설명 하는 빌드 프로세스 이해에 설명 된 분할 프로젝트 파일 방식을 기반으로 합니다. 빌드 프로세스는 모든 대상 환경에 적용 되는 빌드 명령을 포함 하 고 다른 하나는 환경 특정 빌드 및 배포 설정을 포함 합니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="process-overview"></a>프로세스 개요

이 항목에서는 이러한 프로젝트 파일을 사용 하 여 대상 환경에 반복 가능한 배포를 수행 하는 명령 파일을 만들고 실행 하는 방법을 알아봅니다. 기본적으로 명령 파일에는 다음을 수행 하는 MSBuild 명령만 포함 해야 합니다.

- MSBuild에 환경 독립적 *게시 proj* 파일을 실행 하도록 지시 합니다.
- 환경 관련 프로젝트 설정 및 찾을 위치를 포함 하는 파일을 *Publish. proj* 파일에 알립니다.

## <a name="create-an-msbuild-command"></a>MSBuild 명령 만들기

[빌드 프로세스 이해](understanding-the-build-process.md)에 설명 된&#x2014;대로 환경 관련 프로젝트 파일 (예: *Env)* &#x2014;은 빌드 시 환경 독립적인 *Publish proj* 파일로 가져오도록 설계 되었습니다. 이러한 두 파일은 모두 MSBuild에서 솔루션을 빌드하고 배포 하는 방법을 알려 주는 전체 명령 집합을 제공 합니다.

*Publish. proj* 파일은 **import** 요소를 사용 하 여 환경 관련 프로젝트 파일을 가져옵니다.

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

따라서 Msbuild.exe를 사용 하 여 Contact Manager 솔루션을 빌드 및 배포 하는 경우 다음을 수행 해야 합니다.

- *Publish. proj* 파일에서 msbuild.exe를 실행 합니다.
- **TargetEnvPropsFile**라는 명령줄 매개 변수를 제공 하 여 환경 관련 프로젝트 파일의 위치를 지정 합니다.

이렇게 하려면 MSBuild 명령이 다음과 유사 해야 합니다.

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

여기에서 반복 가능한 단일 단계 배포로 이동 하는 간단한 단계입니다. MSBuild 명령을 .cmd 파일에 추가 하기만 하면 됩니다. Contact Manager 솔루션에서 Publish 폴더에는이를 수행 하는 *Publish-Dev* 라는 파일이 포함 되어 있습니다.

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> **/Sfl** 스위치는 msbuild.exe가 호출 된 작업 디렉터리에 *msbuild.exe* 라는 로그 파일을 만들도록 msbuild에 지시 합니다.

Contact Manager 솔루션을 배포 하거나 다시 배포 하려면 *Publish-Dev* 파일을 실행 하기만 하면 됩니다. 이 파일을 실행 하면 MSBuild에서 다음을 수행 합니다.

- 솔루션의 모든 프로젝트를 빌드합니다.
- 웹 응용 프로그램 프로젝트용 배포 가능한 웹 패키지를 생성 합니다.
- 데이터베이스 프로젝트용 .dbschema 및 deploymanifest 파일을 생성 합니다.
- 웹 서버에 웹 패키지를 배포 합니다.
- 데이터베이스 서버에 데이터베이스를 배포 합니다.

## <a name="run-the-deployment"></a>배포 실행

대상 환경에 대 한 명령 파일을 만든 경우 파일을 실행 하 여 전체 배포를 완료할 수 있어야 합니다.

**테스트 환경에 연락처 관리자 솔루션을 배포 하려면**

1. 개발자 워크스테이션에서 Windows 탐색기를 연 다음 *Publish-Dev* 파일의 위치로 이동 합니다.
2. 파일을 두 번 클릭 하 여 실행 합니다.
3. **파일 열기 – 보안 경고** 대화 상자가 나타나면 **실행**을 클릭 합니다.
4. 구성 설정 및 테스트 서버가 올바르게 설정 된 경우 MSBuild가 프로젝트 파일 처리를 완료 하면 명령 프롬프트 창에 **빌드 성공** 메시지가 표시 됩니다.

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. 이 환경에 솔루션을 처음 배포 하는 경우에는 테스트 웹 서버 컴퓨터 **\_계정을 datawriter 여부** 및 **db\_** **데이터베이스에 추가 해야 합니다** . 이 절차는 [웹 배포 게시용 데이터베이스 서버 구성](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)에 설명 되어 있습니다.

    > [!NOTE]
    > 데이터베이스를 만들 때에만 이러한 권한을 할당 해야 합니다. 기본적으로 빌드 프로세스는 모든 배포&#x2014;에서 데이터베이스를 다시 만들지 않고 기존 데이터베이스와 최신 스키마를 비교 하 고 필요한 변경만 수행 합니다. 따라서 솔루션을 처음 배포할 때에만 이러한 데이터베이스 역할을 매핑해야 합니다.
6. Internet Explorer를 열고 연락처 관리자 응용 프로그램의 URL로 이동 합니다 (예: `http://testweb1:85/ContactManager/`).
7. 응용 프로그램이 예상 대로 작동 하 고 연락처를 추가할 수 있는지 확인 합니다.

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a>결론

MSBuild 지침을 포함 하는 명령 파일을 만들면 특정 대상 환경에 다중 프로젝트 솔루션을 빌드하고 배포 하는 빠르고 쉬운 방법을 제공 합니다. 여러 대상 환경에 솔루션을 반복적으로 배포 해야 하는 경우 여러 명령 파일을 만들 수 있습니다. 각 명령 파일에서 MSBuild 명령은 동일한 유니버설 프로젝트 파일을 만들지만 다른 환경 특정 프로젝트 파일을 지정 합니다. 예를 들어 개발자 또는 테스트 환경에 게시 하는 명령 파일에는 다음 MSBuild 명령이 포함 될 수 있습니다.

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

스테이징 환경에 게시할 명령 파일에는 다음 MSBuild 명령이 포함 될 수 있습니다.

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> 사용자의 서버 환경에 맞는 환경 관련 프로젝트 파일을 사용자 지정 하는 방법에 대 한 지침은 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)을 참조 하세요.

MSBuild 명령의 속성을 재정의 하거나 다양 한 다른 스위치를 설정 하 여 각 환경에 대 한 빌드 프로세스를 사용자 지정할 수도 있습니다. 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](deploying-database-projects.md)
> [다음](manually-installing-web-packages.md)
