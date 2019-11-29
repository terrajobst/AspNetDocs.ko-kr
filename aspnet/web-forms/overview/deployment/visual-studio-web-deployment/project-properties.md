---
uid: web-forms/overview/deployment/visual-studio-web-deployment/project-properties
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 프로젝트 속성 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ec1cec4c-a75f-47af-a2ba-b1e2f971d24b
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/project-properties
msc.type: authoredcontent
ms.openlocfilehash: b2811791a897c9166f6222c23dddc6921e5267ab
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614950"
---
# <a name="aspnet-web-deployment-using-visual-studio-project-properties"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 프로젝트 속성

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다. 계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.

## <a name="overview"></a>개요

일부 배포 옵션은 프로젝트 파일 ( *.csproj* 또는 *.vbproj* 파일)에 저장 된 프로젝트 속성에서 구성 됩니다. 대부분의 경우 이러한 설정의 기본값은 원하는 것 이지만 Visual Studio에 기본 제공 되는 **프로젝트 속성** UI를 사용 하 여 변경 해야 하는 경우 이러한 설정으로 작업할 수 있습니다. 이 자습서에서는 **프로젝트 속성**에서 배포 설정을 검토 합니다. 또한 빈 폴더를 배포 하는 자리 표시자 파일도 만듭니다.

## <a name="configure-deployment-settings-in-the-project-properties-window"></a>프로젝트 속성 창에서 배포 설정 구성

배포 하는 동안 발생 하는 작업에 영향을 주는 대부분의 설정은 다음 자습서에서 볼 수 있듯이 게시 프로필에 포함 됩니다. 알고 있어야 하는 몇 가지 설정은 **프로젝트 속성** 창의 **패키지/게시** 탭에 있습니다. 이러한 설정은 각 빌드 구성에 대해 지정 됩니다. 즉, 릴리스 빌드에 대해 디버그 빌드에 대 한 설정과 다른 설정을 사용할 수 있습니다.

**솔루션 탐색기**에서 **ContosoUniversity** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 패키지 및 **웹 게시** 탭을 선택 합니다.

![웹 패키지 및 게시 탭](project-properties/_static/image1.png)

창이 표시 되 면 기본적으로 솔루션에 대해 현재 활성 상태인 빌드 구성에 대 한 설정이 표시 됩니다. **구성** 상자에 **활성 (릴리스)** 이 표시 되어 있지 않으면 릴리스 빌드 구성에 대 한 설정을 표시 하기 위해 **릴리스** 를 선택 합니다. 릴리스 빌드를 테스트 환경과 프로덕션 환경에 모두 배포 합니다.

![릴리스 빌드 구성 선택](project-properties/_static/image2.png)

**활성 (릴리스)** 또는 **릴리스가** 선택 된 상태에서 릴리스 빌드 구성을 사용 하 여 배포할 때 적용 되는 값을 확인할 수 있습니다.

- **배포할 항목** 상자에 **응용 프로그램을 실행 하는 데 필요한 파일만** 선택 됩니다. 다른 옵션은 **이 프로젝트의 모든 파일** 또는 **이 프로젝트 폴더의 모든 파일**입니다. 기본 선택을 변경 하지 않고 소스 코드 파일을 배포 하지 않도록 합니다 (예:). 이 설정은 SQL Server Compact 이진 파일이 포함 된 폴더를 프로젝트에 포함 해야 하는 이유입니다. 이 설정에 대 한 자세한 내용은 [ASP.NET 웹 응용 프로그램 프로젝트 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx)에서 **내 프로젝트 폴더의 모든 파일이 배포 되지 않는 이유** 를 참조 하세요.
- **생성 된 디버그 기호 제외** 를 선택 합니다. 이 빌드 구성을 사용 하는 경우 디버깅 되지 않습니다.
- **SQL 패키지 및 게시 탭에 구성 된 모든 데이터베이스 포함** 이 선택 되어 있습니다. Visual Studio에서 파일 뿐만 아니라 데이터베이스를 배포할지 여부를 지정 합니다. 확인란 레이블은 **SQL 패키지 및 게시** 탭만 언급 하지만이 확인란의 선택을 취소 하면 게시 프로필에 구성 된 데이터베이스 배포도 사용 하지 않도록 설정 됩니다. 나중에이 작업을 수행 하 게 되므로 확인란을 선택 된 상태로 유지 해야 합니다. **SQL 패키지 및 게시** 탭은 이러한 자습서에서 사용 하지 않는 레거시 데이터베이스 게시 방법에 사용 됩니다.
- **웹 배포 패키지 설정** 섹션은이 자습서에서 한 번 클릭으로 게시를 사용 하 고 있으므로 적용 되지 않습니다.

**구성** 드롭다운 상자를 디버그로 변경 하 여 디버그 빌드에 대 한 기본 설정을 확인 합니다. 디버그 빌드를 배포할 때 디버그할 수 있도록 **생성 된 디버그 기호 제외** 를 제외 하 고 값은 동일 합니다.

## <a name="make-sure-that-the-elmah-folder-gets-deployed"></a>Elmah 폴더가 배포 되었는지 확인 합니다.

이전 자습서에서 살펴본 것 처럼 [Elmah NuGet 패키지](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 는 오류 로깅 및 보고를 위한 기능을 제공 합니다. Contoso 대학 응용 프로그램에서 Elmah는 *elmah*라는 폴더에 오류 정보를 저장 하도록 구성 되었습니다.

![Elmah 폴더](project-properties/_static/image3.png)

특정 파일 또는 폴더를 배포에서 제외 하는 것이 일반적인 요구 사항입니다. 또 다른 예는 사용자가 파일을 업로드할 수 있는 폴더입니다. 개발 환경에서 생성 된 로그 파일 또는 업로드 된 파일을 프로덕션 환경에 배포 하지 않으려는 경우 프로덕션에 업데이트를 배포 하는 경우 프로덕션에 존재 하는 파일을 삭제 하지 않도록 배포 프로세스를 원하지 않습니다. 배포 옵션을 설정 하는 방법에 따라 파일이 대상 사이트에 있지만 배포 시 원본 사이트가 아닌 경우 대상 사이트에서 해당 파일을 삭제 웹 배포.

이 자습서의 앞부분에서 살펴본 것 처럼 **웹 패키지 및 게시** 탭에서 **배포할 항목** 옵션은 **이 응용 프로그램을 실행 하는 데 필요한 파일로만**설정 됩니다. 결과적으로, 개발 중인 Elmah에서 만든 로그 파일은 배포 되지 않습니다. 이러한 로그 파일은 수행 하려는 작업입니다. (배포 하기 위해 프로젝트에 포함 되어야 하 고 해당 **빌드 작업** 속성을 **내용**으로 설정 해야 합니다. 자세한 내용은 [ASP.NET 웹 응용 프로그램 프로젝트 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx)에서 **내 프로젝트 폴더의 모든 파일이 배포 되지 않는 이유** 를 참조 하세요. 그러나 복사할 파일이 하나 이상 없는 경우를 제외 하 고 웹 배포는 대상 사이트에 폴더를 만들지 않습니다. 따라서 폴더가 복사 될 수 있도록 자리 표시자 역할을 하는 *.txt* 파일을 폴더에 추가 합니다.

**솔루션 탐색기**에서 *Elmah* 폴더를 마우스 오른쪽 단추로 클릭 하 고, **새 항목 추가**를 선택 하 고, *자리 표시자 .txt*라는 텍스트 파일을 만듭니다. 여기에 다음 텍스트를 입력 합니다. "폴더를 배포 하기 위한 자리 표시자 파일입니다." 파일을 저장 합니다. .Txt 파일의 **빌드 작업** 속성은 기본적으로 **콘텐츠로** 설정 되므로 Visual Studio에서이 파일 및 폴더를 배포 하도록 하기 위해이 작업을 수행 해야 *합니다.*

## <a name="summary"></a>요약

이제 모든 배포 설정 작업을 완료 했습니다. 다음 자습서에서는 Contoso 대학 사이트를 테스트 환경에 배포 하 고 테스트 합니다.

> [!div class="step-by-step"]
> [이전](web-config-transformations.md)
> [다음](deploying-to-iis.md)
