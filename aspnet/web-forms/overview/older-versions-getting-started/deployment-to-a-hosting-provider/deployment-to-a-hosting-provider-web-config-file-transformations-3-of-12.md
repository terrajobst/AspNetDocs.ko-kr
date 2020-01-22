---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: Web.config 파일 변환-3/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 2b0df3d9-450b-4ea6-b315-4c9650722cad
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
msc.type: authoredcontent
ms.openlocfilehash: 9e7902bcf8a16c154aee1a982824bfaedeea7d9d
ms.sourcegitcommit: 7b1e1784213dd4c301635f9e181764f3e2f94162
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76309238"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-webconfig-file-transformations---3-of-12"></a>Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: Web.config 파일 변환-3/12

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다. 시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.

## <a name="overview"></a>개요

이 자습서에서는 web.config 파일을 다른 대상 환경에 배포할 때이 *파일을 변경* 하는 프로세스를 자동화 하는 방법을 보여 줍니다. 대부분의 응용 프로그램에는 응용 프로그램이 배포 될 때 달라 야 하는 설정이 *web.config* 파일에 있습니다. 이러한 변경을 수행 하는 프로세스를 자동화 하면 배포할 때마다 수동으로 작업을 수행할 필요가 없으며,이는 지루한 오류가 발생 하기 쉽습니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 변환과 웹 배포 매개 변수 비교

*Web.config 파일 설정을* 변경 하는 프로세스를 자동화 하는 두 가지 방법이 있습니다. web.config [변환과](https://msdn.microsoft.com/library/dd465326.aspx) [웹 배포 매개 변수](https://msdn.microsoft.com/library/ff398068.aspx)입니다. Web.config *변환 파일* *에는 배포할 때 web.config 파일을* 변경 하는 방법을 지정 하는 XML 태그가 포함 되어 있습니다. 특정 빌드 구성과 특정 게시 프로필에 대해 서로 다른 변경 내용을 지정할 수 있습니다. 기본 빌드 구성은 디버그 및 릴리스 이며 사용자 지정 빌드 구성을 만들 수 있습니다. 게시 프로필은 일반적으로 대상 환경에 해당 합니다. ( [테스트 환경으로 IIS에 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서에서 게시 프로필에 대해 자세히 알아봅니다.)

웹 배포 매개 변수는 web.config 파일에 있는 설정을 포함 하 여 배포 *중에 구성* 해야 하는 다양 한 종류의 설정을 지정 하는 데 사용할 수 있습니다. *Web.config 파일 변경* 내용을 지정 하는 데 사용할 경우 웹 배포 매개 변수를 설정 하는 것이 더 복잡 하지만를 배포할 때까지 설정할 값을 모르는 경우에 유용 합니다. 예를 들어 엔터프라이즈 환경에서 *배포 패키지* 를 만들어 it 부서의 사용자에 게 제공 하 여 프로덕션 환경에 설치할 수 있으며, 사용자가 알지 못하는 연결 문자열이 나 암호를 입력할 수 있어야 합니다.

이 자습서에서 다루는 시나리오의 경우 *web.config* 파일에 대해 수행 해야 하는 모든 작업을 알고 있으므로 웹 배포 매개 변수를 사용할 필요가 없습니다. 사용 되는 빌드 구성에 따라 다르고 사용 되는 게시 프로필에 따라 달라 지는 일부 변환을 구성 합니다.

## <a name="creating-transformation-files-for-publish-profiles"></a>게시 프로필에 대 한 변환 파일 만들기

**솔루션 탐색기**에서 *web.config* 를 확장 하 여 두 기본 빌드 구성에 대해 기본적으로 생성 되는 *web.config 및 web.config 변환 파일을 표시* 합니다.

![Web.config_transform_files](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image1.png)

Web.config 파일을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 **구성 변환 추가** 를 선택 하 여 사용자 지정 빌드 구성에 대 한 변환 파일을 만들 수 있지만이 자습서에서는이 작업을 수행할 필요가 없습니다.

빌드 구성이 아니라 배포 대상과 관련 된 변경 내용을 구성 하기 위해 두 개의 변환 파일이 추가로 필요 합니다. 이러한 종류의 설정에 대 한 일반적인 예는 테스트 및 프로덕션에 대해 다른 WCF 끝점입니다. 이후 자습서에서는 Test 및 Production 이라는 게시 프로필을 만듭니다. 따라서 *web.config 파일 및* *web.config* 파일이 필요 합니다.

게시 프로필에 연결 된 변환 파일을 수동으로 만들어야 합니다. **솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Windows 탐색기에서 폴더 열기**를 선택 합니다.

![Open_folder_in_Windows_Explorer](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image2.png)

**Windows 탐색기**에서 *web.config 파일을 선택 하 고 파일* 을 복사한 다음 두 복사본을 붙여넣습니다. 이러한 복사본의 이름을 *web.config* 및 *Web.config*로 바꾸고 **Windows 탐색기**를 닫습니다.

**솔루션 탐색기**에서 **새로 고침** 을 클릭 하 여 새 파일을 확인 합니다.

새 파일을 선택 하 고 마우스 오른쪽 단추를 클릭 한 다음 상황에 맞는 메뉴에서 **프로젝트에 포함** 을 클릭 합니다.

![프로젝트에 테스트 및 프로덕션 구성 파일 포함](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image3.png)

이러한 파일이 배포 되지 않도록 하려면 **솔루션 탐색기**에서 선택한 다음 **속성** 창에서 **빌드 작업** 속성을 **콘텐츠에서** **없음**으로 변경 합니다. 빌드 구성을 기반으로 하는 변환 파일은 자동으로 배포 되지 않습니다.

이제 *web.config 변환 파일* *에 web.config 변환을 입력할 준비가* 되었습니다.

## <a name="limiting-error-log-access-to-administrators"></a>관리자에 대 한 오류 로그 액세스 제한

응용 프로그램을 실행 하는 동안 오류가 발생 하는 경우 응용 프로그램은 시스템 생성 오류 페이지 대신 일반 오류 페이지를 표시 하 고 오류 로깅 및 보고를 위해 [Elmah NuGet 패키지](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 를 사용 합니다. *Web.config 파일의* `customErrors` 요소는 오류 페이지를 지정 합니다.

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample1.xml)]

오류 페이지를 보려면 `customErrors` 요소의 `mode` 특성을 "RemoteOnly"에서 "On"으로 일시적으로 변경 하 고 Visual Studio에서 응용 프로그램을 실행 합니다. *Studentsxxx*와 같은 잘못 된 URL을 요청 하 여 오류를 발생 시킵니다. IIS에서 생성 된 "페이지를 찾을 수 없습니다" 오류 페이지 대신 *Genericerrorpage .aspx* 페이지가 표시 됩니다.

[![Error_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image5.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image4.png)

오류 로그를 보려면 URL에서 포트 번호 뒤에 있는 모든 항목을 *elmah* 로 바꾸고 (스크린샷 예는 `http://localhost:51130/elmah.axd`) enter 키를 누릅니다.

[![Elmah_log_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image7.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image6.png)

완료 되 면 `customErrors` 요소를 "RemoteOnly" 모드로 다시 설정 해야 합니다.

개발 컴퓨터에서는 오류 로그 페이지에 대 한 무료 액세스를 허용 하는 것이 편리 하지만 프로덕션 환경에서는 보안상 위험할 수 있습니다. 프로덕션 사이트의 경우 *web.config* 파일에서 변환을 구성 하 여 관리자에 게 오류 로그 액세스를 제한 하는 권한 부여 규칙을 추가할 수 있습니다.

여기에 표시 된 것 *처럼 web.config를 열고 여* 는 `configuration` 태그 바로 뒤에 새 `location` 요소를 추가 합니다. `location` 요소만 추가 하 고 여기에 표시 된 주변 태그는 추가 하지 않아야 합니다. 일부 컨텍스트를 제공 하기 위한 것입니다.

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample2.xml?highlight=2-9)]

"Insert"의 `Transform` 특성 값을 설정 하면이 `location` 요소가 *web.config* 파일의 기존 `location` 요소에 형제로 추가 됩니다. ( **크레딧 업데이트** 페이지에 대 한 권한 부여 규칙을 지정 하는 `location` 요소가 이미 하나 있습니다.) 배포 후 프로덕션 사이트를 테스트 하는 경우이 권한 부여 규칙이 적용 되는지 테스트 합니다.

테스트 환경에서 오류 로그 액세스를 제한 하지 않아도 되므로이 코드를 *web.config* 파일에 추가할 필요가 없습니다.

> [!NOTE] 
> 
> **보안 정보** 프로덕션 응용 프로그램에서 오류 정보를 공용에 표시 하지 않거나 해당 정보를 공용 위치에 저장 합니다. 공격자는 오류 정보를 사용 하 여 사이트의 취약성을 검색할 수 있습니다. 사용자 고유의 응용 프로그램에서 ELMAH를 사용 하는 경우 보안 위험을 최소화 하기 위해 ELMAH를 구성할 수 있는 방법을 조사 해야 합니다. 이 자습서의 ELMAH 예제는 권장 구성으로 간주 되지 않아야 합니다. 응용 프로그램에서 파일을 만들 수 있어야 하는 폴더를 처리 하는 방법을 설명 하기 위해 선택한 예제입니다.

## <a name="setting-an-environment-indicator"></a>환경 표시기 설정

일반적으로 배포 하는 각 환경에서 web.config 파일 설정이 달라 야 하 *는 경우가 있습니다* . 예를 들어 WCF 서비스를 호출 하는 응용 프로그램은 테스트 및 프로덕션 환경에서 다른 끝점을 필요로 할 수 있습니다. Contoso 대학 응용 프로그램에는 이러한 종류의 설정도 포함 되어 있습니다. 이 설정은 현재 개발, 테스트 또는 프로덕션 환경과 같은 환경을 알려 주는 사이트 페이지에서 표시 되는 표시기를 제어 합니다. 설정 값은 응용 프로그램이 사이트의 주 제목에 "(Dev)" 또는 "(Test)"를 추가할지 여부를 결정 합니다 *. 마스터* 마스터 페이지:

[![Environment_indicator](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image9.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image8.png)

환경 표시기는 응용 프로그램이 프로덕션 환경에서 실행 되는 경우 생략 됩니다.

Contoso 대학 웹 페이지는 응용 프로그램이 실행 되는 환경을 확인 하기 위해 web.config *파일의* `appSettings`에 설정 된 값을 읽습니다.

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample3.xml)]

값은 테스트 환경에서 "Test"로, 프로덕션 환경에서는 "Prod" 여야 합니다.

*Web.config* 를 열고 앞에서 추가한 `location` 요소의 여는 태그 바로 앞에 `appSettings` 요소를 추가 합니다.

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample4.xml)]

`xdt:Transform` 특성 값 "SetAttributes"는이 변환의 목적이 *web.config* 파일의 기존 요소에 대 한 특성 값을 변경 하는 것을 나타냅니다. `xdt:Locator` 특성 값 "Match (key)"는 수정할 요소가 `key` 특성이 여기에 지정 된 `key` 특성과 일치 함을 나타냅니다. `add` 요소의 다른 특성은 `value`뿐 이며 배포 된 *web.config* 파일에서 변경 됩니다. 이 코드를 통해 `Environment` `appSettings` 요소의 `value` 특성이 프로덕션에 배포 된 *web.config 파일에서* "Prod"로 설정 됩니다.

그런 다음, `value`을 "Prod" 대신 "Test"로 설정 하는 것을 제외 하 고 *web.config* 파일에 동일한 변경 내용을 적용 합니다. 완료 되 면 *web.config* 의 `appSettings` 섹션은 다음 예제와 같이 표시 됩니다.

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample5.xml)]

## <a name="disabling-debug-mode"></a>디버그 모드 해제

릴리스 빌드의 경우 배포 하는 환경에 관계 없이 디버깅을 사용 하지 않도록 설정 하는 것이 좋습니다. 기본적으로 *web.config* 변환 파일은 `compilation` 요소에서 `debug` 특성을 제거 하는 코드를 사용 하 여 자동으로 생성 됩니다.

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample6.xml)]

`Transform` 특성은 릴리스 빌드를 배포할 때마다 배포 된 *web.config 파일에서* `debug` 특성을 생략 합니다.

이 변환은 릴리스 변환 파일을 복사 하 여 만들었기 때문에 테스트 및 프로덕션 변환 파일에 있습니다. 이러한 파일은 중복 되지 않으므로 각 파일을 열고 **컴파일** 요소를 제거 하 고 각 파일을 저장 한 후 닫습니다.

## <a name="setting-connection-strings"></a>연결 문자열 설정

대부분의 경우에는 게시 프로필에서 연결 문자열을 지정할 수 있으므로 연결 문자열 변환을 설정할 필요가 없습니다. 그러나 SQL Server Compact 데이터베이스를 배포 하 고 Entity Framework Code First 마이그레이션를 사용 하 여 대상 서버에서 데이터베이스를 업데이트 하는 경우 예외가 발생 합니다. 이 시나리오에서는 데이터베이스 스키마를 업데이트 하기 위해 서버에서 사용 되는 추가 연결 문자열을 지정 해야 합니다. 이 변환을 설정 하려면 web.config 및 *web.config* 변환 파일에서 열기 **&lt;구성&gt;** 태그 바로 뒤에 **&lt;connectionStrings&gt;** 요소를 *추가 합니다.*

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample7.xml)]

`Transform` 특성은이 연결 문자열이 배포 된 *web.config* 파일의 *connectionStrings* 요소에 추가 되도록 지정 합니다. (존재 하지 않는 경우 게시 프로세스에서 자동으로이 추가 연결 문자열을 만듭니다. 하지만 기본적으로 **providerName** 특성은 SQL Server Compact에 대해 작동 하지 않는 `System.Data.SqlClient`로 설정 됩니다. 연결 문자열을 수동으로 추가 하 여 배포 프로세스에서 잘못 된 공급자 이름으로 연결 문자열 요소를 만들지 않도록 합니다.

이제 테스트 및 프로덕션에 Contoso 대학 응용 프로그램을 배포 하는 데 필요한 모든 *web.config* 변환을 지정 했습니다. 다음 자습서에서는 프로젝트 속성을 설정 해야 하는 배포 설정 작업을 처리 합니다.

## <a name="more-information"></a>자세한 내용

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 [ASP.NET 배포 콘텐츠 맵의](https://msdn.microsoft.com/library/bb386521.aspx)web.config 변환 시나리오를 참조 하세요.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
> [다음](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
