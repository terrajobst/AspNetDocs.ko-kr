---
uid: web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 배포 준비 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ae4def81-fa37-4883-a13e-d9896cbf6c36
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
msc.type: authoredcontent
ms.openlocfilehash: cdcb3578725c41e3c801afd54e6d34455bc4b281
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618526"
---
# <a name="aspnet-web-deployment-using-visual-studio-preparing-for-database-deployment"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 데이터베이스 배포 준비

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다. 계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.

## <a name="overview"></a>개요

이 자습서에서는 데이터베이스 배포를 위해 프로젝트를 준비 하는 방법을 보여 줍니다. 응용 프로그램의 두 데이터베이스에 있는 데이터베이스 구조와 일부 (모두 아님)는 테스트, 준비 및 프로덕션 환경에 배포 되어야 합니다.

일반적으로 응용 프로그램을 개발할 때 라이브 사이트에 배포 하지 않을 데이터베이스에 테스트 데이터를 입력 합니다. 그러나 배포 하려는 일부 프로덕션 데이터도 있을 수 있습니다. 이 자습서에서는를 배포할 때 올바른 데이터가 포함 되도록 Contoso 대학 프로젝트를 구성 하 고 SQL 스크립트를 준비 합니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](troubleshooting.md)를 확인 해야 합니다.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

샘플 응용 프로그램은 SQL Server Express LocalDB를 사용 합니다. SQL Server Express은 SQL Server의 무료 버전입니다. 이는 SQL Server의 전체 버전과 동일한 데이터베이스 엔진을 기반으로 하기 때문에 일반적으로 개발 중에 사용 됩니다. SQL Server Express를 사용 하 여 테스트 하 고 응용 프로그램이 프로덕션에서 동일 하 게 동작 하 게 할 수 있으며 SQL Server 버전에 따라 달라 지는 기능에 대 한 몇 가지 예외가 있습니다.

LocalDB는 데이터베이스를 *.mdf* 파일로 사용할 수 있도록 하는 SQL Server Express의 특수 실행 모드입니다. 일반적으로 LocalDB 데이터베이스 파일은 웹 프로젝트의 *App\_Data* 폴더에 저장 됩니다. SQL Server Express의 사용자 인스턴스 기능을 사용 하면 *.mdf* 파일을 사용할 수도 있지만 사용자 인스턴스 기능은 사용 되지 않습니다. 따라서 *.mdf* 파일을 사용 하는 경우에는 LocalDB를 사용 하는 것이 좋습니다.

일반적으로 SQL Server Express는 프로덕션 웹 응용 프로그램에 사용 되지 않습니다. 특히 LocalDB는 IIS에서 작동 하도록 설계 되지 않았기 때문에 웹 응용 프로그램에서 프로덕션 용도로 사용 하지 않는 것이 좋습니다.

Visual Studio 2012에서 LocalDB는 기본적으로 Visual Studio와 함께 설치 됩니다. Visual Studio 2010 이전 버전에서는 SQL Server Express (LocalDB 제외)가 Visual Studio에서 기본적으로 설치 됩니다. [이는이 시리즈의 첫 번째 자습서](introduction.md)에 있는 필수 구성 요소 중 하나로 설치 하는 이유입니다.

LocalDB를 비롯 한 SQL Server 버전에 대 한 자세한 내용은 다음 리소스 [SQL Server 데이터베이스 작업](../../../../whitepapers/aspnet-data-access-content-map.md#sqlserver)을 참조 하세요.

## <a name="entity-framework-and-universal-providers"></a>Entity Framework 및 Universal Providers

데이터베이스 액세스의 경우 Contoso 대학 응용 프로그램은 .NET Framework에 포함 되지 않으므로 응용 프로그램과 함께 배포 해야 하는 다음과 같은 소프트웨어가 필요 합니다.

- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (ASP.NET 멤버 자격 시스템에서 Azure SQL Database를 사용할 수 있도록 설정)
- [Entity Framework](https://msdn.microsoft.com/library/gg696172.aspx)

이 소프트웨어는 NuGet 패키지에 포함 되어 있으므로 프로젝트를 사용 하 여 필수 어셈블리를 배포 하도록 프로젝트를 이미 설정 했습니다. (이 링크는 이러한 패키지의 최신 버전을 가리키기 때문에이 자습서에 대해 다운로드 한 시작 프로젝트에 설치 된 것 보다 최신 버전 일 수 있습니다.)

Azure 대신 타사 호스팅 공급자에 배포 하는 경우 Entity Framework 5.0 이상을 사용 해야 합니다. 이전 버전의 Code First 마이그레이션에는 완전 신뢰가 필요 하며 대부분의 호스팅 공급자는 보통 신뢰 수준으로 응용 프로그램을 실행 합니다. 보통 신뢰에 대 한 자세한 내용은 [테스트 환경으로 IIS에 배포](deploying-to-iis.md) 자습서를 참조 하세요.

## <a name="configure-code-first-migrations-for-application-database-deployment"></a>응용 프로그램 데이터베이스 배포를 위한 Code First 마이그레이션 구성

Contoso 대학 응용 프로그램 데이터베이스는 Code First에 의해 관리 되며 Code First 마이그레이션를 사용 하 여 배포할 수 있습니다. Code First 마이그레이션를 사용 하 여 데이터베이스를 배포 하는 방법에 대 한 개요는 [이 시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.

응용 프로그램 데이터베이스를 배포 하는 경우 일반적으로 해당 데이터의 대부분이 테스트 목적 으로만 제공 되므로 프로덕션 환경에 모든 데이터를 포함 하는 개발 데이터베이스를 배포 하는 것은 간단 하지 않습니다. 예를 들어 테스트 데이터베이스의 학생 이름은 가상입니다. 반면에 데이터 없이 데이터베이스 구조만 배포할 수 없는 경우가 종종 있습니다. 테스트 데이터베이스의 일부 데이터는 실제 데이터가 될 수 있으며 사용자가 응용 프로그램을 사용 하기 시작할 때이 데이터를 사용 해야 합니다. 예를 들어 데이터베이스에 유효한 등급 값 또는 실제 부서 이름이 포함 된 테이블이 있을 수 있습니다.

이 일반적인 시나리오를 시뮬레이션 하기 위해 프로덕션에 있는 데이터만 데이터베이스에 삽입 하는 Code First 마이그레이션 `Seed` 메서드를 구성 합니다. 이 `Seed` 메서드는 Code First 프로덕션 환경에서 데이터베이스를 만든 후 프로덕션 환경에서 실행 되므로 테스트 데이터를 삽입 해서는 안 됩니다.

이전 버전의 Code First 마이그레이션이 출시 되기 전에는 개발 중에 모든 모델이 변경 되는 경우 데이터베이스를 완전히 삭제 하 고 처음부터 다시 만들어야 하기 때문에 `Seed` 메서드가 테스트 데이터를 삽입 하는 것이 일반적 이었습니다. Code First 마이그레이션를 사용 하면 데이터베이스 변경 후에 테스트 데이터가 유지 되므로 `Seed` 메서드에 테스트 데이터를 포함 하는 것은 필요 하지 않습니다. 다운로드 한 프로젝트는 이니셜라이저 클래스의 `Seed` 메서드에 모든 데이터를 포함 하는 메서드를 사용 합니다. 이 자습서에서는 해당 이니셜라이저 클래스를 사용 하지 않도록 설정 하 고 마이그레이션을 사용 하도록 설정 합니다. 그런 다음, 프로덕션 환경에 삽입 하려는 데이터만 삽입 하도록 마이그레이션 구성 클래스에서 `Seed` 메서드를 업데이트 합니다.

다음 다이어그램은 응용 프로그램 데이터베이스의 스키마를 보여 줍니다.

[![School_database_diagram](preparing-databases/_static/image2.png)](preparing-databases/_static/image1.png)

이러한 자습서에서는 사이트가 처음 배포 될 때 `Student` 및 `Enrollment` 테이블이 비어 있는 것으로 가정 합니다. 다른 테이블에는 응용 프로그램이 라이브 상태로 전환 될 때 미리 로드 해야 하는 데이터가 포함 되어 있습니다.

### <a name="disable-the-initializer"></a>이니셜라이저 사용 안 함

Code First 마이그레이션를 사용할 예정 이므로 `DropCreateDatabaseIfModelChanges` Code First 이니셜라이저를 사용할 필요가 없습니다. 이 이니셜라이저의 코드는 ContosoUniversity 프로젝트의 *SchoolInitializer.cs* 파일에 있습니다. *Web.config 파일의* `appSettings` 요소에 설정 하면 응용 프로그램에서 데이터베이스에 처음으로 액세스 하려고 할 때마다이 이니셜라이저가 실행 됩니다.

[!code-xml[Main](preparing-databases/samples/sample1.xml?highlight=3)]

응용 프로그램 *web.config* 파일을 열고 Code First 이니셜라이저 클래스를 지정 하는 `add` 요소를 제거 하거나 주석으로 처리 합니다. 이제 `appSettings` 요소는 다음과 같습니다.

[!code-xml[Main](preparing-databases/samples/sample2.xml)]

> [!NOTE]
> 이니셜라이저 클래스를 지정 하는 또 다른 방법은 *global.asax* 파일의 `Application_Start` 메서드에서 `Database.SetInitializer`를 호출 하는 것입니다. 해당 메서드를 사용 하 여 이니셜라이저를 지정 하는 프로젝트에서 마이그레이션을 사용 하도록 설정 하는 경우 해당 코드 줄을 제거 합니다.

> [!NOTE]
> Visual Studio 2013를 사용 하는 경우 2 단계와 3 단계 사이에 다음 단계를 추가 합니다. (a) PMC에서 "업데이트-패키지 entityframework-버전 6.1.1"을 입력 하 여 EF의 현재 버전을 가져옵니다. 그런 다음 (b) 프로젝트를 빌드하여 빌드 오류 목록을 가져온 다음 수정 합니다. 더 이상 존재 하지 않는 네임 스페이스에 대 한 using 문을 사용 하 여 삭제 하 고 마우스 오른쪽 단추를 클릭 한 다음 확인을 클릭 하 여 필요한 위치에 사용 문을 추가 하 고 EntityState의 발생을 EntityState로 변경 합니다.

### <a name="enable-code-first-migrations"></a>Code First 마이그레이션 사용

1. ContosoUniversity 프로젝트 (ContosoUniversity)가 시작 프로젝트로 설정 되어 있는지 확인 합니다. **솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트로 설정**을 선택 합니다. Code First 마이그레이션는 시작 프로젝트에서 데이터베이스 연결 문자열을 찾습니다.
2. **도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택 합니다.

    ![Selecting_Package_Manager_Console](preparing-databases/_static/image3.png)
3. **패키지 관리자 콘솔** 창의 맨 위에 있는 ContosoUniversity를 기본 프로젝트로 선택 하 고 `PM>` 프롬프트에서 "마이그레이션 사용"을 입력 합니다.

    ![사용-마이그레이션 명령](preparing-databases/_static/image4.png)

    ( *마이그레이션 사용* 안 함 명령이 인식 되지 않는다는 오류 메시지가 표시 되 면 *업데이트 패키지 Entityframework-Reinstall* 명령을 입력 한 후 다시 시도 하세요.)

    이 명령은 ContosoUniversity 프로젝트에 *migration 폴더를* 만들고,이 폴더에는 마이그레이션을 구성 하는 데 사용할 수 있는 *Configuration.cs* 파일과 데이터베이스를 만드는 첫 번째 마이그레이션의 *InitialCreate.cs* 파일이 있습니다.

    ![마이그레이션 폴더](preparing-databases/_static/image5.png)

    Code First 컨텍스트 클래스가 포함 된 프로젝트에서 `enable-migrations` 명령을 실행 해야 하므로 **패키지 관리자 콘솔** 의 **기본 프로젝트** 드롭다운 목록에서 DAL 프로젝트를 선택 했습니다. 클래스가 클래스 라이브러리 프로젝트에 있는 경우 솔루션에 대 한 시작 프로젝트에서 데이터베이스 연결 문자열을 찾습니다 Code First 마이그레이션. ContosoUniversity 솔루션에서 웹 프로젝트는 시작 프로젝트로 설정 되었습니다. Visual Studio에서 연결 문자열을 포함 하는 프로젝트를 시작 프로젝트로 지정 하지 않으려는 경우 PowerShell 명령에서 시작 프로젝트를 지정할 수 있습니다. 명령 구문을 보려면 `get-help enable-migrations`명령을 입력 합니다.

    데이터베이스가 이미 있기 때문에 `enable-migrations` 명령은 첫 번째 마이그레이션을 자동으로 만들었습니다. 다른 방법은 마이그레이션을 통해 데이터베이스를 만드는 것입니다. 이렇게 하려면 마이그레이션을 사용 하도록 설정 하기 전에 **서버 탐색기** 또는 **SQL Server 개체 탐색기** 를 사용 하 여 ContosoUniversity 데이터베이스를 삭제 합니다. 마이그레이션을 사용 하도록 설정한 후 "추가 마이그레이션 InitialCreate" 명령을 입력 하 여 첫 번째 마이그레이션을 수동으로 만듭니다. 그런 다음 "업데이트-데이터베이스" 명령을 입력 하 여 데이터베이스를 만들 수 있습니다.

### <a name="set-up-the-seed-method"></a>초기값 설정

이 자습서에서는 Code First 마이그레이션 `Configuration` 클래스의 `Seed` 메서드에 코드를 추가 하 여 고정 데이터를 추가 합니다. Code First 마이그레이션는 마이그레이션 때마다 `Seed` 메서드를 호출 합니다.

`Seed` 메서드는 마이그레이션 때마다 실행 되기 때문에 첫 번째 마이그레이션 후 테이블에 이미 데이터가 있습니다. 이러한 상황을 처리 하려면 `AddOrUpdate` 메서드를 사용 하 여 이미 삽입 된 행을 업데이트 하거나 아직 존재 하지 않는 경우 삽입 합니다. `AddOrUpdate` 방법이 시나리오에 가장 적합 한 선택이 아닐 수 있습니다. 자세한 내용은 Julie Lerman의 블로그에서 [EF 4.3 AddOrUpdate 메서드를 사용 하 여 처리](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) 를 참조 하세요.

1. *Configuration.cs* 파일을 열고 `Seed` 메서드의 주석을 다음 코드로 바꿉니다.

    [!code-csharp[Main](preparing-databases/samples/sample3.cs)]
2. 네임 스페이스에 대 한 `using` 문이 아직 없기 때문에 `List`에 대 한 참조에는 빨간색 물결선이 있습니다. `List` 인스턴스 중 하나를 마우스 오른쪽 단추로 클릭 하 고 **해결**을 클릭 한 다음, **Collections 사용**을 클릭 합니다.

    ![Using 문을 사용 하 여 확인](preparing-databases/_static/image6.png)

    이 메뉴를 선택 하면 파일 위쪽 근처의 `using` 문에 다음 코드가 추가 됩니다.

    [!code-csharp[Main](preparing-databases/samples/sample4.cs)]
3. CTRL + SHIFT + B를 눌러 프로젝트를 빌드합니다.

이제 프로젝트에서 *ContosoUniversity* 데이터베이스를 배포할 준비가 되었습니다. 응용 프로그램을 배포한 후 처음 실행 하 고 데이터베이스에 액세스 하는 페이지로 이동 하면 Code First는 데이터베이스를 만들고이 `Seed` 메서드를 실행 합니다.

> [!NOTE]
> `Seed` 메서드에 코드를 추가 하는 것은 데이터베이스에 고정 데이터를 삽입할 수 있는 여러 가지 방법 중 하나입니다. 다른 방법은 각 마이그레이션 클래스의 `Up` 및 `Down` 메서드에 코드를 추가 하는 것입니다. `Up` 및 `Down` 메서드에는 데이터베이스 변경 내용을 구현 하는 코드가 포함 되어 있습니다. [데이터베이스 업데이트 배포](deploying-a-database-update.md) 자습서에서 예제를 볼 수 있습니다.
> 
> `Sql` 메서드를 사용 하 여 SQL 문을 실행 하는 코드를 작성할 수도 있습니다. 예를 들어 예산 열을 부서 테이블에 추가 하 고 마이그레이션의 일부로 모든 부서 예산을 $1000.00로 초기화 하려는 경우 해당 마이그레이션의 `Up` 메서드에 다음 코드 줄을 추가할 수 있습니다.
> 
> `Sql("UPDATE Department SET Budget = 1000");`

## <a name="create-scripts-for-membership-database-deployment"></a>멤버 자격 데이터베이스 배포를 위한 스크립트 만들기

Contoso 대학 응용 프로그램은 ASP.NET 멤버 자격 시스템 및 폼 인증을 사용 하 여 사용자를 인증 하 고 권한을 부여 합니다. **크레딧 업데이트** 페이지는 관리자 역할에 속한 사용자만 액세스할 수 있습니다.

응용 프로그램을 실행 하 고 **강좌**를 클릭 한 다음 **크레딧 업데이트**를 클릭 합니다.

![크레딧 업데이트를 클릭 합니다.](preparing-databases/_static/image7.png)

**업데이트 크레딧을** 페이지에 관리 권한이 필요 하기 때문에 **로그인** 페이지가 표시 됩니다.

사용자 이름으로 *admin* 을 입력 하 고 암호로 *devpwd* 를 입력 하 고 **로그인**을 클릭 합니다.

![로그인 페이지](preparing-databases/_static/image8.png)

**크레딧 업데이트** 페이지가 나타납니다.

![크레딧 업데이트 페이지](preparing-databases/_static/image9.png)

사용자 및 역할 정보는 *web.config* 파일의 **defaultconnection** 연결 문자열에 지정 된 *aspnet-ContosoUniversity* 데이터베이스에 있습니다.

이 데이터베이스는 Entity Framework Code First에서 관리 되지 않으므로 마이그레이션을 사용 하 여 배포할 수 없습니다. DbDacFx 공급자를 사용 하 여 데이터베이스 스키마를 배포 하 고, 게시 프로필을 구성 하 여 초기 데이터를 데이터베이스 테이블에 삽입 하는 스크립트를 실행 합니다.

> [!NOTE]
> 새 ASP.NET 멤버 자격 시스템 (현재 ASP.NET Identity 이름)이 Visual Studio 2013에 도입 되었습니다. 새 시스템을 사용 하면 응용 프로그램 및 멤버 자격 테이블을 모두 같은 데이터베이스에 유지할 수 있으며 Code First 마이그레이션를 사용 하 여 둘 다 배포할 수 있습니다. 이 샘플 응용 프로그램은 Code First 마이그레이션를 사용 하 여 배포할 수 없는 이전 ASP.NET 멤버 자격 시스템을 사용 합니다. 이 멤버 자격 데이터베이스를 배포 하는 절차는 응용 프로그램이 Entity Framework Code First에서 생성 되지 않은 SQL Server 데이터베이스를 배포 해야 하는 다른 모든 시나리오에도 적용 됩니다.

또한 일반적으로 개발 중인 프로덕션에서 동일한 데이터를 원하지 않습니다. 처음으로 사이트를 배포 하는 경우 테스트를 위해 만든 사용자 계정을 대부분 또는 모두 제외 하는 것이 일반적입니다. 따라서 다운로드 한 프로젝트에는 두 개의 멤버 자격 데이터베이스인 *aspnet-ContosoUniversity* development users와 *aspnet-ContosoUniversity-Prod* 가 있습니다. 이 자습서의 경우 사용자 이름은 두 데이터베이스 ( *admin* 및 *nonadmin*)에서 동일 합니다. 두 사용자 모두 개발 데이터베이스의 암호 *devpwd* 와 프로덕션 데이터베이스의 *prodpwd* 을 갖습니다.

개발 사용자를 테스트 환경에 배포 하 고 프로덕션 사용자를 스테이징 및 프로덕션에 배포 합니다. 이 작업을 수행 하려면이 자습서에서 개발 및 프로덕션용으로 두 개의 SQL 스크립트를 만들고 나중에 자습서에서는 게시 프로세스를 실행 하도록 구성 합니다.

> [!NOTE]
> 멤버 자격 데이터베이스는 계정 암호의 해시를 저장 합니다. 한 컴퓨터에서 다른 컴퓨터로 계정을 배포 하려면 해싱 루틴이 원본 컴퓨터에서 수행 하는 것과 다른 해시를 대상 서버에서 생성 하지 않도록 해야 합니다. 기본 알고리즘을 변경 하지 않는 한 ASP.NET Universal Providers 사용할 때 동일한 해시가 생성 됩니다. 기본 알고리즘은 HMACSHA256 이며 web.config 파일에 있는 **[machineKey](https://msdn.microsoft.com/library/system.web.configuration.machinekeysection.aspx)** 요소의 **validation** 특성에 지정 됩니다.

SSMS (SQL Server Management Studio)를 사용 하거나 타사 도구를 사용 하 여 데이터 배포 스크립트를 수동으로 만들 수 있습니다. 이 자습서의 나머지 부분에서는 SSMS에서이 작업을 수행 하는 방법을 보여 주지만 SSMS를 설치 하 고 사용 하지 않으려는 경우 프로젝트의 완료 된 버전에서 스크립트를 가져와 솔루션 폴더에 저장 하는 섹션으로 건너뛸 수 있습니다.

SSMS를 설치 하려면 [다운로드 센터: Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062) 에서 [ENU\x64\SQLManagementStudio\_x64\_enu](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLManagementStudio_x64_ENU.exe) 또는 [ENU\x86\SQLManagementStudio\_x86\_ENU](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLManagementStudio_x86_ENU.exe)를 클릭 하 여 설치 합니다. 시스템에 대해 잘못 된 항목을 선택 하는 경우 설치에 실패 하 고 다른 항목을 사용해 볼 수 있습니다.

(600 메가바이트 다운로드입니다. 설치 하는 데 시간이 오래 걸릴 수 있으며 컴퓨터를 다시 부팅 해야 합니다.

SQL Server 설치 센터의 첫 페이지에서 **새로 만들기 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 클릭 하 고 지침에 따라 기본 선택 항목을 적용 합니다.

### <a name="create-the-development-database-script"></a>개발 데이터베이스 스크립트 만들기

1. SSMS를 실행 합니다.
2. **서버에 연결** 대화 상자에서 **서버 이름**으로 *(localdb) \v11.0* 을 입력 하 고 **인증** 을 **Windows 인증**으로 유지 한 다음 **연결**을 클릭 합니다.

    ![SSMS 서버에 연결](preparing-databases/_static/image10.png)
3. **개체 탐색기** 창에서 **데이터베이스**를 확장 하 고 **ContosoUniversity**를 마우스 오른쪽 단추로 클릭 한 다음 **태스크**, **스크립트 생성**을 차례로 클릭 합니다.

    ![SSMS에서 스크립트 생성](preparing-databases/_static/image11.png)
4. **스크립트 생성 및 게시** 대화 상자에서 **스크립팅 옵션 설정**을 클릭 합니다.

    기본값은 **스크립트 전체 데이터베이스 및 모든 데이터베이스 개체** 이며 원하는 것 이므로 **개체 선택** 단계를 건너뛸 수 있습니다.
5. **고급**을 클릭합니다.

    ![SSMS 스크립팅 옵션](preparing-databases/_static/image12.png)
6. **고급 스크립팅 옵션** 대화 상자에서 **스크립팅할 데이터 형식**으로 스크롤하고 드롭다운 목록 **에서 데이터만 (데이터만) 옵션을** 클릭 합니다.
7. **스크립트 사용 데이터베이스** 를 **False**로 변경 합니다. USE 문은 Azure SQL Database에 유효 하지 않으며 테스트 환경에서 SQL Server Express에 배포 하는 데 필요 하지 않습니다.

    ![SSMS 스크립트 데이터만, USE 문 없음](preparing-databases/_static/image13.png)
8. **확인**을 클릭합니다.
9. **스크립트 생성 및 게시** 대화 상자에서 **파일 이름** 상자에 스크립트를 만들 위치를 지정 합니다. 솔루션 폴더 (ContosoUniversity 파일이 있는 폴더)의 경로와 파일 이름을 *aspnet-data-dev*로 변경 합니다.
10. **다음** 을 클릭 하 여 **요약** 탭으로 이동한 후 다시 **다음** 을 클릭 하 여 스크립트를 만듭니다.

    ![SSMS 스크립트를 만듦](preparing-databases/_static/image14.png)
11. **마침**을 클릭합니다.

### <a name="create-the-production-database-script"></a>프로덕션 데이터베이스 스크립트 만들기

프로덕션 데이터베이스를 사용 하 여 프로젝트를 실행 하지 않았기 때문에 아직 LocalDB 인스턴스에 연결 되지 않습니다. 따라서 먼저 데이터베이스를 연결 해야 합니다.

1. SSMS **개체 탐색기**에서 **데이터베이스** 를 마우스 오른쪽 단추로 클릭 하 고 **연결**을 클릭 합니다.

    ![SSMS 연결](preparing-databases/_static/image15.png)
2. **데이터베이스 연결** 대화 상자에서 **추가** 를 클릭 한 다음 *App\_Data* 폴더의 *aspnet-ContosoUniversity-Prod* 파일로 이동 합니다.

     ![SSMS 연결할 .mdf 파일을 추가 합니다.](preparing-databases/_static/image16.png)
3. **확인**을 클릭합니다.
4. 이전에 사용 했던 것과 동일한 절차에 따라 프로덕션 파일에 대 한 스크립트를 만듭니다. 스크립트 파일의 이름을 *aspnet-data-prod*로 합니다.

## <a name="summary"></a>요약

이제 두 데이터베이스를 배포할 준비가 되었으며 솔루션 폴더에 두 개의 데이터 배포 스크립트가 있습니다.

![데이터 배포 스크립트](preparing-databases/_static/image17.png)

다음 자습서에서는 배포에 영향을 주는 프로젝트 설정을 구성 하 고 배포 된 응용 프로그램에서 다른 설정에 *대해 자동 web.config* 파일 변환을 설정 합니다.

## <a name="more-information"></a>자세한 내용

NuGet에 대 한 자세한 내용은 nuget 및 Nuget을 [사용 하 여 프로젝트 라이브러리 관리](https://msdn.microsoft.com/magazine/hh547106.aspx) [설명서](http://docs.nuget.org/docs/start-here/overview)를 참조 하세요. NuGet을 사용 하지 않으려면 NuGet 패키지를 분석 하 여 설치 시 수행 되는 작업을 확인 하는 방법을 알아야 합니다. 예를 들어 *web.config* 변환을 구성 하 고 빌드 시에 실행 되도록 PowerShell 스크립트를 구성할 수 있습니다. NuGet의 작동 방식에 대해 자세히 알아보려면 [패키지 만들기 및 게시](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) 및 [구성 파일 및 소스 코드 변환](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)을 참조 하세요.

> [!div class="step-by-step"]
> [이전](introduction.md)
> [다음](web-config-transformations.md)
