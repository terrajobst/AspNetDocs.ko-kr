---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 데이터베이스 업데이트 배포-9/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582001"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a>Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 데이터베이스 업데이트 배포-9/12

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다. 시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.

## <a name="overview"></a>개요

이 자습서에서는 데이터베이스를 변경 하 고 관련 코드를 변경 하 고, Visual Studio에서 변경 내용을 테스트 하 고, 테스트 환경과 프로덕션 환경 모두에 업데이트를 배포 합니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.

## <a name="adding-a-new-column-to-a-table"></a>테이블에 새 열 추가

이 섹션에서는 `Student` 및 `Instructor` 엔터티에 대 한 `Person` 기본 클래스에 생년월일 열을 추가 합니다. 그런 다음 새 열을 표시 하도록 강사 데이터를 표시 하는 페이지를 업데이트 합니다.

*ContosoUniversity* 프로젝트에서 *Person.cs* 를 열고 `Person` 클래스의 끝에 다음 속성을 추가 합니다. 다음에 닫는 중괄호가 두 개 있어야 합니다.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

그런 다음 새 열에 대 한 값을 제공 하도록 초기값 메서드를 업데이트 합니다. *Migrations\ configuration.cs* 를 열고 `var instructors = new List<Instructor>` 시작 하는 코드 블록을 출생 날짜 정보를 포함 하는 다음 코드 블록으로 바꿉니다.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

ContosoUniversity 프로젝트에서 *강사 .aspx* 를 열고 생년월일을 표시할 새 템플릿 필드를 추가 합니다. 채용 날짜 및 사무실 할당에 대 한 항목 사이에 추가 합니다.

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

코드 들여쓰기가 동기화 되지 않으면 CTRL + K를 누르고 CTRL + D를 눌러 자동으로 파일의 서식을 다시 지정할 수 있습니다.

솔루션을 빌드한 다음 **패키지 관리자 콘솔** 창을 엽니다. ContosoUniversity가 여전히 **기본 프로젝트로**선택 되어 있는지 확인 합니다.

**패키지 관리자 콘솔** 창에서 **기본 프로젝트로** **ContosoUniversity** 를 선택 하 고 다음 명령을 입력 합니다.

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

이 명령이 완료 되 면 Visual Studio는 새 `DbMigration` 클래스를 정의 하는 클래스 파일을 열고 `Up` 메서드에서 새 열을 만드는 코드를 볼 수 있습니다.

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

솔루션을 빌드한 후 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다 (ContosoUniversity 프로젝트를 계속 선택 해야 합니다).

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

명령이 완료 되 면 응용 프로그램을 실행 하 고 강사 페이지를 선택 합니다. 페이지가 로드 되 면 새 생년월일 필드가 표시 됩니다.

[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>테스트 환경에 데이터베이스 업데이트 배포

**솔루션 탐색기** 에서 ContosoUniversity 프로젝트를 선택 합니다.

웹에서 **게시** 도구 모음을 클릭 한 다음 **테스트** 게시 프로필을 선택 하 고 **웹 게시**를 클릭 합니다. (도구 모음을 사용할 수 없는 경우 **솔루션 탐색기**에서 ContosoUniversity 프로젝트를 선택 합니다.)

Visual Studio는 업데이트 된 응용 프로그램을 배포 하 고 홈 페이지에 브라우저를 엽니다. 강사 페이지를 실행 하 여 업데이트가 성공적으로 배포 되었는지 확인 합니다. 응용 프로그램에서이 페이지의 데이터베이스에 액세스 하려고 하면 Code First는 데이터베이스 스키마를 업데이트 하 고 `Seed` 메서드를 실행 합니다. 페이지가 표시 되 면 예상 **생년월일** 열에 날짜가 표시 됩니다.

[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>프로덕션 환경에 데이터베이스 업데이트 배포

이제 프로덕션 환경에 배포할 수 있습니다. 유일한 차이점은 사용자가 사이트에 액세스 하 여 변경 내용을 배포 하는 동안 데이터베이스를 업데이트 하는 것을 방지 하기 위해 *\_오프 라인 .htm 앱* 을 사용 한다는 것입니다. 프로덕션 배포의 경우 다음 단계를 수행 합니다.

- *앱\_오프 라인 .htm* 파일을 프로덕션 사이트에 업로드 합니다.
- Visual Studio의 **웹에서 게시** 도구 모음을 클릭 한 후 **웹 게시**를 클릭 하 여 프로덕션 프로필을 선택 합니다.
- 프로덕션 사이트에서 *앱\_오프 라인 .htm* 파일을 삭제 합니다.

> [!NOTE]
> 프로덕션 환경에서 응용 프로그램을 사용 하는 동안에는 백업 계획을 구현 해야 합니다. 즉, 프로덕션 사이트에서 안전한 저장소 위치에 *School-Prod* 및 *aspnet-Prod* 파일을 주기적으로 복사 해야 하며, 이러한 백업에 대 한 여러 세대를 유지 해야 합니다. 데이터베이스를 업데이트 하는 경우 변경 직전에 백업 복사본을 만들어야 합니다. 그런 다음, 실수를 하 고 프로덕션 환경에 배포한 후에도이를 검색 하지 않으면 데이터베이스가 손상 되기 전의 상태로 복구 될 수 있습니다.

Visual Studio가 브라우저에서 홈 페이지 URL을 열면 *앱\_오프 라인 .htm* 페이지가 표시 됩니다. *응용 프로그램\_오프 라인 .htm* 파일을 삭제 한 후 홈 페이지로 이동 하 여 업데이트가 성공적으로 배포 되었는지 확인할 수 있습니다.

[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)

이제 테스트와 프로덕션 모두에 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트를 배포 했습니다. 다음 자습서에서는 데이터베이스를 SQL Server Compact에서 SQL Server Express 및 SQL Server로 마이그레이션하는 방법을 보여 줍니다.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [다음](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
