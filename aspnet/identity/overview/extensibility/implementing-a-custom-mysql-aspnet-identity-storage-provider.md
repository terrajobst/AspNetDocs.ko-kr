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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500069"
---
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a><span data-ttu-id="e8bb9-103">사용자 지정 MySQL ASP.NET Identity 스토리지 공급자 구현</span><span class="sxs-lookup"><span data-stu-id="e8bb9-103">Implementing a Custom MySQL ASP.NET Identity Storage Provider</span></span>

<span data-ttu-id="e8bb9-104">[Raquel Soares De Almeida](https://github.com/raquelsa), [suhas Joshi](https://github.com/suhasj), [Tom fitzmacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e8bb9-104">by [Raquel Soares De Almeida](https://github.com/raquelsa), [Suhas Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e8bb9-105">ASP.NET Identity는 사용자 고유의 저장소 공급자를 만들고 응용 프로그램을 다시 작동 시 키 지 않고도 응용 프로그램에 연결할 수 있도록 하는 확장 가능한 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-105">ASP.NET Identity is an extensible system which enables you to create your own storage provider and plug it into your application without re-working the application.</span></span> <span data-ttu-id="e8bb9-106">이 항목에서는 ASP.NET Identity에 대 한 MySQL 저장소 공급자를 만드는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-106">This topic describes how to create a MySQL storage provider for ASP.NET Identity.</span></span> <span data-ttu-id="e8bb9-107">사용자 지정 저장소 공급자를 만드는 방법에 대 한 개요는 [ASP.NET Identity에 대 한 사용자 지정 저장소 공급자 개요](overview-of-custom-storage-providers-for-aspnet-identity.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-107">For an overview of creating custom storage providers, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>
> 
> <span data-ttu-id="e8bb9-108">이 자습서를 완료 하려면 업데이트 2와 Visual Studio 2013 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-108">To complete this tutorial, you must have Visual Studio 2013 with Update 2.</span></span>
> 
> <span data-ttu-id="e8bb9-109">이 자습서에서는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-109">This tutorial will:</span></span>
> 
> - <span data-ttu-id="e8bb9-110">Azure에서 MySQL 데이터베이스 인스턴스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-110">Show how to create a MySQL database instance on Azure.</span></span>
> - <span data-ttu-id="e8bb9-111">MySQL 클라이언트 도구 (MySQL 워크 벤치)를 사용 하 여 테이블을 만들고 Azure에서 원격 데이터베이스를 관리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-111">Show how to use a MySQL client tool (MySQL Workbench) to create tables and manage your remote database on Azure.</span></span>
> - <span data-ttu-id="e8bb9-112">기본 ASP.NET Identity 저장소 구현을 MVC 응용 프로그램 프로젝트의 사용자 지정 구현으로 바꾸는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-112">Show how to replace the default ASP.NET Identity storage implementation with our custom implementation on a MVC application project.</span></span>
> 
> <span data-ttu-id="e8bb9-113">이 자습서는 원래 Raquel Soares De Almeida 및 Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )에 의해 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-113">This tutorial was originally written by Raquel Soares De Almeida and Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).</span></span> <span data-ttu-id="e8bb9-114">Joshi에서 Id 2.0에 대 한 샘플 프로젝트가 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-114">The sample project was updated for Identity 2.0 by Suhas Joshi.</span></span> <span data-ttu-id="e8bb9-115">이 항목은 Id 2.0에서 Tom FitzMacken에 대해 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-115">The topic was updated for Identity 2.0 by Tom FitzMacken.</span></span>

## <a name="download-completed-project"></a><span data-ttu-id="e8bb9-116">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="e8bb9-116">Download completed project</span></span>

<span data-ttu-id="e8bb9-117">이 자습서의 끝 부분에서는 Azure에서 호스트 되는 MySQL 데이터베이스를 사용 하 여 ASP.NET Identity 있는 MVC 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-117">At the end of this tutorial, you will have an MVC application project with ASP.NET Identity working with a MySQL database hosted on Azure.</span></span>

<span data-ttu-id="e8bb9-118">완성 된 MySQL 저장소 공급자는 [AspNet. id. mysql (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-118">You can download the completed MySQL storage provider at [AspNet.Identity.MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL).</span></span>

## <a name="the-steps-you-will-perform"></a><span data-ttu-id="e8bb9-119">수행 하는 단계</span><span class="sxs-lookup"><span data-stu-id="e8bb9-119">The steps you will perform</span></span>

<span data-ttu-id="e8bb9-120">이 자습서에서는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-120">In this tutorial you will:</span></span>

1. <span data-ttu-id="e8bb9-121">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e8bb9-121">Create a MySQL database on Azure</span></span>
2. <span data-ttu-id="e8bb9-122">MySQL에서 ASP.NET Identity 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="e8bb9-122">Create the ASP.NET Identity tables in MySQL</span></span>
3. <span data-ttu-id="e8bb9-123">MVC 응용 프로그램을 만들고 MySQL 공급자를 사용 하도록 구성</span><span class="sxs-lookup"><span data-stu-id="e8bb9-123">Create an MVC application and configure it to use the MySQL provider</span></span>
4. <span data-ttu-id="e8bb9-124">앱 실행</span><span class="sxs-lookup"><span data-stu-id="e8bb9-124">Run the app</span></span>

<span data-ttu-id="e8bb9-125">이 항목에서는 ASP.NET Identity의 아키텍처 및 고객 저장소 공급자를 구현할 때 결정 해야 하는 사항을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-125">This topic does not cover the architecture of ASP.NET Identity and the decisions you must make when implementing a customer storage provider.</span></span> <span data-ttu-id="e8bb9-126">해당 정보는 [ASP.NET Identity에 대 한 사용자 지정 저장소 공급자 개요](overview-of-custom-storage-providers-for-aspnet-identity.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-126">For that information, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>

## <a name="review-mysql-storage-provider-classes"></a><span data-ttu-id="e8bb9-127">MySQL 저장소 공급자 클래스 검토</span><span class="sxs-lookup"><span data-stu-id="e8bb9-127">Review MySQL storage provider classes</span></span>

<span data-ttu-id="e8bb9-128">MySQL 저장소 공급자를 만드는 단계를 수행 하기 전에 저장소 공급자를 구성 하는 클래스를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-128">Before jumping into the steps to create the MySQL storage provider, let's look at the classes that make up the storage provider.</span></span> <span data-ttu-id="e8bb9-129">사용자 및 역할을 관리 하기 위해 응용 프로그램에서 호출 되는 데이터베이스 작업 및 클래스를 관리 하는 클래스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-129">You will need classes that manage the database operations and classes that are called from the application to manage users and roles.</span></span>

### <a name="storage-classes"></a><span data-ttu-id="e8bb9-130">스토리지 클래스</span><span class="sxs-lookup"><span data-stu-id="e8bb9-130">Storage classes</span></span>

- <span data-ttu-id="e8bb9-131">[IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -사용자에 대 한 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-131">[IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) - contains properties for the user.</span></span>
- <span data-ttu-id="e8bb9-132">[Userstore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) -사용자를 추가, 업데이트 또는 검색 하는 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-132">[UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) - contains operations for adding, updating or retrieving users.</span></span>
- <span data-ttu-id="e8bb9-133">[IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -역할에 대 한 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-133">[IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) - contains properties for roles.</span></span>
- <span data-ttu-id="e8bb9-134">[Rolestore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) -역할을 추가, 삭제, 업데이트 및 검색 하는 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-134">[RoleStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) - contains operations for adding, deleting, updating and retrieving roles.</span></span>

### <a name="data-access-layer-classes"></a><span data-ttu-id="e8bb9-135">데이터 액세스 계층 클래스</span><span class="sxs-lookup"><span data-stu-id="e8bb9-135">Data access layer classes</span></span>

<span data-ttu-id="e8bb9-136">이 예에서는 데이터 액세스 계층 클래스에 테이블 작업을 위한 SQL 문이 포함 되어 있습니다. 그러나 코드에서 Entity Framework 또는 NHibernate 모드와 같은 ORM (개체-관계형 매핑)을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-136">For this example, the data access layer classes contain SQL statements for working with the tables; however, in your code you might want to use object-relational mapping (ORM) such as Entity Framework or NHibernate.</span></span> <span data-ttu-id="e8bb9-137">특히 응용 프로그램에는 지연 로드 및 개체 캐싱이 포함 된 ORM 없이 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-137">In particular, your application may experience poor performance without an ORM that includes lazy loading and object caching.</span></span> <span data-ttu-id="e8bb9-138">자세한 내용은 [Entity Framework 없는 ASP.NET Identity 2.0](https://aspnetidentity.codeplex.com/discussions/561828) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-138">For more information, see [ASP.NET Identity 2.0 without Entity Framework?](https://aspnetidentity.codeplex.com/discussions/561828)</span></span>

- <span data-ttu-id="e8bb9-139">[MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -MySQL 데이터베이스 연결 및 데이터베이스 작업을 수행 하기 위한 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-139">[MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) - contains the MySQL database connection and methods for performing database operations.</span></span> <span data-ttu-id="e8bb9-140">UserStore 및 RoleStore는 모두이 클래스의 인스턴스를 사용 하 여 인스턴스화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-140">UserStore and RoleStore are both instantiated with an instance of this class.</span></span>
- <span data-ttu-id="e8bb9-141">[Roletable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) -역할을 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-141">[RoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) - contains database operations for the table that stores roles.</span></span>
- <span data-ttu-id="e8bb9-142">[Userclaimstable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -사용자 클레임을 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-142">[UserClaimsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) - contains database operations for the table that stores user claims.</span></span>
- <span data-ttu-id="e8bb9-143">[Userloginstable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -사용자 로그인 정보를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-143">[UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) - contains database operations for the table that stores user login information.</span></span>
- <span data-ttu-id="e8bb9-144">[Userroletable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -역할에 할당 된 사용자를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-144">[UserRoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) - contains database operations for the table that stores which users are assigned to which roles.</span></span>
- <span data-ttu-id="e8bb9-145">[Usertable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) -사용자를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-145">[UserTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) - contains database operations for the table that stores users.</span></span>

## <a name="create-a-mysql-database-instance-on-azure"></a><span data-ttu-id="e8bb9-146">Azure에서 MySQL 데이터베이스 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="e8bb9-146">Create a MySQL database instance on Azure</span></span>

1. <span data-ttu-id="e8bb9-147">[Azure Portal](https://manage.windowsazure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-147">Log in to the [Azure Portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="e8bb9-148">페이지 맨 아래에서 **+ 새로 만들기** 를 클릭 한 다음 **스토어**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-148">Click **+NEW** at the bottom of the page, and then select **STORE**.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. <span data-ttu-id="e8bb9-149">**선택 및 추가 기능** 마법사에서 **ClearDB MySQL 데이터베이스** 를 선택 하 고 대화 상자의 오른쪽 아래에 있는 다음 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-149">In the **Choose and Add-on** wizard, select **ClearDB MySQL Database** and click on the next arrow at the bottom right of the dialog.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. <span data-ttu-id="e8bb9-150">기본 **무료** 요금제를 유지 하 고 **이름을** **IdentityMySQLDatabase**로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-150">Keep the default **Free** plan and change the **Name** to **IdentityMySQLDatabase**.</span></span> <span data-ttu-id="e8bb9-151">가장 가까운 지역을 선택 하 고 다음 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-151">Select the region nearest you and then click the next arrow.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. <span data-ttu-id="e8bb9-152">확인 표시를 클릭 하 여 데이터베이스 만들기를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-152">Click the checkmark to complete the database creation.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. <span data-ttu-id="e8bb9-153">데이터베이스가 만들어진 후 관리 포털의 **ADD-ONS** 탭에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-153">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. <span data-ttu-id="e8bb9-154">페이지 맨 아래에서 **연결 정보** 를 클릭 하 여 데이터베이스 연결 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-154">You can get the database connection information by clicking on **CONNECTION INFO** at the bottom of the page.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. <span data-ttu-id="e8bb9-155">복사 단추를 클릭 하 여 연결 문자열을 복사 하 고 나중에 MVC 응용 프로그램에서 사용할 수 있도록 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-155">Copy the connection string by clicking on the copy button and save it so you can use later in your MVC application.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a><span data-ttu-id="e8bb9-156">MySQL 데이터베이스에 ASP.NET Identity 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="e8bb9-156">Create the ASP.NET Identity tables in a MySQL database</span></span>

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a><span data-ttu-id="e8bb9-157">Mysql 워크 벤치 도구를 설치 하 여 MySQL 데이터베이스 연결 및 관리</span><span class="sxs-lookup"><span data-stu-id="e8bb9-157">Install MySQL Workbench tool to connect and manage MySQL database</span></span>

1. <span data-ttu-id="e8bb9-158">[Mysql 다운로드 페이지](http://dev.mysql.com/downloads/windows/installer/) 에서 **mysql 워크 벤치** 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-158">Install the **MySQL Workbench** tool from the [MySQL downloads page](http://dev.mysql.com/downloads/windows/installer/)</span></span>
2. <span data-ttu-id="e8bb9-159">앱을 시작 하 고 **Mysqlconnections +** 단추를 클릭 하 여 새 연결을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-159">Launch the app and add click on the **MySQLConnections +** button to add a new connection.</span></span> <span data-ttu-id="e8bb9-160">이 자습서의 앞부분에서 만든 Azure MySQL 데이터베이스에서 복사한 연결 문자열 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-160">Use the connection string data you copied from the Azure MySQL database you created earlier in this tutorial.</span></span>
3. <span data-ttu-id="e8bb9-161">연결을 설정한 후 새 **쿼리** 탭을 엽니다. [MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) 의 명령을 쿼리에 붙여넣고 데이터베이스 테이블을 만들기 위해 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-161">After establishing the connection, open a new **Query** tab; paste the commands from [MySQLIdentity.sql](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) into the query and execute it in order to create the database tables.</span></span>
4. <span data-ttu-id="e8bb9-162">이제 아래와 같이 Azure에서 호스트 되는 MySQL 데이터베이스에서 모든 ASP.NET Identity 필요한 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-162">You now have all the ASP.NET Identity necessary tables created on a MySQL database hosted on Azure as shown below.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a><span data-ttu-id="e8bb9-163">템플릿에서 MVC 응용 프로그램 프로젝트를 만들고 MySQL 공급자를 사용 하도록 구성</span><span class="sxs-lookup"><span data-stu-id="e8bb9-163">Create an MVC application project from template and configure it to use MySQL provider</span></span>

<span data-ttu-id="e8bb9-164">필요한 경우 [웹 용 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 업데이트 2와 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-164">If needed, install either [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) with Update 2.</span></span>

### <a name="download-the-aspnetidentitymysql-project-from-github"></a><span data-ttu-id="e8bb9-165">GitHub에서 ASP.NET. n e t. n e t. i n t 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="e8bb9-165">Download the ASP.NET.Identity.MySQL project from GitHub</span></span>

1. <span data-ttu-id="e8bb9-166">[AspNet. Identity (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/)에서 리포지토리 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-166">Browse to the repository URL at [AspNet.Identity.MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/).</span></span>
2. <span data-ttu-id="e8bb9-167">소스 코드를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-167">Download the source code.</span></span>
3. <span data-ttu-id="e8bb9-168">.Zip 파일을 로컬 폴더에 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-168">Extract the .zip file into a local folder.</span></span>
4. <span data-ttu-id="e8bb9-169">AspNet. n. i n. i n. i n.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-169">Open the AspNet.Identity.MySQL solution and build it.</span></span>

### <a name="create-a-new-mvc-application-project-from-template"></a><span data-ttu-id="e8bb9-170">템플릿에서 새 MVC 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e8bb9-170">Create a new MVC application project from template</span></span>

1. <span data-ttu-id="e8bb9-171">**AspNet. n. i n.**</span><span class="sxs-lookup"><span data-stu-id="e8bb9-171">Right click the **AspNet.Identity.MySQL** solution and **Add**, **New Project**</span></span>
2. <span data-ttu-id="e8bb9-172">**새 프로젝트 추가** 대화 상자에서 왼쪽 **의 C# 시각적 개체** 와 **웹** 을 차례로 선택한 다음 **ASP.NET 웹 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-172">In the **Add New Project** Dialog select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="e8bb9-173">프로젝트 이름 **IdentityMySQLDemo**; 그런 다음 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-173">Name your project **IdentityMySQLDemo**; and then click OK.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. <span data-ttu-id="e8bb9-174">**새 ASP.NET 프로젝트** 대화 상자에서 기본 옵션 (인증 방법으로 **개별 사용자 계정** 포함)이 포함 된 MVC 템플릿을 선택 하 고 **확인**을 클릭 합니다.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span><span class="sxs-lookup"><span data-stu-id="e8bb9-174">In the **New ASP.NET Project** dialog, select the MVC template with the default options (that includes **Individual User Accounts** as authentication method) and click **OK**.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span></span>
4. <span data-ttu-id="e8bb9-175">솔루션 탐색기에서 IdentityMySQLDemo 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-175">In Solution Explorer, right-click your IdentityMySQLDemo project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="e8bb9-176">검색 텍스트 상자 대화 상자에서 **Identity. EntityFramework**를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-176">In the search text box dialog, type **Identity.EntityFramework**.</span></span> <span data-ttu-id="e8bb9-177">결과 목록에서이 패키지를 선택 하 고 **제거**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-177">Select this package in the list of results and click **Uninstall**.</span></span> <span data-ttu-id="e8bb9-178">종속성 패키지 EntityFramework를 제거할지 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-178">You will be prompted to uninstall the dependency package EntityFramework.</span></span> <span data-ttu-id="e8bb9-179">이 응용 프로그램에이 패키지가 더 이상 나타나지 않으므로 예를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-179">Click on Yes as we will no longer this package on this application.</span></span>
5. <span data-ttu-id="e8bb9-180">IdentityMySQLDemo 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **참조, 솔루션, 프로젝트** 를 차례로 선택한 다음, 프로젝트를 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-180">Right click the IdentityMySQLDemo project, select **Add**, **Reference, Solution, Projects;** select the AspNet.Identity.MySQL project and click **OK**.</span></span>
6. <span data-ttu-id="e8bb9-181">IdentityMySQLDemo 프로젝트에서 다음에 대 한 모든 참조를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-181">In the IdentityMySQLDemo project, replace all references to</span></span>  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   <span data-ttu-id="e8bb9-182">다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-182">with</span></span>  
     `using AspNet.Identity.MySQL;`
7. <span data-ttu-id="e8bb9-183">IdentityModels.cs에서 **ApplicationDbContext** 를 **MySqlDatabase** 에서 파생 하도록 설정 하 고 연결 이름과 함께 단일 매개 변수를 사용 하는 생성자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-183">In IdentityModels.cs, set **ApplicationDbContext** to derive from **MySqlDatabase** and include a constructor that take a single parameter with the connection name.</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. <span data-ttu-id="e8bb9-184">IdentityConfig.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-184">Open the IdentityConfig.cs file.</span></span> <span data-ttu-id="e8bb9-185">**Applicationusermanager. Create** 메서드에서 usermanager 인스턴스화를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-185">In the **ApplicationUserManager.Create** method, replace instantiating UserManager with the following code:</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. <span data-ttu-id="e8bb9-186">Web.config 파일을 열고, 강조 표시 된 값을 이전 단계에서 만든 MySQL 데이터베이스의 연결 문자열로 대체 하 여 DefaultConnection 문자열을이 항목으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-186">Open the web.config file and replace the DefaultConnection string with this entry replacing the highlighted values with the connection string of the MySQL database you created on previous steps:</span></span>  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a><span data-ttu-id="e8bb9-187">앱을 실행 하 고 MySQL DB에 연결</span><span class="sxs-lookup"><span data-stu-id="e8bb9-187">Run the app and connect to the MySQL DB</span></span>

1. <span data-ttu-id="e8bb9-188">**IdentityMySQLDemo** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트로 설정** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-188">Right click the **IdentityMySQLDemo** project and select **Set as Startup Project**</span></span>
2. <span data-ttu-id="e8bb9-189">**Ctrl + F5** 키를 눌러 앱을 빌드하고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-189">Press **Ctrl + F5** to build and run the app.</span></span>
3. <span data-ttu-id="e8bb9-190">페이지 위쪽에서 **등록** 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-190">Click on **Register** tab on the top of the page.</span></span>
4. <span data-ttu-id="e8bb9-191">새 사용자 이름 및 암호를 입력 한 다음 **등록**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-191">Enter a new user name and password and then click on **Register**.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. <span data-ttu-id="e8bb9-192">이제 새 사용자가 등록 되 고 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-192">The new user is now registered and logged in.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. <span data-ttu-id="e8bb9-193">MySQL 워크 벤치 도구로 돌아가서 **IdentityMySQLDatabase** 테이블의 내용을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-193">Go back to the MySQL Workbench tool and inspect the **IdentityMySQLDatabase** table's contents.</span></span> <span data-ttu-id="e8bb9-194">새 사용자를 등록할 때 사용자 테이블에서 항목을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-194">Inspect the users table for the entries as you register new users.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a><span data-ttu-id="e8bb9-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8bb9-195">Next Steps</span></span>

<span data-ttu-id="e8bb9-196">이 앱에서 다른 인증 방법을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [Facebook 및 Google OAuth2 및 Openid connect sign-on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-196">For more information on how to enable other authentication methods on this app, refer to [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<span data-ttu-id="e8bb9-197">DB를 OAuth와 통합 하 고 사용자가 앱에 대 한 액세스를 제한 하도록 역할을 설정 하는 방법을 알아보려면 [멤버 자격, OAuth 및 SQL Database를 Azure에 배포 하는 Secure ASP.NET MVC 5 앱 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e8bb9-197">To learn how to integrate your DB with OAuth and to set up roles to limit users access to your app, see [Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>
