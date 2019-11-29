---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 폴더 권한 설정-6/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: cd03a188-e947-4f55-9bda-b8bce201d8c6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
msc.type: authoredcontent
ms.openlocfilehash: 85a77a196cf3458bbb2e6308838a846936cd070b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633571"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-setting-folder-permissions---6-of-12"></a>Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 폴더 권한 설정-6/12

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다. 시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.

## <a name="overview"></a>개요

이 자습서에서는 응용 프로그램이 해당 폴더에 로그 파일을 만들 수 있도록 배포 된 웹 사이트의 *Elmah* 폴더에 대 한 폴더 권한을 설정 합니다.

Visual Studio 개발 서버 (Cassini)를 사용 하 여 Visual Studio에서 웹 응용 프로그램을 테스트 하면 응용 프로그램이 사용자의 id로 실행 됩니다. 사용자는 개발 컴퓨터의 관리자 이며 모든 폴더의 모든 파일에 대해 모든 작업을 수행할 수 있는 권한이 있어야 합니다. 그러나 응용 프로그램이 IIS에서 실행 되는 경우 사이트에 할당 된 응용 프로그램 풀에 대해 정의 된 id로 실행 됩니다. 이는 일반적으로 권한이 제한 된 시스템 정의 계정입니다. 기본적으로 웹 응용 프로그램의 파일 및 폴더에 대 한 읽기 및 실행 권한이 있지만 쓰기 권한이 없습니다.

응용 프로그램에서 파일을 만들거나 업데이트 하는 경우이 문제가 발생 합니다 .이는 웹 응용 프로그램에서 일반적으로 필요 합니다. Contoso 대학 응용 프로그램에서 Elmah는 오류에 대 한 세부 정보를 저장 하기 위해 *elmah* 폴더에 XML 파일을 만듭니다. Elmah와 같은 항목을 사용 하지 않더라도 사이트에서 사용자가 파일을 업로드 하거나 사이트의 폴더에 데이터를 기록 하는 기타 작업을 수행할 수 있습니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.

## <a name="testing-error-logging-and-reporting"></a>오류 로깅 및 보고 테스트

응용 프로그램이 IIS에서 제대로 작동 하지 않는 방법을 확인 하려면 (Visual Studio에서 테스트 했을 경우에도) 일반적으로 Elmah에서 기록 되는 오류를 발생 시킨 다음 Elmah 오류 로그를 열어 세부 정보를 확인 합니다. Elmah가 XML 파일을 만들고 오류 정보를 저장할 수 없는 경우 빈 오류 보고서가 표시 됩니다.

브라우저를 열고 `http://localhost/ContosoUniversity`로 이동한 다음 *Studentsxxx*와 같은 잘못 된 URL을 요청 합니다. Web.config 파일의 `customErrors` 설정이 "RemoteOnly"이 고 IIS를 로컬로 실행 하므로 *Genericerrorpage .aspx* 페이지 대신 시스템 생성 오류 페이지가 표시 됩니다.

[![Error_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image2.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image1.png)

이제 *Elmah* 를 실행 하 여 오류 보고서를 확인 합니다. *Elmah 폴더에* XML 파일을 만들 수 없기 때문에 빈 오류 로그 페이지가 표시 됩니다.

[![Error_log_page_empty](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image4.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image3.png)

## <a name="setting-write-permission-on-the-elmah-folder"></a>Elmah 폴더에 대 한 쓰기 권한 설정

폴더 권한은 수동으로 설정 하거나 배포 프로세스의 자동으로 만들 수 있습니다. 이를 자동으로 수행 하려면 복잡 한 MSBuild 코드가 필요 하며, 처음 배포할 때만이 작업을 수행 하면 됩니다 .이 자습서에서는이 작업을 수동으로 수행 하는 방법을 보여 줍니다. 배포 프로세스의이 부분을 만드는 방법에 대 한 자세한 내용은 Sayed Hashimi의 웹 게시에 대 한 [폴더 권한 설정](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) 블로그를 참조 하세요.

**Windows 탐색기**에서 *C:\inetpub\wwwroot\ContosoUniversity*로 이동 합니다. *Elmah* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 **보안** 탭을 선택 합니다.

[![Elmah_folder_Properties_Security_tab](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image6.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image5.png)

**그룹 또는 사용자 이름** 목록에 **DefaultAppPool** 가 표시 되지 않으면이 자습서에 지정 된 것과 다른 방법을 사용 하 여 컴퓨터에서 IIS 및 ASP.NET 4를 설정 하는 것입니다. 이 경우 Contoso 대학 응용 프로그램에 할당 된 응용 프로그램 풀에서 사용 되는 id를 확인 하 고 해당 id에 대 한 쓰기 권한을 부여 합니다. 이 자습서의 끝부분에 있는 응용 프로그램 풀 id에 대 한 링크를 참조 하세요.)

**편집**을 클릭합니다. **Elmah에 대 한 사용 권한** 대화 상자에서 **DefaultAppPool**을 선택 하 고 **허용** 열에서 **쓰기** 확인란을 선택 합니다.

[![Permissions_for_Elmah_dialog_box](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image8.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image7.png)

두 대화 상자에서 **확인을** 클릭 합니다.

## <a name="retesting-error-logging-and-reporting"></a>다시 테스트 오류 로깅 및 보고

동일한 방식으로 오류를 다시 발생 시켜 테스트 합니다 (잘못 된 URL 요청) 하 고 **오류 로그** 페이지를 실행 합니다. 이번에는 페이지에 오류가 표시 됩니다.

[![Elmah_Error_Log_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image10.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image9.png)

또한 해당 폴더에 SQL Server Compact 데이터베이스 파일이 있고 해당 데이터베이스의 데이터를 업데이트할 수 있도록 하기 때문에 *앱\_데이터* 폴더에 대 한 쓰기 권한이 있어야 합니다. 그러나이 경우에는 배포 프로세스에서 *앱\_데이터* 폴더에 대 한 쓰기 권한을 자동으로 설정 하므로 추가 작업을 수행할 필요가 없습니다.

이제 Contoso 대학이 로컬 컴퓨터의 IIS에서 올바르게 작동 하는 데 필요한 모든 작업을 완료 했습니다. 다음 자습서에서는 호스팅 공급자에 게 배포 하 여 사이트를 공개적으로 사용할 수 있도록 설정 합니다.

## <a name="more-information"></a>자세한 내용

이 예제에서 Elmah가 로그 파일을 저장할 수 없는 이유는 매우 명확 합니다. 문제의 원인이 명확 하지 않은 경우에 IIS 추적을 사용할 수 있습니다. IIS.net 사이트에서 [IIS 7에서 추적을 사용 하 여 실패 한 요청 문제 해결](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) 을 참조 하세요.

응용 프로그램 풀 id에 대 한 사용 권한을 부여 하는 방법에 대 한 자세한 내용은 IIS.net 사이트의 [파일 시스템 acl을 통해 IIS의](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) [응용 프로그램 풀 Id](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) 및 보안 콘텐츠를 참조 하세요.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
