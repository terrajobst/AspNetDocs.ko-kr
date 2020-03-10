---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
title: 'Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server Compact 데이터베이스 배포-2/12 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: c3c76516-4c48-4153-bd03-d70e3a3edbb0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
msc.type: authoredcontent
ms.openlocfilehash: 56ceabc79947967846d342354fd033510be5f05a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458255"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-sql-server-compact-databases---2-of-12"></a>Visual Studio 또는 Visual Web Developer를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server Compact 데이터베이스 배포-2/12

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다. 시리즈에 대 한 소개는 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하십시오.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.

## <a name="overview"></a>개요

이 자습서에서는 배포를 위해 두 개의 SQL Server Compact 데이터베이스와 데이터베이스 엔진을 설정 하는 방법을 보여 줍니다.

데이터베이스 액세스의 경우 Contoso 대학 응용 프로그램은 .NET Framework에 포함 되지 않으므로 응용 프로그램과 함께 배포 해야 하는 다음과 같은 소프트웨어가 필요 합니다.

- [SQL Server Compact](https://www.microsoft.com/sqlserver/en/us/editions/compact.aspx) (데이터베이스 엔진)
- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) (ASP.NET 멤버 자격 시스템에서 SQL Server Compact를 사용할 수 있도록 함)
- [Entity Framework 5.0](https://msdn.microsoft.com/library/gg696172(d=lightweight,v=vs.103).aspx)(마이그레이션과 Code First).

데이터베이스 구조와 응용 프로그램의 두 데이터베이스에 있는 데이터 중 일부 (모두 아님)도 배포 되어야 합니다. 일반적으로 응용 프로그램을 개발할 때 라이브 사이트에 배포 하지 않을 데이터베이스에 테스트 데이터를 입력 합니다. 그러나 배포 하려는 일부 프로덕션 데이터를 입력할 수도 있습니다. 이 자습서에서는를 배포할 때 필요한 소프트웨어와 올바른 데이터가 포함 되도록 Contoso 대학 프로젝트를 구성 합니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)를 확인 해야 합니다.

## <a name="sql-server-compact-versus-sql-server-express"></a>SQL Server Compact 대 SQL Server Express

샘플 응용 프로그램은 SQL Server Compact 4.0를 사용 합니다. 이 데이터베이스 엔진은 웹 사이트에 대 한 비교적 새로운 옵션입니다. 이전 버전의 SQL Server Compact는 웹 호스팅 환경에서 작동 하지 않습니다. SQL Server Compact은 SQL Server Express를 사용 하 여 개발 하 고 전체 SQL Server에 배포 하는 보다 일반적인 시나리오에 비해 몇 가지 이점을 제공 합니다. 선택한 호스팅 공급자에 따라 일부 공급자는 전체 SQL Server 데이터베이스를 지원 하기 위해 추가 비용을 부과 하므로 배포 비용이 더 적게 SQL Server Compact. 웹 응용 프로그램의 일부로 데이터베이스 엔진 자체를 배포할 수 있으므로 SQL Server Compact에 대 한 추가 요금이 부과 되지 않습니다.

그러나 이러한 제한 사항에 대해서도 알고 있어야 합니다. SQL Server Compact는 저장 프로시저, 트리거, 뷰 또는 복제를 지원 하지 않습니다. SQL Server Compact에서 지원 하지 않는 SQL Server 기능의 전체 목록은 [SQL Server Compact와 SQL Server의 차이점](https://msdn.microsoft.com/library/bb896140.aspx)을 참조 하세요.) 또한 SQL Server Express 및 SQL Server 데이터베이스에서 스키마 및 데이터를 조작 하는 데 사용할 수 있는 일부 도구는 SQL Server Compact에서 작동 하지 않습니다. 예를 들어 Visual Studio의 SQL Server Compact 데이터베이스에서 SQL Server Management Studio 또는 SQL Server Data Tools를 사용할 수 없습니다. SQL Server Compact 데이터베이스를 사용 하기 위한 다른 옵션이 있습니다.

- SQL Server Compact에 대해 제한 된 데이터베이스 조작 기능을 제공 하는 Visual Studio에서 서버 탐색기를 사용할 수 있습니다.
- 서버 탐색기 보다 많은 기능을 포함 하는 [WebMatrix](https://www.microsoft.com/web/webmatrix/)의 데이터베이스 조작 기능을 사용할 수 있습니다.
- [SQL Server Compact 도구 상자](https://github.com/ErikEJ/SqlCeToolbox) 및 [SQL Compact 데이터 및 스키마 스크립트 유틸리티](https://github.com/ErikEJ/SqlCeToolbox)와 같은 비교적 완전 한 기능의 타사 또는 오픈 소스 도구를 사용할 수 있습니다.
- 고유한 DDL (데이터 정의 언어) 스크립트를 작성 하 고 실행 하 여 데이터베이스 스키마를 조작할 수 있습니다.

SQL Server Compact 시작 하 고 필요에 따라 나중에 업그레이드할 수 있습니다. 이 시리즈의 이후 자습서에서는 SQL Server Compact에서 SQL Server Express으로, SQL Server으로 마이그레이션하는 방법을 보여 줍니다. 그러나 새 응용 프로그램을 만들고 가까운 장래에 SQL Server 필요할 것으로 생각 되는 경우 SQL Server 또는 SQL Server Express으로 시작 하는 것이 가장 좋습니다.

## <a name="configuring-the-sql-server-compact-database-engine-for-deployment"></a>배포용 SQL Server Compact 데이터베이스 엔진 구성

다음 NuGet 패키지를 설치 하 여 Contoso 대학 응용 프로그램의 데이터 액세스에 필요한 소프트웨어를 추가 했습니다.

- [SqlServerCompact](http://nuget.org/List/Packages/SqlServerCompact)
- [System.web. 공급자](http://nuget.org/List/Packages/System.Web.Providers) (ASP.NET 유니버설 공급자)
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework)
- [EntityFramework. SqlServerCompact](http://nuget.org/List/Packages/EntityFramework.sqlservercompact)

링크는 이러한 패키지의 최신 버전을 가리키기 때문에이 자습서에서 다운로드 한 시작 프로젝트에 설치 된 것 보다 최신 버전 일 수 있습니다. 호스팅 공급자에 배포 하려면 Entity Framework 5.0 이상을 사용 해야 합니다. 이전 버전의 Code First 마이그레이션에는 완전 신뢰가 필요 하며, 대부분의 호스팅 공급자에서 응용 프로그램은 보통 신뢰 수준으로 실행 됩니다. 보통 신뢰에 대 한 자세한 내용은 [테스트 환경으로 IIS에 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서를 참조 하세요.

NuGet 패키지 설치는 일반적으로 응용 프로그램과 함께이 소프트웨어를 배포 하기 위해 필요한 모든 항목을 처리 합니다. 일부 경우에는 Web.config 파일을 변경 하 고 솔루션을 빌드할 때마다 실행 되는 PowerShell 스크립트를 추가 하는 등의 작업이 포함 됩니다. **NuGet을 사용 하지 않고 이러한 기능 (예: SQL Server Compact 및 Entity Framework)에 대 한 지원을 추가 하려는 경우 동일한 작업을 수동으로 수행할 수 있도록 NuGet 패키지 설치를 확인 해야 합니다.**

성공적인 배포를 위해 NuGet에서 수행 해야 하는 모든 작업을 수행 해야 하는 한 가지 예외가 있습니다. SqlServerCompact NuGet 패키지는 프로젝트 *bin* 폴더의 *x86* 및 *amd64* 하위 폴더에 네이티브 어셈블리를 복사 하는 빌드 후 스크립트를 프로젝트에 추가 하지만 스크립트는 프로젝트에 이러한 폴더를 포함 하지 않습니다. 따라서 프로젝트에 수동으로 포함 하지 않는 한 웹 배포는 대상 웹 사이트에 해당 파일을 복사 하지 않습니다. 이 동작은 기본 배포 구성으로 인해 발생 합니다. 이러한 자습서에서 사용 하지 않는 또 다른 옵션은이 동작을 제어 하는 설정을 변경 하는 것입니다. 변경할 수 있는 설정은 **프로젝트 속성** 창의 **웹 패키지 및 게시** 탭에 있는 **배포할 항목** 에서 **응용 프로그램을 실행 하는 데 필요한 파일** 입니다. 이 설정을 변경 하는 것은 필요한 것 보다 많은 파일을 프로덕션 환경에 배포할 수 있기 때문에 일반적으로 권장 되지 않습니다. 대안에 대 한 자세한 내용은 [프로젝트 속성 구성](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md) 자습서를 참조 하세요.

프로젝트를 빌드한 다음 **솔루션 탐색기** **모든 파일 표시** 를 클릭 합니다 (아직 수행 하지 않은 경우). **새로 고침**을 클릭 해야 할 수도 있습니다.

![Solution_Explorer_Show_All_Files](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image1.png)

**Bin** 폴더를 확장 하 여 **amd64** 및 **x86** 폴더를 표시 한 다음 해당 폴더를 선택 하 고 마우스 오른쪽 단추를 클릭 한 다음 **프로젝트에 포함**을 선택 합니다.

![amd64_and_x86_in_Solution_Explorer.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image2.png)

폴더 아이콘이 프로젝트에 포함 되어 있음을 표시 하도록 변경 됩니다.

![Solution_Explorer_amd64_included.png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image3.png)

## <a name="configuring-code-first-migrations-for-application-database-deployment"></a>응용 프로그램 데이터베이스 배포를 위한 Code First 마이그레이션 구성

응용 프로그램 데이터베이스를 배포 하는 경우 일반적으로 해당 데이터의 대부분이 테스트 목적 으로만 제공 되므로 프로덕션 환경에 모든 데이터를 포함 하는 개발 데이터베이스를 배포 하는 것은 간단 하지 않습니다. 예를 들어 테스트 데이터베이스의 학생 이름은 가상입니다. 반면에 데이터 없이 데이터베이스 구조만 배포할 수 없는 경우가 종종 있습니다. 테스트 데이터베이스의 일부 데이터는 실제 데이터가 될 수 있으며 사용자가 응용 프로그램을 사용 하기 시작할 때이 데이터를 사용 해야 합니다. 예를 들어 데이터베이스에 유효한 등급 값 또는 실제 부서 이름이 포함 된 테이블이 있을 수 있습니다.

이 일반적인 시나리오를 시뮬레이션 하기 위해 프로덕션에 있는 데이터만 데이터베이스에 삽입 하는 Code First 마이그레이션 초기값 메서드를 구성 합니다. 이 초기값 메서드는 프로덕션 환경에서 데이터베이스를 Code First 만든 후 프로덕션 환경에서 실행 되므로 테스트 데이터를 삽입 하지 않습니다.

이전 버전의 Code First 마이그레이션이 출시 되기 전에는 테스트 데이터를 삽입 하는 시드 방법이 일반적 이었습니다. 개발 중에 모든 모델이 변경 되 면 데이터베이스를 완전히 삭제 하 고 처음부터 다시 만들어야 하기 때문입니다. Code First 마이그레이션를 사용 하면 데이터베이스 변경 후에 테스트 데이터가 유지 되므로 시드 메서드에 테스트 데이터를 포함 하는 것은 필요 하지 않습니다. 다운로드 한 프로젝트는 이니셜라이저 클래스의 초기값 메서드에 모든 데이터를 포함 하는 사전 마이그레이션 방법을 사용 합니다. 이 자습서에서는 이니셜라이저 클래스를 사용 하지 않도록 설정 하 고 마이그레이션을 사용 하도록 설정 합니다. 그런 다음 프로덕션 환경에 삽입 하려는 데이터만 삽입 하도록 마이그레이션 구성 클래스에서 초기값 메서드를 업데이트 합니다.

다음 다이어그램은 응용 프로그램 데이터베이스의 스키마를 보여 줍니다.

[![School_database_diagram](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image4.png)

이러한 자습서에서는 사이트가 처음 배포 될 때 `Student` 및 `Enrollment` 테이블이 비어 있는 것으로 가정 합니다. 다른 테이블에는 응용 프로그램이 라이브 상태로 전환 될 때 미리 로드 해야 하는 데이터가 포함 되어 있습니다.

Code First 마이그레이션를 사용할 예정 이므로 더 이상 **Dropcreatedatabaseifmodelchanges** Code First 이니셜라이저를 사용할 필요가 없습니다. 이 이니셜라이저의 코드는 ContosoUniversity 프로젝트의 SchoolInitializer.cs 파일에 있습니다. Web.config 파일의 **appSettings** 요소에 설정 되어 있으면 응용 프로그램이 처음으로 데이터베이스에 액세스 하려고 할 때마다이 이니셜라이저가 실행 됩니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample1.xml?highlight=3)]

응용 프로그램 Web.config 파일을 열고 appSettings 요소에서 Code First 이니셜라이저 클래스를 지정 하는 요소를 제거 합니다. 이제 appSettings 요소는 다음과 같습니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample2.xml)]

> [!NOTE]
> 이니셜라이저 클래스를 지정 하는 또 다른 방법은 *global.asax* 파일의 `Application_Start` 메서드에서 `Database.SetInitializer`를 호출 하는 것입니다. 해당 메서드를 사용 하 여 이니셜라이저를 지정 하는 프로젝트에서 마이그레이션을 사용 하도록 설정 하는 경우 해당 코드 줄을 제거 합니다.

다음으로 Code First 마이그레이션를 사용 하도록 설정 합니다.

첫 번째 단계는 ContosoUniversity 프로젝트가 시작 프로젝트로 설정 되어 있는지 확인 하는 것입니다. **솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트로 설정**을 선택 합니다. Code First 마이그레이션는 시작 프로젝트에서 데이터베이스 연결 문자열을 찾습니다.

**도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 차례로 클릭합니다.

![Selecting_Package_Manager_Console](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image6.png)

**패키지 관리자 콘솔** 창의 맨 위에 있는 ContosoUniversity를 기본 프로젝트로 선택 하 고 `PM>` 프롬프트에서 "마이그레이션 사용"을 입력 합니다.

![enable-migrations_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image7.png)

이 명령은 ContosoUniversity 프로젝트의 새 *마이그레이션* 폴더에 *Configuration.cs* 파일을 만듭니다.

![Migrations_folder_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image8.png)

Code First 컨텍스트 클래스를 포함 하는 프로젝트에서 "마이그레이션 사용" 명령을 실행 해야 하므로 DAL 프로젝트를 선택 했습니다. 클래스가 클래스 라이브러리 프로젝트에 있는 경우 솔루션에 대 한 시작 프로젝트에서 데이터베이스 연결 문자열을 찾습니다 Code First 마이그레이션. ContosoUniversity 솔루션에서 웹 프로젝트는 시작 프로젝트로 설정 되었습니다. Visual Studio에서 연결 문자열이 있는 프로젝트를 시작 프로젝트로 지정 하지 않으려는 경우 PowerShell 명령에서 시작 프로젝트를 지정할 수 있습니다. 마이그레이션 사용 명령에 대 한 명령 구문을 보려면 "get-help 사용-마이그레이션" 명령을 입력 하면 됩니다.

Configuration.cs 파일을 열고 `Seed` 메서드의 주석을 다음 코드로 바꿉니다.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample3.cs)]

네임 스페이스에 대 한 `using` 문이 아직 없기 때문에 `List`에 대 한 참조에는 빨간색 물결선이 있습니다. `List` 인스턴스 중 하나를 마우스 오른쪽 단추로 클릭 하 고 **해결**을 클릭 한 다음, **Collections 사용**을 클릭 합니다.

![Using 문을 사용 하 여 확인](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image9.png)

이 메뉴를 선택 하면 파일 위쪽 근처의 `using` 문에 다음 코드가 추가 됩니다.

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample4.cs)]

> [!NOTE]
> `Seed` 메서드에 코드를 추가 하는 것은 데이터베이스에 고정 데이터를 삽입할 수 있는 여러 가지 방법 중 하나입니다. 다른 방법은 각 마이그레이션 클래스의 `Up` 및 `Down` 메서드에 코드를 추가 하는 것입니다. `Up` 및 `Down` 메서드에는 데이터베이스 변경 내용을 구현 하는 코드가 포함 되어 있습니다. [데이터베이스 업데이트 배포](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) 자습서에서 예제를 볼 수 있습니다.
> 
> `Sql` 메서드를 사용 하 여 SQL 문을 실행 하는 코드를 작성할 수도 있습니다. 예를 들어 예산 열을 부서 테이블에 추가 하 고 마이그레이션의 일부로 모든 부서 예산을 $1000.00로 초기화 하려는 경우 해당 마이그레이션의 `Up` 메서드에 다음 코드 줄을 추가할 수 있습니다.
> 
> `Sql("UPDATE Department SET Budget = 1000");`
> 
> 이 자습서에 대해 보여 주는이 예제에서는 Code First 마이그레이션 `Configuration` 클래스의 `Seed` 메서드에 있는 `AddOrUpdate` 메서드를 사용 합니다. Code First 마이그레이션은 모든 마이그레이션 후에 `Seed` 메서드를 호출 하 고,이 메서드는 이미 삽입 된 행을 업데이트 하거나 아직 존재 하지 않는 경우 삽입 합니다. `AddOrUpdate` 방법이 시나리오에 가장 적합 한 선택이 아닐 수 있습니다. 자세한 내용은 Julie Lerman의 블로그에서 [EF 4.3 AddOrUpdate 메서드를 사용 하 여 처리](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) 를 참조 하세요.

CTRL + SHIFT + B를 눌러 프로젝트를 빌드합니다.

다음 단계는 초기 마이그레이션에 대 한 `DbMigration` 클래스를 만드는 것입니다. 이 마이그레이션을 통해 새 데이터베이스를 만들 수 있으므로 이미 존재 하는 데이터베이스를 삭제 해야 합니다. SQL Server Compact 데이터베이스는 *응용 프로그램\_Data* 폴더의 *.sdf* 파일에 포함 되어 있습니다. **솔루션 탐색기**에서 ContosoUniversity 프로젝트의 *앱\_데이터* 를 확장 하 여 *.sdf* 파일로 표시 되는 두 개의 SQL Server Compact 데이터베이스를 확인 합니다.

*School .sdf* 파일을 마우스 오른쪽 단추로 클릭 하 고 **삭제**를 클릭 합니다.

![sdf_files_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image10.png)

**패키지 관리자 콘솔** 창에서 "추가 마이그레이션 초기" 명령을 입력 하 여 초기 마이그레이션을 만들고 이름을 "초기"로 이름을 입력 합니다.

![add-migration_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image11.png)

Code First 마이그레이션는 *마이그레이션* 폴더에 다른 클래스 파일을 만들고,이 클래스에는 데이터베이스 스키마를 만드는 코드가 포함 되어 있습니다.

**패키지 관리자 콘솔**에서 "업데이트-데이터베이스" 명령을 입력 하 여 데이터베이스를 만들고 **초기값** 메서드를 실행 합니다.

![update-database_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image12.png)

테이블이 이미 존재 하 고 만들 수 없음을 나타내는 오류가 발생 하는 경우 데이터베이스를 삭제 한 후 `update-database`를 실행 하기 전에 응용 프로그램을 실행 했기 때문일 수 있습니다. 이 경우 *School* 파일을 다시 삭제 하 고 `update-database` 명령을 다시 시도 하세요.)

애플리케이션을 실행합니다. 이제 학생 페이지가 비어 있지만 강사 페이지가 강사를 포함 합니다. 응용 프로그램을 배포한 후 프로덕션 환경에서이 작업을 수행할 수 있습니다.

![Empty_Students_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image13.png)

![Instructors_page_after_initial_migration](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image14.png)

이제 프로젝트가 *School* 데이터베이스를 배포할 준비가 되었습니다.

## <a name="creating-a-membership-database-for-deployment"></a>배포용 멤버 자격 데이터베이스 만들기

Contoso 대학 응용 프로그램은 ASP.NET 멤버 자격 시스템 및 폼 인증을 사용 하 여 사용자를 인증 하 고 권한을 부여 합니다. 해당 페이지 중 하나는 관리자만 액세스할 수 있습니다. 이 페이지를 표시 하려면 응용 프로그램을 실행 하 고 **과정**의 플라이 아웃 메뉴에서 **크레딧 업데이트** 를 선택 합니다. 관리자 에게만 **크레딧 업데이트** 페이지를 사용할 수 있는 권한이 있으므로 응용 프로그램은 **로그인** 페이지를 표시 합니다.

[![Log_in_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image15.png)

"Pas $ w0rd" 암호를 사용 하 여 "admin"으로 로그인 합니다 ("w0rd"에서 문자 "o" 대신 숫자 0). 로그인 하면 **크레딧을 업데이트** 합니다. 페이지가 표시 됩니다.

[![Update_Credits_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image17.png)

처음으로 사이트를 배포 하는 경우 테스트를 위해 만든 사용자 계정을 대부분 또는 모두 제외 하는 것이 일반적입니다. 이 경우 관리자 계정을 배포 하 고 사용자 계정을 배포 하지 않습니다. 테스트 계정을 수동으로 삭제 하는 대신 프로덕션에 필요한 관리자 사용자 계정이 하나뿐인 새 멤버 자격 데이터베이스를 만듭니다.

> [!NOTE]
> 멤버 자격 데이터베이스는 계정 암호의 해시를 저장 합니다. 한 컴퓨터에서 다른 컴퓨터로 계정을 배포 하려면 해싱 루틴이 원본 컴퓨터에서 수행 하는 것과 다른 해시를 대상 서버에서 생성 하지 않도록 해야 합니다. 기본 알고리즘을 변경 하지 않는 한 ASP.NET Universal Providers 사용할 때 동일한 해시가 생성 됩니다. 기본 알고리즘은 HMACSHA256 이며 web.config 파일에 있는 **[machineKey](https://msdn.microsoft.com/library/w8h3skw9.aspx)** 요소의 **validation** 특성에 지정 됩니다.

멤버 자격 데이터베이스는 Code First 마이그레이션에 의해 유지 관리 되지 않으며, 테스트 계정 (School 데이터베이스의 경우)을 사용 하 여 데이터베이스를 시드 하는 자동 이니셜라이저가 없습니다. 따라서 테스트 데이터를 사용 가능 하 게 유지 하려면 새 테스트 데이터베이스를 만들기 전에 테스트 데이터베이스의 복사본을 만듭니다.

**솔루션 탐색기**에서 *App\_Data* 폴더에 있는 *aspnet .sdf* 파일의 이름을 *aspnet-Dev*로 바꿉니다. 복사본을 만들지 말고 이름을 바꾸면 잠시 후 새 데이터베이스를 만듭니다.

**솔루션 탐색기**에서 웹 프로젝트 (ContosoUniversity, not ContosoUniversity)가 선택 되어 있는지 확인 합니다. 그런 다음 **프로젝트** 메뉴에서 **ASP.NET 구성** 을 선택 하 여 **웹 사이트 관리 도구**(메커니즘)를 실행 합니다.

**보안** 탭을 선택합니다.

[![WAT_Security_tab](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image19.png)

**역할 만들기 또는 관리** 를 클릭 하 고 **관리자** 역할을 추가 합니다.

[![WAT_Create_New_Role](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image21.png)

**보안** 탭으로 다시 이동 하 여 **사용자 만들기**를 클릭 하 고 관리자 권한으로 사용자 "관리자"를 추가 합니다. **사용자 만들기** 페이지에서 **사용자 만들기** 단추를 클릭 하기 전에 **관리자** 확인란을 선택 했는지 확인 합니다. 이 자습서에 사용 된 암호는 "Pas $ w0rd" 이며 모든 전자 메일 주소를 입력할 수 있습니다.

[![WAT_Create_User](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image23.png)

브라우저를 닫습니다. **솔루션 탐색기**에서 새로 고침 단추를 클릭 하 여 새 *aspnet .sdf* 파일을 확인 합니다.

![New_aspnet.sdf_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image25.png)

**Aspnet .sdf** 를 마우스 오른쪽 단추로 클릭 하 고 **프로젝트에 포함**을 선택 합니다.

## <a name="distinguishing-development-from-production-databases"></a>프로덕션 데이터베이스에서 개발 구분

이 섹션에서는 개발 버전이 School-Dev 및 aspnet-Dev이 고 프로덕션 버전이 School-Prod 및 aspnet-Prod이 되도록 데이터베이스의 이름을 바꿉니다. 이렇게 해야 하는 것은 아니지만, 이렇게 하면 테스트 및 프로덕션 버전의 데이터베이스를 혼동 하지 않도록 방지할 수 있습니다.

**솔루션 탐색기**에서 **새로 고침** 을 클릭 하 고 App\_Data 폴더를 확장 하 여 이전에 만든 School 데이터베이스를 확인 합니다. 마우스 오른쪽 단추로 클릭 하 고 **프로젝트에 포함**을 선택 합니다.

![Including_School.sdf_in_project](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image26.png)

*Aspnet-Prod를* *로 바꿉니다.*

*학교의* 이름을 *School-Dev*로 바꿉니다.

Visual Studio에서 응용 프로그램을 실행할 때 *-Prod* 버전의 데이터베이스 파일을 사용 하지 않으려는 경우 *-Dev* 버전을 사용 하려고 합니다. 따라서 데이터베이스의 *Dev* 버전을 가리키도록 web.config 파일에서 연결 문자열을 변경 해야 합니다. School-Prod 파일을 만들지 않았습니다 .이 파일은 처음에 앱을 실행할 때 프로덕션 환경에서 해당 데이터베이스를 만들기 때문에 Code First.

응용 프로그램 Web.config 파일을 열고 연결 문자열을 찾습니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample5.xml)]

"Aspnet .sdf"를 "aspnet-Dev"로 변경 하 고 "School"을 "School-Dev"로 변경 합니다.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample6.xml?highlight=4-5)]

이제 SQL Server Compact 데이터베이스 엔진과 두 데이터베이스를 모두 배포할 준비가 되었습니다. 다음 자습서에서는 개발, 테스트 및 프로덕션 환경에서 달라 야 하는 설정에 대 한 자동 *web.config* 파일 변환을 설정 합니다. 변경 해야 하는 설정 중에는 연결 문자열이 있지만 나중에 게시 프로필을 만들 때 이러한 변경 내용을 설정 합니다.

## <a name="more-information"></a>추가 정보

NuGet에 대 한 자세한 내용은 nuget 및 Nuget을 [사용 하 여 프로젝트 라이브러리 관리](https://msdn.microsoft.com/magazine/hh547106.aspx) [설명서](http://docs.nuget.org/docs/start-here/overview)를 참조 하세요. NuGet을 사용 하지 않으려면 NuGet 패키지를 분석 하 여 설치 시 수행 되는 작업을 확인 하는 방법을 알아야 합니다. 예를 들어 *web.config* 변환을 구성 하 고 빌드 시에 실행 되도록 PowerShell 스크립트를 구성할 수 있습니다. NuGet의 작동 방식에 대 한 자세한 내용은 특히 [패키지 만들기 및 게시](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package) 및 [구성 파일 및 소스 코드 변환](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)을 참조 하세요.

> [!div class="step-by-step"]
> [이전](deployment-to-a-hosting-provider-introduction-1-of-12.md)
> [다음](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
