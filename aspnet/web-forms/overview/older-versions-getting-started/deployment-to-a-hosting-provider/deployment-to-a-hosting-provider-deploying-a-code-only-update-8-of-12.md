---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 코드 전용 업데이트 배포-8/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74572757"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a>Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 코드 전용 업데이트 배포-8/12

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다. 시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.

## <a name="overview"></a>개요

초기 배포 후에는 웹 사이트를 유지 관리 하 고 개발 하는 작업이 계속 진행 되며 업데이트를 배포 하는 데 오랜 시간이 걸립니다. 이 자습서는 응용 프로그램 코드에 업데이트를 배포 하는 과정을 안내 합니다. 이 업데이트에는 데이터베이스 변경 내용이 포함 되지 않습니다. 다음 자습서에서 데이터베이스 변경 내용을 배포 하는 것과 관련 된 다른 것을 확인할 수 있습니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.

## <a name="making-a-code-change"></a>코드 변경

응용 프로그램에 대 한 업데이트의 간단한 예로, **강사** 페이지에 선택한 강사가 학습 한 과정 목록을 추가 합니다.

**강사** 페이지를 실행 하는 경우 표에 **Select** 링크가 있지만 행 배경이 회색으로 전환 되는 것 외에는 아무것도 수행 하지 않습니다.

[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

이제 **선택** 링크를 클릭 하면 실행 되는 코드를 추가 하 고 선택한 강사가 학습 한 과정의 목록을 표시 합니다.

*강사 .aspx*에서 **ErrorMessageLabel** `Label` 컨트롤 바로 뒤에 다음 태그를 추가 합니다.

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

페이지를 실행 하 고 강사를 선택 합니다. 강사가 학습 한 과정의 목록이 표시 됩니다.

[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a>테스트 환경에 코드 업데이트 배포

테스트 환경에 배포 하는 것은 한 번의 클릭으로 게시를 다시 실행 하는 것과 같습니다. 이 프로세스를 빠르게 수행 하기 위해 **웹에서 게시** 도구 모음을 클릭 하 여 사용할 수 있습니다.

**보기** 메뉴에서 **도구 모음** 을 선택 하 고 **웹 하나**를 선택 하 여 게시를 클릭 합니다.

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

**솔루션 탐색기**에서 ContosoUniversity 프로젝트를 선택 합니다.

**웹에서 게시** 도구 모음을 클릭 한 다음 **테스트** 게시 프로필을 선택 하 고 **웹 게시** 를 클릭 합니다 (화살표가 왼쪽 및 오른쪽을 가리키는 아이콘).

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 브라우저는 홈 페이지에 자동으로 열립니다. 강사 페이지를 실행 하 고 강사를 선택 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.

[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

또한 일반적으로 재발 테스트를 수행 합니다. 즉, 사이트의 나머지 부분을 테스트 하 여 새 변경으로 인해 기존 기능이 중단 되지 않는지 확인 합니다. 그러나이 자습서에서는이 단계를 건너뛰고 업데이트를 프로덕션에 배포 하는 과정을 진행 합니다.

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a>프로덕션에 초기 데이터베이스 상태 다시 배포 방지

실제 응용 프로그램에서 사용자는 초기 배포 후 프로덕션 사이트와 상호 작용 하며 데이터베이스는 라이브 데이터로 채워집니다. 따라서 모든 라이브 데이터를 초기화 하는 초기 상태에서 멤버 자격 데이터베이스를 다시 배포 하는 것을 원하지 않습니다. SQL Server Compact 데이터베이스는 *app\_data* 폴더에 있는 파일 이므로 *앱\_데이터* 폴더의 파일이 배포 되지 않도록 배포 설정을 변경 하 여이를 방지 해야 합니다.

ContosoUniversity 프로젝트에 대 한 **프로젝트 속성** 창을 열고 **웹 패키지 및 게시** 탭을 선택 합니다. **구성** 드롭다운 상자에 **활성 (릴리스)** 또는 **릴리스** 가 선택 되어 있는지 확인 하 고, **앱\_데이터 폴더에서 파일 제외**를 선택 합니다.

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

나중에 디버그 빌드를 배포 하기로 결정 한 경우 디버그 빌드 구성에 대해 동일한 변경 작업을 수행 하는 것이 좋습니다. **구성** 을 **디버그** 로 변경 하 고 **앱\_데이터 폴더에서 파일 제외**를 선택 합니다.

**웹 패키지 및 게시** 탭을 저장 하 고 닫습니다.

> [!NOTE] 
> 
> [!IMPORTANT]
> 게시 프로필에서 선택한 **대상에서 추가 파일을 제거** 하지 않았는지 확인 합니다. 이 옵션을 선택 하면 배포 프로세스에서 앱\_데이터에 포함 된 데이터베이스를 삭제 하 고, 응용 프로그램\_데이터 폴더 자체를 삭제 합니다.

## <a name="preventing-user-access-to-the-production-site-during-update"></a>업데이트 중에 프로덕션 사이트에 대 한 사용자 액세스 방지

이제 배포 하는 변경 내용이 단일 페이지에 간단 하 게 변경 됩니다. 하지만 경우에 따라 대규모 변경 사항을 배포 하는 경우에는 사용자가 배포를 완료 하기 전에 페이지를 요청 하는 경우 사이트가 이상으로 동작할 수 있습니다. 이를 방지 하기 위해 *오프 라인 .htm 파일\_앱* 을 사용할 수 있습니다. 응용 프로그램의 루트 폴더에 *app\_* 라는 파일을 배치 하는 경우 IIS는 응용 프로그램을 실행 하는 대신 해당 파일을 자동으로 표시 합니다. 따라서 배포 중에 액세스를 차단 하려면 앱을 루트 폴더에 *\_오프 라인* 으로 설정 하 고, 배포 프로세스를 실행 한 다음, *응용 프로그램\_오프 라인으로*제거 합니다.

**솔루션 탐색기**에서 솔루션 (프로젝트 중 하나가 아님)을 마우스 오른쪽 단추로 클릭 하 고 **새 솔루션 폴더**를 선택 합니다.

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

폴더 이름을 *솔루션*으로 합니다.

새 폴더에서 *앱\_오프 라인 .htm*이라는 HTML 페이지를 만듭니다. 기존 내용을 다음 태그로 바꿉니다.

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

호스팅 공급자의 제어판에서 FTP 연결 또는 **파일 관리자** 유틸리티를 사용 하 여 *오프 라인 .htm 파일\_응용 프로그램* 을 사이트에 복사할 수 있습니다. 이 자습서에서는 **파일 관리자**를 사용 합니다.

[프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에서 했던 것 처럼 제어판을 열고 **파일 관리자** 를 선택 합니다. **Contosouniversity.com** 를 선택한 다음 **wwwroot** 를 선택 하 여 응용 프로그램의 루트 폴더를 가져온 다음 **업로드**를 클릭 합니다.

[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

**파일 업로드** 대화 상자에서 *오프 라인 .htm 파일\_앱* 을 선택 하 고 **업로드**를 클릭 합니다.

[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

사이트의 URL로 이동 합니다. 이제 홈 페이지 대신 *앱\_오프 라인 .htm* 페이지가 표시 되는 것을 볼 수 있습니다.

[App_offline ![htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

이제 프로덕션 환경에 배포할 준비가 되었습니다.

## <a name="deploying-the-code-update-to-the-production-environment"></a>프로덕션 환경에 코드 업데이트 배포

웹에서 **게시** 도구 모음을 클릭 한 다음 **프로덕션** 게시 프로필을 선택 하 고 **웹 게시**를 클릭 합니다.

Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 사이트의 홈 페이지에 브라우저를 엽니다. *앱\_오프 라인 .htm* 파일이 표시 됩니다. 테스트를 완료 하 여 성공적인 배포를 확인 하려면 먼저 *오프 라인 .htm 파일\_앱* 을 제거 해야 합니다.

제어판에서 **파일 관리자** 응용 프로그램으로 돌아갑니다. **Contosouniversity.com** 및 **wwwroot**를 선택 하 고 **앱\_오프 라인 .htm**을 선택한 다음 **삭제**를 클릭 합니다.

[Deleting_app_offline ![](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

브라우저에서 공용 사이트의 강사 페이지를 열고 강사를 선택 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.

[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

이제 데이터베이스 변경 내용이 포함 되지 않은 응용 프로그램 업데이트를 배포 했습니다. 다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
