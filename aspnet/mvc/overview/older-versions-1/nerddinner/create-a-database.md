---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 데이터베이스 만들기 | Microsoft 문서
author: microsoft
description: 2 단계에서는 팀 간 Ddinner 응용 프로그램에 대 한 모든 dinner 및 RSVP 데이터를 보유 하는 데이터베이스를 만드는 단계를 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469301"
---
# <a name="create-a-database"></a><span data-ttu-id="658d2-103">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="658d2-103">Create a Database</span></span>

<span data-ttu-id="658d2-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="658d2-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="658d2-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="658d2-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="658d2-106">ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 2 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="658d2-107">2 단계에서는 팀 간 Ddinner 응용 프로그램에 대 한 모든 dinner 및 RSVP 데이터를 보유 하는 데이터베이스를 만드는 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="658d2-108">ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="658d2-109">NerdDinner Step 2: 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="658d2-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="658d2-110">여기서는 데이터베이스를 사용 하 여 전체 고객 Ddinner 응용 프로그램에 대 한 모든 저녁 및 RSVP 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="658d2-111">아래 단계는 무료 SQL Server Express 버전을 사용 하 여 데이터베이스를 만드는 것을 보여 줍니다 ( [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)의 V2를 사용 하 여 쉽게 설치할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="658d2-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="658d2-112">작성 하는 모든 코드는 SQL Server Express와 전체 SQL Server 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="658d2-113">새 SQL Server Express 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="658d2-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="658d2-114">먼저 웹 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **추가-&gt;새 항목** 메뉴 명령을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="658d2-115">그러면 Visual Studio의 "새 항목 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="658d2-116">"Data" 범주를 기준으로 필터링 하 고 "SQL Server 데이터베이스" 항목 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="658d2-117">SQL Server Express 데이터베이스의 이름을 "NerdDinner. .mdf"로 만들고 확인을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="658d2-118">그러면 Visual Studio에서이 파일을 \App\_데이터 디렉터리 (읽기 및 쓰기 보안 Acl을 사용 하 여 이미 설정 된 디렉터리)에 추가 하고자 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="658d2-119">"예"를 클릭 하면 새 데이터베이스가 생성 되 고 솔루션 탐색기에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="658d2-120">데이터베이스 내에 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="658d2-120">Creating Tables within our Database</span></span>

<span data-ttu-id="658d2-121">이제 빈 데이터베이스를 새로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-121">We now have a new empty database.</span></span> <span data-ttu-id="658d2-122">여기에 일부 테이블을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-122">Let's add some tables to it.</span></span>

<span data-ttu-id="658d2-123">이렇게 하려면 데이터베이스와 서버를 관리할 수 있게 해 주는 Visual Studio 내에서 "서버 탐색기" 탭 창으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="658d2-124">응용 프로그램의 \App\_Data 폴더에 저장 된 SQL Server Express 데이터베이스는 자동으로 서버 탐색기 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="658d2-125">선택적으로 "서버 탐색기" 창의 맨 위에 있는 "데이터베이스에 연결" 아이콘을 사용 하 여 목록에 SQL Server 데이터베이스 (로컬 및 원격 모두)를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="658d2-126">Dinners를 저장 하 고 다른 하나는 RSVP acceptances을 추적 하는 두 개의 테이블을 두 개의 테이블에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="658d2-127">데이터베이스 내에서 "Tables" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 테이블 추가" 메뉴 명령을 선택 하 여 새 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="658d2-128">이렇게 하면 테이블의 스키마를 구성 하는 데 사용할 수 있는 테이블 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="658d2-129">"Dinners" 테이블의 경우 10 개의 데이터 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="658d2-130">"DinnerID" 열을 테이블의 고유 기본 키로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="658d2-131">"DinnerID" 열을 마우스 오른쪽 단추로 클릭 하 고 "기본 키 설정" 메뉴 항목을 선택 하 여이를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="658d2-132">테이블에 새 데이터 행이 추가 될 때 해당 값이 자동으로 증가 하는 "id" 열로 구성 하는 것 외에도이를 기본 키로 구성 하는 것이 좋습니다. 즉, 첫 번째 삽입 된 Dinner row에는 두 번째 삽입 된 행이 포함 됩니다. 은 (는) 2, 등의 d Innerid를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="658d2-133">"DinnerID" 열을 선택한 다음 "열 속성" 편집기를 사용 하 여 열의 "(Id)" 속성을 "예"로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="658d2-134">표준 id 기본값 (1에서 시작 하 고 새 Dinner row에서 1 씩 증가)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="658d2-135">그런 다음 Ctrl + S를 입력 하거나 **파일&gt;저장** 메뉴 명령을 사용 하 여 테이블을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="658d2-136">그러면 테이블의 이름을 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-136">This will prompt us to name the table.</span></span> <span data-ttu-id="658d2-137">이름을 "Dinners"로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="658d2-138">그러면 새 Dinners 테이블이 서버 탐색기의 데이터베이스 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="658d2-139">그런 다음 위의 단계를 반복 하 고 "RSVP" 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="658d2-140">의이 테이블에는 3 개의 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-140">This table with have 3 columns.</span></span> <span data-ttu-id="658d2-141">RsvpID 열을 기본 키로 설정 하 고 id 열로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="658d2-142">이를 저장 하 고 이름을 "RSVP"로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="658d2-143">테이블 간의 외래 키 관계 설정</span><span class="sxs-lookup"><span data-stu-id="658d2-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="658d2-144">이제 데이터베이스에 두 개의 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-144">We now have two tables within our database.</span></span> <span data-ttu-id="658d2-145">마지막 스키마 디자인 단계는 이러한 두 테이블 간에 "일 대 다" 관계를 설정 하 여 각 Dinner row에 적용 되는 0 개 이상의 RSVP 행과 연결할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="658d2-146">이렇게 하려면 "Dinners" 테이블의 "DinnerID" 열에 대 한 외래 키 관계를 갖도록 RSVP 테이블의 "DinnerID" 열을 구성 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="658d2-147">이렇게 하려면 서버 탐색기에서 테이블 디자이너를 두 번 클릭 하 여 테이블 디자이너 내에서 RSVP 테이블을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="658d2-148">그런 다음 해당 내에서 "DinnerID" 열을 선택 하 고 마우스 오른쪽 단추를 클릭 한 다음 "관계 ..."를 선택 합니다. 상황에 맞는 메뉴 명령:</span><span class="sxs-lookup"><span data-stu-id="658d2-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="658d2-149">그러면 테이블 간의 관계를 설정 하는 데 사용할 수 있는 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="658d2-150">"추가" 단추를 클릭 하 여 대화 상자에 새 관계를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="658d2-151">관계가 추가 되 면 대화 상자 오른쪽에 있는 속성 그리드 내에서 "테이블 및 열 사양" 트리 뷰 노드를 확장 한 다음 "..."를 클릭 합니다. 오른쪽에 있는 단추:</span><span class="sxs-lookup"><span data-stu-id="658d2-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="658d2-152">"..."를 클릭 합니다. 단추를 클릭 하면 관계에 포함 된 테이블과 열을 지정할 수 있을 뿐만 아니라 관계의 이름을 지정할 수 있는 다른 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="658d2-153">기본 키 테이블을 "Dinners"로 변경 하 고 Dinners 테이블 내에서 기본 키로 "DinnerID" 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="658d2-154">RSVP 테이블은 외래 키 테이블 및 RSVP입니다. DinnerID 열은 외래 키로 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="658d2-155">이제 RSVP 테이블의 각 행이 Dinner table의 행과 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="658d2-156">SQL Server는 microsoft의 참조 무결성을 유지 하 고 유효한 저녁 행을 가리키지 않는 경우 새 RSVP 행을 추가 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="658d2-157">또한 여전히 RSVP 행을 참조 하는 경우 Dinner row를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="658d2-158">테이블에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="658d2-158">Adding Data to our Tables</span></span>

<span data-ttu-id="658d2-159">Dinners 테이블에 몇 가지 샘플 데이터를 추가 하는 것부터 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="658d2-160">서버 탐색기 내에서 테이블을 마우스 오른쪽 단추로 클릭 하 고 "테이블 데이터 표시" 명령을 선택 하 여 테이블에 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="658d2-161">나중에 응용 프로그램 구현을 시작할 때 사용할 수 있는 Dinner data 행을 몇 개 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="658d2-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="658d2-162">Next Step</span></span>

<span data-ttu-id="658d2-163">데이터베이스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-163">We've finished creating our database.</span></span> <span data-ttu-id="658d2-164">이제 쿼리 및 업데이트에 사용할 수 있는 모델 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="658d2-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="658d2-165">[이전](create-a-new-aspnet-mvc-project.md)
> [다음](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="658d2-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
