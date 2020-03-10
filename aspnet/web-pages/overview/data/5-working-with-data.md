---
uid: web-pages/overview/data/5-working-with-data
title: ASP.NET 웹 페이지 (Razor) 사이트에서 데이터베이스 작업 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 데이터베이스의 데이터에 액세스 하 고 ASP.NET 웹 페이지를 사용 하 여 표시 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 45e988d037465e59ad352bb9444af2c69fd3cd70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474041"
---
# <a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="0127d-103">ASP.NET 웹 페이지 (Razor) 사이트에서 데이터베이스 작업 소개</span><span class="sxs-lookup"><span data-stu-id="0127d-103">Introduction to Working with a Database in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="0127d-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0127d-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0127d-105">이 문서에서는 Microsoft WebMatrix 도구를 사용 하 여 Razor (ASP.NET 웹 페이지) 웹 사이트에서 데이터베이스를 만드는 방법과 데이터를 표시, 추가, 편집 및 삭제할 수 있는 페이지를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-105">This article describes how to use Microsoft WebMatrix tools to create a database in an ASP.NET Web Pages (Razor) website, and how to create pages that let you display, add, edit, and delete data.</span></span>
> 
> <span data-ttu-id="0127d-106">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="0127d-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="0127d-107">데이터베이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="0127d-107">How to create a database.</span></span>
> - <span data-ttu-id="0127d-108">데이터베이스에 연결 하는 방법</span><span class="sxs-lookup"><span data-stu-id="0127d-108">How to connect to a database.</span></span>
> - <span data-ttu-id="0127d-109">웹 페이지에 데이터를 표시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="0127d-109">How to display data in a web page.</span></span>
> - <span data-ttu-id="0127d-110">데이터베이스 레코드를 삽입, 업데이트 및 삭제 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-110">How to insert, update, and delete database records.</span></span>
> 
> <span data-ttu-id="0127d-111">다음은이 문서에 도입 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-111">These are the features introduced in the article:</span></span>
> 
> - <span data-ttu-id="0127d-112">Microsoft SQL Server Compact Edition 데이터베이스 작업</span><span class="sxs-lookup"><span data-stu-id="0127d-112">Working with a Microsoft SQL Server Compact Edition database.</span></span>
> - <span data-ttu-id="0127d-113">SQL 쿼리 작업</span><span class="sxs-lookup"><span data-stu-id="0127d-113">Working with SQL queries.</span></span>
> - <span data-ttu-id="0127d-114">`Database` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-114">The `Database` class.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="0127d-115">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="0127d-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="0127d-116">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="0127d-116">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="0127d-117">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="0127d-117">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="0127d-118">이 자습서는 WebMatrix 3 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-118">This tutorial also works with WebMatrix 3.</span></span> <span data-ttu-id="0127d-119">ASP.NET 웹 페이지 3과 Visual Studio 2013 (또는 웹의 경우 2013 Visual Studio Express)를 사용할 수 있습니다. 그러나 사용자 인터페이스는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-119">You can use ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web); however, the user interface will be different.</span></span>

## <a name="introduction-to-databases"></a><span data-ttu-id="0127d-120">데이터베이스 소개</span><span class="sxs-lookup"><span data-stu-id="0127d-120">Introduction to Databases</span></span>

<span data-ttu-id="0127d-121">일반적인 주소록을 상상해 보세요.</span><span class="sxs-lookup"><span data-stu-id="0127d-121">Imagine a typical address book.</span></span> <span data-ttu-id="0127d-122">주소록의 각 항목에 대해 (즉, 각 사람에 대 한) 이름, 성, 주소, 전자 메일 주소 및 전화 번호와 같은 여러 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-122">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

<span data-ttu-id="0127d-123">이와 같이 데이터를 그림 하는 일반적인 방법은 행과 열이 있는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-123">A typical way to picture data like this is as a table with rows and columns.</span></span> <span data-ttu-id="0127d-124">데이터베이스 용어로 각 행을 레코드 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-124">In database terms, each row is often referred to as a record.</span></span> <span data-ttu-id="0127d-125">각 열 (필드 라고도 함)에는 각 데이터 형식에 대 한 값 (이름, 성 등)이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-125">Each column (sometimes referred to as fields) contains a value for each type of data: first name, last name, and so on.</span></span>

| <span data-ttu-id="0127d-126">**ID**</span><span class="sxs-lookup"><span data-stu-id="0127d-126">**ID**</span></span> | <span data-ttu-id="0127d-127">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="0127d-127">**FirstName**</span></span> | <span data-ttu-id="0127d-128">**LastName**</span><span class="sxs-lookup"><span data-stu-id="0127d-128">**LastName**</span></span> | <span data-ttu-id="0127d-129">**주소**</span><span class="sxs-lookup"><span data-stu-id="0127d-129">**Address**</span></span> | <span data-ttu-id="0127d-130">**Email**</span><span class="sxs-lookup"><span data-stu-id="0127d-130">**Email**</span></span> | <span data-ttu-id="0127d-131">**전화**</span><span class="sxs-lookup"><span data-stu-id="0127d-131">**Phone**</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0127d-132">1</span><span class="sxs-lookup"><span data-stu-id="0127d-132">1</span></span> | <span data-ttu-id="0127d-133">Jim</span><span class="sxs-lookup"><span data-stu-id="0127d-133">Jim</span></span> | <span data-ttu-id="0127d-134">Abrus</span><span class="sxs-lookup"><span data-stu-id="0127d-134">Abrus</span></span> | <span data-ttu-id="0127d-135">210 100th St SE Orcas WA 98031</span><span class="sxs-lookup"><span data-stu-id="0127d-135">210 100th St SE Orcas WA 98031</span></span> | jim@contoso.com | <span data-ttu-id="0127d-136">555 0100</span><span class="sxs-lookup"><span data-stu-id="0127d-136">555 0100</span></span> |
| <span data-ttu-id="0127d-137">2</span><span class="sxs-lookup"><span data-stu-id="0127d-137">2</span></span> | <span data-ttu-id="0127d-138">Terry</span><span class="sxs-lookup"><span data-stu-id="0127d-138">Terry</span></span> | <span data-ttu-id="0127d-139">Adams</span><span class="sxs-lookup"><span data-stu-id="0127d-139">Adams</span></span> | <span data-ttu-id="0127d-140">1234 Main St. Seattle WA 99011</span><span class="sxs-lookup"><span data-stu-id="0127d-140">1234 Main St. Seattle WA 99011</span></span> | terry@cohowinery.com | <span data-ttu-id="0127d-141">555 0101</span><span class="sxs-lookup"><span data-stu-id="0127d-141">555 0101</span></span> |

<span data-ttu-id="0127d-142">대부분의 데이터베이스 테이블에 대해 테이블에는 고객 번호, 계좌 번호 등과 같은 고유 식별자가 포함 된 열이 있어야 합니다. 이를 테이블의 *기본 키*라고 하며 테이블의 각 행을 식별 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-142">For most database tables, the table has to have a column that contains a unique identifier, like a customer number, account number, etc. This is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="0127d-143">이 예에서 ID 열은 주소록의 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-143">In the example, the ID column is the primary key for the address book.</span></span>

<span data-ttu-id="0127d-144">데이터베이스에 대 한 기본적인 이해를 통해 간단한 데이터베이스를 만들고 데이터 추가, 수정 및 삭제와 같은 작업을 수행 하는 방법을 배울 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-144">With this basic understanding of databases, you're ready to learn how to create a simple database and perform operations such as adding, modifying, and deleting data.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="0127d-145">**관계형 데이터베이스**</span><span class="sxs-lookup"><span data-stu-id="0127d-145">**Relational Databases**</span></span>
> 
> <span data-ttu-id="0127d-146">텍스트 파일 및 스프레드시트를 비롯 한 다양 한 방법으로 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-146">You can store data in lots of ways, including text files and spreadsheets.</span></span> <span data-ttu-id="0127d-147">그러나 대부분의 비즈니스에서는 데이터가 관계형 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-147">For most business uses, though, data is stored in a relational database.</span></span>
> 
> <span data-ttu-id="0127d-148">이 문서는 데이터베이스에 대해 그다지 복잡 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-148">This article doesn't go very deeply into databases.</span></span> <span data-ttu-id="0127d-149">그러나이에 대 한 이해를 최소화 하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-149">However, you might find it useful to understand a little about them.</span></span> <span data-ttu-id="0127d-150">관계형 데이터베이스에서 정보는 논리적으로 개별 테이블로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-150">In a relational database, information is logically divided into separate tables.</span></span> <span data-ttu-id="0127d-151">예를 들어 school 데이터베이스에는 학생 및 수업 제공을 위한 별도의 테이블이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-151">For example, a database for a school might contain separate tables for students and for class offerings.</span></span> <span data-ttu-id="0127d-152">데이터베이스 소프트웨어 (예: SQL Server)는 테이블 간의 관계를 동적으로 설정할 수 있는 강력한 명령을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-152">The database software (such as SQL Server) supports powerful commands that let you dynamically establish relationships between the tables.</span></span> <span data-ttu-id="0127d-153">예를 들어 관계형 데이터베이스를 사용 하 여 일정을 만들기 위해 학생 및 수업 간의 논리적 관계를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-153">For example, you can use the relational database to establish a logical relationship between students and classes in order to create a schedule.</span></span> <span data-ttu-id="0127d-154">별도의 테이블에 데이터를 저장 하면 테이블 구조의 복잡성이 줄어들고 테이블에 중복 데이터를 보관할 필요성이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-154">Storing data in separate tables reduces the complexity of the table structure and reduces the need to keep redundant data in tables.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="0127d-155">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="0127d-155">Creating a Database</span></span>

<span data-ttu-id="0127d-156">이 절차에서는 WebMatrix에 포함 된 SQL Server Compact 데이터베이스 디자인 도구를 사용 하 여 SmallBakery 라는 데이터베이스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-156">This procedure shows you how to create a database named SmallBakery by using the SQL Server Compact Database design tool that's included in WebMatrix.</span></span> <span data-ttu-id="0127d-157">코드를 사용 하 여 데이터베이스를 만들 수 있지만 WebMatrix와 같은 디자인 도구를 사용 하 여 데이터베이스와 데이터베이스 테이블을 만드는 것이 더 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-157">Although you can create a database using code, it's more typical to create the database and database tables using a design tool like WebMatrix.</span></span>

1. <span data-ttu-id="0127d-158">WebMatrix를 시작 하 고 빠른 시작 페이지에서 **템플릿에서 사이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-158">Start WebMatrix, and on the Quick Start page, click **Site From Template**.</span></span>
2. <span data-ttu-id="0127d-159">**빈 사이트**를 선택 하 고 **사이트 이름** 상자에 "SmallBakery"를 입력 한 다음 **확인을**클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-159">Select **Empty Site**, and in the **Site Name** box enter "SmallBakery" and then click **OK**.</span></span> <span data-ttu-id="0127d-160">사이트가 만들어지고 WebMatrix에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-160">The site is created and displayed in WebMatrix.</span></span>
3. <span data-ttu-id="0127d-161">왼쪽 창에서 **데이터베이스** 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-161">In the left pane, click the **Databases** workspace.</span></span>
4. <span data-ttu-id="0127d-162">리본에서 **새 데이터베이스**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-162">In the ribbon, click **New Database**.</span></span> <span data-ttu-id="0127d-163">사이트와 같은 이름을 사용 하 여 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-163">An empty database is created with the same name as your site.</span></span>
5. <span data-ttu-id="0127d-164">왼쪽 창에서 **SmallBakery** 노드를 확장 한 다음 **테이블**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-164">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
6. <span data-ttu-id="0127d-165">리본에서 **새 테이블**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-165">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="0127d-166">WebMatrix 테이블 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-166">WebMatrix opens the table designer.</span></span>

    ![[이미지]](5-working-with-data/_static/image1.jpg)
7. <span data-ttu-id="0127d-168">**이름** 열을 클릭 하 고 &quot;Id&quot;을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-168">Click in the **Name** column and enter &quot;Id&quot;.</span></span>
8. <span data-ttu-id="0127d-169">**데이터 형식** 열에서 **int**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-169">In the **Data Type** column, select **int**.</span></span>
9. <span data-ttu-id="0127d-170">**기본 키** 로 설정 하 고 **확인?** 옵션을 **예**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-170">Set the **Is Primary Key?** and **Is Identify?** options to **Yes**.</span></span>

    <span data-ttu-id="0127d-171">이름에서 알 수 있듯이 **은 기본 키** 로 데이터베이스에 테이블의 기본 키가 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-171">As the name suggests, **Is Primary Key** tells the database that this will be the table's primary key.</span></span> <span data-ttu-id="0127d-172">**Id는** 데이터베이스에 모든 새 레코드에 대 한 ID 번호를 자동으로 만들고 1부터 시작 하 여 다음 일련 번호를 할당 하도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-172">**Is Identity** tells the database to automatically create an ID number for every new record and to assign it the next sequential number (starting at 1).</span></span>
10. <span data-ttu-id="0127d-173">다음 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-173">Click in the next row.</span></span> <span data-ttu-id="0127d-174">편집기에서 새 열 정의를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-174">The editor starts a new column definition.</span></span>
11. <span data-ttu-id="0127d-175">이름 값에&quot;&quot;이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-175">For the Name value, enter &quot;Name&quot;.</span></span>
12. <span data-ttu-id="0127d-176">**데이터 형식**에서 &quot;nvarchar&quot;를 선택 하 고 길이를 50으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-176">For **Data Type**, choose &quot;nvarchar&quot; and set the length to 50.</span></span> <span data-ttu-id="0127d-177">`nvarchar`의 *var* 부분은이 열에 대 한 데이터가 레코드에 대 한 레코드에 따라 달라질 수 있는 문자열이 되도록 데이터베이스에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-177">The *var* part of `nvarchar` tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="0127d-178">*N* 접두사는 *국가*를 나타내며,이 필드는 영문자 또는 쓰기 시스템 &#8212; 을 나타내는 문자 데이터를 보유할 수 있습니다. 즉, 필드에 유니코드 데이터가 포함 되어 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-178">(The *n* prefix represents *national*, indicating that the field can hold character data that represents any alphabet or writing system &#8212; that is, that the field holds Unicode data.)</span></span>
13. <span data-ttu-id="0127d-179">**Null 허용** 옵션을 **아니요**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-179">Set the **Allow Nulls** option to **No**.</span></span> <span data-ttu-id="0127d-180">이렇게 하면 *이름* 열이 비어 있지 않은 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-180">This will enforce that the *Name* column is not left blank.</span></span>
14. <span data-ttu-id="0127d-181">이와 동일한 프로세스를 사용 하 여 *Description*이라는 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-181">Using this same process, create a column named *Description*.</span></span> <span data-ttu-id="0127d-182">**데이터 형식을** "nvarchar"로 설정 하 고 길이를 50로 설정 하 고 **null 허용** 을 false로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-182">Set **Data Type** to "nvarchar" and 50 for the length, and set **Allow Nulls** to false.</span></span>
15. <span data-ttu-id="0127d-183">*Price*라는 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-183">Create a column named *Price*.</span></span> <span data-ttu-id="0127d-184">**데이터 형식을 "money"로** 설정 하 고 **null 허용** 을 false로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-184">Set **Data Type to "money"** and set **Allow Nulls** to false.</span></span>
16. <span data-ttu-id="0127d-185">맨 위에 있는 상자에서 Product&quot;&quot;테이블 이름을로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-185">In the box at the top, name the table &quot;Product&quot;.</span></span>

    <span data-ttu-id="0127d-186">완료 되 면 정의가 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-186">When you're done, the definition will look like this:</span></span>

    ![[이미지]](5-working-with-data/_static/image2.png)
17. <span data-ttu-id="0127d-188">Ctrl + S를 눌러 테이블을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-188">Press Ctrl+S to save the table.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="0127d-189">데이터베이스에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="0127d-189">Adding Data to the Database</span></span>

<span data-ttu-id="0127d-190">이제이 문서의 뒷부분에서 작업할 몇 가지 샘플 데이터를 데이터베이스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-190">Now you can add some sample data to your database that you'll work with later in the article.</span></span>

1. <span data-ttu-id="0127d-191">왼쪽 창에서 **SmallBakery** 노드를 확장 한 다음 **테이블**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-191">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
2. <span data-ttu-id="0127d-192">Product 테이블을 마우스 오른쪽 단추로 클릭 한 다음 **데이터**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-192">Right-click the Product table and then click **Data**.</span></span>
3. <span data-ttu-id="0127d-193">편집 창에서 다음 레코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-193">In the edit pane, enter the following records:</span></span>

    | <span data-ttu-id="0127d-194">**이름**</span><span class="sxs-lookup"><span data-stu-id="0127d-194">**Name**</span></span> | <span data-ttu-id="0127d-195">**설명**</span><span class="sxs-lookup"><span data-stu-id="0127d-195">**Description**</span></span> | <span data-ttu-id="0127d-196">**Price**</span><span class="sxs-lookup"><span data-stu-id="0127d-196">**Price**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="0127d-197">빵</span><span class="sxs-lookup"><span data-stu-id="0127d-197">Bread</span></span> | <span data-ttu-id="0127d-198">매일 새로 구운.</span><span class="sxs-lookup"><span data-stu-id="0127d-198">Baked fresh every day.</span></span> | <span data-ttu-id="0127d-199">2.99</span><span class="sxs-lookup"><span data-stu-id="0127d-199">2.99</span></span> |
    | <span data-ttu-id="0127d-200">Strawberry 디저트</span><span class="sxs-lookup"><span data-stu-id="0127d-200">Strawberry Shortcake</span></span> | <span data-ttu-id="0127d-201">유기적 딸기를 사용 하 여 정원에서 만든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-201">Made with organic strawberries from our garden.</span></span> | <span data-ttu-id="0127d-202">9.99</span><span class="sxs-lookup"><span data-stu-id="0127d-202">9.99</span></span> |
    | <span data-ttu-id="0127d-203">Apple 원형</span><span class="sxs-lookup"><span data-stu-id="0127d-203">Apple Pie</span></span> | <span data-ttu-id="0127d-204">두 번째는 mom 원형에만 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-204">Second only to your mom's pie.</span></span> | <span data-ttu-id="0127d-205">12.99</span><span class="sxs-lookup"><span data-stu-id="0127d-205">12.99</span></span> |
    | <span data-ttu-id="0127d-206">Pecan 원형</span><span class="sxs-lookup"><span data-stu-id="0127d-206">Pecan Pie</span></span> | <span data-ttu-id="0127d-207">Pecans 마음에 들면이는 사용자를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-207">If you like pecans, this is for you.</span></span> | <span data-ttu-id="0127d-208">10.99</span><span class="sxs-lookup"><span data-stu-id="0127d-208">10.99</span></span> |
    | <span data-ttu-id="0127d-209">레몬 원형</span><span class="sxs-lookup"><span data-stu-id="0127d-209">Lemon Pie</span></span> | <span data-ttu-id="0127d-210">세계 최고의 lemons.</span><span class="sxs-lookup"><span data-stu-id="0127d-210">Made with the best lemons in the world.</span></span> | <span data-ttu-id="0127d-211">11.99</span><span class="sxs-lookup"><span data-stu-id="0127d-211">11.99</span></span> |
    | <span data-ttu-id="0127d-212">컵케이크</span><span class="sxs-lookup"><span data-stu-id="0127d-212">Cupcakes</span></span> | <span data-ttu-id="0127d-213">어린이와 어린이는이를 좋아합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-213">Your kids and the kid in you will love these.</span></span> | <span data-ttu-id="0127d-214">7.99</span><span class="sxs-lookup"><span data-stu-id="0127d-214">7.99</span></span> |

    <span data-ttu-id="0127d-215">*Id* 열에는 아무것도 입력할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-215">Remember that you don't have to enter anything for the *Id* column.</span></span> <span data-ttu-id="0127d-216">*Id* 열을 만들 때 **Is Identity** 속성을 true로 설정 하면 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-216">When you created the *Id* column, you set its **Is Identity** property to true, which causes it to automatically be filled in.</span></span>

    <span data-ttu-id="0127d-217">데이터 입력을 마치면 테이블 디자이너는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-217">When you're finished entering the data, the table designer will look like this:</span></span>

    ![[이미지]](5-working-with-data/_static/image3.jpg)
4. <span data-ttu-id="0127d-219">데이터베이스 데이터를 포함 하는 탭을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-219">Close the tab that contains the database data.</span></span>

## <a name="displaying-data-from-a-database"></a><span data-ttu-id="0127d-220">데이터베이스에서 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="0127d-220">Displaying Data from a Database</span></span>

<span data-ttu-id="0127d-221">데이터를 포함 하는 데이터베이스가 있으면 ASP.NET 웹 페이지에 데이터를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-221">Once you've got a database with data in it, you can display the data in an ASP.NET web page.</span></span> <span data-ttu-id="0127d-222">표시할 테이블 행을 선택 하려면 데이터베이스에 전달 하는 명령에 해당 하는 SQL 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-222">To select the table rows to display, you use a SQL statement, which is a command that you pass to the database.</span></span>

1. <span data-ttu-id="0127d-223">왼쪽 창에서 **파일** 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-223">In the left pane, click the **Files** workspace.</span></span>
2. <span data-ttu-id="0127d-224">웹 사이트의 루트에서 *Listproducts. cshtml*이라는 새 CSHTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-224">In the root of the website, create a new CSHTML page named *ListProducts.cshtml*.</span></span>
3. <span data-ttu-id="0127d-225">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-225">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    <span data-ttu-id="0127d-226">첫 번째 코드 블록에서 이전에 만든 *SmallBakery* 파일 (데이터베이스)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-226">In the first code block, you open the *SmallBakery.sdf* file (database) that you created earlier.</span></span> <span data-ttu-id="0127d-227">`Database.Open` 메서드는 *.sdf* 파일이 웹 사이트의 *앱\_데이터* 폴더에 있는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-227">The `Database.Open` method assumes that the *.sdf* file is in your website's *App\_Data* folder.</span></span> <span data-ttu-id="0127d-228">실제로 *.sdf* 확장명 &#8212; 을 지정할 필요는 없습니다. 이렇게 하면 `Open` 방법이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-228">(Notice that you don't need to specify the *.sdf* extension &#8212; in fact, if you do, the `Open` method won't work.)</span></span>

    > [!NOTE]
    > <span data-ttu-id="0127d-229">*앱\_데이터* 폴더는 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-229">The *App\_Data* folder is a special folder in ASP.NET that's used to store data files.</span></span> <span data-ttu-id="0127d-230">자세한 내용은이 문서의 뒷부분에 나오는 [데이터베이스에 연결](#SB_ConnectingToADatabase) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0127d-230">For more information, see [Connecting to a Database](#SB_ConnectingToADatabase) later in this article.</span></span>

    <span data-ttu-id="0127d-231">그런 다음, 다음 SQL `Select` 문을 사용 하 여 데이터베이스 쿼리 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-231">You then make a request to query the database using the following SQL `Select` statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    <span data-ttu-id="0127d-232">문에서 `Product`는 쿼리할 테이블을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-232">In the statement, `Product` identifies the table to query.</span></span> <span data-ttu-id="0127d-233">`*` 문자는 쿼리에서 테이블의 모든 열을 반환 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-233">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="0127d-234">열을 일부만 표시 하려는 경우 열을 쉼표로 구분 하 여 나열할 수도 있습니다. `Order By` 절은 *이름* 열을 기준으로이 경우 &#8212; 데이터를 정렬 하는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-234">(You could also list columns individually, separated by commas, if you wanted to see only some of the columns.) The `Order By` clause indicates how the data should be sorted &#8212; in this case, by the *Name* column.</span></span> <span data-ttu-id="0127d-235">즉, 각 행에 대 한 *Name* 열의 값을 기준으로 데이터를 사전순으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-235">This means that the data is sorted alphabetically based on the value of the *Name* column for each row.</span></span>

    <span data-ttu-id="0127d-236">페이지 본문에서 태그는 데이터를 표시 하는 데 사용 되는 HTML 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-236">In the body of the page, the markup creates an HTML table that will be used to display the data.</span></span> <span data-ttu-id="0127d-237">`<tbody>` 요소 내에서 `foreach` 루프를 사용 하 여 쿼리에서 반환 되는 각 데이터 행을 개별적으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-237">Inside the `<tbody>` element, you use a `foreach` loop to individually get each data row that's returned by the query.</span></span> <span data-ttu-id="0127d-238">각 데이터 행에 대해 HTML 테이블 행 (`<tr>` 요소)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-238">For each data row, you create an HTML table row (`<tr>` element).</span></span> <span data-ttu-id="0127d-239">그런 다음 각 열에 대해 HTML 테이블 셀 (`<td>` 요소)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-239">Then you create HTML table cells (`<td>` elements) for each column.</span></span> <span data-ttu-id="0127d-240">루프를 진행할 때마다 데이터베이스에서 사용할 수 있는 다음 행이 `row` 변수에 있습니다 (`foreach` 문에서이를 설정).</span><span class="sxs-lookup"><span data-stu-id="0127d-240">Each time you go through the loop, the next available row from the database is in the `row` variable (you set this up in the `foreach` statement).</span></span> <span data-ttu-id="0127d-241">행에서 개별 열을 가져오기 위해 `row.Name` 또는 `row.Description` 또는 원하는 열 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-241">To get an individual column from the row, you can use `row.Name` or `row.Description` or whatever the name is of the column you want.</span></span>
4. <span data-ttu-id="0127d-242">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-242">Run the page in a browser.</span></span> <span data-ttu-id="0127d-243">(파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 이 페이지에는 다음과 같은 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-243">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays a list like the following:</span></span>

    ![[이미지]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="0127d-245">**SQL(구조적 쿼리 언어)**</span><span class="sxs-lookup"><span data-stu-id="0127d-245">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="0127d-246">SQL은 데이터베이스에서 데이터를 관리 하기 위한 대부분의 관계형 데이터베이스에 사용 되는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-246">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="0127d-247">여기에는 데이터를 검색 하 고 업데이트 하는 데 사용할 수 있는 명령이 포함 되어 있으며,이를 통해 데이터베이스 테이블을 만들고 수정 하 고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-247">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage database tables.</span></span> <span data-ttu-id="0127d-248">Sql은 SQL을 사용 하 여 사용자가 원하는 것을 데이터베이스에 알려 주므로 데이터를 가져오는 방법이 나 작업을 수행 하는 방법을 파악 하기 위한 데이터베이스 작업 이라는 점을 제외 하 고, sql은 WebMatrix에서 사용 중인 프로그래밍 언어와는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-248">SQL is different than a programming language (like the one you're using in WebMatrix) because with SQL, the idea is that you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="0127d-249">다음은 몇 가지 SQL 명령의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-249">Here are examples of some SQL commands and what they do:</span></span>
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="0127d-250">*Price* 값이 10 보다 많은 경우 *Product* 테이블의 레코드에서 *Id*, *이름*및 *가격* 열을 페치하고 *이름* 열의 값을 기준으로 결과를 사전순으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-250">This fetches the *Id*, *Name*, and *Price* columns from records in the *Product* table if the value of *Price* is more than 10, and returns the results in alphabetical order based on the values of the *Name* column.</span></span> <span data-ttu-id="0127d-251">이 명령은 조건을 충족 하는 레코드를 포함 하는 결과 집합을 반환 하거나, 일치 하는 레코드가 없는 경우 빈 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-251">This command will return a result set that contains the records that meet the criteria, or an empty set if no records match.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> <span data-ttu-id="0127d-252">*Product* 테이블에 새 레코드를 삽입 하 고 *Name* 열을 &quot;크 라 상&quot;로 설정 하 고 *설명* 열에 부실 즐거움&quot;를 &quot;하 고 price를 1.99으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-252">This inserts a new record into the *Product* table, setting the *Name* column to &quot;Croissant&quot;, the *Description* column to &quot;A flaky delight&quot;, and the price to 1.99.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> <span data-ttu-id="0127d-253">이 명령은 만료 날짜 열이 2008 년 1 월 1 일 이전인 *Product* 테이블의 레코드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-253">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="0127d-254">이 경우 *Product* 테이블에 이러한 열이 있다고 가정 합니다. 날짜는 여기에 MM/DD/YYYY 형식으로 입력 되지만 로캘에 사용 되는 형식으로 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-254">(This assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="0127d-255">`Insert Into` 및 `Delete` 명령은 결과 집합을 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-255">The `Insert Into` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="0127d-256">대신 명령의 영향을 받은 레코드 수를 나타내는 숫자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-256">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="0127d-257">이러한 작업 중 일부 (예: 레코드 삽입 및 삭제)의 경우 작업을 요청 하는 프로세스에 데이터베이스에 대 한 적절 한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-257">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="0127d-258">따라서 프로덕션 데이터베이스의 경우 데이터베이스에 연결할 때 사용자 이름과 암호를 제공 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-258">This is why for production databases you often have to supply a username and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="0127d-259">수십 개의 SQL 명령이 있지만 모두 이와 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-259">There are dozens of SQL commands, but they all follow a pattern like this.</span></span> <span data-ttu-id="0127d-260">SQL 명령을 사용 하 여 데이터베이스 테이블을 만들고, 테이블의 레코드 수를 계산 하 고, 가격을 계산 하 고, 더 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-260">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>

## <a name="inserting-data-in-a-database"></a><span data-ttu-id="0127d-261">데이터베이스에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="0127d-261">Inserting Data in a Database</span></span>

<span data-ttu-id="0127d-262">이 섹션에서는 사용자가 *제품* 데이터베이스 테이블에 새 제품을 추가할 수 있는 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-262">This section shows how to create a page that lets users add a new product to the *Product* database table.</span></span> <span data-ttu-id="0127d-263">새 제품 레코드를 삽입 한 후에는 이전 섹션에서 만든 *Listproducts. cshtml* 페이지를 사용 하 여 업데이트 된 테이블이 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-263">After a new product record is inserted, the page displays the updated table using the *ListProducts.cshtml* page that you created in the previous section.</span></span>

<span data-ttu-id="0127d-264">이 페이지에는 사용자가 입력 하는 데이터가 데이터베이스에 대해 유효한 지 확인 하기 위한 유효성 검사가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-264">The page includes validation to make sure that the data that the user enters is valid for the database.</span></span> <span data-ttu-id="0127d-265">예를 들어 페이지의 코드를 사용 하면 모든 필수 열에 대해 값이 입력 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-265">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>

1. <span data-ttu-id="0127d-266">웹 사이트에서 이름이 *Insertproducts. cshtml*인 새 CSHTML 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-266">In the website, create a new CSHTML file named *InsertProducts.cshtml*.</span></span>
2. <span data-ttu-id="0127d-267">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-267">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    <span data-ttu-id="0127d-268">페이지 본문에는 사용자가 이름, 설명 및 가격을 입력할 수 있는 세 개의 텍스트 상자를 포함 하는 HTML 폼이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-268">The body of the page contains an HTML form with three text boxes that let users enter a name, description, and price.</span></span> <span data-ttu-id="0127d-269">사용자가 **삽입** 단추를 클릭 하면 페이지 맨 위에 있는 코드가 *SmallBakery* 데이터베이스에 대 한 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-269">When users click the **Insert** button, the code at the top of the page opens a connection to the *SmallBakery.sdf* database.</span></span> <span data-ttu-id="0127d-270">그런 다음 `Request` 개체를 사용 하 여 사용자가 제출한 값을 가져와 로컬 변수에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-270">You then get the values that the user has submitted by using the `Request` object and assign those values to local variables.</span></span>

    <span data-ttu-id="0127d-271">사용자가 각 필수 열에 대 한 값을 입력 했는지 확인 하려면 유효성 검사를 수행 하려는 각 `<input>` 요소를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-271">To validate that the user entered a value for each required column, you register each `<input>` element that you want to validate:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    <span data-ttu-id="0127d-272">`Validation` 도우미는 등록 한 각 필드에 값이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-272">The `Validation` helper checks that there is a value in each of the fields that you've registered.</span></span> <span data-ttu-id="0127d-273">사용자가 가져오는 정보를 처리 하기 전에 일반적으로 수행 하는 `Validation.IsValid()`를 확인 하 여 모든 필드가 유효성 검사를 통과 했는지 여부를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-273">You can test whether all the fields passed validation by checking `Validation.IsValid()`, which you typically do before you process the information you get from the user:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    <span data-ttu-id="0127d-274">`&&` 연산자는 및를 의미 합니다 .이 테스트는 *이 형식이 양식 전송 이며 모든 필드가 유효성 검사를 통과 한 경우*에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-274">(The `&&` operator means AND — this test is *If this is a form submission AND all the fields have passed validation*.)</span></span>

    <span data-ttu-id="0127d-275">유효성을 검사 한 모든 열이 비어 있지 않은 경우 계속 진행 하 여 데이터를 삽입 하는 SQL 문을 만들고 다음 그림과 같이 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-275">If all the columns validated (none were empty), you go ahead and create a SQL statement to insert the data and then execute it as shown next:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    <span data-ttu-id="0127d-276">삽입할 값에 대 한 매개 변수 자리 표시자 (`@0`, `@1`, `@2`)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-276">For the values to insert, you include parameter placeholders (`@0`, `@1`, `@2`).</span></span>

    > [!NOTE]
    > <span data-ttu-id="0127d-277">보안 예방 조치로, 앞의 예제에서와 같이 매개 변수를 사용 하 여 항상 값을 SQL 문에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-277">As a security precaution, always pass values to a SQL statement using parameters, as you see in the preceding example.</span></span> <span data-ttu-id="0127d-278">이렇게 하면 사용자 데이터의 유효성을 검사할 수 있을 뿐만 아니라 데이터베이스에 악성 명령을 전송 하려는 시도를 방지할 수 있습니다 (종종 SQL 삽입 공격 이라고 함).</span><span class="sxs-lookup"><span data-stu-id="0127d-278">This gives you a chance to validate the user's data, plus it helps protect against attempts to send malicious commands to your database (sometimes referred to as SQL injection attacks).</span></span>

    <span data-ttu-id="0127d-279">쿼리를 실행 하려면이 문을 사용 하 여 자리 표시자를 대체할 값을 포함 하는 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-279">To execute the query, you use this statement, passing to it the variables that contain the values to substitute for the placeholders:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    <span data-ttu-id="0127d-280">`Insert Into` 문을 실행 한 후에는 다음 줄을 사용 하 여 제품을 나열 하는 페이지로 사용자를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-280">After the `Insert Into` statement has executed, you send the user to the page that lists the products using this line:</span></span>

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    <span data-ttu-id="0127d-281">유효성 검사가 성공 하지 못한 경우 삽입을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-281">If validation didn't succeed, you skip the insert.</span></span> <span data-ttu-id="0127d-282">대신 누적 된 오류 메시지 (있는 경우)를 표시할 수 있는 도우미가 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-282">Instead, you have a helper in the page that can display the accumulated error messages (if any):</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    <span data-ttu-id="0127d-283">태그의 스타일 블록에는 `.validation-summary-errors`라는 CSS 클래스 정의가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-283">Notice that the style block in the markup includes a CSS class definition named `.validation-summary-errors`.</span></span> <span data-ttu-id="0127d-284">유효성 검사 오류를 포함 하는 `<div>` 요소에 대해 기본적으로 사용 되는 CSS 클래스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-284">This is the name of the CSS class that's used by default for the `<div>` element that contains any validation errors.</span></span> <span data-ttu-id="0127d-285">이 경우 CSS 클래스는 유효성 검사 요약 오류가 빨강 및 굵게 표시 되도록 지정 하지만 원하는 서식을 표시 하는 `.validation-summary-errors` 클래스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-285">In this case, the CSS class specifies that validation summary errors are displayed in red and in bold, but you can define the `.validation-summary-errors` class to display any formatting you like.</span></span>

### <a name="testing-the-insert-page"></a><span data-ttu-id="0127d-286">삽입 페이지 테스트</span><span class="sxs-lookup"><span data-stu-id="0127d-286">Testing the Insert Page</span></span>

1. <span data-ttu-id="0127d-287">브라우저에서 페이지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-287">View the page in a browser.</span></span> <span data-ttu-id="0127d-288">이 페이지에는 다음 그림에 표시 된 것과 비슷한 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-288">The page displays a form that's similar to the one that's shown in the following illustration.</span></span>

    ![[이미지]](5-working-with-data/_static/image5.jpg)
2. <span data-ttu-id="0127d-290">모든 열에 대 한 값을 입력 하 고 *Price* 열을 비워 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-290">Enter values for all the columns, but make sure that you leave the *Price* column blank.</span></span>
3. <span data-ttu-id="0127d-291">**삽입**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-291">Click **Insert**.</span></span> <span data-ttu-id="0127d-292">다음 그림과 같이 페이지에 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-292">The page displays an error message, as shown in the following illustration.</span></span> <span data-ttu-id="0127d-293">새 레코드가 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-293">(No new record is created.)</span></span>

    ![[이미지]](5-working-with-data/_static/image6.jpg)
4. <span data-ttu-id="0127d-295">양식을 완전히 채운 다음 **삽입**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-295">Fill the form out completely, and then click **Insert**.</span></span> <span data-ttu-id="0127d-296">이번에는 *Listproducts. cshtml* 페이지가 표시 되 고 새 레코드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-296">This time, the *ListProducts.cshtml* page is displayed and shows the new record.</span></span>

## <a name="updating-data-in-a-database"></a><span data-ttu-id="0127d-297">데이터베이스의 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="0127d-297">Updating Data in a Database</span></span>

<span data-ttu-id="0127d-298">테이블에 데이터를 입력 한 후에는 업데이트 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-298">After data has been entered into a table, you might need to update it.</span></span> <span data-ttu-id="0127d-299">이 절차에서는 앞에서 데이터 삽입을 위해 만든 페이지와 유사한 두 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-299">This procedure shows you how to create two pages that are similar to the ones you created for data insertion earlier.</span></span> <span data-ttu-id="0127d-300">첫 번째 페이지에는 제품이 표시 되 고 사용자가 변경할 항목을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-300">The first page displays products and lets users select one to change.</span></span> <span data-ttu-id="0127d-301">두 번째 페이지에서는 사용자가 실제로 편집을 수행 하 고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-301">The second page lets the users actually make the edits and save them.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="0127d-302">**중요** 프로덕션 웹 사이트에서는 일반적으로 데이터를 변경할 수 있는 사용자를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-302">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="0127d-303">멤버 자격을 설정 하는 방법과 사용자에 게 사이트에서 작업을 수행할 수 있는 권한을 부여 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격 추가](https://go.microsoft.com/fwlink/?LinkId=202904)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0127d-303">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="0127d-304">웹 사이트에서 이름이 *Editproducts. cshtml*인 새 CSHTML 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-304">In the website, create a new CSHTML file named *EditProducts.cshtml*.</span></span>
2. <span data-ttu-id="0127d-305">파일의 기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-305">Replace the existing markup in the file with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    <span data-ttu-id="0127d-306">이 페이지와 이전 페이지의 *Listproducts* 의 유일한 차이점은이 페이지의 HTML 테이블에 **편집** 링크를 표시 하는 추가 열이 포함 되어 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-306">The only difference between this page and the *ListProducts.cshtml* page from earlier is that the HTML table in this page includes an extra column that displays an **Edit** link.</span></span> <span data-ttu-id="0127d-307">이 링크를 클릭 하면 선택한 레코드를 편집할 수 있는 *Updateproducts. cshtml 페이지로 이동 합니다.*</span><span class="sxs-lookup"><span data-stu-id="0127d-307">When you click this link, it takes you to the *UpdateProducts.cshtml* page (which you'll create next) where you can edit the selected record.</span></span>

    <span data-ttu-id="0127d-308">**편집** 링크를 만드는 코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-308">Look at the code that creates the **Edit** link:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    <span data-ttu-id="0127d-309">이렇게 하면 `href` 특성이 동적으로 설정 되는 HTML `<a>` 요소가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-309">This creates an HTML `<a>` element whose `href` attribute is set dynamically.</span></span> <span data-ttu-id="0127d-310">`href` 특성은 사용자가 링크를 클릭할 때 표시할 페이지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-310">The `href` attribute specifies the page to display when the user clicks the link.</span></span> <span data-ttu-id="0127d-311">또한 현재 행의 `Id` 값을 링크에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-311">It also passes the `Id` value of the current row to the link.</span></span> <span data-ttu-id="0127d-312">페이지가 실행 될 때 페이지 소스에는 다음과 같은 링크가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-312">When the page runs, the page source might contain links like these:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    <span data-ttu-id="0127d-313">`href` 특성은 `UpdateProducts/n`으로 설정 되어 있습니다. 여기서 *n* 은 제품 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-313">Notice that the `href` attribute is set to `UpdateProducts/n`, where *n* is a product number.</span></span> <span data-ttu-id="0127d-314">사용자가 이러한 링크 중 하나를 클릭 하면 결과 URL은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-314">When a user clicks one of these links, the resulting URL will look something like this:</span></span>

    `http://localhost:18816/UpdateProducts/6`

    <span data-ttu-id="0127d-315">즉, 편집할 제품 번호가 URL에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-315">In other words, the product number to be edited will be passed in the URL.</span></span>
3. <span data-ttu-id="0127d-316">브라우저에서 페이지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-316">View the page in a browser.</span></span> <span data-ttu-id="0127d-317">페이지는 다음과 같은 형식으로 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-317">The page displays the data in a format like this:</span></span>

    ![[이미지]](5-working-with-data/_static/image7.jpg)

    <span data-ttu-id="0127d-319">다음으로 사용자가 실제로 데이터를 업데이트할 수 있도록 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-319">Next, you'll create the page that lets users actually update the data.</span></span> <span data-ttu-id="0127d-320">업데이트 페이지에는 사용자가 입력 한 데이터의 유효성을 검사 하는 유효성 검사가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-320">The update page includes validation to validate the data that the user enters.</span></span> <span data-ttu-id="0127d-321">예를 들어 페이지의 코드를 사용 하면 모든 필수 열에 대해 값이 입력 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-321">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>
4. <span data-ttu-id="0127d-322">웹 사이트에서 *Updateproducts. cshtml*라는 새 CSHTML 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-322">In the website, create a new CSHTML file named *UpdateProducts.cshtml*.</span></span>
5. <span data-ttu-id="0127d-323">파일의 기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-323">Replace the existing markup in the file with the following.</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    <span data-ttu-id="0127d-324">페이지 본문에는 제품이 표시 되는 HTML 폼과 사용자가 편집할 수 있는 위치가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-324">The body of the page contains an HTML form where a product is displayed and where users can edit it.</span></span> <span data-ttu-id="0127d-325">제품을 표시 하려면 다음 SQL 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-325">To get the product to display, you use this SQL statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    <span data-ttu-id="0127d-326">그러면 `@0` 매개 변수에 전달 된 값과 일치 하는 ID를 가진 제품이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-326">This will select the product whose ID matches the value that's passed in the `@0` parameter.</span></span> <span data-ttu-id="0127d-327">*Id* 는 기본 키 이므로 고유 해야 하므로 하나의 제품 레코드를 이러한 방식으로 선택할 수 있습니다. 이 `Select` 문에 전달할 ID 값을 가져오려면 다음 구문을 사용 하 여 페이지에 URL의 일부로 전달 되는 값을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-327">(Because *Id* is the primary key and therefore must be unique, only one product record can ever be selected this way.) To get the ID value to pass to this `Select` statement, you can read the value that's passed to the page as part of the URL, using the following syntax:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    <span data-ttu-id="0127d-328">실제로 제품 레코드를 인출 하려면 하나의 레코드만 반환 하는 `QuerySingle` 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-328">To actually fetch the product record, you use the `QuerySingle` method, which will return just one record:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    <span data-ttu-id="0127d-329">단일 행이 `row` 변수로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-329">The single row is returned into the `row` variable.</span></span> <span data-ttu-id="0127d-330">각 열에서 데이터를 가져와 다음과 같이 로컬 변수에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-330">You can get data out of each column and assign it to local variables like this:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    <span data-ttu-id="0127d-331">양식의 태그에서 이러한 값은 다음과 같이 포함 된 코드를 사용 하 여 개별 텍스트 상자에 자동으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-331">In the markup for the form, these values are displayed automatically in individual text boxes by using embedded code like the following:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    <span data-ttu-id="0127d-332">코드의 해당 부분에서 업데이트할 제품 레코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-332">That part of the code displays the product record to be updated.</span></span> <span data-ttu-id="0127d-333">레코드가 표시 되 면 사용자는 개별 열을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-333">Once the record has been displayed, the user can edit individual columns.</span></span>

    <span data-ttu-id="0127d-334">사용자가 **업데이트** 단추를 클릭 하 여 양식을 제출 하면 `if(IsPost)` 블록의 코드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-334">When the user submits the form by clicking the **Update** button, the code in the `if(IsPost)` block runs.</span></span> <span data-ttu-id="0127d-335">그러면 `Request` 개체에서 사용자 값을 가져오고, 변수에 값을 저장 하 고, 각 열이 채워져 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-335">This gets the user's values from the `Request` object, stores the values in variables, and validates that each column has been filled in.</span></span> <span data-ttu-id="0127d-336">유효성 검사에 통과 하면 코드에서 다음과 같은 SQL Update 문을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-336">If validation passes, the code creates the following SQL Update statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    <span data-ttu-id="0127d-337">SQL `Update` 문에서 업데이트할 각 열을 지정 하 고 값을로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-337">In a SQL `Update` statement, you specify each column to update and the value to set it to.</span></span> <span data-ttu-id="0127d-338">이 코드에서는 매개 변수 자리 표시자 `@0`, `@1`, `@2`등을 사용 하 여 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-338">In this code, the values are specified using the parameter placeholders `@0`, `@1`, `@2`, and so on.</span></span> <span data-ttu-id="0127d-339">앞에서 설명한 것 처럼 보안을 위해 항상 매개 변수를 사용 하 여 SQL 문에 값을 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-339">(As noted earlier, for security, you should always pass values to a SQL statement by using parameters.)</span></span>

    <span data-ttu-id="0127d-340">`db.Execute` 메서드를 호출 하는 경우 SQL 문의 매개 변수에 해당 하는 순서 대로 값을 포함 하는 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-340">When you call the `db.Execute` method, you pass the variables that contain the values in the order that corresponds to the parameters in the SQL statement:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    <span data-ttu-id="0127d-341">`Update` 문을 실행 한 후에는 다음 메서드를 호출 하 여 사용자를 편집 페이지로 다시 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-341">After the `Update` statement has been executed, you call the following method in order to redirect the user back to the edit page:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    <span data-ttu-id="0127d-342">이는 사용자에 게 데이터베이스에 있는 데이터의 업데이트 된 목록이 표시 되 고 다른 제품을 편집할 수 있는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-342">The effect is that the user sees an updated listing of the data in the database and can edit another product.</span></span>
6. <span data-ttu-id="0127d-343">페이지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-343">Save the page.</span></span>
7. <span data-ttu-id="0127d-344">업데이트 페이지가 아닌 *Editproducts. cshtml* 페이지를 실행 한 다음 **편집** 을 클릭 하 여 편집할 제품을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-344">Run the *EditProducts.cshtml* page (not the update page) and then click **Edit** to select a product to edit.</span></span> <span data-ttu-id="0127d-345">*Updateproducts. cshtml* 페이지가 표시 되 고 선택한 레코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-345">The *UpdateProducts.cshtml* page is displayed, showing the record you selected.</span></span>

    ![[이미지]](5-working-with-data/_static/image8.jpg)
8. <span data-ttu-id="0127d-347">변경을 수행 하 고 **업데이트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-347">Make a change and click **Update**.</span></span> <span data-ttu-id="0127d-348">제품 목록이 업데이트 된 데이터와 함께 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-348">The products list is shown again with your updated data.</span></span>

## <a name="deleting-data-in-a-database"></a><span data-ttu-id="0127d-349">데이터베이스의 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="0127d-349">Deleting Data in a Database</span></span>

<span data-ttu-id="0127d-350">이 섹션에서는 사용자가 *제품* 데이터베이스 테이블에서 제품을 삭제 하도록 허용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-350">This section shows how to let users delete a product from the *Product* database table.</span></span> <span data-ttu-id="0127d-351">이 예제는 두 페이지로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-351">The example consists of two pages.</span></span> <span data-ttu-id="0127d-352">첫 번째 페이지에서는 사용자가 삭제할 레코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-352">In the first page, users select a record to delete.</span></span> <span data-ttu-id="0127d-353">그런 다음 삭제할 레코드가 레코드를 삭제할 것인지 확인할 수 있는 두 번째 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-353">The record to be deleted is then displayed in a second page that lets them confirm that they want to delete the record.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="0127d-354">**중요** 프로덕션 웹 사이트에서는 일반적으로 데이터를 변경할 수 있는 사용자를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-354">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="0127d-355">멤버 자격을 설정 하는 방법과 사용자에 게 사이트에서 작업을 수행할 수 있는 권한을 부여 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격 추가](https://go.microsoft.com/fwlink/?LinkId=202904)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0127d-355">For information about how to set up membership and about ways to authorize user to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="0127d-356">웹 사이트에서 이름이 *ListProductsForDelete*인 새 CSHTML 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-356">In the website, create a new CSHTML file named *ListProductsForDelete.cshtml*.</span></span>
2. <span data-ttu-id="0127d-357">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-357">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    <span data-ttu-id="0127d-358">이 페이지는 이전 버전의 *Editproducts. cshtml* 페이지와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-358">This page is similar to the *EditProducts.cshtml* page from earlier.</span></span> <span data-ttu-id="0127d-359">그러나 각 제품에 대 한 **편집** 링크를 표시 하는 대신 **삭제** 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-359">However, instead of displaying an **Edit** link for each product, it displays a **Delete** link.</span></span> <span data-ttu-id="0127d-360">태그에 다음 포함 코드를 사용 하 여 **삭제** 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-360">The **Delete** link is created using the following embedded code in the markup:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    <span data-ttu-id="0127d-361">그러면 사용자가 링크를 클릭할 때 다음과 같은 URL이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-361">This creates a URL that looks like this when users click the link:</span></span>

    `http://<server>/DeleteProduct/4`

    <span data-ttu-id="0127d-362">URL은 *deleteproduct. cshtml* (다음에 만들) 라는 페이지를 호출 하 고 삭제할 제품의 ID (여기서 4)를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-362">The URL calls a page named *DeleteProduct.cshtml* (which you'll create next) and passes it the ID of the product to delete (here, 4).</span></span>
3. <span data-ttu-id="0127d-363">파일을 저장 하지만 열린 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-363">Save the file, but leave it open.</span></span>
4. <span data-ttu-id="0127d-364">*Deleteproduct. cshtml*라는 다른 CHTML 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-364">Create another CHTML file named *DeleteProduct.cshtml*.</span></span> <span data-ttu-id="0127d-365">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-365">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    <span data-ttu-id="0127d-366">이 페이지는 *ListProductsForDelete* 에서 호출 되며, 사용자가 제품을 삭제 하 려 함을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-366">This page is called by *ListProductsForDelete.cshtml* and lets users confirm that they want to delete a product.</span></span> <span data-ttu-id="0127d-367">삭제할 제품을 나열 하려면 다음 코드를 사용 하 여 URL에서 삭제할 제품의 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-367">To list the product to be deleted, you get the ID of the product to delete from the URL using the following code:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    <span data-ttu-id="0127d-368">그러면 페이지에서 사용자에 게 실제로 레코드를 삭제 하는 단추를 클릭 하도록 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-368">The page then asks the user to click a button to actually delete the record.</span></span> <span data-ttu-id="0127d-369">이는 중요 한 보안 조치입니다. 데이터 업데이트 또는 삭제와 같은 웹 사이트에서 중요 한 작업을 수행 하는 경우 이러한 작업은 항상 GET 작업이 아닌 POST 작업을 사용 하 여 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-369">This is an important security measure: when you perform sensitive operations in your website like updating or deleting data, these operations should always be done using a POST operation, not a GET operation.</span></span> <span data-ttu-id="0127d-370">가져오기 작업을 사용 하 여 삭제 작업을 수행할 수 있도록 사이트를 설정 하는 경우 모든 사용자가 `http://<server>/DeleteProduct/4` 같은 URL을 전달 하 고 데이터베이스에서 원하는 모든 항목을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-370">If your site is set up so that a delete operation can be performed using a GET operation, anyone can pass a URL like `http://<server>/DeleteProduct/4` and delete anything they want from your database.</span></span> <span data-ttu-id="0127d-371">확인을 추가 하 고 페이지를 코딩 하 여 게시물을 통해서만 삭제를 수행할 수 있도록 하려면 사이트에 보안 측정값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-371">By adding the confirmation and coding the page so that the deletion can be performed only by using a POST, you add a measure of security to your site.</span></span>

    <span data-ttu-id="0127d-372">실제 삭제 작업은 다음 코드를 사용 하 여 수행 됩니다 .이 코드는 먼저 post 작업 이며 ID가 비어 있지 않은지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-372">The actual delete operation is performed using the following code, which first confirms that this is a post operation and that the ID isn't empty:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    <span data-ttu-id="0127d-373">이 코드는 지정 된 레코드를 삭제 한 다음 사용자를 다시 목록 페이지로 리디렉션하는 SQL 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-373">The code runs a SQL statement that deletes the specified record and then redirects the user back to the listing page.</span></span>
5. <span data-ttu-id="0127d-374">브라우저에서 *ListProductsForDelete* 를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-374">Run *ListProductsForDelete.cshtml* in a browser.</span></span>

    ![[이미지]](5-working-with-data/_static/image9.jpg)
6. <span data-ttu-id="0127d-376">제품 중 하나에 대 한 **삭제** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-376">Click the **Delete** link for one of the products.</span></span> <span data-ttu-id="0127d-377">*Deleteproduct. cshtml* 페이지가 표시 되어 해당 레코드를 삭제할 것인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-377">The *DeleteProduct.cshtml* page is displayed to confirm that you want to delete that record.</span></span>
7. <span data-ttu-id="0127d-378">**삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-378">Click the **Delete** button.</span></span> <span data-ttu-id="0127d-379">제품 레코드가 삭제 되 고 업데이트 된 제품 목록으로 페이지가 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-379">The product record is deleted and the page is refreshed with an updated product listing.</span></span>

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a><span data-ttu-id="0127d-380">데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="0127d-380">Connecting to a Database</span></span>
> 
> <span data-ttu-id="0127d-381">두 가지 방법으로 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-381">You can connect to a database in two ways.</span></span> <span data-ttu-id="0127d-382">첫 번째 방법은 `Database.Open` 메서드를 사용 하 고 데이터베이스 파일의 이름을 지정 하는 것입니다 ( *.sdf* 확장명 보다 낮음).</span><span class="sxs-lookup"><span data-stu-id="0127d-382">The first is to use the `Database.Open` method and to specify the name of the database file (less the *.sdf* extension):</span></span>
> 
> `var db = Database.Open("SmallBakery");`
> 
> <span data-ttu-id="0127d-383">`Open` 메서드는이 인 것으로 가정 합니다. *.sdf* 파일은 웹 사이트의 *App\_Data* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-383">The `Open` method assumes that the .*sdf* file is in the website's *App\_Data* folder.</span></span> <span data-ttu-id="0127d-384">이 폴더는 데이터를 저장 하기 위해 특별히 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-384">This folder is designed specifically for holding data.</span></span> <span data-ttu-id="0127d-385">예를 들어 웹 사이트에서 데이터를 읽고 쓸 수 있도록 하는 적절 한 권한이 있으며, 보안 조치로 WebMatrix는이 폴더의 파일에 대 한 액세스를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-385">For example, it has appropriate permissions to allow the website to read and write data, and as a security measure, WebMatrix does not allow access to files from this folder.</span></span>
> 
> <span data-ttu-id="0127d-386">두 번째 방법은 연결 문자열을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-386">The second way is to use a connection string.</span></span> <span data-ttu-id="0127d-387">데이터베이스에 연결하는 방법에 대한 정보를 포함하는 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-387">A connection string contains information about how to connect to a database.</span></span> <span data-ttu-id="0127d-388">이는 파일 경로를 포함 하거나, 해당 서버에 연결할 사용자 이름 및 암호와 함께 로컬 또는 원격 서버에 SQL Server 데이터베이스의 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-388">This can include a file path, or it can include the name of a SQL Server database on a local or remote server, along with a user name and password to connect to that server.</span></span> <span data-ttu-id="0127d-389">호스팅 공급자의 사이트와 같이 중앙에서 관리 되는 버전의 SQL Server에서 데이터를 유지 하는 경우 항상 연결 문자열을 사용 하 여 데이터베이스 연결 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-389">(If you keep data in a centrally managed version of SQL Server, such as on a hosting provider's site, you always use a connection string to specify the database connection information.)</span></span>
> 
> <span data-ttu-id="0127d-390">WebMatrix에서 연결 문자열은 일반적으로 *web.config*라는 XML 파일에 저장 됩니다. 이름에서 알 수 있듯이 웹 사이트의 루트에 있는 *web.config 파일을* 사용 하 여 사이트에 필요할 수 있는 연결 문자열을 포함 하 여 사이트의 구성 정보를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-390">In WebMatrix, connection strings are usually stored in an XML file named *Web.config*. As the name implies, you can use a *Web.config* file in the root of your website to store the site's configuration information, including any connection strings that your site might require.</span></span> <span data-ttu-id="0127d-391">*Web.config 파일에* 있는 연결 문자열의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-391">An example of a connection string in a *Web.config* file might look like the following:</span></span>
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> <span data-ttu-id="0127d-392">이 예에서는 연결 문자열은 로컬 *.sdf* 파일이 아닌 다른 위치에 있는 서버에서 실행 되는 SQL Server의 인스턴스에 있는 데이터베이스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-392">In the example, the connection string points to a database in an instance of SQL Server that's running on a server somewhere (as opposed to a local *.sdf* file).</span></span> <span data-ttu-id="0127d-393">`myServer` 및 `myDatabase`에 대 한 적절 한 이름을 대체 하 고 `username` 및 `password`에 대 한 SQL Server 로그인 값을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-393">You would need to substitute the appropriate names for `myServer` and `myDatabase`, and specify SQL Server login values for `username` and `password`.</span></span> <span data-ttu-id="0127d-394">사용자 이름 및 암호 값은 사용자의 서버에 로그인 하기 위해 사용자가 제공 하는 Windows 자격 증명 또는 호스팅 공급자가 제공 하는 값과 동일할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-394">(The username and password values are not necessarily the same as your Windows credentials or as the values that your hosting provider has given you for logging in to their servers.</span></span> <span data-ttu-id="0127d-395">관리자에 게 필요한 정확한 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-395">Check with the administrator for the exact values you need.)</span></span>
> 
> <span data-ttu-id="0127d-396">`Database.Open` 메서드는 데이터베이스 *.sdf* 파일의 이름 또는 *web.config* 파일에 저장 된 연결 문자열의 이름을 전달할 수 있으므로 유연 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-396">The `Database.Open` method is flexible, because it lets you pass either the name of a database *.sdf* file or the name of a connection string that's stored in the *Web.config* file.</span></span> <span data-ttu-id="0127d-397">다음 예에서는 이전 예제에 나와 있는 연결 문자열을 사용 하 여 데이터베이스에 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-397">The following example shows how to connect to the database using the connection string illustrated in the previous example:</span></span>
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> <span data-ttu-id="0127d-398">앞서 설명한 것 처럼 `Database.Open` 메서드를 사용 하 여 데이터베이스 이름 또는 연결 문자열을 전달할 수 있으며,이를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-398">As noted, the `Database.Open` method lets you pass either a database name or a connection string, and it'll figure out which to use.</span></span> <span data-ttu-id="0127d-399">이는 웹 사이트를 배포 (게시) 할 때 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-399">This is very useful when you deploy (publish) your website.</span></span> <span data-ttu-id="0127d-400">사이트를 개발 하 고 테스트할 때 *앱\_데이터* 폴더에 .sdf 파일을 사용할 수 있습니다 *.*</span><span class="sxs-lookup"><span data-stu-id="0127d-400">You can use an *.sdf* file in the *App\_Data* folder when you're developing and testing your site.</span></span> <span data-ttu-id="0127d-401">그런 다음 사이트를 프로덕션 서버로 이동할 때 *.sdf* 파일과 동일한 이름을 가진 &#8212; *web.config* 파일의 연결 문자열을 사용할 수 있지만, 코드를 변경 하지 않고도 모든 호스팅 공급자의 데이터베이스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-401">Then when you move your site to a production server, you can use a connection string in the *Web.config* file that has the same name as your *.sdf* file but that points to the hosting provider's database &#8212; all without having to change your code.</span></span>
> 
> <span data-ttu-id="0127d-402">마지막으로 연결 문자열을 직접 사용 하려는 경우 `Database.OpenConnectionString` 메서드를 호출 하 고 *web.config* 파일의 이름 뿐 아니라 실제 연결 문자열을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-402">Finally, if you want to work directly with a connection string, you can call the `Database.OpenConnectionString` method and pass it the actual connection string instead of just the name of one in the *Web.config* file.</span></span> <span data-ttu-id="0127d-403">이는 페이지가 실행 될 때까지 연결 문자열 (또는 *.sdf* 파일 이름 등의 값)에 액세스할 수 없는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-403">This might be useful in situations where for some reason you don't have access to the connection string (or values in it, such as the *.sdf* file name) until the page is running.</span></span> <span data-ttu-id="0127d-404">그러나 대부분의 시나리오에서는이 문서에 설명 된 대로 `Database.Open`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0127d-404">However, for most scenarios, you can use `Database.Open` as described in this article.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0127d-405">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0127d-405">Additional Resources</span></span>

- [<span data-ttu-id="0127d-406">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="0127d-406">SQL Server Compact</span></span>](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [<span data-ttu-id="0127d-407">WebMatrix에서 SQL Server 또는 MySQL 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="0127d-407">Connecting to a SQL Server or MySQL Database in WebMatrix</span></span>](https://go.microsoft.com/fwlink/?LinkId=208661)
- [<span data-ttu-id="0127d-408">ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="0127d-408">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
