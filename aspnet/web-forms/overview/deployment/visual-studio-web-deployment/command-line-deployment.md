---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 명령줄 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512075"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 명령줄 배포

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다. 계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.

## <a name="overview"></a>개요

이 자습서에서는 명령줄에서 Visual Studio 웹 게시 파이프라인을 호출 하는 방법을 보여 줍니다. 이는 일반적으로 [소스 코드 버전 제어 시스템](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)을 사용 하 여 Visual Studio에서 수동으로 수행 하는 대신 [배포 프로세스를 자동화](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 하려는 시나리오에 유용 합니다.

## <a name="make-a-change-to-deploy"></a>배포를 변경 합니다.

현재 정보 페이지에 템플릿 코드가 표시 됩니다.

![템플릿 코드가 포함 된 정보 페이지](command-line-deployment/_static/image1.png)

학생 등록의 요약을 표시 하는 코드로 대체 합니다.

*About .aspx* 페이지를 열고 `MainContent` `Content` 요소 내의 모든 태그를 삭제 한 후 다음 태그를 해당 위치에 삽입 합니다.

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

프로젝트를 실행 하 고 **정보** 페이지를 선택 합니다.

![[정보] 페이지](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a>명령줄을 사용 하 여 테스트에 배포

다른 데이터베이스 변경 내용을 배포 하지 않으므로 aspnet-ContosoUniversity 데이터베이스에 대해 dbDacFx 데이터베이스 배포를 사용 하지 않도록 설정 합니다. **웹 게시** 마법사를 열고 세 개의 게시 프로필 각각의 **설정** 탭에서 **데이터베이스 업데이트** 확인란의 선택을 취소 합니다.

Windows 8 시작 페이지에서 **v s 2012에 대 한 개발자 명령 프롬프트**를 검색 합니다.

**V s 2012에** 대 한 개발자 명령 프롬프트 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 클릭 합니다.

명령 프롬프트에서 다음 명령을 입력 하 여 솔루션 파일의 경로를 솔루션 파일의 경로로 바꿉니다.

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

MSBuild는 솔루션을 빌드하고 테스트 환경에 배포 합니다.

![명령줄 출력](command-line-deployment/_static/image3.png)

브라우저를 열고 `http://localhost/ContosoUniversity`로 이동한 다음 **정보** 페이지를 클릭 하 여 배포가 성공 했는지 확인 합니다.

테스트에서 학생을 만들지 않은 경우 **학생 본문 통계** 제목 아래에 빈 페이지가 표시 됩니다. **학생 페이지로 이동** 하 여 **학생 추가**를 클릭 하 고, 일부 학생을 추가한 후 **정보** 페이지로 돌아와서 학생 통계를 확인 합니다.

![테스트 환경의 정보 페이지](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a>키 명령줄 옵션

입력 한 명령이 솔루션 파일 경로 및 두 개의 속성을 MSBuild에 전달 했습니다.

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a>솔루션 배포 및 개별 프로젝트 배포

솔루션 파일을 지정 하면 솔루션의 모든 프로젝트가 빌드됩니다. 솔루션에 여러 웹 프로젝트가 있는 경우 다음 MSBuild 동작이 적용 됩니다.

- 명령줄에서 지정 하는 속성은 모든 프로젝트에 전달 됩니다. 따라서 각 웹 프로젝트에는 사용자가 지정한 이름의 게시 프로필이 있어야 합니다. `/p:PublishProfile=Test`지정 하는 경우 각 웹 프로젝트에 *Test*라는 게시 프로필이 있어야 합니다.
- 다른 프로젝트를 빌드할 수 없는 경우 한 프로젝트를 성공적으로 게시할 수 있습니다. 자세한 내용은 stackoverflow 스레드 [MSBuild가 두 개의 패키지와 함께 실패](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)하는 경우를 참조 하세요.

솔루션 대신 개별 프로젝트를 지정 하는 경우 Visual Studio 버전을 지정 하는 매개 변수를 추가 해야 합니다. Visual Studio 2012을 사용 하는 경우 명령줄은 다음 예제와 유사 합니다.

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

Visual Studio 2010의 버전 번호는 10.0입니다. 자세한 내용은 [Visual Studio project compatibility And VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) On Sayed Hashimi 블로그 (영문)를 참조 하세요.

### <a name="specifying-the-publish-profile"></a>게시 프로필 지정

다음 예제와 같이 이름이 나 *pubxml* 파일의 전체 경로로 게시 프로필을 지정할 수 있습니다.

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a>명령줄 게시에 대해 지원 되는 웹 게시 방법

명령줄 게시에는 세 가지 게시 방법이 지원 됩니다.

- `MSDeploy`-웹 배포를 사용 하 여 게시 합니다.
- `Package`-웹 배포 패키지를 만들어 게시 합니다. 패키지를 만드는 MSBuild 명령과 별도로 패키지를 설치 해야 합니다.
- `FileSystem`-지정 된 폴더에 파일을 복사 하 여 게시 합니다.

### <a name="specifying-the-build-configuration-and-platform"></a>빌드 구성 및 플랫폼 지정

Visual Studio 또는 명령줄에서 빌드 구성 및 플랫폼을 설정 해야 합니다. 게시 프로필에는 `LastUsedBuildConfiguration` 및 `LastUsedPlatform`라는 속성이 포함 되지만, 프로젝트가 빌드되는 방식을 결정 하기 위해 이러한 속성을 설정할 수는 없습니다. 자세한 내용은 MSBuild: Sayed Hashimi의 블로그에서 [구성 속성을 설정 하는 방법](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) 을 참조 하세요.

## <a name="deploy-to-staging"></a>스테이징에 배포

Azure에 배포 하려면 명령줄에 암호를 추가 해야 합니다. Visual Studio의 게시 프로필에 암호를 저장 한 경우 해당 암호는 *pubxml 사용자* 파일에 암호화 된 형식으로 저장 됩니다. 명령줄 배포를 수행할 때 MSBuild에서 해당 파일에 액세스할 수 없으므로 명령줄 매개 변수에서 암호를 전달 해야 합니다.

1. 준비 웹 사이트에 대해 이전에 다운로드 한 *publishsettings* 파일에서 필요한 암호를 복사 합니다. 암호는 웹 배포 `publishProfile` 요소에 대 한 `userPWD` 특성의 값입니다.

    ![웹 배포 암호](command-line-deployment/_static/image5.png)
2. Windows 8 시작 페이지에서 **v s 2012에 대 한 개발자 명령 프롬프트**를 검색 하 고 아이콘을 클릭 하 여 명령 프롬프트를 엽니다. (로컬 컴퓨터에서 IIS에 배포 하지 않으므로 이번에는 관리자 권한으로 열 필요가 없습니다.)
3. 명령 프롬프트에서 다음 명령을 입력 하 여 솔루션 파일의 경로를 솔루션 파일의 경로로 바꾸고 암호를 사용 하 여 암호를 바꿉니다.

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    이 명령줄에는 `/p:AllowUntrustedCertificate=true`추가 매개 변수가 포함 되어 있습니다. 이 자습서를 작성 하는 동안 명령줄에서 Azure에 게시할 때 `AllowUntrustedCertificate` 속성을 설정 해야 합니다. 이 버그에 대 한 수정이 해제 되 면 해당 매개 변수는 필요 하지 않습니다.
4. 브라우저를 열고 준비 사이트의 URL로 이동한 다음 **정보** 페이지를 클릭 하 여 배포에 성공 했는지 확인 합니다.

    앞에서 설명한 것 처럼 테스트 환경에 대 한 몇 가지 학생을 만들어 **정보** 페이지에 대 한 통계를 볼 수 있습니다.

## <a name="deploy-to-production"></a>프로덕션에 배포

프로덕션에 배포 하는 프로세스는 스테이징 프로세스와 유사 합니다.

1. 프로덕션 웹 사이트에 대해 이전에 다운로드 한 *publishsettings* 파일에서 필요한 암호를 복사 합니다.
2. **V s 2012에 대 한 개발자 명령 프롬프트를**엽니다.
3. 명령 프롬프트에서 다음 명령을 입력 하 여 솔루션 파일의 경로를 솔루션 파일의 경로로 바꾸고 암호를 사용 하 여 암호를 바꿉니다.

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    실제 프로덕션 사이트의 경우 데이터베이스가 변경 된 경우 일반적으로 응용 프로그램을 배포 하기 전에 *오프 라인 .htm 파일\_* 사이트에 복사 하 고 성공적인 배포 후에 삭제 합니다.
4. 브라우저를 열고 준비 사이트의 URL로 이동한 다음 **정보** 페이지를 클릭 하 여 배포에 성공 했는지 확인 합니다.

## <a name="summary"></a>요약

이제 명령줄을 사용 하 여 응용 프로그램 업데이트를 배포 했습니다.

![테스트 환경의 정보 페이지](command-line-deployment/_static/image6.png)

다음 자습서에는 웹 게시 파이프라인을 확장 하는 방법의 예제가 표시 됩니다. 이 예제에서는 프로젝트에 포함 되지 않은 파일을 배포 하는 방법을 보여 줍니다.

> [!div class="step-by-step"]
> [이전](deploying-a-database-update.md)
> [다음](deploying-extra-files.md)
