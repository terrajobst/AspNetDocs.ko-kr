---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: 수동으로 웹 패키지 설치 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 배포 패키지를 인터넷 정보 서비스 (IIS)로 수동으로 가져오는 방법에 대해 설명 합니다. 웹 항목을 빌드 및 패키징 하는 항목 ...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: f778549d3e26989a2e71ef21171adec521842729
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514889"
---
# <a name="manually-installing-web-packages"></a>수동으로 웹 패키지 설치

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 웹 배포 패키지를 인터넷 정보 서비스 (IIS)로 수동으로 가져오는 방법에 대해 설명 합니다.
> 
> [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md) 항목에서는 IIS 웹 배포 도구 (웹 배포)를 Microsoft Build Engine (MSBuild) 및 웹 게시 파이프라인 (WPP)과 함께 사용 하 여 웹 응용 프로그램 프로젝트를 단일 zip 파일로 패키지할 수 있는 방법에 대해 설명 했습니다. 일반적으로 웹 배포 패키지 (또는 배포 패키지) 라고 하는이 파일에는 웹 서버에서 웹 응용 프로그램을 다시 만들기 위해 IIS에 필요한 모든 콘텐츠 및 구성 정보가 포함 되어 있습니다.
> 
> 웹 배포 패키지를 만든 후에는 다양 한 방법으로 IIS 서버에 게시할 수 있습니다. 많은 시나리오에서 MSBuild, WPP 및 웹 배포 간의 통합 요소를 활용 하 여 자동화 된 단일 단계 빌드 및 배포 프로세스의 일부로 웹 패키지를 원격으로 만들고 설치할 수 있습니다. 이 프로세스는 [웹 패키지 배포](deploying-web-packages.md)에 설명 되어 있습니다. 그러나이는 항상 가능 하지는 않습니다. 인터넷 연결 프로덕션 환경에 웹 응용 프로그램을 배포 하려는 경우를 가정해 보겠습니다. 보안상의 이유로, 이러한 프로덕션 환경은 빌드 서버와 별도의 서브넷에 있는 방화벽을 기반으로 하는 경계 네트워크 (DMZ, 완충 지역 및 스크린 된 서브넷이 라고도 함)의 방화벽 뒤에 있을 가능성이 가장 적습니다. 대부분의 경우 프로덕션 환경은 별도의 도메인 이나 물리적으로 격리 된 네트워크에 있습니다.
> 
> 이러한 시나리오에서 유일한 옵션은 웹 패키지를 대상 서버로 이식 하 고 IIS로 수동으로 가져오는 것입니다. 이 방법으로는 자동화 된 배포가 불가능 하지만 웹 응용 프로그램&#x2014;을 게시 하는 매우 효율적인 기술은 웹 서버에 단일 zip 파일을 복사 하 고 마법사를 사용 하 여 가져오기 프로세스를 안내 하는 것입니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

## <a name="task-overview"></a>작업 개요

웹 배포 패키지를 IIS로 가져오려면 이러한 개략적인 작업을 완료 해야 합니다.

- MSBuild 명령줄, 팀 빌드 또는 Visual Studio 2010을 사용 하 여 웹 배포 패키지를 만듭니다.
- 웹 패키지를 대상 웹 서버에 복사 합니다.
- IIS 관리자의 응용 프로그램 패키지 가져오기 마법사를 사용 하 여 웹 패키지를 설치 하 고 연결 문자열 및 서비스 끝점과 같은 변수에 대 한 값을 제공할 수 있습니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 보여 줍니다. 이 항목의 작업 및 연습에서는 웹 패키지, 웹 배포 및 WPP의 개념에 대해 이미 잘 알고 있다고 가정 합니다. 자세한 내용은 [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)을 참조 하세요.

> [!NOTE]
> 이 항목은 필요한 구성 요소를 설치 하 고 패키지를 가져오기 위해 IIS 웹 사이트를 준비 하는 방법을 설명 하는 [웹 배포 게시용 웹 서버 구성 (오프 라인 배포)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)과 함께 사용 하는 것이 가장 좋습니다.

## <a name="create-a-web-deployment-package"></a>웹 배포 패키지 만들기

첫 번째 작업은 배포할 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지를 만드는 것입니다. 다양 한 방법으로 웹 패키지를 만들 수 있습니다.

**방법 1: Visual Studio를 사용 하 여 빌드 프로세스의 일부로 패키지 만들기**

프로젝트 속성 페이지의 **웹 패키지 및 게시** 탭을 통해 모든 빌드 후 웹 배포 패키지를 만들도록 웹 응용 프로그램 프로젝트를 구성할 수 있습니다. 이 프로세스는 [웹 응용 프로그램 프로젝트 빌드 및 패키징](building-and-packaging-web-application-projects.md)에 설명 되어 있습니다.

**방법 2: MSBuild를 사용 하 여 빌드 프로세스의 일부로 패키지 만들기**

사용자 지정 MSBuild 프로젝트 파일이 나 명령줄에서 MSBuild를 직접 사용 하 여 웹 응용 프로그램 프로젝트를 빌드하는 경우 명령에 **Deployonbuild = true** 및 **Deploytarget = package** 속성을 포함 하 여 빌드 프로세스의 일부로 웹 배포 패키지를 만들 수 있습니다. 이 프로세스는 [빌드 프로세스 이해](understanding-the-build-process.md)에 설명 되어 있습니다.

**방법 3: Visual Studio에서 주문형 패키지 만들기**

언제 든 지 Visual Studio 2010에서 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지를 만들 수 있습니다. 이렇게 하려면 **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **배포 패키지 빌드**를 클릭 합니다.

![](manually-installing-web-packages/_static/image1.png)

**방법 4: 명령줄에서 주문형 패키지 만들기**

MSBuild를 사용 하 여 웹 응용 프로그램 프로젝트에서 **패키지** 대상을 호출 하 여 명령줄에서 웹 배포 패키지를 만들 수 있습니다. 명령은 다음과 유사 합니다.

[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]

어떤 방법을 사용 하 든 최종 결과는 동일 합니다. WPP는 웹 응용 프로그램 프로젝트의 출력 폴더에 다양 한 지원 리소스와 함께 zip 파일로 웹 배포 패키지를 만듭니다.

![](manually-installing-web-packages/_static/image2.png)

웹 패키지를 수동으로 가져올 계획인 경우 zip 파일만 필요 합니다. 이 파일을 대상 웹 서버에 복사 하 고 가져오기 프로세스를 시작할 수 있습니다.

## <a name="import-a-web-package-into-iis"></a>웹 패키지를 IIS로 가져오기

다음 절차를 사용 하 여 로컬 파일 시스템에서 IIS 웹 사이트로 웹 배포 패키지를 가져올 수 있습니다. 이 절차를 수행 하기 전에 다음이 있는지 확인 합니다.

- 웹 배포 패키지를 웹 서버에 복사 했습니다.
- 응용 프로그램을 호스팅하도록 IIS 웹 서버를 구성 했습니다.

웹 배포 패키지를 지원 하도록 IIS 웹 서버를 구성 하는 방법에 대 한 자세한 내용은 [웹 배포 게시용 웹 서버 구성 (오프 라인 배포)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)을 참조 하세요.

**IIS 관리자를 사용 하 여 웹 배포 패키지를 가져오려면**

1. IIS 관리자의 **연결** 창에서 iis 웹 사이트를 마우스 오른쪽 단추로 클릭 하 고 **배포**를 가리킨 다음 **응용 프로그램 가져오기**를 클릭 합니다.

    ![](manually-installing-web-packages/_static/image3.png)
2. 응용 프로그램 패키지 가져오기 마법사의 **패키지 선택** 페이지에서 웹 배포 패키지의 위치로 이동한 후 **다음**을 클릭 합니다.
3. **패키지 콘텐츠 선택** 페이지에서 필요 하지 않은 콘텐츠를 모두 선택 취소 하 고 **다음**을 클릭 합니다.

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > 많은 경우에 웹 배포 패키지와 함께 제공 되는 모든 항목을 가져오지 않으려고 할 수 있습니다. 예를 들어 웹 배포 연결 된 데이터베이스를 대체할 수 있도록 허용 하지 않을 수 있습니다.  
    > **권한 부여** 항목은 응용 프로그램 풀 id가 웹 사이트 콘텐츠를 저장 하는 물리적 폴더에 액세스할 수 있도록 대상 파일 시스템에 대 한 권한을 설정 합니다. 또한 익명 인증 사용자에 게는 응용 프로그램에서 MIME (다목적 Internet Mail Extensions) 형식 파일을 제공할 수 있도록 폴더에 대 한 읽기 권한이 부여 됩니다. 원하는 경우 이러한 항목을 제거 하 고 수동으로 사용 권한을 구성할 수 있습니다.
4. **응용 프로그램 패키지 정보 입력** 페이지에서 요청 된 정보를 제공 합니다.

    ![](manually-installing-web-packages/_static/image5.png)
5. 웹 패키지를 만들 때 WPP는 응용 프로그램에 대 한 구성 파일을 분석 하 고 연결 문자열 및 서비스 끝점과 같은 모든 변수를 검색 합니다. 이 경우 다음과 같습니다.

    1. **응용 프로그램 경로** 는 응용 프로그램을 설치 하려는 IIS 경로입니다. 이 설정은 WPP에서 만드는 모든 배포 패키지에 공통적입니다.
    2. **연락처 서비스 끝점 주소** 는 응용 프로그램이 배포 된 WCF 서비스와 통신 하는 데 사용 해야 하는 주소입니다. 이 설정은 web.config 파일의 항목에 해당 *합니다.*
    3. 첫 번째 **연결 문자열** 설정은 응용 프로그램과 연결 된 데이터베이스 (이 경우 ASP.NET membership database)를 배포 하는 데 사용 해야 하 웹 배포는 연결 문자열입니다. 이 설정은 Visual Studio의 **SQL 패키지 및 게시** 탭에 있는 설정에 해당 합니다.
    4. 두 번째 **연결 문자열** 설정은 응용 프로그램이 실행 될 때 데이터베이스와 통신 하는 데 실제로 사용 하는 연결 문자열입니다. 이 *는 web.config 파일의* 연결 문자열 항목에 해당 합니다.

        > [!NOTE]
        > 이러한 매개 변수를 제공 하는 위치에 대 한 자세한 내용은 [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)을 참조 하세요.
6. **다음**을 클릭합니다.
7. 이 웹 사이트에 응용 프로그램을 처음 배포 하는 경우를 설치 하기 전에 기존 콘텐츠를 모두 삭제할지 여부를 지정 하 라는 메시지가 표시 됩니다. 요구 사항에 적합 한 옵션을 선택 하 고 **다음**을 클릭 합니다.

    ![](manually-installing-web-packages/_static/image6.png)
8. IIS에서 패키지 설치를 완료 한 후 **마침**을 클릭 합니다.

    ![](manually-installing-web-packages/_static/image7.png)

이 시점에서 IIS에 웹 응용 프로그램을 게시 했습니다.

## <a name="conclusion"></a>결론

이 항목에서는 IIS 관리자를 사용 하 여 웹 배포 패키지를 IIS 웹 사이트로 가져오는 방법에 대해 설명 했습니다. 이 웹 응용 프로그램 게시 방식은 보안 또는 인프라 제약 조건으로 인해 원격 배포가 불가능 하거나 바람직하지 않은 경우에 적합 합니다.

## <a name="further-reading"></a>추가 참고 자료

웹 패키지를 수동으로 가져오는 기능을 지원 하도록 IIS 웹 서버를 구성 하는 방법에 대 한 지침은 [웹 배포 게시용 웹 서버 구성 (오프 라인 배포)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)을 참조 하세요. 웹 패키지를 배포 하는 방법에 대 한 일반적인 지침은 [연습: 웹 배포 패키지를 사용 하 여 웹 응용 프로그램 프로젝트 배포 (1/4 부)](https://msdn.microsoft.com/library/dd483479.aspx)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](creating-and-running-a-deployment-command-file.md)
