---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 프로덕션 환경에 배포-7/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: b83ab819-2b05-4776-b7b4-79ef78d457a5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
msc.type: authoredcontent
ms.openlocfilehash: db838633accdedd7c0693b126a007e254ca681e4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74627458"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-the-production-environment---7-of-12"></a>Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 프로덕션 환경에 배포-7/12

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다. 시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.

## <a name="overview"></a>개요

이 자습서에서는 호스팅 공급자를 사용 하 여 계정을 설정 하 고 Visual Studio one 클릭 게시 기능을 사용 하 여 ASP.NET 웹 응용 프로그램을 프로덕션 환경에 배포 합니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.

## <a name="selecting-a-hosting-provider"></a>호스팅 공급자 선택

Contoso 대학 응용 프로그램 및이 자습서 시리즈의 경우 ASP.NET 4 및 웹 배포를 지 원하는 공급자가 필요 합니다. 특정 호스팅 회사를 선택 하 여 자습서에서 라이브 웹 사이트에 배포 하는 전체 환경을 보여 줄 수 있습니다. 각 호스팅 회사는 다양 한 기능을 제공 하 고 해당 서버에 배포 하는 환경은 약간 다릅니다. 그러나이 자습서에서 설명 하는 프로세스는 전반적인 프로세스에 일반적입니다. 이 자습서에 사용 되는 호스팅 공급자 (Cytanium.com)는 사용할 수 있는 여러 항목 중 하나 이며이 자습서에서 사용 하는 공급자는 인증 또는 권장 사항을 구성 하지 않습니다.

사용자 고유의 호스팅 공급자를 선택할 준비가 되 면 Microsoft.com/web 사이트의 [공급자 갤러리](https://www.microsoft.com/web/hosting) 에 있는 기능 및 가격을 비교할 수 있습니다.

## <a name="creating-an-account"></a>계정 만들기

선택한 공급자에 계정을 만듭니다. 전체 SQL Server 데이터베이스에 대 한 지원이 추가 되는 경우이 자습서에서 선택할 필요가 없지만이 시리즈의 뒷부분에 나오는 [SQL Server로 마이그레이션](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) 자습서에는이 데이터베이스를 추가 해야 합니다.

이러한 자습서에서는 새 도메인 이름을 등록 하지 않아도 됩니다. 공급자에 의해 사이트에 할당 된 임시 URL을 사용 하 여 성공적인 배포를 확인 하는 테스트를 수행할 수 있습니다.

계정이 생성 된 후에는 일반적으로 사이트를 배포 하 고 관리 하는 데 필요한 모든 정보를 포함 하는 환영 전자 메일을 받게 됩니다. 호스팅 공급자가 보내는 정보는 여기에 표시 된 것과 비슷합니다. 새 계정 소유자에 게 전송 되는 Cytanium 환영 전자 메일에는 다음 정보가 포함 됩니다.

- 사이트에 대 한 설정을 관리할 수 있는 공급자의 제어판 사이트에 대 한 URL입니다. 지정 된 ID와 암호는 쉽게 참조할 수 있도록 환영 전자 메일의이 부분에 포함 되어 있습니다. (이 그림의 데모 값으로 변경 되었습니다.)

    [![Welcome_Email_Control_Panel_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image1.png)
- 기본 .NET Framework 버전 및 변경 하는 방법에 대 한 정보입니다. 대부분의 호스팅 사이트는 .NET Framework 2.0, 3.0 또는 3.5을 대상으로 하는 ASP.NET 응용 프로그램에서 작동 하는 2.0를 기본값으로 사용 합니다. 그러나 Contoso 대학은 .NET Framework 4 응용 프로그램 이므로이 설정을 변경 해야 합니다. ASP.NET 4.5 응용 프로그램의 경우 .NET 4.0 설정을 사용 합니다.

    [![Welcome_Email_Framework_Version](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image3.png)
- 웹 사이트에 액세스 하는 데 사용할 수 있는 임시 URL입니다. 이 계정을 만든 후에는 "contosouniversity.com"가 기존 도메인 이름으로 입력 되었습니다. 따라서 임시 URL이 `http://contosouniversity.com.vserver01.cytanium.com`됩니다.

    [![Welcome_Email_Temporary_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image5.png)
- 데이터베이스를 설정 하는 방법에 대 한 정보 및 데이터베이스에 액세스 하기 위해 필요한 연결 문자열:

    [![Welcome_Email_Database_Info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image7.png)
- 사이트 배포를 위한 도구 및 설정에 대 한 정보입니다. (Cytanium의 전자 메일 에서도 WebMatrix를 언급 합니다. 여기서 생략 됩니다.)

    [![Welcome_Email_Deploy_info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image10.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image9.png)

## <a name="setting-the-net-framework-version"></a>.NET Framework 버전 설정

Cytanium 환영 전자 메일에는 .NET Framework 버전을 변경 하는 방법에 대 한 지침에 대 한 링크가 포함 되어 있습니다. 이 지침에서는 Cytanium 제어판을 통해이 작업을 수행할 수 있음을 설명 합니다. 다른 공급자는 다른 방식으로 표시 되는 제어판 사이트를 포함 하거나 다른 방식으로이 작업을 수행 하도록 지시할 수 있습니다.

제어판 URL로 이동 합니다. 사용자 이름 및 암호를 사용 하 여 로그인 한 후 제어판이 표시 됩니다.

[![Cytanium_Control_Panel](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image11.png)

**호스팅 공간** 상자에서 웹 아이콘 위에 포인터를 놓고 메뉴에서 **웹 사이트** 를 선택 합니다.

[![Cytanium_Control_Panel_selecting_Web_Sites](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image13.png)

**웹 사이트** 상자에서 **contosouniversity.com** (계정을 만들 때 사용한 사이트의 이름)를 클릭 합니다.

[![Cytanium_Control_Panel_selecting_contosouniversity](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image15.png)

**웹 사이트 속성** 상자에서 **확장** 탭을 선택 합니다.

[![Cytanium_Control_Panel_Extensions_tab](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image17.png)

ASP.NET를 **2.0 통합 파이프라인** 에서 **4.0 (통합 파이프라인)** 로 변경 하 고 **업데이트**를 클릭 합니다.

## <a name="publishing-to-the-hosting-provider"></a>호스팅 공급자에 게시

호스팅 공급자의 환영 전자 메일에는 프로젝트를 게시 하기 위해 필요한 모든 설정이 포함 되어 있으며, 게시 프로필에 해당 정보를 수동으로 입력할 수 있습니다. 그러나 더 쉽고 간단한 오류가 발생 하기 쉬운 방법을 사용 하 여 공급자에 대 한 배포를 구성 *합니다. publishsettings* 파일을 다운로드 하 여 게시 프로필에 가져옵니다.

브라우저에서 Cytanium 컨트롤 패널로 이동 하 고 **웹** 을 선택한 다음 웹 사이트를 선택 **합니다.**

![웹 사이트 선택 제어판](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image19.png)

**Contosouniversity.com** 웹 사이트를 선택 합니다.

![Contosouniversity.com를 선택 하 여 제어판](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image20.png)

**웹 게시** 탭을 선택 합니다.

![제어판 웹 게시 탭](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image21.png)

사용자 이름 및 암호를 입력 하 여 웹 게시에 사용할 자격 증명을 만듭니다. 제어판에 로그온 하는 데 사용 하는 것과 동일한 자격 증명을 입력할 수 있습니다. 그런 다음 **사용**을 클릭 합니다.

![제어판에서 게시 자격 증명 만들기](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image22.png)

**이 웹 사이트에 대 한 게시 프로필 다운로드를**클릭 합니다.

![제어판 게시 프로필 다운로드](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image23.png)

파일을 열거나 저장 하 라는 메시지가 표시 되 면 파일을 저장 합니다.

![게시 프로필 파일 저장](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image24.png)

Visual Studio의 **솔루션 탐색기** 에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다. **웹 게시** 대화 상자는 **미리 보기** 탭에서 열립니다 .이 대화 상자는 마지막으로 사용한 프로필 이므로 **테스트** 프로필을 선택 합니다.

**프로필** 탭을 선택 하 고 **가져오기**를 클릭 합니다.

![웹 게시 마법사 가져오기 단추](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image25.png)

**게시 설정 가져오기** 대화 상자에서 다운로드 한 *publishsettings* 파일을 선택 하 고 **열기**를 클릭 합니다. 마법사가 입력 한 모든 필드가 포함 된 연결 탭으로 이동 합니다.

![웹 게시 마법사 연결 탭](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image26.png)

Publishsettings 파일은 사이트에 대해 계획 된 영구 URL을 대상 URL 상자에 배치 하지만 해당 도메인을 아직 구입 하지 않은 경우에는 값을 임시 URL로 바꿉니다. 이 예제에서는 URL이  *[http://contosouniversity.com.vserver01.cytanium.com](http://contosouniversity.com.vserver01.cytanium.com)됩니다.* 이 상자는 배포 후 브라우저에서 자동으로 열리는 URL을 지정 하는 용도로만 제공 됩니다. 비워 두면 브라우저가 배포 후 자동으로 시작 되지 않습니다.

**연결 유효성 검사** 를 클릭 하 여 설정이 올바른지 그리고 서버에 연결할 수 있는지 확인 합니다. 앞서 살펴본 것 처럼 녹색 확인 표시는 연결에 성공 했는지 확인 합니다.

연결 유효성 검사를 클릭 하면 **인증서 오류** 대화 상자가 표시 될 수 있습니다. 이 경우 서버 이름이 필요한 지 확인 합니다. 이 경우 **나중에 Visual Studio의 세션에 대해이 인증서 저장** 을 선택 하 고 **동의**를 클릭 합니다. (이 오류는 배포 하는 URL에 대 한 SSL 인증서 구매 비용을 방지 하기 위해 호스팅 공급자가 선택 했음을 의미 합니다. 유효한 인증서를 사용 하 여 보안 연결을 설정 하는 것을 선호 하는 경우 호스팅 공급자에 게 문의 하세요.)

![인증서 오류](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image27.png)

**다음**을 클릭합니다.

**설정** 탭의 **데이터베이스** 섹션에서 테스트 게시 프로필에 대해 입력 한 것과 동일한 값을 입력 합니다. 드롭다운 목록에서 필요한 연결 문자열을 찾을 수 있습니다.

- Schoolcontext.cs에 대 한 연결 문자열 상자에서 `Data Source=|DataDirectory|School-Prod.sdf` **를** 선택 합니다.
- **Schoolcontext.cs**아래에서 **Code First 마이그레이션 적용**을 선택 합니다.
- **Defaultconnection**에 대 한 연결 문자열 상자에서 `Data Source=|DataDirectory|aspnet-Prod.sdf`를 선택 합니다.
- **Defaultconnection**에서 **업데이트 데이터베이스** 를 지운 채로 둡니다.

![웹 게시 마법사 설정 탭](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image28.png)

**다음**을 클릭합니다.

**미리 보기** 탭에서 **미리 보기 시작** 을 클릭 하 여 복사할 파일의 목록을 확인 합니다. 로컬 컴퓨터에서 IIS에 배포할 때 표시 된 것과 동일한 목록이 표시 됩니다.

게시 하기 전에 Web.config 변환 파일이 적용 되도록 프로필의 이름을 변경 합니다. **프로필** 탭을 선택 하 고 **프로필 관리**를 클릭 합니다.

![웹 게시 마법사 프로필 관리](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image29.png)

**웹 게시 프로필 편집** 대화 상자에서 프로덕션 프로필을 선택 하 고 **이름 바꾸기**를 클릭 한 다음 프로필 이름을 production로 변경 합니다. 그런 다음 **닫기**를 클릭 합니다.

![웹 게시 프로필 편집 대화 상자](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image30.png)

**게시**를 클릭합니다.

응용 프로그램이 호스팅 공급자에 게시 됩니다. 결과는 **출력** 창에 표시 됩니다.

![배포 후 출력 창](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image31.png)

**웹 게시** 마법사의 **연결** 탭에 있는 **대상 URL** 상자에 입력 한 url이 브라우저에서 자동으로 열립니다. Visual Studio에서 사이트를 실행할 때와 동일한 홈 페이지가 표시 됩니다. 단, 제목 표시줄에는 "(테스트)" 또는 "(Dev)" 환경 표시기가 없습니다. 이는 환경 표시기 *web.config* 변환이 제대로 작동 했음을 나타냅니다.

> [!NOTE]
> 제목에 "(테스트)"가 계속 표시 되는 경우 ContosoUniversity 프로젝트에서 *obj* 폴더를 삭제 하 고 다시 배포 합니다. 소프트웨어의 시험판 버전에서는 프로덕션 프로필을 사용 하는 경우에도 이전에 적용 한 변환 파일 (web.config)이 다시 적용 될 수 있습니다.

[![Home_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image33.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image32.png)

데이터베이스에 액세스 하는 페이지를 실행 하기 전에 Elmah가 발생 하는 모든 오류를 기록할 수 있도록 해야 합니다.

## <a name="setting-folder-permissions-for-elmah"></a>Elmah에 대 한 폴더 권한 설정

이 시리즈의 이전 자습서에서 알 수 있듯이, Elmah에서 오류 로그 파일을 저장 하는 응용 프로그램의 폴더에 대 한 쓰기 권한이 응용 프로그램에 있는지 확인 해야 합니다. 컴퓨터에서 로컬로 IIS에 배포 하는 경우 해당 권한을 수동으로 설정 합니다. 이 섹션에서는 Cytanium에서 권한을 설정 하는 방법을 알아봅니다. (일부 호스팅 공급자는이 작업을 수행할 수 없습니다. 쓰기 권한이 있는 미리 정의 된 폴더를 하나 이상 제공할 수 있습니다. 이 경우 지정 된 폴더를 사용 하도록 응용 프로그램을 수정 해야 합니다.

Cytanium 제어판에서 폴더 사용 권한을 설정할 수 있습니다. 제어판 URL로 이동 하 여 **파일 관리자**를 선택 합니다.

[![Cytanium_Control_Panel_with_File_Manager_selected](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image35.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image34.png)

**파일 관리자** 상자에서 **contosouniversity.com** 을 선택한 다음 **wwwroot** 를 선택 하 여 응용 프로그램의 루트 폴더를 확인 합니다. **Elmah**옆에 있는 자물쇠 아이콘을 클릭 합니다.

[![Cytanium_Control_Panel_File_Manager_at_root_folder](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image37.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image36.png)

**파일**/**폴더 사용 권한** 창에서 **contosouniversity.com** 에 대 한 **읽기** 및 **쓰기** 확인란을 선택 하 고 **사용 권한 설정**을 클릭 합니다.

[![Cytanium_Control_Panel_File_Folder_Permissions_Elmah](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image39.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image38.png)

Elmah에 오류가 발생 한 다음 Elmah 오류 보고서를 표시 하 여 *elmah 폴더에* 대 한 쓰기 권한이 있는지 확인 합니다. *Studentsxxx*와 같은 잘못 된 URL을 요청 합니다. 이전과 마찬가지로 *Genericerrorpage .aspx* 페이지가 표시 됩니다. **로그 아웃** 링크를 클릭 한 다음 *Elmah*를 실행 합니다. 먼저 **로그인** 페이지를 가져와 *Web.config* 변환에서 Elmah 권한 부여를 성공적으로 추가 했는지 확인 합니다. 로그인 하면 방금 발생 한 오류를 표시 하는 보고서가 표시 됩니다.

[![Elmah axd_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image41.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image40.png)

## <a name="testing-in-the-production-environment"></a>프로덕션 환경에서 테스트

**학생** 페이지를 실행 합니다. 응용 프로그램은 처음으로 School 데이터베이스에 액세스 하려고 합니다. 그러면 데이터베이스를 만드는 Code First 마이그레이션 트리거됩니다. 잠시 후에 페이지가 표시 되 면 학생은 표시 되지 않습니다.

[![Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image43.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image42.png)

**강사** 페이지를 실행 하 여 시드 데이터가 데이터베이스의 강사 데이터를 성공적으로 삽입 했는지 확인 합니다.

[![Instructors_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image45.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image44.png)

테스트 환경에서와 같이 데이터베이스 업데이트가 프로덕션 환경에서 작동 하는지 확인 하려고 하지만 일반적으로 프로덕션 데이터베이스에 테스트 데이터를 입력 하지 않으려고 합니다. 이 자습서에서는 테스트에서 수행한 것과 동일한 방법을 사용 합니다. 그러나 실제 응용 프로그램에서는 프로덕션 데이터베이스에 테스트 데이터를 도입 하지 않고 데이터베이스 업데이트가 성공 했는지 확인 하는 메서드를 찾으려고 할 수 있습니다. 일부 응용 프로그램에서는 항목을 추가한 다음 삭제 하는 것이 효과적일 수 있습니다.

학생을 추가한 다음, **학생** 페이지에 입력 한 데이터를 검토 하 여 데이터베이스의 데이터를 업데이트할 수 있는지 확인 합니다.

[![Add_Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image47.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image46.png)

[![Students_page_with_new_student_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image49.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image48.png)

**강좌** 메뉴에서 **크레딧 업데이트** 를 선택 하 여 권한 부여 규칙이 제대로 작동 하는지 확인 합니다. **로그인** 페이지가 표시 됩니다. 관리자 계정 자격 증명을 입력 하 고 **로그인**을 클릭 하면 **크레딧 업데이트** 페이지가 표시 됩니다.

[![Log_In_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image51.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image50.png)

로그인에 성공 하면 **업데이트 크레딧** 페이지가 표시 됩니다. 이는 단일 관리자 계정으로 ASP.NET 멤버 자격 데이터베이스를 성공적으로 배포 했음을 나타냅니다.

[![Update_Credits_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image53.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image52.png)

이제 사이트를 성공적으로 배포 하 고 테스트 했으며 인터넷을 통해 공개적으로 사용할 수 있습니다.

## <a name="creating-a-more-reliable-test-environment"></a>보다 안정적인 테스트 환경 만들기

[테스트 환경에 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서에 설명 된 것 처럼 가장 안정적인 테스트 환경은 프로덕션 계정과 마찬가지로 호스팅 공급자에서 두 번째 계정입니다. 이렇게 하면 두 번째 호스팅 계정에 등록 해야 하므로 로컬 IIS를 테스트 환경으로 사용 하는 것 보다 비용이 많이 듭니다. 하지만 프로덕션 사이트 오류 또는 중단을 방지 하는 경우 비용을 가치가 있음을 결정할 수 있습니다.

테스트 계정을 만들고 배포 하는 프로세스의 대부분은 프로덕션 환경에 배포 하기 위해 이미 수행한 것과 비슷합니다.

- *Web.config 변환 파일* 을 만듭니다.
- 호스팅 공급자에 계정을 만듭니다.
- 새 게시 프로필을 만들고 테스트 계정에 배포 합니다.

### <a name="preventing-public-access-to-the-test-site"></a>테스트 사이트에 대 한 공용 액세스 방지

테스트 계정에 대 한 중요 한 고려 사항은 인터넷에서 라이브 이지만 공용에서 사용 하지 않으려는 경우입니다. 사이트를 비공개로 유지 하려면 다음 방법 중 하나 이상을 사용할 수 있습니다.

- 테스트에 사용 하는 IP 주소 에서만 테스트 사이트에 대 한 액세스를 허용 하는 방화벽 규칙을 설정 하려면 호스팅 공급자에 게 문의 하세요.
- URL을 위장 하 여 공용 사이트의 URL과 유사 하 게 합니다.
- *로봇 .txt* 파일을 사용 하 여 검색 엔진이 테스트 사이트와 해당 사이트에 대 한 보고서 링크를 검색 결과에 탐색 하지 않도록 합니다.

이러한 메서드 중 첫 번째 메서드는 분명히 가장 안전 하지만의 절차는 각 호스팅 공급자에만 해당 되며이 자습서에서는 다루지 않습니다. 호스트 공급자를 사용 하 여 사용자의 IP 주소만 테스트 계정 URL을 탐색할 수 있도록 하는 것으로 정렬 하는 경우 이론적으로 탐색 하는 검색 엔진에 대해 걱정할 필요가 없습니다. 그러나이 경우에도, 방화벽 규칙이 실수로 해제 된 경우에는 *로봇 .txt* 파일을 배포 하는 것이 좋습니다.

*로봇 .txt* 파일은 프로젝트 폴더로 이동 하 고 다음 텍스트를 포함 해야 합니다.

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/samples/sample1.cmd)]

`User-agent` 줄은 파일의 규칙이 모든 검색 엔진 웹 크롤러 (로봇)에 적용 된다는 것을 검색 엔진에 지시 하 고 `Disallow` 줄은 사이트의 어떤 페이지도 크롤링되지 않도록 지정 합니다.

검색 엔진에서 프로덕션 사이트를 카탈로그로 만들려고 할 수 있으므로 프로덕션 배포에서이 파일을 제외 해야 합니다. 이렇게 하려면 [ASP.NET 웹 응용 프로그램 프로젝트 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment)에서 **배포에서 특정 파일 또는 폴더를 제외할 수 있나요?** 를 참조 하세요. 프로덕션 게시 프로필에 대 한 제외만 지정 해야 합니다.

두 번째 호스팅 계정을 만드는 것은 필수는 아니지만 비용이 추가 될 수 있는 테스트 환경에서 작업 하는 방법입니다. 다음 자습서에서는 계속 해 서 IIS를 테스트 환경으로 사용 합니다.

다음 자습서에서는 응용 프로그램 코드를 업데이트 하 고 변경 내용을 테스트 및 프로덕션 환경에 배포 합니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
