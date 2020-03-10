---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: 'ASP.NET Identity: EntityFramework MySQL 공급자 ()에서 MySQL 저장소 사용C#()-ASP.NET 4.x'
author: maumar
description: 이 자습서에서는 ASP.NET Identity에 대 한 기본 데이터 저장소 메커니즘을 EntityFramework (SQL 클라이언트 공급자)와 MySQL provid 대체 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 12/10/2013
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: e89ed139657c5ce9ddcc56879946c62038919483
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471875"
---
# <a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a>ASP.NET Identity: EntityFramework MySQL 공급자 (C#)에서 Mysql 저장소 사용

[Maurycy Markowski](https://github.com/maumar), [Raquel Soares De Almeida](https://github.com/raquelsa), [Robert McMurray](https://github.com/rmcmurray)

> 이 자습서에서는 [**ASP.NET Identity**](introduction-to-aspnet-identity.md) 에 대 한 기본 데이터 저장소 메커니즘을 ENTITYFRAMEWORK (SQL 클라이언트 공급자)와 MySQL 공급자로 바꾸는 방법을 보여 줍니다.

이 자습서에서는 다음 항목을 다룹니다.

- Azure에서 MySQL 데이터베이스 만들기
- Visual Studio 2013 MVC 템플릿을 사용 하 여 MVC 응용 프로그램 만들기
- MySQL 데이터베이스 공급자와 작동 하도록 EntityFramework 구성
- 응용 프로그램을 실행 하 여 결과 확인

이 자습서의 끝 부분에서는 Azure에서 호스트 되는 MySQL 데이터베이스를 사용 하는 ASP.NET Identity 저장소를 사용 하는 MVC 응용 프로그램을 만듭니다.

## <a name="creating-a-mysql-database-instance-on-azure"></a>Azure에서 MySQL 데이터베이스 인스턴스 만들기

1. [Azure Portal](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409)에 로그인합니다.
2. 페이지 맨 아래에 있는 **새로 만들기** 를 클릭 한 다음 **스토어**를 선택 합니다.

    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. **선택 및 추가 기능** 마법사에서 **ClearDB MySQL 데이터베이스**를 선택 하 고 프레임 맨 아래에 있는 **다음** 화살표를 클릭 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. 기본 **무료** 요금제를 유지 하 고, **이름을** **IdentityMySQLDatabase**로 변경 하 고, 사용자에 게 가장 가까운 지역을 선택 하 고, 프레임 맨 아래에 있는 **다음** 화살표를 클릭 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. **구매** 확인 표시를 클릭 하 여 데이터베이스 만들기를 완료 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. 데이터베이스가 만들어진 후 관리 포털의 **ADD-ONS** 탭에서 관리할 수 있습니다. 데이터베이스에 대 한 연결 정보를 검색 하려면 페이지 맨 아래에 있는 **연결** 정보를 클릭 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. **CONNECTIONSTRING** 필드에서 복사 단추를 클릭 하 여 연결 문자열을 복사 하 고 저장 합니다. MVC 응용 프로그램에 대 한이 자습서의 뒷부분에서이 정보를 사용 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a>MVC 응용 프로그램 프로젝트 만들기

자습서의이 섹션에 있는 단계를 완료 하려면 먼저 웹 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [에 대 한 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 을 설치 해야 합니다. Visual Studio가 설치 되 면 다음 단계를 사용 하 여 새 MVC 응용 프로그램 프로젝트를 만듭니다.

1. Visual Studio 2103을 엽니다.
2. **시작** 페이지에서 **새 프로젝트** 를 클릭 하거나 **파일** 메뉴를 클릭 한 후 **새 프로젝트**를 클릭 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. **새 프로젝트** 대화 상자가 표시 되 면 템플릿 목록에서 **시각적 C# 개체** 를 확장 한 다음 **웹**을 클릭 하 고 **ASP.NET 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름을 **IdentityMySQLDemo** 로 지정한 다음 **확인을**클릭 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. **새 ASP.NET 프로젝트** 대화 상자에서 기본 옵션을 사용 하 여 **MVC** 템플릿을 선택 합니다. 그러면 **개별 사용자 계정이** 인증 방법으로 구성 됩니다. **확인**을 클릭합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a>MySQL 데이터베이스를 사용 하도록 EntityFramework 구성

### <a name="update-the-entity-framework-assembly-for-your-project"></a>프로젝트에 대 한 Entity Framework 어셈블리 업데이트

Visual Studio 2013 템플릿에서 만든 MVC 응용 프로그램에는 [Entityframework 6.0.0](http://www.nuget.org/packages/EntityFramework) 패키지에 대 한 참조가 포함 되어 있지만 해당 어셈블리의 릴리스 이후 상당한 성능 향상이 포함 되어 있습니다. 응용 프로그램에서 이러한 최신 업데이트를 사용 하려면 다음 단계를 사용 합니다.

1. Visual Studio에서 MVC 프로젝트를 엽니다.
2. **도구**를 클릭 하 고 **NuGet 패키지 관리자**를 클릭 한 다음 **패키지 관리자 콘솔**을 클릭 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. Visual Studio의 아래쪽 섹션에 **패키지 관리자 콘솔이** 표시 됩니다. &quot;**업데이트 패키지 EntityFramework**&quot;를 입력 하 고 enter 키를 누릅니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a>EntityFramework 용 MySQL 공급자 설치

EntityFramework를 MySQL 데이터베이스에 연결 하려면 MySQL 공급자를 설치 해야 합니다. 이렇게 하려면 **패키지 관리자 콘솔** 을 열고 &quot;**설치-패키지 MySql.** &quot;를 입력 한 다음 enter 키를 누릅니다.

> [!NOTE]
> 이 버전은 어셈블리의 시험판 버전 이며 버그를 포함할 수 있습니다. 프로덕션 환경에서는 시험판 버전의 공급자를 사용해 서는 안 됩니다.

[다음 이미지를 클릭 하 여 확장 하십시오.]

[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a>응용 프로그램에 대 한 web.config 파일의 프로젝트 구성 변경

이 섹션에서는 방금 설치한 MySQL 공급자를 사용 하 여 Entity Framework를 구성 하 고, MySQL 공급자 팩터리를 등록 하 고, Azure에서 연결 문자열을 추가 합니다.

> [!NOTE]
> 다음 예제에는 MySql의 특정 어셈블리 버전이 포함 되어 있습니다. 어셈블리 버전이 변경 되는 경우 올바른 버전으로 적절 한 구성 설정을 수정 해야 합니다.

1. Visual Studio 2013에서 프로젝트에 대 한 web.config 파일을 엽니다.
2. Entity Framework에 대 한 기본 데이터베이스 공급자 및 팩터리를 정의 하는 다음 구성 설정을 찾습니다.

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. 이러한 구성 설정을 다음으로 바꿔 MySQL 공급자를 사용 하도록 Entity Framework를 구성 합니다.

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. &lt;connectionStrings&gt; 섹션을 찾아 다음 코드로 바꿉니다 .이 코드는 Azure에서 호스트 되는 MySQL 데이터베이스에 대 한 연결 문자열을 정의 합니다 (providerName 값도 원래에서 변경 됨).

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a>사용자 지정 MigrationHistory 컨텍스트 추가

Entity Framework Code First는 **MigrationHistory** 테이블을 사용 하 여 모델 변경 내용을 추적 하 고 데이터베이스 스키마와 개념 스키마 간에 일관성을 유지 합니다. 그러나 기본 키가 너무 크기 때문에이 테이블은 기본적으로 MySQL에 대해 작동 하지 않습니다. 이러한 상황을 해결 하려면 해당 테이블에 대 한 키 크기를 축소 해야 합니다. 이렇게 하려면 다음 단계를 수행합니다.

1. 이 테이블에 대 한 스키마 정보는 다른 **DbContext**로 수정할 수 있는 **HistoryContext**에서 캡처됩니다. 이렇게 하려면 **MySqlHistoryContext.cs** 이라는 새 클래스 파일을 프로젝트에 추가 하 고 해당 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. 그런 다음 수정 된 **HistoryContext**를 사용 하도록 Entity Framework를 구성 해야 합니다 (기본값은 아님). 코드 기반 구성 기능을 활용 하 여이 작업을 수행할 수 있습니다. 이렇게 하려면 **MySqlConfiguration.cs** 이라는 새 클래스 파일을 프로젝트에 추가 하 고 해당 내용을로 바꿉니다.

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a>ApplicationDbContext에 대 한 사용자 지정 EntityFramework 이니셜라이저 만들기

이 자습서에 제공 되는 MySQL 공급자는 현재 Entity Framework 마이그레이션을 지원 하지 않으므로 데이터베이스에 연결 하려면 모델 이니셜라이저를 사용 해야 합니다. 이 자습서에서는 Azure에서 MySQL 인스턴스를 사용 하므로 사용자 지정 Entity Framework 이니셜라이저를 만들어야 합니다.

> [!NOTE]
> Azure의 SQL Server 인스턴스에 연결 하거나 온-프레미스에서 호스트 되는 데이터베이스를 사용 하는 경우에는이 단계가 필요 하지 않습니다.

MySQL에 대 한 사용자 지정 Entity Framework 이니셜라이저를 만들려면 다음 단계를 사용 합니다.

1. **MySqlInitializer.cs** 라는 새 클래스 파일을 프로젝트에 추가 하 고 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. **모델** 디렉터리에 있는 프로젝트에 대 한 **IdentityModels.cs** 파일을 열고 내용을 다음으로 바꿉니다.

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a>응용 프로그램 실행 및 데이터베이스 확인

이전 섹션의 단계를 완료 한 후에는 데이터베이스를 테스트 해야 합니다. 이렇게 하려면 다음 단계를 수행합니다.

1. **Ctrl +** f 5를 눌러 웹 응용 프로그램을 빌드하고 실행 합니다.
2. 페이지 위쪽에서 **등록** 탭을 클릭 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. 새 사용자 이름 및 암호를 입력 한 다음 **등록**을 클릭 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. 이 시점에서 MySQL 데이터베이스에 ASP.NET Identity 테이블이 생성 되 고 사용자가 등록 되 고 응용 프로그램에 로그인 됩니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a>MySQL 워크 벤치 도구를 설치 하 여 데이터 확인

1. [Mysql 다운로드 페이지](http://dev.mysql.com/downloads/windows/installer/) 에서 **mysql 워크 벤치** 도구를 설치 합니다.
2. 설치 마법사: **기능 선택** 탭의 **응용 프로그램** 섹션에서 **MySQL 워크 벤치** 를 선택 합니다.
3. 앱을 시작 하 고이 자습서의 begging에서 만든 Azure MySQL 데이터베이스의 연결 문자열 데이터를 사용 하 여 새 연결을 추가 합니다.
4. 연결을 설정한 후 IdentityMySQLDatabase에서 만든 **ASP.NET Identity** 테이블을 검사 합니다 **.**
5. 아래 이미지에 표시 된 것 처럼 모든 ASP.NET Identity 필수 테이블이 생성 된 것을 확인할 수 있습니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. 새 사용자를 등록할 때 항목을 확인 하려면 **aspnetusers** 테이블에서 인스턴스를 검사 합니다.

   [다음 이미지를 클릭 하 여 확장 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
