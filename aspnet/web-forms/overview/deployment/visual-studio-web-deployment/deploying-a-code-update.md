---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457643"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다. 계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.

## <a name="overview"></a>개요

초기 배포 후에는 웹 사이트를 유지 관리 하 고 개발 하는 작업이 계속 진행 되며 업데이트를 배포 하는 데 오랜 시간이 걸립니다. 이 자습서는 응용 프로그램 코드에 업데이트를 배포 하는 과정을 안내 합니다. 이 자습서에서 구현 하 고 배포 하는 업데이트에는 데이터베이스 변경 내용이 포함 되지 않습니다. 다음 자습서에서 데이터베이스 변경 내용을 배포 하는 것과 관련 된 다른 것을 확인할 수 있습니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](troubleshooting.md)를 확인 해야 합니다.

## <a name="make-a-code-change"></a>코드 변경

응용 프로그램에 대 한 업데이트의 간단한 예로, **강사** 페이지에 선택한 강사가 학습 한 과정 목록을 추가 합니다.

**강사** 페이지를 실행 하는 경우 표에 **Select** 링크가 있지만 행 배경이 회색으로 전환 되는 것 외에는 아무것도 수행 하지 않습니다.

![선택 항목이 있는 강사 페이지](deploying-a-code-update/_static/image1.png)

이제 **선택** 링크를 클릭 하면 실행 되는 코드를 추가 하 고 선택한 강사가 학습 한 과정의 목록을 표시 합니다.

1. *강사 .aspx*에서 **ErrorMessageLabel** `Label` 컨트롤 바로 뒤에 다음 태그를 추가 합니다.

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. 페이지를 실행 하 고 강사를 선택 합니다. 강사가 학습 한 과정의 목록이 표시 됩니다.

    ![학습 코스를 사용 하는 강사 페이지](deploying-a-code-update/_static/image2.png)
3. 브라우저를 닫습니다.

## <a name="deploy-the-code-update-to-the-test-environment"></a>테스트 환경에 코드 업데이트 배포

게시 프로필을 사용 하 여 테스트, 스테이징 및 프로덕션 환경에 배포 하려면 먼저 데이터베이스 게시 옵션을 변경 해야 합니다. 더 이상 멤버 자격 데이터베이스에 대 한 권한 부여 및 데이터 배포 스크립트를 실행할 필요가 없습니다.

1. ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 하 여 **웹 게시** 마법사를 엽니다.
2. **프로필** 드롭다운 목록에서 **테스트** 프로필을 클릭 합니다.
3. **설정** 탭을 클릭합니다.
4. **데이터베이스** 섹션의 **Defaultconnection** 에서 **데이터베이스 업데이트** 확인란의 선택을 취소 합니다.
5. **프로필** 탭을 클릭 한 다음 **프로필** 드롭다운 목록에서 **스테이징** 프로필을 클릭 합니다.
6. **테스트** 프로필에 대 한 변경 내용을 저장할지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.
7. 준비 프로필에서 동일한 변경을 수행 합니다.
8. 이 프로세스를 반복 하 여 프로덕션 프로필에서 동일한 변경을 수행 합니다.
9. **웹 게시** 마법사를 닫습니다.

이제 테스트 환경에 배포 하는 것은 한 번의 클릭으로 다시 게시를 실행 하는 것과 같습니다. 이 프로세스를 빠르게 수행 하기 위해 **웹에서 게시** 도구 모음을 클릭 하 여 사용할 수 있습니다.

1. **보기** 메뉴에서 **도구 모음** 을 선택 하 고 **웹 하나**를 선택 하 여 게시를 클릭 합니다.

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. **솔루션 탐색기**에서 ContosoUniversity 프로젝트를 선택 합니다.
3. **웹에서 게시** 도구 모음을 클릭 한 다음 **테스트** 게시 프로필을 선택 하 고 **웹 게시** 를 클릭 합니다 (화살표가 왼쪽 및 오른쪽을 가리키는 아이콘).

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 브라우저는 홈 페이지에 자동으로 열립니다.
5. 강사 페이지를 실행 하 고 강사를 선택 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.

또한 일반적으로 재발 테스트를 수행 합니다. 즉, 사이트의 나머지 부분을 테스트 하 여 새 변경으로 인해 기존 기능이 중단 되지 않는지 확인 합니다. 그러나이 자습서에서는이 단계를 건너뛰고 스테이징 및 프로덕션에 업데이트를 배포 하는 과정을 진행 합니다.

를 다시 배포 하면 웹 배포는 변경 된 파일을 자동으로 확인 하 고 변경 된 파일만 서버로 복사 합니다. 기본적으로 웹 배포는 파일에 마지막으로 변경 된 날짜를 사용 하 여 변경 된 내용을 확인 합니다. 일부 원본 제어 시스템은 파일 내용을 변경 하지 않는 경우에도 파일 날짜를 변경 합니다. 이 경우 파일 체크섬을 사용 하 여 변경 된 파일을 확인 하도록 웹 배포를 구성 하는 것이 좋습니다. 자세한 내용은 ASP.NET 배포 FAQ에서 [모든 파일을 변경 하지 않았지만 재배포 하는 이유](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) 를 참조 하세요.

## <a name="take-the-application-offline-during-deployment"></a>배포 하는 동안 응용 프로그램을 오프 라인 상태로 만들기

이제 배포 하는 변경 내용이 단일 페이지에 간단 하 게 변경 됩니다. 그러나 경우에 따라 더 큰 변경 내용을 배포 하거나, 코드 및 데이터베이스 변경 내용을 모두 배포 하는 경우, 사용자가 배포를 완료 하기 전에 페이지를 요청 하면 사이트가 제대로 동작 하지 않을 수 있습니다. 배포가 진행 되는 동안 사용자가 사이트에 액세스 하지 못하도록 하려면 *오프 라인 .htm 파일\_앱* 을 사용할 수 있습니다. 응용 프로그램의 루트 폴더에 *app\_* 라는 파일을 배치 하는 경우 IIS는 응용 프로그램을 실행 하는 대신 해당 파일을 자동으로 표시 합니다. 따라서 배포 중에 액세스를 차단 하려면 앱을 루트 폴더에 *\_오프 라인* 으로 전환 하 고 배포 프로세스를 실행 한 후 배포를 완료 한 후에 *앱\_오프 라인으로* 제거 합니다.

배포를 시작할 때 서버에 기본 *앱\_오프 라인 .htm* 파일을 자동으로 배치 하 고 완료 되 면 해당 파일을 제거 하도록 웹 배포를 구성할 수 있습니다. 이렇게 하려면 게시 프로필 (pubxml) 파일에 다음 XML 요소를 추가 하면 됩니다.

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

이 자습서의 경우 *오프 라인 .htm 파일\_* 사용자 지정 앱을 만들고 사용 하는 방법을 알아봅니다.

스테이징 사이트에 액세스 하는 사용자가 없기 때문에 준비 사이트에서 *앱\_오프 라인* 으로 사용 하지 않아도 됩니다. 그러나 준비를 사용 하 여 프로덕션 환경에서 배포 하려는 모든 항목을 테스트 하는 것이 좋습니다.

### <a name="create-app_offlinehtm"></a>앱\_오프 라인으로 만들기

1. **솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 항목**을 클릭 합니다.
2. *App\_* 이라는 **html 페이지** 를 만듭니다. Visual Studio에서 기본적으로 만드는 *.html* 확장명에서 최종 "l"을 삭제 합니다.
3. 템플릿 태그를 다음 태그로 바꿉니다.

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. 파일을 저장하고 닫습니다.

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a>응용 프로그램을 웹 사이트의 루트 폴더에\_오프 라인으로 복사

임의의 FTP 도구를 사용 하 여 웹 사이트에 파일을 복사할 수 있습니다. [FileZilla](http://filezilla-project.org/) 은 인기 있는 FTP 도구 이며 스크린 샷에 표시 됩니다.

FTP 도구를 사용 하려면 FTP URL, 사용자 이름 및 암호의 세 가지가 필요 합니다.

URL은 Azure 관리 포털의 웹 사이트 대시보드 페이지에 표시 되며, FTP의 사용자 이름 및 암호는 앞에서 다운로드 한 *publishsettings* 파일에서 찾을 수 있습니다. 다음 단계에서는 이러한 값을 가져오는 방법을 보여 줍니다.

1. Azure 관리 포털에서 **웹 사이트** 탭을 클릭 한 다음 스테이징 웹 사이트를 클릭 합니다.
2. **대시보드** 페이지에서 아래쪽으로 스크롤하여 **빠른** 보기 섹션에서 FTP 호스트 이름을 찾습니다.

    ![FTP 호스트 이름](deploying-a-code-update/_static/image5.png)
3. 메모장 또는 다른 텍스트 편집기에서 *publishsettings* 파일을 엽니다.
4. FTP 프로필에 대 한 `publishProfile` 요소를 찾습니다.
5. `userName` 및 `userPWD` 값을 복사 합니다.

    ![FTP 자격 증명](deploying-a-code-update/_static/image6.png)
6. FTP 도구를 열고 FTP URL에 로그온 합니다.
7. 솔루션 폴더의 *응용 프로그램\_오프 라인 .htm* 을 준비 사이트의 */site/pers* 폴더에 복사 합니다.

    ![App_offline 복사](deploying-a-code-update/_static/image7.png)
8. 준비 사이트의 URL로 이동 합니다. 이제 홈 페이지 대신 *앱\_오프 라인 .htm* 페이지가 표시 되는 것을 볼 수 있습니다.

    ![브라우저 창의 app_offline](deploying-a-code-update/_static/image8.png)

이제 스테이징에 배포할 준비가 되었습니다.

## <a name="deploy-the-code-update-to-staging-and-production"></a>스테이징 및 프로덕션에 코드 업데이트 배포

1. 웹에서 **게시** 도구 모음을 클릭 한 다음 **스테이징** 게시 프로필을 선택 하 고 **웹 게시**를 클릭 합니다.

    Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 사이트의 홈 페이지에 브라우저를 엽니다. *앱\_오프 라인 .htm* 파일이 표시 됩니다. 테스트를 완료 하 여 성공적인 배포를 확인 하려면 먼저 *오프 라인 .htm 파일\_앱* 을 제거 해야 합니다.
2. FTP 도구로 돌아가서 준비 사이트에서 **앱\_오프 라인** 으로 삭제 합니다.
3. 브라우저에서 준비 사이트의 강사 페이지를 열고 강사를 선택 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.
4. 스테이징 에서처럼 프로덕션에 대해 동일한 절차를 수행 합니다.

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a>변경 내용 검토 및 특정 파일 배포

Visual Studio 2012는 개별 파일을 배포 하는 기능을 제공 합니다. 선택한 파일의 경우 로컬 버전과 배포 된 버전 간의 차이점을 확인 하거나, 대상 환경에 파일을 배포 하거나, 대상 환경에서 로컬 프로젝트로 파일을 복사할 수 있습니다. 자습서의이 섹션에서는 이러한 기능을 사용 하는 방법을 보여 줍니다.

### <a name="make-a-change-to-deploy"></a>배포를 변경 합니다.

1. *Content/사이트인 .css*를 열고 `body` 태그의 블록을 찾습니다.
2. `background-color`의 값을 `#fff`에서 `darkblue`으로 변경 합니다.

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a>게시 미리 보기 창에서 변경 내용 보기

**웹 게시** 마법사를 사용 하 여 프로젝트를 게시 하는 경우 **미리 보기** 창에서 파일을 두 번 클릭 하 여 게시 될 변경 내용을 확인할 수 있습니다.

1. ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 합니다.
2. **프로필** 드롭다운 목록에서 **테스트** 게시 프로필을 선택 합니다.
3. **미리 보기**를 클릭 한 다음 **미리 보기 시작**을 클릭 합니다.
4. **미리 보기** 창에서 **사이트 .css**를 두 번 클릭 합니다.

    ![Site .css를 두 번 클릭 합니다.](deploying-a-code-update/_static/image9.png)

    **변경 내용 미리 보기** 대화 상자에 배포할 변경 내용에 대 한 미리 보기가 표시 됩니다.

    ![사이트 css에 대 한 변경 내용 미리 보기](deploying-a-code-update/_static/image10.png)

    *Web.config 파일을* 두 번 클릭 하면 **변경 내용 미리 보기** 대화 상자에 빌드 구성 변환과 게시 프로필 변환의 결과가 표시 됩니다. 이 시점에서 서버에서 *web.config 파일을 변경 하는 작업* 을 수행 하지 않았기 때문에 변경 내용이 표시 되지 않을 것입니다. 그러나 **변경 내용 미리 보기** 창에는 두 가지 변경 내용이 잘못 표시 됩니다. 두 XML 요소가 제거 되는 것 처럼 보입니다. 이러한 요소는 Code First context 클래스에 대해 **응용 프로그램에서 Code First 마이그레이션 실행을** 선택 하면 게시 프로세스를 통해 추가 됩니다. 비교는 게시 프로세스에서 해당 요소를 추가 하기 전에 수행 되므로 제거 되지 않더라도 제거 되는 것 처럼 보입니다. 이 오류는 이후 릴리스에서 수정 될 예정입니다.
5. **닫기**를 클릭합니다.
6. **게시**를 클릭합니다.
7. 브라우저가 테스트 사이트의 홈 페이지로 열리면 CTRL + F5 키를 눌러 CSS 변경의 영향을 확인 하기 위해 하드 새로 고침을 수행 합니다.

    ![CSS 변경의 효과](deploying-a-code-update/_static/image11.png)
8. 브라우저를 닫습니다.

### <a name="publish-specific-files-from-solution-explorer"></a>솔루션 탐색기에서 특정 파일 게시

파란색 배경을 원하지 않고 원래 색으로 되돌려야 한다고 가정 합니다. 이 섹션에서는 **솔루션 탐색기**에서 직접 특정 파일을 게시 하 여 원래 설정을 복원 합니다.

1. *Content/사이트인 .css* 를 열고 `background-color` 설정을 `#fff`으로 복원 합니다.
2. **솔루션 탐색기**에서 *Content/Site .css* 파일을 마우스 오른쪽 단추로 클릭 합니다.

    상황에 맞는 메뉴에는 세 가지 게시 옵션이 표시 됩니다.

    ![솔루션 탐색기에서 옵션 게시](deploying-a-code-update/_static/image12.png)
3. **사이트 css에 대 한 변경 내용 미리 보기를**클릭 합니다.

    로컬 파일과 대상 환경에 있는 버전의 차이점을 보여 주는 창이 열립니다.

    ![Diff-Content/Site.css](deploying-a-code-update/_static/image13.png)
4. **솔루션 탐색기**에서 **site. .css** 를 다시 마우스 오른쪽 단추로 클릭 하 고 **Publish Publish**를 클릭 합니다.

    **웹 게시 작업** 창에 파일이 게시 된 것으로 표시 됩니다.

    ![웹 게시 작업 창](deploying-a-code-update/_static/image14.png)
5. 브라우저에서 `http://localhost/contosouniversity` URL을 연 다음 CTRL + f 5를 눌러 CSS 변경의 효과를 확인 합니다.

    ![일반 CSS를 사용 하는 홈 페이지](deploying-a-code-update/_static/image15.png)
6. 브라우저를 닫습니다.

## <a name="summary"></a>요약

이제 데이터베이스 변경 내용이 포함 되지 않은 응용 프로그램 업데이트를 배포 하는 여러 가지 방법에 대해 알아보았습니다. 변경 사항을 미리 보고 업데이트를 확인 하는 방법을 살펴보았습니다. 강사 페이지에는 이제 학습 된 **강좌가** 있습니다.

![학습 코스를 사용 하는 강사 페이지](deploying-a-code-update/_static/image16.png)

다음 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법을 보여 줍니다. 데이터베이스와 강사 페이지에 생년월일 필드를 추가 합니다.

> [!div class="step-by-step"]
> [이전](deploying-to-production.md)
> [다음](deploying-a-database-update.md)
