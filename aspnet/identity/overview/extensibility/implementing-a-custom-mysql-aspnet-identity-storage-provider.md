---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: 사용자 지정 MySQL ASP.NET Identity 저장소 공급자 (ASP.NET 4.x) 구현
author: raquelsa
description: ASP.NET Identity는 사용자 고유의 저장소 공급자를 만들어 응용 프로그램에 연결 하는 데 사용할 수 있는 확장 가능한 시스템입니다.
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 2f0b47d45bce82c71d1864536309f9e2ffed2d63
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519130"
---
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a>사용자 지정 MySQL ASP.NET Identity 스토리지 공급자 구현

[Raquel Soares De Almeida](https://github.com/raquelsa), [suhas Joshi](https://github.com/suhasj), [Tom fitzmacken](https://github.com/tfitzmac)

> ASP.NET Identity는 사용자 고유의 저장소 공급자를 만들고 응용 프로그램을 다시 작동 시 키 지 않고도 응용 프로그램에 연결할 수 있도록 하는 확장 가능한 시스템입니다. 이 항목에서는 ASP.NET Identity에 대 한 MySQL 저장소 공급자를 만드는 방법에 대해 설명 합니다. 사용자 지정 저장소 공급자를 만드는 방법에 대 한 개요는 [ASP.NET Identity에 대 한 사용자 지정 저장소 공급자 개요](overview-of-custom-storage-providers-for-aspnet-identity.md)를 참조 하세요.
> 
> 이 자습서를 완료 하려면 업데이트 2와 Visual Studio 2013 있어야 합니다.
> 
> 이 자습서에서는 다음을 수행 합니다.
> 
> - Azure에서 MySQL 데이터베이스 인스턴스를 만드는 방법을 보여 줍니다.
> - MySQL 클라이언트 도구 (MySQL 워크 벤치)를 사용 하 여 테이블을 만들고 Azure에서 원격 데이터베이스를 관리 하는 방법을 보여 줍니다.
> - 기본 ASP.NET Identity 저장소 구현을 MVC 응용 프로그램 프로젝트의 사용자 지정 구현으로 바꾸는 방법을 보여 줍니다.
> 
> 이 자습서는 원래 Raquel Soares De Almeida 및 Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )에 의해 작성 되었습니다. Joshi에서 Id 2.0에 대 한 샘플 프로젝트가 업데이트 되었습니다. 이 항목은 Id 2.0에서 Tom FitzMacken에 대해 업데이트 되었습니다.

## <a name="download-completed-project"></a>완료 된 프로젝트 다운로드

이 자습서의 끝 부분에서는 Azure에서 호스트 되는 MySQL 데이터베이스를 사용 하 여 ASP.NET Identity 있는 MVC 응용 프로그램 프로젝트를 만듭니다.

완성 된 MySQL 저장소 공급자는 [AspNet. id. mysql (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL)에서 다운로드할 수 있습니다.

## <a name="the-steps-you-will-perform"></a>수행 하는 단계

이 자습서에서는 다음 작업을 수행하게 됩니다.

1. Azure에서 MySQL 데이터베이스 만들기
2. MySQL에서 ASP.NET Identity 테이블 만들기
3. MVC 응용 프로그램을 만들고 MySQL 공급자를 사용 하도록 구성
4. 앱 실행

이 항목에서는 ASP.NET Identity의 아키텍처 및 고객 저장소 공급자를 구현할 때 결정 해야 하는 사항을 다루지 않습니다. 해당 정보는 [ASP.NET Identity에 대 한 사용자 지정 저장소 공급자 개요](overview-of-custom-storage-providers-for-aspnet-identity.md)를 참조 하세요.

## <a name="review-mysql-storage-provider-classes"></a>MySQL 저장소 공급자 클래스 검토

MySQL 저장소 공급자를 만드는 단계를 수행 하기 전에 저장소 공급자를 구성 하는 클래스를 살펴보겠습니다. 사용자 및 역할을 관리 하기 위해 응용 프로그램에서 호출 되는 데이터베이스 작업 및 클래스를 관리 하는 클래스가 필요 합니다.

### <a name="storage-classes"></a>스토리지 클래스

- [IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -사용자에 대 한 속성을 포함 합니다.
- [Userstore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) -사용자를 추가, 업데이트 또는 검색 하는 작업을 포함 합니다.
- [IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -역할에 대 한 속성을 포함 합니다.
- [Rolestore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) -역할을 추가, 삭제, 업데이트 및 검색 하는 작업을 포함 합니다.

### <a name="data-access-layer-classes"></a>데이터 액세스 계층 클래스

이 예에서는 데이터 액세스 계층 클래스에 테이블 작업을 위한 SQL 문이 포함 되어 있습니다. 그러나 코드에서 Entity Framework 또는 NHibernate 모드와 같은 ORM (개체-관계형 매핑)을 사용 하는 것이 좋습니다. 특히 응용 프로그램에는 지연 로드 및 개체 캐싱이 포함 된 ORM 없이 성능이 저하 될 수 있습니다. 자세한 내용은 [Entity Framework 없는 ASP.NET Identity 2.0](https://aspnetidentity.codeplex.com/discussions/561828) 을 참조 하세요.

- [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -MySQL 데이터베이스 연결 및 데이터베이스 작업을 수행 하기 위한 메서드를 포함 합니다. UserStore 및 RoleStore는 모두이 클래스의 인스턴스를 사용 하 여 인스턴스화됩니다.
- [Roletable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) -역할을 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [Userclaimstable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -사용자 클레임을 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [Userloginstable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -사용자 로그인 정보를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [Userroletable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -역할에 할당 된 사용자를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [Usertable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) -사용자를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.

## <a name="create-a-mysql-database-instance-on-azure"></a>Azure에서 MySQL 데이터베이스 인스턴스 만들기

1. [Azure Portal](https://manage.windowsazure.com/)에 로그인합니다.
2. 페이지 맨 아래에서 **+ 새로 만들기** 를 클릭 한 다음 **스토어**를 선택 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. **선택 및 추가 기능** 마법사에서 **ClearDB MySQL 데이터베이스** 를 선택 하 고 대화 상자의 오른쪽 아래에 있는 다음 화살표를 클릭 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. 기본 **무료** 요금제를 유지 하 고 **이름을** **IdentityMySQLDatabase**로 변경 합니다. 가장 가까운 지역을 선택 하 고 다음 화살표를 클릭 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. 확인 표시를 클릭 하 여 데이터베이스 만들기를 완료 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. 데이터베이스가 만들어진 후 관리 포털의 **ADD-ONS** 탭에서 관리할 수 있습니다.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. 페이지 맨 아래에서 **연결 정보** 를 클릭 하 여 데이터베이스 연결 정보를 가져올 수 있습니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. 복사 단추를 클릭 하 여 연결 문자열을 복사 하 고 나중에 MVC 응용 프로그램에서 사용할 수 있도록 저장 합니다.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a>MySQL 데이터베이스에 ASP.NET Identity 테이블 만들기

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a>Mysql 워크 벤치 도구를 설치 하 여 MySQL 데이터베이스 연결 및 관리

1. [Mysql 다운로드 페이지](http://dev.mysql.com/downloads/windows/installer/) 에서 **mysql 워크 벤치** 도구를 설치 합니다.
2. 앱을 시작 하 고 **Mysqlconnections +** 단추를 클릭 하 여 새 연결을 추가 합니다. 이 자습서의 앞부분에서 만든 Azure MySQL 데이터베이스에서 복사한 연결 문자열 데이터를 사용 합니다.
3. 연결을 설정한 후 새 **쿼리** 탭을 엽니다. [MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) 의 명령을 쿼리에 붙여넣고 데이터베이스 테이블을 만들기 위해 실행 합니다.
4. 이제 아래와 같이 Azure에서 호스트 되는 MySQL 데이터베이스에서 모든 ASP.NET Identity 필요한 테이블을 만들었습니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a>템플릿에서 MVC 응용 프로그램 프로젝트를 만들고 MySQL 공급자를 사용 하도록 구성

필요한 경우 [웹 용 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 업데이트 2와 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 를 설치 합니다.

### <a name="download-the-aspnetidentitymysql-project-from-github"></a>GitHub에서 ASP.NET. n e t. n e t. i n t 프로젝트 다운로드

1. [AspNet. Identity (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/)에서 리포지토리 URL로 이동 합니다.
2. 소스 코드를 다운로드 합니다.
3. .Zip 파일을 로컬 폴더에 추출 합니다.
4. AspNet. n. i n. i n. i n.

### <a name="create-a-new-mvc-application-project-from-template"></a>템플릿에서 새 MVC 응용 프로그램 프로젝트 만들기

1. **AspNet. n. i n.**
2. **새 프로젝트 추가** 대화 상자에서 왼쪽 **의 C# 시각적 개체** 와 **웹** 을 차례로 선택한 다음 **ASP.NET 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름 **IdentityMySQLDemo**; 그런 다음 확인을 클릭 합니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. **새 ASP.NET 프로젝트** 대화 상자에서 기본 옵션 (인증 방법으로 **개별 사용자 계정** 포함)이 포함 된 MVC 템플릿을 선택 하 고 **확인**을 클릭 합니다.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)
4. 솔루션 탐색기에서 IdentityMySQLDemo 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다. 검색 텍스트 상자 대화 상자에서 **Identity. EntityFramework**를 입력 합니다. 결과 목록에서이 패키지를 선택 하 고 **제거**를 클릭 합니다. 종속성 패키지 EntityFramework를 제거할지 묻는 메시지가 표시 됩니다. 이 응용 프로그램에이 패키지가 더 이상 나타나지 않으므로 예를 클릭 합니다.
5. IdentityMySQLDemo 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **참조, 솔루션, 프로젝트** 를 차례로 선택한 다음, 프로젝트를 선택 하 고 **확인**을 클릭 합니다.
6. IdentityMySQLDemo 프로젝트에서 다음에 대 한 모든 참조를 바꿉니다.  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   를 사용하는 경우  
     `using AspNet.Identity.MySQL;`
7. IdentityModels.cs에서 **ApplicationDbContext** 를 **MySqlDatabase** 에서 파생 하도록 설정 하 고 연결 이름과 함께 단일 매개 변수를 사용 하는 생성자를 포함 합니다.  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. IdentityConfig.cs 파일을 엽니다. **Applicationusermanager. Create** 메서드에서 usermanager 인스턴스화를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. Web.config 파일을 열고, 강조 표시 된 값을 이전 단계에서 만든 MySQL 데이터베이스의 연결 문자열로 대체 하 여 DefaultConnection 문자열을이 항목으로 바꿉니다.  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a>앱을 실행 하 고 MySQL DB에 연결

1. **IdentityMySQLDemo** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트로 설정** 을 선택 합니다.
2. **Ctrl + F5** 키를 눌러 앱을 빌드하고 실행 합니다.
3. 페이지 위쪽에서 **등록** 탭을 클릭 합니다.
4. 새 사용자 이름 및 암호를 입력 한 다음 **등록**을 클릭 합니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. 이제 새 사용자가 등록 되 고 로그인 됩니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. MySQL 워크 벤치 도구로 돌아가서 **IdentityMySQLDatabase** 테이블의 내용을 검사 합니다. 새 사용자를 등록할 때 사용자 테이블에서 항목을 검사 합니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a>다음 단계

이 앱에서 다른 인증 방법을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [Facebook 및 Google OAuth2 및 Openid connect sign-on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)를 참조 하세요.

DB를 OAuth와 통합 하 고 사용자가 앱에 대 한 액세스를 제한 하도록 역할을 설정 하는 방법을 알아보려면 [멤버 자격, OAuth 및 SQL Database를 Azure에 배포 하는 Secure ASP.NET MVC 5 앱 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)를 참조 하세요.
