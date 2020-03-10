---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 업데이트 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440789"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 업데이트 배포

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다. 계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.

## <a name="overview"></a>개요

이 자습서에서는 데이터베이스를 변경 하 고 관련 코드를 변경 하 고, Visual Studio에서 변경 내용을 테스트 하 고, 테스트, 스테이징 및 프로덕션 환경에 업데이트를 배포 합니다.

이 자습서에서는 먼저 Code First 마이그레이션로 관리 되는 데이터베이스를 업데이트 한 다음 나중에 dbDacFx 공급자를 사용 하 여 데이터베이스를 업데이트 하는 방법을 보여 줍니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](troubleshooting.md)를 확인 해야 합니다.

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a>Code First 마이그레이션를 사용 하 여 데이터베이스 업데이트 배포

이 섹션에서는 `Student` 및 `Instructor` 엔터티에 대 한 `Person` 기본 클래스에 생년월일 열을 추가 합니다. 그런 다음 새 열을 표시 하도록 강사 데이터를 표시 하는 페이지를 업데이트 합니다. 마지막으로 테스트, 스테이징 및 프로덕션에 대 한 변경 내용을 배포 합니다.

### <a name="add-a-column-to-a-table-in-the-application-database"></a>응용 프로그램 데이터베이스의 테이블에 열 추가

1. *ContosoUniversity* 프로젝트에서 *Person.cs* 를 열고 `Person` 클래스의 끝에 다음 속성을 추가 합니다. 다음에 닫는 중괄호가 두 개 있어야 합니다.

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    그런 다음 새 열에 대 한 값을 제공 하도록 `Seed` 메서드를 업데이트 합니다. *Migrations\ configuration.cs* 를 열고 `var instructors = new List<Instructor>` 시작 하는 코드 블록을 출생 날짜 정보를 포함 하는 다음 코드 블록으로 바꿉니다.

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. 솔루션을 빌드한 다음 **패키지 관리자 콘솔** 창을 엽니다. ContosoUniversity가 여전히 **기본 프로젝트로**선택 되어 있는지 확인 합니다.
3. **패키지 관리자 콘솔** 창에서 **기본 프로젝트로** **ContosoUniversity** 를 선택 하 고 다음 명령을 입력 합니다.

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    이 명령이 완료 되 면 Visual Studio는 새 `DbMigration` 클래스를 정의 하는 클래스 파일을 열고 `Up` 메서드에서 새 열을 만드는 코드를 볼 수 있습니다. `Up` 메서드는 변경을 구현할 때 열을 만들고, `Down` 메서드는 변경을 롤백할 때 열을 삭제 합니다.

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. 솔루션을 빌드한 후 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다 (ContosoUniversity 프로젝트를 계속 선택 해야 합니다).

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    Entity Framework `Up` 메서드를 실행 한 다음 `Seed` 메서드를 실행 합니다.

### <a name="display-the-new-column-in-the-instructors-page"></a>강사 페이지에 새 열을 표시 합니다.

1. ContosoUniversity 프로젝트에서 *강사 .aspx* 를 열고 생년월일을 표시할 새 템플릿 필드를 추가 합니다. 채용 날짜 및 사무실 할당에 대 한 항목 사이에 추가 합니다.

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    코드 들여쓰기가 동기화 되지 않으면 CTRL + K를 누르고 CTRL + D를 눌러 자동으로 파일의 서식을 다시 지정할 수 있습니다.
2. 응용 프로그램을 실행 하 고 **강사** 링크를 클릭 합니다.

    페이지가 로드 되 면 새 생년월일 필드가 표시 됩니다.

    ![생일을 사용 하는 강사 페이지](deploying-a-database-update/_static/image2.png)
3. 브라우저를 닫습니다.

### <a name="deploy-the-database-update"></a>데이터베이스 업데이트 배포

1. **솔루션 탐색기** 에서 ContosoUniversity 프로젝트를 선택 합니다.
2. 웹에서 **게시** 도구 모음을 클릭 하 고 **테스트** 게시 프로필을 클릭 한 다음 **웹 게시**를 클릭 합니다. (도구 모음을 사용할 수 없는 경우 **솔루션 탐색기**에서 ContosoUniversity 프로젝트를 선택 합니다.)

    Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 홈 페이지에 브라우저를 엽니다.
3. **강사** 페이지를 실행 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.

    응용 프로그램에서이 페이지의 데이터베이스에 액세스 하려고 하면 Code First는 데이터베이스 스키마를 업데이트 하 고 `Seed` 메서드를 실행 합니다. 페이지가 표시 되 면 예상 **생년월일** 열에 날짜가 표시 됩니다.
4. 웹에서 **게시** 도구 모음을 클릭 한 다음 **스테이징** 게시 프로필을 클릭 하 고 **웹 게시**를 클릭 합니다.
5. 스테이징에서 **강사** 페이지를 실행 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.
6. 웹에서 **게시** 도구 모음을 클릭 한 다음 **프로덕션** 게시 프로필을 클릭 하 고 **웹 게시**를 클릭 합니다.
7. 프로덕션에서 **강사** 페이지를 실행 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다.

    데이터베이스 변경을 포함 하는 실제 프로덕션 응용 프로그램 업데이트의 경우 일반적으로 이전 자습서에서 살펴본 것 처럼 응용 프로그램을 *\_오프 라인*으로 사용 하 여 배포 하는 동안 응용 프로그램을 오프 라인으로 전환 합니다.

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a>DbDacFx 공급자를 사용 하 여 데이터베이스 업데이트 배포

이 섹션에서는 멤버 자격 데이터베이스의 *사용자* 테이블에 *comments* 열을 추가 하 고 각 사용자에 대 한 설명을 표시 하 고 편집할 수 있는 페이지를 만듭니다. 그런 다음 테스트, 스테이징 및 프로덕션에 대 한 변경 내용을 배포 합니다.

### <a name="add-a-column-to-a-table-in-the-membership-database"></a>멤버 자격 데이터베이스의 테이블에 열 추가

1. Visual Studio에서 **SQL Server 개체 탐색기**를 엽니다.
2. **(Localdb) \v11.0**, **데이터베이스**, **aspnet-ContosoUniversity** ( **ContosoUniversity-Prod**)를 차례로 확장 한 다음 **테이블**을 확장 합니다.

    **SQL Server** 노드 아래에 **(localdb) \v11.0** 이 표시 되지 않으면 **SQL Server** 노드를 마우스 오른쪽 단추로 클릭 하 고 **SQL Server 추가**를 클릭 합니다. **서버에 연결** 대화 상자에서 **서버 이름**으로 *(localdb) \v11.0* 을 입력 한 다음 **연결**을 클릭 합니다.

    **ContosoUniversity**가 표시 되지 않으면 프로젝트를 실행 하 고 *관리자* 자격 증명 (암호는 *devpwd*)을 사용 하 여 로그인 한 다음 **SQL Server 개체 탐색기** 창을 새로 고칩니다.
3. **사용자** 테이블을 마우스 오른쪽 단추로 클릭 한 다음 **뷰 디자이너**를 클릭 합니다.

    ![SSOX 뷰 디자이너](deploying-a-database-update/_static/image3.png)
4. 디자이너에서 *주석* 열을 추가 하 고 *nvarchar (128)* 및 nullable로 설정 하 고 **업데이트**를 클릭 합니다.

    ![설명 열 추가](deploying-a-database-update/_static/image4.png)
5. 데이터베이스 업데이트 **미리 보기** 상자에서 **데이터베이스 업데이트**를 클릭 합니다.

    ![데이터베이스 업데이트 미리 보기](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a>새 열을 표시 하 고 편집할 페이지를 만듭니다.

1. **솔루션 탐색기**에서 ContosoUniversity 프로젝트의 **계정** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 항목**을 클릭 합니다.
2. **마스터 페이지를 사용 하 여 새 Web Form** 을 만들고 이름을 *login.aspx*로 이름을로 합니다. 기본 site.master 파일을 마스터 페이지로 적용 *합니다.*
3. 다음 태그를 `MainContent` `Content` 요소 (3 개의 `Content` 요소 중 마지막 요소)에 복사 합니다.

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. *UserInfo* 페이지를 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 보기**를 클릭 합니다.
5. *관리자* 사용자 자격 증명을 사용 하 여 로그인 하 고 (암호는 *devpwd*) 사용자에 게 일부 의견을 추가 하 여 페이지가 제대로 작동 하는지 확인 합니다.

    ![UserInfo 페이지](deploying-a-database-update/_static/image6.png)
6. 브라우저를 닫습니다.

## <a name="deploy-the-database-update"></a>데이터베이스 업데이트 배포

DbDacFx 공급자를 사용 하 여 배포 하려면 게시 프로필에서 **데이터베이스 업데이트** 옵션을 선택 하기만 하면 됩니다. 그러나이 옵션을 사용 하는 경우 초기 배포의 경우 몇 가지 추가 SQL 스크립트를 실행할 수도 있습니다. 이러한 스크립트는 여전히 프로필에 포함 되어 있으므로 다시 실행 하지 않도록 해야 합니다.

1. ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 하 여 **웹 게시** 마법사를 엽니다.
2. **테스트** 프로필을 선택 합니다.
3. **설정** 탭을 클릭합니다.
4. **Defaultconnection**에서 **데이터베이스 업데이트**를 선택 합니다.
5. 초기 배포에 대해 실행 하도록 구성한 추가 스크립트를 사용 하지 않도록 설정 합니다.

    1. **데이터베이스 업데이트 구성**을 클릭 합니다.
    2. **데이터베이스 업데이트 구성** 대화 상자에서 *Grant .sql* and *aspnet-data-dev*옆에 있는 확인란의 선택을 취소 합니다.
    3. **닫기**를 클릭합니다.
6. 미리 보기 도구 모음에서 **미리 보기** 탭을 클릭합니다.
7. 데이터베이스 **에서** **defaultconnection**의 오른쪽에 있는 **데이터베이스 미리 보기** 링크를 클릭 합니다.

    ![데이터베이스 미리 보기](deploying-a-database-update/_static/image7.png)

    미리 보기 창에는 데이터베이스 스키마가 원본 데이터베이스의 스키마와 일치 하도록 대상 데이터베이스에서 실행 될 스크립트가 표시 됩니다. 스크립트에는 새 열을 추가 하는 ALTER TABLE 명령이 포함 되어 있습니다.
8. **데이터베이스 미리 보기** 대화 상자를 닫은 다음 **게시**를 클릭 합니다.

    Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 홈 페이지에 브라우저를 엽니다.
9. 정보 페이지 (홈 페이지 URL에 *계정/개인 정보 .aspx* 추가)를 실행 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다. *관리자* 및 *devpwd*를 입력 하 여 로그인 해야 합니다.

    테이블의 데이터는 기본적으로 배포 되지 않으며 데이터 배포 스크립트를 실행 하도록 구성 하지 않았기 때문에 개발에서 추가한 주석이 검색 되지 않습니다. 이제 준비에 새 설명을 추가 하 여 변경 내용이 데이터베이스에 배포 되 고 페이지가 제대로 작동 하는지 확인할 수 있습니다.
10. 동일한 절차에 따라 스테이징 및 프로덕션에 배포 합니다.

    추가 스크립트를 사용 하지 않도록 설정 하는 것을 잊지 마세요. 테스트 프로필에 비해 유일한 차이점은 준비 및 프로덕션 프로필은 *aspnet-prod-data*만 실행 하도록 구성 되었기 때문에 한 개의 스크립트만 사용 하지 않도록 설정 한다는 것입니다.

    스테이징 및 프로덕션에 대 한 자격 증명은 admin 및 prodpwd입니다.

    데이터베이스 변경을 포함 하는 실제 프로덕션 응용 프로그램 업데이트의 경우 [이전 자습서](deploying-a-code-update.md)에서 살펴본 것 처럼 나중에 게시 하 고 삭제 하기 전에 *오프 라인으로 앱\_* 업로드 하 여 배포 중에 응용 프로그램을 오프 라인으로 전환 합니다.

## <a name="summary"></a>요약

이제 Code First 마이그레이션 및 dbDacFx 공급자를 사용 하 여 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트를 배포 했습니다.

![생일을 사용 하는 강사 페이지](deploying-a-database-update/_static/image8.png)

![UserInfo 페이지](deploying-a-database-update/_static/image9.png)

다음 자습서는 명령줄을 사용 하 여 배포를 실행 하는 방법을 보여 줍니다.

> [!div class="step-by-step"]
> [이전](deploying-a-code-update.md)
> [다음](command-line-deployment.md)
