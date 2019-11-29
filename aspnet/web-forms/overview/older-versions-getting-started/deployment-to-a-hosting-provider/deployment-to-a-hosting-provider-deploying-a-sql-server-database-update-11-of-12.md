---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server 데이터베이스 업데이트 배포-11/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621065"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a>Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server 데이터베이스 업데이트 배포-11/12

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다. 시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여주고, Windows Azure 웹 사이트에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 웹 배포 ASP.NET](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.

## <a name="overview"></a>개요

이 자습서에서는 전체 SQL Server 데이터베이스에 데이터베이스 업데이트를 배포 하는 방법을 보여 줍니다. Code First 마이그레이션는 데이터베이스 업데이트 작업을 모두 수행 하기 때문에이 프로세스는 [데이터베이스 업데이트 배포](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) 자습서에서 SQL Server Compact 했던 프로세스와 거의 동일 합니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.

## <a name="adding-a-new-column-to-a-table"></a>테이블에 새 열 추가

자습서의이 섹션에서는 데이터베이스를 변경 하 고 해당 코드를 변경한 다음 테스트 및 프로덕션 환경에 배포 하기 위해 Visual Studio에서 테스트 합니다. 변경 내용에는 `OfficeHours` 열을 `Instructor` 엔터티에 추가 하 고 **강사** 웹 페이지에 새 정보를 표시 하는 작업이 포함 됩니다.

ContosoUniversity 프로젝트에서 *Instructor.cs* 를 열고 `HireDate`와 `Courses` 속성 사이에 다음 속성을 추가 합니다.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

테스트 데이터를 사용 하 여 새 열을 시드 하도록 이니셜라이저 클래스를 업데이트 합니다. *Migrations\ configuration.cs* 를 열고 `var instructors = new List<Instructor>` 시작 하는 코드 블록을 새 열을 포함 하는 다음 코드 블록으로 바꿉니다.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

ContosoUniversity 프로젝트에서 *강사 .aspx* 를 열고 첫 번째 `GridView` 컨트롤에서 닫는 `</Columns>` 태그 바로 앞에 office 시간에 대 한 새 템플릿 필드를 추가 합니다.

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

솔루션을 빌드합니다.

**패키지 관리자 콘솔** 창을 열고 **기본 프로젝트로**ContosoUniversity를 선택 합니다.

다음 명령을 입력합니다.

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

응용 프로그램을 실행 하 고 **강사** 페이지를 선택 합니다. Entity Framework는 데이터베이스를 다시 만들고 테스트 데이터를 사용 하 여 시드 하므로 페이지를 로드 하는 데 평소 보다 약간 더 시간이 걸립니다.

[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>테스트 환경에 데이터베이스 업데이트 배포

Code First 마이그레이션를 사용 하는 경우 데이터베이스 변경 내용을 SQL Server에 배포 하는 방법은 SQL Server Compact와 동일 합니다. 그러나 SQL Server Compact에서 SQL Server로 마이그레이션하도록 설정 되어 있으므로 테스트 게시 프로필을 변경 해야 합니다.

첫 번째 단계는 이전 자습서에서 만든 연결 문자열 변환을 제거 하는 것입니다. SQL Server로 마이그레이션하기 위해 **SQL 패키지 및 게시** 탭을 구성 하기 전과 같이 게시 프로필에 연결 문자열 변환을 지정 하므로 더 이상 필요 하지 않습니다.

*Web.config* 파일을 열고 `connectionStrings` 요소를 제거 합니다. *Web.config 파일에서* 유일 하 게 남은 변환은 `appSettings` 요소의 `Environment` 값에 대 한 것입니다.

이제 게시 프로필을 업데이트 하 고 테스트 환경에 게시할 수 있습니다.

**웹 게시** 마법사를 열고 **프로필** 탭으로 전환 합니다.

**테스트** 게시 프로필을 선택 합니다.

**설정** 탭을 선택합니다.

**새 데이터베이스 게시 개선 기능 사용을**클릭 합니다.

**Schoolcontext.cs**에 대 한 연결 문자열 상자에 이전 자습서의 web.config 변환 파일에서 사용한 것과 동일한 값을 *입력 합니다.*

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

**Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행)** 을 선택 합니다. 사용자의 Visual Studio 버전에서 확인란에 **Code First 마이그레이션 적용**이 표시 될 수 있습니다.

**Defaultconnection**에 대 한 연결 문자열 상자에 이전 자습서의 web.config 변환 파일에서 사용한 것과 동일한 값을 *입력 합니다.*

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

**업데이트 데이터베이스** 를 지운 채로 둡니다.

**게시**를 클릭합니다.

Visual Studio는 테스트 환경에 코드 변경 내용을 배포 하 고 브라우저를 Contoso 대학 홈 페이지로 엽니다.

강사 페이지를 선택 합니다.

응용 프로그램은이 페이지를 실행할 때 데이터베이스에 액세스를 시도 합니다. Code First 마이그레이션 데이터베이스가 최신 인지 확인 하 고 최신 마이그레이션이 아직 적용 되지 않은 것을 찾습니다. Code First 마이그레이션 최신 마이그레이션을 적용 하 고 `Seed` 메서드를 실행 한 다음 페이지가 정상적으로 실행 됩니다. 시드 된 데이터와 함께 새 Office 시간 열이 표시 됩니다.

[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>프로덕션 환경에 데이터베이스 업데이트 배포

프로덕션 환경에 대 한 게시 프로필도 변경 해야 합니다. 이 경우 기존 프로필을 제거 하 고 publishsettings 파일을 가져와 새 프로필을 만듭니다. 업데이트 된 파일에는 Cytanium의 SQL Server 데이터베이스에 대 한 연결 문자열이 포함 됩니다.

테스트 환경에 배포할 때 볼 수 있듯이, *web.config* 변환 파일에 연결 문자열 변환이 더 이상 필요 하지 않습니다. 해당 파일을 열고 `connectionStrings` 요소를 제거 합니다. 나머지 변환은 `appSettings` 요소의 `Environment` 값 및 Elmah 오류 보고서에 대 한 액세스를 제한 하는 `location` 요소에 대 한 것입니다.

프로덕션 환경에 대 한 새 게시 프로필을 만들기 전에 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서의 이전 단계와 동일한 방식으로 업데이트 된 publishsettings 파일을 다운로드 합니다. Cytanium 컨트롤 패널에서 **웹 사이트**를 클릭 한 다음 **contosouniversity.com** 웹 사이트를 클릭 합니다. **웹 게시** 탭을 선택 하 고 **이 웹 사이트에 대 한 게시 프로필 다운로드**를 클릭 합니다. 이 작업을 수행 하는 이유는 publishsettings 파일에서 데이터베이스 연결 문자열을 선택 하는 것입니다. 연결 문자열은 파일을 처음 다운로드할 때 사용할 수 없습니다. 아직 SQL Server Compact를 사용 하 고 있으므로 아직 Cytanium에서 SQL Server 데이터베이스를 만들지 않았기 때문입니다.

이제 게시 프로필을 업데이트 하 고 프로덕션 환경에 게시할 수 있습니다.

**웹 게시** 마법사를 열고 **프로필** 탭으로 전환 합니다.

**프로필 관리**를 클릭 한 다음 프로덕션 프로필을 삭제 합니다.

이 변경 내용을 저장 하려면 **웹 게시** 마법사를 닫습니다.

**웹 게시** 마법사를 다시 열고 **가져오기**를 클릭 합니다.

임시 URL을 사용 하는 경우 **연결** 탭에서 **대상 url** 을 적절 한 값으로 변경 합니다.

**다음**을 클릭합니다.

**설정** 탭에서 **새 데이터베이스 게시 개선 기능 사용**을 클릭 합니다.

**Schoolcontext.cs**에 대 한 연결 문자열 드롭다운 목록에서 Cytanium 연결 문자열을 선택 합니다.

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

**Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행)** 을 선택 합니다.

**Defaultconnection**에 대 한 연결 문자열 드롭다운 목록에서 Cytanium 연결 문자열을 선택 합니다.

**프로필** 탭을 선택 하 고, 프로필 **관리**를 클릭 하 고, 프로필 이름을 "contosouniversity.com-웹 배포"에서 "Production"로 바꿉니다.

게시 프로필을 닫아 변경 내용을 저장 한 다음 다시 엽니다.

**게시**를 클릭합니다. 실제 프로덕션 웹 사이트의 경우에는 *응용 프로그램\_오프 라인* 으로 복사 하 고 게시 하기 전에 프로젝트 폴더에 넣은 다음 배포가 완료 되 면 제거 합니다.

Visual Studio는 테스트 환경에 코드 변경 내용을 배포 하 고 브라우저를 Contoso 대학 홈 페이지로 엽니다.

강사 페이지를 선택 합니다.

Code First 마이그레이션는 테스트 환경에서와 동일한 방식으로 데이터베이스를 업데이트 합니다. 시드 된 데이터와 함께 새 Office 시간 열이 표시 됩니다.

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

이제 SQL Server 데이터베이스를 사용 하 여 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트를 성공적으로 배포 했습니다.

## <a name="more-information"></a>자세한 내용

이는 ASP.NET 웹 응용 프로그램을 타사 호스팅 공급자에 배포 하는 방법에 대 한 자습서 시리즈를 완료 합니다. 이러한 자습서에서 설명 하는 항목에 대 한 자세한 내용은 MSDN 웹 사이트에서 [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) 을 참조 하십시오.

## <a name="acknowledgements"></a>승인

이 자습서 시리즈의 내용에 대해 상당한 기여를 수행한 다음 사용자에 게 감사 합니다.

- [Alberto Poblacion, MVP &amp; MCT, 스페인](https://mvp.support.microsoft.com/profile/Alberto)
- Jarod Ferguson, Data Platform Development MVP, 미국
- Microsoft의 거칠게 Mittal
- [Kristina Olson, Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope, Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava, Microsoft
- [Raffaele Rialdi, 이탈리아](http://www.iamraf.net/)
- [Rick Anderson, Microsoft](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))
- [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))
- [Scott 헌터, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))
- [Srđan Božović, 세르비아](http://msforge.net/blogs/zmajcek/)
- [인 vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [다음](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)
