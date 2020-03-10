---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
title: 웹 응용 프로그램 프로젝트 빌드 및 패키징 | Microsoft Docs
author: jrjlee
description: 원격 서버 환경에 웹 응용 프로그램 프로젝트를 배포 하려는 경우 첫 번째 작업은 프로젝트를 빌드하고 웹 배포를 생성 하는 것입니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 94e92f80-a7e3-4d18-9375-ff8be5d666ac
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
msc.type: authoredcontent
ms.openlocfilehash: 1d0ee0264ce6461d7b0159f1a44de4de31e2d079
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463229"
---
# <a name="building-and-packaging-web-application-projects"></a>웹 애플리케이션 프로젝트 빌드 및 패키징

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 원격 서버 환경에 웹 응용 프로그램 프로젝트를 배포 하려는 경우 첫 번째 작업은 프로젝트를 빌드하고 웹 배포 패키지를 생성 하는 것입니다. 이 항목에서는 웹 응용 프로그램 프로젝트에 대 한 빌드 프로세스의 작동 방식에 대해 설명 합니다. 특히 다음을 설명 합니다.
> 
> - 웹 게시 파이프라인 (WPP)이 배포 기능을 포함 하도록 빌드 프로세스를 확장 하는 방법입니다.
> - 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)가 웹 응용 프로그램을 배포 패키지로 전환 하는 방법입니다.
> - 빌드 및 패키징 프로세스의 작동 방식 및 생성 되는 파일입니다.

Visual Studio 2010에서 웹 응용 프로그램 프로젝트에 대 한 빌드 및 배포 프로세스는 WPP에서 지원 됩니다. WPP는 MSBuild의 기능을 확장 하 고 웹 배포와 통합할 수 있도록 하는 MSBuild (Microsoft Build Engine) 대상 집합을 제공 합니다. Visual Studio 내에서 웹 응용 프로그램 프로젝트에 대 한 속성 페이지에서이 확장 된 기능을 확인할 수 있습니다. **패키지/게시 웹** 페이지에서 **SQL 패키지 및 게시** 페이지와 함께 빌드 프로세스가 완료 될 때 배포를 위해 웹 응용 프로그램 프로젝트를 패키징하는 방법을 구성할 수 있습니다.

![](building-and-packaging-web-application-projects/_static/image1.png)

## <a name="how-does-the-wpp-work"></a>WPP는 어떻게 작동 하나요?

기반 웹 응용 프로그램 프로젝트에 대 한 C#프로젝트 파일을 살펴보면 두 개의 .targets 파일을 가져오는 것을 볼 수 있습니다.

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample1.xml)]

첫 번째 **Import** 문은 모든 시각적 C# 프로젝트에 공통적입니다. 이 파일에는 Visual C#에 관련 된 대상과 작업이 포함 되어 있습니다. 예를 들어 C# 컴파일러 (**Csc**) 태스크가 여기에서 호출 됩니다. 그러면 *Microsoft CSharp* 파일은 *microsoft 공용 .targets* 파일을 가져옵니다. 이는 **빌드**, **다시**빌드, **실행**, **컴파일**및 **정리**와 같은 모든 프로젝트에 공통적인 대상을 정의 합니다. 두 번째 **Import** 문은 웹 응용 프로그램 프로젝트에만 적용 됩니다. 그러면 *Microsoft WebApplication* . .targets 파일은 *microsoft web.config* 파일을 가져옵니다. *Microsoft 웹 게시 .targets* 파일 *은 기본적으로 WPP입니다.* 웹 배포를 호출 하 여 다양 한 배포 작업을 완료 하는 **패키지** 및 **MSDeployPublish**와 같은 대상을 정의 합니다.

이러한 추가 대상을 사용 하는 방법을 이해 하려면 Contact Manager 샘플 솔루션에서 *게시 proj* 파일을 열고 **buildprojects** 대상을 확인 합니다.

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample2.xml)]

이 대상은 **MSBuild** 작업을 사용 하 여 다양 한 프로젝트를 빌드합니다. **Deployonbuild** 및 **deploytarget** 속성을 확인 합니다.

- **Deployonbuild = true** 속성은 기본적으로 "빌드가 성공적으로 완료 될 때 추가 대상을 실행 하려고 합니다."를 의미 합니다.
- **Deploytarget** 속성은 **deployonbuild** 속성이 **true**일 때 실행 하려는 대상의 이름을 식별 합니다. 이 경우 프로젝트를 빌드한 후 MSBuild에서 **패키지** 대상을 실행 하도록 지정 합니다.

**패키지** 대상은 *Microsoft .targets. .targets* 파일에 정의 되어 있습니다. 기본적으로이 대상은 웹 응용 프로그램 프로젝트의 빌드 출력을 사용 하 여 IIS 웹 서버에 게시할 수 있는 웹 배포 패키지로 바꿉니다.

> [!NOTE]
> Visual Studio 2010에서 프로젝트 파일 (예: 프로젝트 파일 <em>(예: 프로젝트 파일)을</em>보려면 먼저 솔루션에서 프로젝트를 언로드합니다. <strong>솔루션 탐색기</strong> 창에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭 한 다음 <strong>프로젝트 언로드</strong>를 클릭 합니다. 프로젝트 노드를 다시 마우스 오른쪽 단추로 클릭 하 고<em>[프로젝트 파일]</em> <strong>편집</strong>을 클릭 합니다. 프로젝트 파일이 원시 XML 형식으로 열립니다. 완료 되 면 프로젝트를 다시 로드 해야 합니다.  
> MSBuild 대상, 작업 및 <strong>가져오기</strong> 문에 대 한 자세한 내용은 [프로젝트 파일 이해](understanding-the-project-file.md)를 참조 하세요. 프로젝트 파일 및 WPP에 대 한 자세한 소개는 Microsoft Build Engine 내부: Sayed Ibrahim Hashimi에서 [MSBuild 및 Team Foundation Build 사용](http://amzn.com/0735645248) 및 WILLIAM, ISBN: 978-0-7356-4524-0을 참조 하세요.

## <a name="what-is-a-web-deployment-package"></a>웹 배포 패키지 란?

Visual Studio 2010을 사용 하거나 MSBuild를 직접 사용 하 여 웹 응용 프로그램 프로젝트를 빌드하고 배포 하는 경우 최종 결과는 일반적으로 *웹 배포 패키지*입니다. 웹 배포 패키지는 .zip 파일입니다. 여기에는 다음을 포함 하 여 웹 응용 프로그램을 다시 만들기 위해 IIS와 웹 배포 필요한 모든 항목이 포함 됩니다.

- 콘텐츠, 리소스 파일, 구성 파일, JavaScript 및 CSS 스타일 시트 (CSS) 리소스 등을 비롯 한 웹 응용 프로그램의 컴파일된 출력입니다.
- 웹 응용 프로그램 프로젝트 및 솔루션 내에서 참조 되는 모든 프로젝트에 대 한 어셈블리입니다.
- SQL 스크립트를 사용 하 여 웹 응용 프로그램과 함께 배포 하는 모든 데이터베이스를 생성 합니다.

웹 배포 패키지를 생성 한 후에는 다양 한 방법으로 IIS 웹 서버에 게시할 수 있습니다. 예를 들어 대상 웹 서버에서 웹 배포 원격 에이전트 서비스 또는 웹 배포 처리기를 대상으로 지정 하 여 원격으로 배포 하거나, IIS 관리자를 사용 하 여 대상 웹 서버에서 패키지를 수동으로 가져올 수 있습니다. 이러한 배포 방법에 대 한 자세한 내용은 [웹 배포에 대 한 올바른 방법 선택](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)을 참조 하세요.

## <a name="how-does-the-build-process-work"></a>빌드 프로세스는 어떻게 작동 하나요?

이는 웹 응용 프로그램 프로젝트를 빌드하고 패키지할 때 발생 하는 상황을 보여 줍니다.

![](building-and-packaging-web-application-projects/_static/image2.png)

웹 응용 프로그램 프로젝트를 빌드하면 빌드 프로세스에서 *[project name] 이라는 파일을 생성 합니다. SourceManifest*. 프로젝트 파일 및 빌드 출력과 함께이를 사용 *합니다. SourceManifest* 파일은 웹 배포 패키지에 포함 해야 하는 항목 웹 배포를 알려 줍니다. 이러한 입력을 사용 하 웹 배포는 *[project name] .zip*이라는 웹 배포 패키지를 생성 합니다.

웹 배포 패키지와 함께 빌드 프로세스는 패키지를 사용 하는 데 도움이 되는 두 개의 파일을 생성 합니다.

- *.Deploy. .cmd* 파일에는 원격 IIS 웹 서버에 웹 배포 패키지를 게시 하는 매개 변수가 있는 웹 배포 (msdeploy.exe) 명령이 포함 되어 있습니다. 적절 한 매개 변수를 사용 하 여 *.deploy. .cmd* 파일을 실행 하면 일반적으로 msdeploy.exe 명령을 직접 생성 하는 것 보다 더 빠르고 쉬운 대안을 제공 합니다.
- *Setparameters .xml* 파일은 msdeploy.exe 명령에 매개 변수 값 집합을 제공 합니다. 이러한 값에는 패키지를 배포 하려는 IIS 웹 응용 프로그램의 이름, *web.config 파일에 정의 된 서비스* 끝점 및 연결 문자열의 값, 프로젝트 속성 페이지에 정의 된 배포 속성 값 등의 속성이 포함 됩니다.

*Setparameters .xml* 파일은 배포 프로세스를 관리 하는 데 중요 합니다. 이 파일은 웹 응용 프로그램 프로젝트의 내용에 따라 동적으로 생성 됩니다. 예를 들어 *web.config 파일에* 연결 문자열을 추가 하는 경우 빌드 프로세스에서 자동으로 연결 문자열을 검색 하 고, 적절 하 게 배포를 매개 변수화 하 고, *setparameters .xml* 파일에 항목을 만들어 배포 프로세스의 일부로 연결 문자열을 수정할 수 있도록 합니다. 다음 항목인 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)에서는이 파일의 역할에 대해 자세히 설명 하 고 빌드 및 배포 중에 수정할 수 있는 다양 한 방법을 설명 합니다.

> [!NOTE]
> Visual Studio 2010에서 웹 응용 프로그램을 패키징 하기 전에 웹 응용 프로그램에서 페이지를 미리 컴파일하는 것은 지원 되지 않습니다. 다음 버전의 Visual Studio 및 WPP에는 웹 응용 프로그램을 패키징 옵션으로 미리 컴파일하는 기능이 포함 됩니다.

## <a name="conclusion"></a>결론

이 항목에서는 Visual Studio 2010의 웹 응용 프로그램 프로젝트에 대 한 빌드 및 패키징 프로세스의 개요를 제공 했습니다. 여기서는 WPP를 사용 하 여 MSBuild에서 웹 배포 명령을 호출 하는 방법에 대해 설명 했으며 빌드 및 패키징 프로세스의 작동 방식에 대해 설명 했습니다.

웹 배포 패키지를 만들었으면 다음 단계는 배포 하는 것입니다. 이에 대 한 자세한 내용은 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md) 및 [웹 패키지 배포](deploying-web-packages.md)를 참조 하세요.

## <a name="further-reading"></a>추가 참고 자료

이 자습서의 다음 항목인 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md) 및 [웹 패키지 배포](deploying-web-packages.md)에서는 사용자가 만든 웹 패키지를 사용 하는 방법에 대 한 지침을 제공 합니다. 이 시리즈 [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)의 최종 자습서에서는 패키징 프로세스를 사용자 지정 하 고 문제를 해결 하는 방법에 대 한 지침을 제공 합니다.

프로젝트 파일 및 WPP에 대 한 자세한 소개는 Microsoft Build Engine 내부: Sayed Ibrahim Hashimi에서 [MSBuild 및 Team Foundation Build 사용](http://amzn.com/0735645248) 및 WILLIAM, ISBN: 978-0-7356-4524-0을 참조 하세요.

> [!div class="step-by-step"]
> [이전](understanding-the-build-process.md)
> [다음](configuring-parameters-for-web-package-deployment.md)
