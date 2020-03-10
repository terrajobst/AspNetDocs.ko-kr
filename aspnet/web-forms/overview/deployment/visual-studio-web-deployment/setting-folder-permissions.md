---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 폴더 권한 설정 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: 410525bb2e3f6e5a0be6d7d6b33fb3a40509041a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465065"
---
# <a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 폴더 사용 권한 설정

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다. 계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.

## <a name="overview"></a>개요

이 자습서에서는 응용 프로그램이 해당 폴더에 로그 파일을 만들 수 있도록 배포 된 웹 사이트의 *Elmah* 폴더에 대 한 폴더 권한을 설정 합니다.

Visual Studio 개발 서버 (Cassini) 또는 IIS Express를 사용 하 여 Visual Studio에서 웹 응용 프로그램을 테스트 하는 경우 응용 프로그램은 사용자의 id로 실행 됩니다. 사용자는 개발 컴퓨터의 관리자 이며 모든 폴더의 모든 파일에 대해 모든 작업을 수행할 수 있는 권한이 있어야 합니다. 그러나 응용 프로그램이 IIS에서 실행 되는 경우 사이트에 할당 된 응용 프로그램 풀에 대해 정의 된 id로 실행 됩니다. 이는 일반적으로 권한이 제한 된 시스템 정의 계정입니다. 기본적으로 웹 응용 프로그램의 파일 및 폴더에 대 한 읽기 및 실행 권한이 있지만 쓰기 권한이 없습니다.

응용 프로그램에서 파일을 만들거나 업데이트 하는 경우이 문제가 발생 합니다 .이는 웹 응용 프로그램에서 일반적으로 필요 합니다. Contoso 대학 응용 프로그램에서 Elmah는 오류에 대 한 세부 정보를 저장 하기 위해 *elmah* 폴더에 XML 파일을 만듭니다. Elmah와 같은 항목을 사용 하지 않더라도 사이트에서 사용자가 파일을 업로드 하거나 사이트의 폴더에 데이터를 기록 하는 기타 작업을 수행할 수 있습니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](troubleshooting.md)를 확인 해야 합니다.

## <a name="test-error-logging-and-reporting"></a>오류 로깅 및 보고 테스트

응용 프로그램이 IIS에서 제대로 작동 하지 않는 방법을 확인 하려면 (Visual Studio에서 테스트 했을 경우에도) 일반적으로 Elmah에서 기록 되는 오류를 발생 시킨 다음 Elmah 오류 로그를 열어 세부 정보를 확인 합니다. Elmah가 XML 파일을 만들고 오류 정보를 저장할 수 없는 경우 빈 오류 보고서가 표시 됩니다.

브라우저를 열고 `http://localhost/ContosoUniversity`로 이동한 다음 *Studentsxxx*와 같은 잘못 된 URL을 요청 합니다. Web.config 파일의 `customErrors` 설정이 "RemoteOnly"이 고 IIS를 로컬로 실행 하므로 *Genericerrorpage .aspx* 페이지 대신 시스템 생성 오류 페이지가 표시 됩니다.

![HTTP 404 오류 페이지](setting-folder-permissions/_static/image1.png)

이제 *Elmah* 를 실행 하 여 오류 보고서를 확인 합니다. 관리자 계정 자격 증명 (&quot;admin&quot; 및 &quot;devpwd&quot;)을 사용 하 여 로그인 한 후에는 Elmah가 *elmah* 폴더에 XML 파일을 만들 수 없기 때문에 빈 오류 로그 페이지가 표시 됩니다.

![오류 로그가 비어 있습니다.](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a>Elmah 폴더에 대 한 쓰기 권한 설정

폴더 권한은 수동으로 설정 하거나 배포 프로세스의 자동으로 만들 수 있습니다. 이러한 작업을 자동으로 수행 하려면 복잡 한 MSBuild 코드가 필요 합니다 .이 작업은 처음 배포할 때만 수행 하면 됩니다. 다음 단계에서는 수동으로 작업을 수행 하는 방법을 설명 합니다. 배포 프로세스의이 부분을 만드는 방법에 대 한 자세한 내용은 Sayed Hashimi의 웹 게시에 대 한 [폴더 권한 설정](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) 블로그를 참조 하세요.

1. **파일 탐색기**에서 *C:\inetpub\wwwroot\ContosoUniversity*로 이동 합니다. *Elmah* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 **보안** 탭을 선택 합니다.
2. **편집**을 클릭합니다.
3. **Elmah에 대 한 사용 권한** 대화 상자에서 **DefaultAppPool**을 선택 하 고 **허용** 열에서 **쓰기** 확인란을 선택 합니다.

    ![ELMAH 폴더에 대 한 사용 권한](setting-folder-permissions/_static/image3.png)

    **그룹 또는 사용자 이름** 목록에 **DefaultAppPool** 가 표시 되지 않으면이 자습서에 지정 된 것과 다른 방법을 사용 하 여 컴퓨터에서 IIS 및 ASP.NET 4를 설정 하는 것입니다. 이 경우 Contoso 대학 응용 프로그램에 할당 된 응용 프로그램 풀에서 사용 되는 id를 확인 하 고 해당 id에 대 한 쓰기 권한을 부여 합니다. 이 자습서의 끝부분에 있는 응용 프로그램 풀 id에 대 한 링크를 참조 하세요.) 두 대화 상자에서 **확인을** 클릭 합니다.

## <a name="retest-error-logging-and-reporting"></a>오류 로깅 및 보고 다시 테스트

동일한 방식으로 오류를 다시 발생 시켜 테스트 합니다 (잘못 된 URL 요청) 하 고 **오류 로그** 페이지를 실행 합니다. 이번에는 페이지에 오류가 표시 됩니다.

![ELMAH 오류 로그 페이지](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a>요약

이제 Contoso 대학이 로컬 컴퓨터의 IIS에서 올바르게 작동 하는 데 필요한 모든 작업을 완료 했습니다. 다음 자습서에서는 Azure에 배포 하 여 사이트를 공개적으로 사용할 수 있도록 설정 합니다.

## <a name="more-information"></a>자세한 정보

이 예제에서 Elmah가 로그 파일을 저장할 수 없는 이유는 매우 명확 합니다. 문제의 원인이 명확 하지 않은 경우에 IIS 추적을 사용할 수 있습니다. IIS.net 사이트에서 [IIS 7에서 추적을 사용 하 여 실패 한 요청 문제 해결](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) 을 참조 하세요.

응용 프로그램 풀 id에 대 한 사용 권한을 부여 하는 방법에 대 한 자세한 내용은 IIS.net 사이트의 [파일 시스템 acl을 통해 IIS의](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) [응용 프로그램 풀 Id](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) 및 보안 콘텐츠를 참조 하세요.

> [!div class="step-by-step"]
> [이전](deploying-to-iis.md)
> [다음](deploying-to-production.md)
