---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: ASP.NET 웹 페이지 데이터 표시 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 WebMatrix에서 데이터베이스를 만드는 방법과 ASP.NET 웹 페이지 (Razor)를 사용할 때 페이지에 데이터베이스 데이터를 표시 하는 방법을 보여 줍니다. Y ...를 가정 합니다.
ms.author: riande
ms.date: 05/28/2015
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: 9e665ca8dd064c23a8b8bd3593014969d0c3da48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421487"
---
# <a name="introducing-aspnet-web-pages---displaying-data"></a><span data-ttu-id="2ac64-104">ASP.NET 웹 페이지 데이터 표시 소개</span><span class="sxs-lookup"><span data-stu-id="2ac64-104">Introducing ASP.NET Web Pages - Displaying Data</span></span>

<span data-ttu-id="2ac64-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2ac64-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="2ac64-106">이 자습서에서는 WebMatrix에서 데이터베이스를 만드는 방법과 ASP.NET 웹 페이지 (Razor)를 사용할 때 페이지에 데이터베이스 데이터를 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-106">This tutorial shows you how to create a database in WebMatrix and how to display database data in a page when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="2ac64-107">[ASP.NET 웹 페이지 프로그래밍에 대 한 소개를](../introducing-razor-syntax-c.md)통해 시리즈를 완료 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-107">It assumes you have completed the series through [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md).</span></span>
> 
> <span data-ttu-id="2ac64-108">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="2ac64-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="2ac64-109">WebMatrix 도구를 사용 하 여 데이터베이스 및 데이터베이스 테이블을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="2ac64-109">How to use WebMatrix tools to create a database and database tables.</span></span>
> - <span data-ttu-id="2ac64-110">WebMatrix 도구를 사용 하 여 데이터베이스에 데이터를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-110">How to use WebMatrix tools to add data to a database.</span></span>
> - <span data-ttu-id="2ac64-111">페이지의 데이터베이스에서 데이터를 표시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2ac64-111">How to display data from the database on a page.</span></span>
> - <span data-ttu-id="2ac64-112">ASP.NET 웹 페이지에서 SQL 명령을 실행 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2ac64-112">How to run SQL commands in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="2ac64-113">`WebGrid` 도우미를 사용자 지정 하 여 데이터 표시를 변경 하 고 페이징 및 정렬을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-113">How to customize the `WebGrid` helper to change the data display and to add paging and sorting.</span></span>
>   
> 
> <span data-ttu-id="2ac64-114">설명 하는 기능/기술:</span><span class="sxs-lookup"><span data-stu-id="2ac64-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="2ac64-115">WebMatrix 데이터베이스 도구.</span><span class="sxs-lookup"><span data-stu-id="2ac64-115">WebMatrix database tools.</span></span>
> - <span data-ttu-id="2ac64-116">도우미를 `WebGrid` 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-116">`WebGrid` helper.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="2ac64-117">만들 내용</span><span class="sxs-lookup"><span data-stu-id="2ac64-117">What You'll Build</span></span>

<span data-ttu-id="2ac64-118">이전 자습서에서는 Razor 구문 및 도우미에 대 한 기본 사항에 ASP.NET 웹 페이지 (*cshtml* 파일)를 도입 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-118">In the previous tutorial, you were introduced to ASP.NET Web Pages (*.cshtml* files), to the basics of Razor syntax, and to helpers.</span></span> <span data-ttu-id="2ac64-119">이 자습서에서는 나머지 시리즈에 사용할 실제 웹 응용 프로그램을 만들기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-119">In this tutorial, you'll begin creating the actual web application that you'll use for the rest of the series.</span></span> <span data-ttu-id="2ac64-120">앱은 영화에 대 한 정보를 보고 추가, 변경 및 삭제할 수 있는 간단한 영화 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-120">The app is a simple movie application that lets you view, add, change, and delete information about movies.</span></span>

<span data-ttu-id="2ac64-121">이 자습서를 완료 하면이 페이지와 같은 영화 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-121">When you're done with this tutorial, you'll be able to view a movie listing that looks like this page:</span></span>

![CSS 클래스 이름으로 설정 된 매개 변수를 포함 하는 WebGrid 표시](displaying-data/_static/image1.png)

<span data-ttu-id="2ac64-123">하지만 시작 하려면 데이터베이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-123">But to begin, you have to create a database.</span></span>

## <a name="a-very-brief-introduction-to-databases"></a><span data-ttu-id="2ac64-124">데이터베이스에 대 한 간략 한 소개</span><span class="sxs-lookup"><span data-stu-id="2ac64-124">A Very Brief Introduction to Databases</span></span>

<span data-ttu-id="2ac64-125">이 자습서에서는 데이터베이스에 대 한 briefest 소개만 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-125">This tutorial will provide only the briefest introduction to databases.</span></span> <span data-ttu-id="2ac64-126">데이터베이스 환경이 있는 경우이 짧은 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-126">If you have database experience, you can skip this short section.</span></span>

<span data-ttu-id="2ac64-127">데이터베이스에는 정보 &mdash; (예: 고객, 주문, 공급 업체 테이블 또는 학생, 교사, 수업 및 학점)를 포함 하는 테이블이 하나 이상 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-127">A database contains one or more tables that contain information &mdash; for example, tables for customers, orders, and vendors, or for students, teachers, classes, and grades.</span></span> <span data-ttu-id="2ac64-128">구조적으로 데이터베이스 테이블은 스프레드시트와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-128">Structurally, a database table is like a spreadsheet.</span></span> <span data-ttu-id="2ac64-129">일반적인 주소록을 상상해 보세요.</span><span class="sxs-lookup"><span data-stu-id="2ac64-129">Imagine a typical address book.</span></span> <span data-ttu-id="2ac64-130">주소록의 각 항목에 대해 (즉, 각 사람에 대 한) 이름, 성, 주소, 전자 메일 주소 및 전화 번호와 같은 여러 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-130">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

![간단한 표 형태의 샘플 데이터베이스 테이블](displaying-data/_static/image2.png)

<span data-ttu-id="2ac64-132">(행을 *레코드*라고도 하며 열을 *필드*라고도 합니다.)</span><span class="sxs-lookup"><span data-stu-id="2ac64-132">(Rows are sometimes referred to as *records*, and columns are sometimes referred to as *fields*.)</span></span>

<span data-ttu-id="2ac64-133">대부분의 데이터베이스 테이블에 대해 테이블에는 고객 번호, 계좌 번호 등과 같은 고유한 값을 포함 하는 열이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-133">For most database tables, the table has to have a column that contains a unique value, like a customer number, account number, and so on.</span></span> <span data-ttu-id="2ac64-134">이 값을 테이블의 *기본 키*라고 하며,이 값을 사용 하 여 테이블의 각 행을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-134">This value is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="2ac64-135">이 예에서 ID 열은 이전 예제에 표시 된 주소록의 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-135">In the example, the ID column is the primary key for the address book shown in the previous example.</span></span>

<span data-ttu-id="2ac64-136">웹 응용 프로그램에서 수행 하는 작업의 대부분은 데이터베이스에서 정보를 읽고 페이지에 표시 하는 것으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-136">Much of the work you do in web applications consists of reading information out of the database and displaying it on a page.</span></span> <span data-ttu-id="2ac64-137">또한 사용자 로부터 정보를 수집 하 여 데이터베이스에 추가 하거나 이미 데이터베이스에 있는 레코드를 수정 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-137">You'll also often gather information from users and add it to a database, or you'll modify records that are already in the database.</span></span> <span data-ttu-id="2ac64-138">(이 자습서 집합의 과정에서 이러한 모든 작업을 다룹니다.)</span><span class="sxs-lookup"><span data-stu-id="2ac64-138">(We'll cover all of these operations in the course of this tutorial set.)</span></span>

<span data-ttu-id="2ac64-139">데이터베이스 작업은 있으므로 매우 복잡할 수 있으며 전문 지식이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-139">Database work can be enormously complex and can require specialized knowledge.</span></span> <span data-ttu-id="2ac64-140">그러나이 자습서에서는 기본 개념을 이해 해야 합니다 .이 개념은 모든 사용자에 게 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-140">For this tutorial set, though, you have to understand only basic concepts, which will all be explained as you go.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="2ac64-141">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="2ac64-141">Creating a Database</span></span>

<span data-ttu-id="2ac64-142">WebMatrix에는 데이터베이스를 쉽게 만들고 데이터베이스에서 테이블을 만들 수 있도록 하는 도구가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-142">WebMatrix includes tools that make it easy to create a database and to create tables in the database.</span></span> <span data-ttu-id="2ac64-143">데이터베이스의 구조를 데이터베이스의 *스키마*라고 합니다. 이 자습서를 설정 하는 경우 동영상 &mdash; 하나의 테이블만 있는 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-143">(The structure of a database is referred to as the database's *schema*.) For this tutorial set, you'll create a database that has only one table in it &mdash; Movies.</span></span>

<span data-ttu-id="2ac64-144">아직 수행 하지 않은 경우 WebMatrix를 열고 이전 자습서에서 만든 WebPagesMovies 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-144">Open WebMatrix if you haven't already done so, and open the WebPagesMovies site that you created in the previous tutorial.</span></span>

<span data-ttu-id="2ac64-145">왼쪽 창에서 **데이터베이스** 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-145">In the left pane, click the **Database** workspace.</span></span>

![WebMatrix 데이터베이스 작업 영역 탭](displaying-data/_static/image3.png)

<span data-ttu-id="2ac64-147">리본은 데이터베이스 관련 태스크를 표시 하도록 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-147">The ribbon changes to show database-related tasks.</span></span> <span data-ttu-id="2ac64-148">리본에서 **새 데이터베이스**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-148">In the ribbon, click **New Database**.</span></span>

![WebMatrix 리본의 ' 새 데이터베이스 ' 단추](displaying-data/_static/image4.png)

<span data-ttu-id="2ac64-150">WebMatrix는 사이트 &mdash; *webstel.sdf*와 동일한 이름을 가진 SQL Server CE 데이터베이스 ( *.sdf* 파일)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-150">WebMatrix creates a SQL Server CE database (an *.sdf* file) that has the same name as your site &mdash; *WebPagesMovies.sdf*.</span></span> <span data-ttu-id="2ac64-151">여기서는이 작업을 수행 하지 않지만 확장명이 *.sdf* 인 경우 파일 이름을 원하는 이름으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-151">(You won't do this here, but you can rename the file to anything you like, as long as it has an *.sdf* extension.)</span></span>

## <a name="creating-a-table"></a><span data-ttu-id="2ac64-152">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="2ac64-152">Creating a Table</span></span>

<span data-ttu-id="2ac64-153">리본에서 **새 테이블**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-153">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="2ac64-154">WebMatrix 새 탭에서 테이블 디자이너를 엽니다. 새 테이블 옵션을 사용할 수 없는 경우 왼쪽의 트리 뷰에서 새 데이터베이스를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-154">WebMatrix opens the table designer in a new tab. (If the New Table option isn't available, make sure that the new database is selected in the tree view on the left.)</span></span>

![WebMatrix 리본의 ' 새 테이블 ' 단추](displaying-data/_static/image5.png)

<span data-ttu-id="2ac64-156">위쪽의 텍스트 상자 (워터 마크에 "테이블 이름 입력"이 표시 됨)에 "영화"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-156">In the text box at the top (where the watermark says "Enter table name"), enter "Movies".</span></span>

![WebMatrix 데이터베이스 디자이너에 테이블 이름 입력](displaying-data/_static/image6.png)

<span data-ttu-id="2ac64-158">테이블 이름 아래의 창은 개별 열을 정의 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-158">The pane underneath the table name is where you define individual columns.</span></span> <span data-ttu-id="2ac64-159">이 자습서의 *영화* 테이블에는 *ID*, *제목*, *장르*및 *연도*열만 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-159">For the *Movies* table in this tutorial, you'll create only a few columns: *ID*, *Title*, *Genre*, and *Year*.</span></span>

<span data-ttu-id="2ac64-160">**이름** 상자에 "ID"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-160">In the **Name** box, enter "ID".</span></span> <span data-ttu-id="2ac64-161">여기에 값을 입력 하면 새 열에 대 한 모든 컨트롤이 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-161">Entering a value here activates all the controls for the new column.</span></span>

<span data-ttu-id="2ac64-162">**데이터 형식** 목록으로 탭 하 고 **int**를 선택 합니다. 이 값은 ID 열에 정수 (숫자) 데이터를 포함 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-162">Tab to the **Data Type** list and choose **int**. This value specifies that the ID column will contain integer (number) data.</span></span>

> [!NOTE]
> <span data-ttu-id="2ac64-163">여기서는 더 이상 호출 하지 않지만 표준 Windows 키보드 제스처를 사용 하 여이 표를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-163">We won't call it out any more here (much), but you can use standard Windows keyboard gestures to navigate in this grid.</span></span> <span data-ttu-id="2ac64-164">예를 들어 필드 사이에서 tab 키를 누르면 목록에서 항목을 선택 하기 위해 입력을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-164">For example, you can tab between fields, you can just start typing in order to select an item in a list, and so on.</span></span>

<span data-ttu-id="2ac64-165">**기본값** 상자를 지나서 탭 합니다. 즉, 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-165">Tab past the **Default Value** box (that is, leave it blank).</span></span> <span data-ttu-id="2ac64-166">**기본 키** 로 Tab 키를 누르고 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-166">Tab to the **Is Primary Key** check box and select it.</span></span> <span data-ttu-id="2ac64-167">이 옵션은 *ID* 열에 개별 행을 식별 하는 데이터가 포함 되도록 데이터베이스에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-167">This option tells the database that the *ID* column will contain the data that identifies individual rows.</span></span> <span data-ttu-id="2ac64-168">즉, 각 행에는 해당 행을 찾는 데 사용할 수 있는 ID 열에 고유한 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-168">(That is, each row will have a unique value in the ID column that you can use to find that row.)</span></span>

<span data-ttu-id="2ac64-169">Id 옵션 **을** 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-169">Choose the **Is Identity** option.</span></span> <span data-ttu-id="2ac64-170">이 옵션은 데이터베이스에 각 새 행에 대 한 다음 일련 번호를 자동으로 생성 하도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-170">This option tells the database that it should automatically generate the next sequential number for each new row.</span></span> <span data-ttu-id="2ac64-171">Is **Identity** 옵션은 **기본 키** 옵션을 선택한 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-171">(The **Is Identity** option works only if you've also selected the **Is Primary Key** option.)</span></span>

<span data-ttu-id="2ac64-172">다음 표 형태 창의 행을 클릭 하거나 Tab 키를 두 번 눌러 현재 행을 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-172">Click in the next grid row, or press Tab twice to finish the current row.</span></span> <span data-ttu-id="2ac64-173">두 제스처는 현재 행을 저장 하 고 다음 항목을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-173">Either gesture saves the current row and starts the next one.</span></span> <span data-ttu-id="2ac64-174">이제 **기본값** 열에 **Null**이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-174">Notice that the **Default Value** column now says **Null**.</span></span> <span data-ttu-id="2ac64-175">기본값은 기본값입니다 .이 경우에는에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-175">(Null is the default value for the default value, so to speak.)</span></span>

<span data-ttu-id="2ac64-176">새 **ID** 열을 정의 하는 작업을 마치면 디자이너는 다음 그림과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-176">When you've finished defining the new **ID** column, the designer will look like this illustration:</span></span>

![WebMatrix 데이터베이스 디자이너에서 영화 테이블의 ID 열을 정의한 후](displaying-data/_static/image7.png)

<span data-ttu-id="2ac64-178">다음 열을 만들려면 **이름** 열에서 상자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-178">To create the next column, click in the box in the **Name** column.</span></span> <span data-ttu-id="2ac64-179">열에 대해 "Title"을 입력 한 다음 **데이터 형식** 값으로 **nvarchar** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-179">Enter "Title" for the column and then select **nvarchar** for the **Data Type** value.</span></span> <span data-ttu-id="2ac64-180">**Nvarchar** 의 "var" 부분은이 열에 대 한 데이터가 레코드에 대 한 레코드에 따라 달라질 수 있는 문자열이 되도록 데이터베이스에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-180">The "var" part of **nvarchar** tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="2ac64-181">"N" 접두사는 "국가"를 나타내며이는 필드에서 문자 데이터를 입력할 수 있습니다. 즉, 필드에 유니코드 데이터가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-181">(The "n" prefix represents "national," which indicates that the field can hold character data for any alphabet or writing system — that is, the field holds Unicode data.)</span></span>

<span data-ttu-id="2ac64-182">**Nvarchar**를 선택 하면 필드의 최대 길이를 입력할 수 있는 다른 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-182">When you choose **nvarchar**, another box appears where you can enter the maximum length for the field.</span></span> <span data-ttu-id="2ac64-183">50을 입력 합니다 .이 자습서에서 작업할 영화 제목은 50 자 보다 깁니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-183">Enter 50, on the assumption that no movie title that you'll work with in this tutorial will be longer than 50 characters.</span></span>

<span data-ttu-id="2ac64-184">**기본값** 을 건너뛰고 **null 허용** 옵션을 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-184">Skip **Default Value** and clear the **Allow Nulls** option.</span></span> <span data-ttu-id="2ac64-185">데이터베이스가 제목이 없는 데이터베이스에 입력 되는 것을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-185">You don't want the database to allow any movies to be entered into the database that don't have a title.</span></span>

<span data-ttu-id="2ac64-186">작업을 완료 하 고 다음 행으로 이동 하면 디자이너는 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-186">When you're done and move to the next row, the designer looks like this illustration:</span></span>

![WebMatrix 데이터베이스 디자이너에서 영화 테이블의 제목 열을 정의한 후](displaying-data/_static/image8.png)

<span data-ttu-id="2ac64-188">이러한 단계를 반복 하 여 길이를 제외 하 고 "장르" 라는 열을 만들어 30으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-188">Repeat these steps to create a column named "Genre", except for the length, set it to just 30.</span></span>

<span data-ttu-id="2ac64-189">"Year" 라는 다른 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-189">Create another column named "Year."</span></span> <span data-ttu-id="2ac64-190">데이터 형식에 대해 **nchar** ( **nvarchar**아님)를 선택 하 고 길이를 4로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-190">For the data type, choose **nchar** (not **nvarchar**) and set the length to 4.</span></span> <span data-ttu-id="2ac64-191">연도에는 "1995" 또는 "2010"과 같은 4 자리 숫자를 사용 하므로 가변 크기 열이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-191">For the year, you're going to use a 4-digit number like "1995" or "2010", so you don't require a variable-sized column.</span></span>

<span data-ttu-id="2ac64-192">완성 된 디자인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-192">Here's what the finished design looks like:</span></span>

![모든 필드가 영화 테이블에 대해 정의 된 후 WebMatrix 데이터베이스 디자이너](displaying-data/_static/image9.png)

<span data-ttu-id="2ac64-194">Ctrl + S를 누르거나 빠른 실행 도구 모음에서 **저장** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-194">Press Ctrl+S or click the **Save** button in the Quick Access toolbar.</span></span> <span data-ttu-id="2ac64-195">탭을 닫아 데이터베이스 디자이너를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-195">Close the database designer by closing the tab.</span></span>

## <a name="adding-some-example-data"></a><span data-ttu-id="2ac64-196">몇 가지 예제 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="2ac64-196">Adding Some Example Data</span></span>

<span data-ttu-id="2ac64-197">이 자습서 시리즈의 뒷부분에서는 폼에 새 동영상을 입력할 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-197">Later in this tutorial series you'll create a page where you can enter new movies in a form.</span></span> <span data-ttu-id="2ac64-198">그러나 지금은 페이지에 표시할 수 있는 몇 가지 예제 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-198">For now, however, you can add some example data that you can then display on a page.</span></span>

<span data-ttu-id="2ac64-199">WebMatrix의 **데이터베이스** 작업 영역에서 이전에 만든 *.sdf* 파일을 보여 주는 트리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-199">In the **Database** workspace in WebMatrix, notice that there's a tree that shows you the *.sdf* file you created earlier.</span></span> <span data-ttu-id="2ac64-200">새 *.sdf* 파일의 노드를 연 다음 **테이블** 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-200">Open the node for your new *.sdf* file, and then open the **Tables** node.</span></span>

![트리를 사용 하 여 영화를 연 WebMatrix 데이터베이스 작업 영역 테이블](displaying-data/_static/image10.png)

<span data-ttu-id="2ac64-202">**동영상** 노드를 마우스 오른쪽 단추로 클릭 한 다음 **데이터**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-202">Right-click the **Movies** node and then choose **Data**.</span></span> <span data-ttu-id="2ac64-203">WebMatrix는 *동영상* 테이블에 대 한 데이터를 입력할 수 있는 그리드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-203">WebMatrix opens a grid where you can enter data for the *Movies* table:</span></span>

![WebMatrix의 데이터베이스 항목 그리드 (비어 있음)](displaying-data/_static/image11.png)

<span data-ttu-id="2ac64-205">**Title** 열을 클릭 하 고 "When Harry Sally"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-205">Click the **Title** column and enter "When Harry Met Sally".</span></span> <span data-ttu-id="2ac64-206">Tab 키를 사용 하 여 **장르** 열로 이동 하 고 "Romantic 코미디"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-206">Move to the **Genre** column (you can use the Tab key) and enter "Romantic Comedy".</span></span> <span data-ttu-id="2ac64-207">**Year** 열로 이동 하 고 "1989"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-207">Move to the **Year** column and enter "1989":</span></span>

![한 레코드를 포함 하는 WebMatrix의 데이터베이스 입력 표](displaying-data/_static/image12.png)

<span data-ttu-id="2ac64-209">Enter 키를 누르고, WebMatrix는 새 영화를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-209">Press Enter, and WebMatrix saves the new movie.</span></span> <span data-ttu-id="2ac64-210">**ID** 열이 채워져 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-210">Notice that the **ID** column has been filled in.</span></span>

![하나의 레코드와 자동 생성 된 ID가 있는 WebMatrix의 데이터베이스 입력 그리드](displaying-data/_static/image13.png)

<span data-ttu-id="2ac64-212">다른 영화를 입력 합니다 (예: "바람", "드라마", "1939").</span><span class="sxs-lookup"><span data-stu-id="2ac64-212">Enter another movie (for example, "Gone with the Wind", "Drama", "1939").</span></span> <span data-ttu-id="2ac64-213">ID 열이 다시 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-213">The ID column is filled in again:</span></span>

![두 개의 레코드와 자동 생성 Id가 있는 WebMatrix의 데이터베이스 입력 표](displaying-data/_static/image14.png)

<span data-ttu-id="2ac64-215">세 번째 영화를 입력 합니다 (예: "Ghostbusters", "코미디").</span><span class="sxs-lookup"><span data-stu-id="2ac64-215">Enter a third movie (for example, "Ghostbusters", "Comedy").</span></span> <span data-ttu-id="2ac64-216">실험으로 **Year** 열을 비워 두고 enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-216">As an experiment, leave the **Year** column blank and then press Enter.</span></span> <span data-ttu-id="2ac64-217">**Null 허용** 옵션을 선택 취소 했기 때문에 데이터베이스에 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-217">Because you unselected the **Allow Nulls** option, the database shows an error:</span></span>

![필요한 열 값을 비워 두면 ' 잘못 된 데이터 ' 오류가 표시 됨](displaying-data/_static/image15.png)

<span data-ttu-id="2ac64-219">**확인** 을 클릭 하 여 뒤로 돌아가서 항목 ("Ghostbusters"의 연도는 1984)을 수정 하 고 enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-219">Click **OK** to go back and fix the entry (the year for "Ghostbusters" is 1984), and then press Enter.</span></span>

<span data-ttu-id="2ac64-220">8 가지가 될 때까지 여러 영화를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-220">Fill in several movies until you have 8 or so.</span></span> <span data-ttu-id="2ac64-221">(8을 입력 하면 나중에 페이징 작업을 더 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-221">(Entering 8 makes it easier to work with paging later.</span></span> <span data-ttu-id="2ac64-222">그러나 너무 많은 경우 지금은 몇 가지만 입력 하세요. 실제 데이터는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-222">But if that's too many, enter just a few for now.) The actual data doesn't matter.</span></span>

![두 레코드를 포함 하는 WebMatrix의 데이터베이스 입력 표](displaying-data/_static/image16.png)

<span data-ttu-id="2ac64-224">모든 영화를 오류 없이 입력 한 경우 ID 값은 순차적입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-224">If you entered all the movies without any errors, the ID values are sequential.</span></span> <span data-ttu-id="2ac64-225">불완전 한 동영상 레코드를 저장 하려고 하면 ID 번호가 순차적이 지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-225">If you tried to save an incomplete movie record, the ID numbers might not be sequential.</span></span> <span data-ttu-id="2ac64-226">그렇다면 이것이 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-226">If so, that's okay.</span></span> <span data-ttu-id="2ac64-227">이 숫자에는 내재 된 의미가 없으며, 중요 한 것은 *동영상* 테이블에서 고유 하다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-227">The numbers don't have any inherent meaning, and the only thing that's important is that they're unique in the *Movies* table.</span></span>

<span data-ttu-id="2ac64-228">데이터베이스 디자이너를 포함 하는 탭을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-228">Close the tab that contains the database designer.</span></span>

<span data-ttu-id="2ac64-229">이제이 데이터를 웹 페이지에 표시 하도록 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-229">Now you can turn to displaying this data on a web page.</span></span>

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a><span data-ttu-id="2ac64-230">WebGrid 도우미를 사용 하 여 페이지에 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="2ac64-230">Displaying Data in a Page by Using the WebGrid Helper</span></span>

<span data-ttu-id="2ac64-231">페이지에 데이터를 표시 하려면 `WebGrid` 도우미를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-231">To display data in a page, you're going to use the `WebGrid` helper.</span></span> <span data-ttu-id="2ac64-232">이 도우미는 표 또는 테이블 (행 및 열)에 표시를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-232">This helper produces a display in a grid or table (rows and columns).</span></span> <span data-ttu-id="2ac64-233">여기에서 볼 수 있듯이 서식 지정 및 기타 기능을 사용 하 여 그리드를 구체화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-233">As you'll see, you'll be able refine the grid with formatting and other features.</span></span>

<span data-ttu-id="2ac64-234">표를 실행 하려면 몇 줄의 코드를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-234">To run the grid, you'll have to write a few lines of code.</span></span> <span data-ttu-id="2ac64-235">이러한 몇 가지 줄은이 자습서에서 수행 하는 거의 모든 데이터 액세스에 대 한 일종의 패턴으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-235">These few lines will serve as a kind of pattern for almost all of the data access that you do in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="2ac64-236">실제로는 페이지에 데이터를 표시 하는 다양 한 옵션이 있습니다. `WebGrid` 도우미는 하나 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-236">You actually have many options for displaying data on a page; the `WebGrid` helper is just one.</span></span> <span data-ttu-id="2ac64-237">이 자습서에서는 데이터를 표시 하는 가장 쉬운 방법 이며 매우 유연 하기 때문에이 자습서를 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-237">We chose it for this tutorial because it's the easiest way to display data and because it's reasonably flexible.</span></span> <span data-ttu-id="2ac64-238">다음 자습서 집합에서 페이지의 데이터로 작업 하는 "수동" 방법을 사용 하 여 데이터를 표시 하는 방법에 대 한 직접 제어를 제공 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-238">In the next tutorial set, you'll see how to use a more "manual" way to work with data in the page, which gives you more direct control over how to display the data.</span></span>

<span data-ttu-id="2ac64-239">WebMatrix의 왼쪽 창에서 **파일** 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-239">In the left pane in WebMatrix, click the **Files** workspace.</span></span>

<span data-ttu-id="2ac64-240">만든 새 데이터베이스는 *App\_Data* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-240">The new database you created is in the *App\_Data* folder.</span></span> <span data-ttu-id="2ac64-241">폴더가 아직 없는 경우 WebMatrix는 새 데이터베이스에 대해 해당 폴더를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-241">If the folder didn't already exist, WebMatrix created it for your new database.</span></span> <span data-ttu-id="2ac64-242">이전에 도우미를 설치 했을 때 폴더가 존재 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-242">(The folder might have existed if you'd previously installed helpers.)</span></span>

<span data-ttu-id="2ac64-243">트리 뷰에서 웹 사이트의 루트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-243">In the tree view, select the root of the website.</span></span> <span data-ttu-id="2ac64-244">웹 사이트의 루트를 선택 해야 합니다. 그렇지 않으면 새 파일이 App\_Data 폴더에 추가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-244">You must select the root of the website; otherwise, the new file might be added to the App\_Data folder.</span></span>

<span data-ttu-id="2ac64-245">리본에서 **새로 만들기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-245">In the ribbon, click **New**.</span></span> <span data-ttu-id="2ac64-246">**파일 형식 선택** 상자에서 **CSHTML**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-246">In the **Choose a File Type** box, choose **CSHTML**.</span></span>

<span data-ttu-id="2ac64-247">**이름** 상자에서 새 페이지의 이름을 "동영상이. cshtml"로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-247">In the **Name** box, name the new page "Movies.cshtml":</span></span>

![' 동영상 ' 페이지를 표시 하는 ' 파일 형식 선택 ' 대화 상자](displaying-data/_static/image17.png)

<span data-ttu-id="2ac64-249">**확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-249">Click the **OK** button.</span></span> <span data-ttu-id="2ac64-250">WebMatrix는 일부 기본 요소가 포함 된 새 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-250">WebMatrix opens a new file with some skeleton elements in it.</span></span> <span data-ttu-id="2ac64-251">먼저 데이터베이스에서 데이터를 가져오는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-251">First you'll write some code to go get the data from the database.</span></span> <span data-ttu-id="2ac64-252">그런 다음 페이지에 태그를 추가 하 여 실제로 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-252">Then you'll add markup to the page to actually display the data.</span></span>

### <a name="writing-the-data-query-code"></a><span data-ttu-id="2ac64-253">데이터 쿼리 코드 작성</span><span class="sxs-lookup"><span data-stu-id="2ac64-253">Writing the Data Query Code</span></span>

<span data-ttu-id="2ac64-254">페이지 맨 위에서 `@{`와 `}` 문자 사이에 다음 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-254">At the top of the page, between the `@{` and `}` characters, enter the following code.</span></span> <span data-ttu-id="2ac64-255">(여는 중괄호와 닫는 중괄호 사이에이 코드를 입력 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="2ac64-255">(Make sure that you enter this code between the opening and closing braces.)</span></span>

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

<span data-ttu-id="2ac64-256">첫 번째 줄은 앞에서 만든 데이터베이스를 엽니다 .이 데이터베이스는 데이터베이스를 사용 하 여 작업을 수행 하기 전에 항상 첫 번째 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-256">The first line opens the database that you created earlier, which is always the first step before doing something with the database.</span></span> <span data-ttu-id="2ac64-257">열려는 데이터베이스의 `Database.Open` 메서드 이름을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-257">You tell the `Database.Open` method name of the database to open.</span></span> <span data-ttu-id="2ac64-258">이름에는 *.sdf* 를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-258">Notice that you don't include *.sdf* in the name.</span></span> <span data-ttu-id="2ac64-259">`Open` 메서드는 *.sdf* 파일 (즉, *webpagesmovies .sdf*)을 찾고 있으며 *.sdf* 파일이 *App\_Data* 폴더에 있는지를 전제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-259">The `Open` method assumes that it's looking for an *.sdf* file (that is, *WebPagesMovies.sdf*) and that the *.sdf* file is in the *App\_Data* folder.</span></span> <span data-ttu-id="2ac64-260">(이전에는 *앱\_데이터* 폴더를 예약 했습니다 .이 시나리오는 ASP.NET에서 해당 이름에 대 한 가정을 수행 하는 위치 중 하나입니다.)</span><span class="sxs-lookup"><span data-stu-id="2ac64-260">(Earlier we noted that the *App\_Data* folder is reserved; this scenario is one of the places where ASP.NET makes assumptions about that name.)</span></span>

<span data-ttu-id="2ac64-261">데이터베이스를 열 때이에 대 한 참조는 `db`라는 변수에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-261">When the database is opened, a reference to it is put into the variable named `db`.</span></span> <span data-ttu-id="2ac64-262">(임의의 이름을 지정할 수 있음) `db` 변수는 데이터베이스와의 상호 작용을 종료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-262">(Which could be named anything.) The `db` variable is how you'll end up interacting with the database.</span></span>

<span data-ttu-id="2ac64-263">두 번째 줄은 실제로 `Query` 메서드를 사용 하 여 데이터베이스 데이터를 인출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-263">The second line actually fetches the database data by using the `Query` method.</span></span> <span data-ttu-id="2ac64-264">이 코드가 작동 하는 방식 확인: `db` 변수는 열린 데이터베이스에 대 한 참조를 포함 하 고 `db` 변수 (`db.Query`)를 사용 하 여 `Query` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-264">Notice how this code works: the `db` variable has a reference to the opened database, and you invoke the `Query` method by using the `db` variable (`db.Query`).</span></span>

<span data-ttu-id="2ac64-265">쿼리 자체는 SQL `Select` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-265">The query itself is a SQL `Select` statement.</span></span> <span data-ttu-id="2ac64-266">SQL에 대 한 약간의 배경 정보는 뒷부분에서 설명 합니다. 문에서 `Movies`는 쿼리할 테이블을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-266">(For a little background about SQL, see the explanation later.) In the statement, `Movies` identifies the table to query.</span></span> <span data-ttu-id="2ac64-267">`*` 문자는 쿼리에서 테이블의 모든 열을 반환 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-267">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="2ac64-268">열을 쉼표로 구분 하 여 나열할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-268">(You could also list columns individually, separated by commas.)</span></span>

<span data-ttu-id="2ac64-269">쿼리의 결과 (있는 경우)가 반환 되 고 `selectedData` 변수에서 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-269">The results of the query, if any, are returned and made available in the `selectedData` variable.</span></span> <span data-ttu-id="2ac64-270">마찬가지로 변수 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-270">Again, the variable could be named anything.</span></span>

<span data-ttu-id="2ac64-271">마지막으로 세 번째 줄은 `WebGrid` 도우미의 인스턴스를 사용 하도록 ASP.NET에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-271">Finally, the third line tells ASP.NET that you want to use an instance of the `WebGrid` helper.</span></span> <span data-ttu-id="2ac64-272">`new` 키워드를사용 하 여 도우미 개체를 만들고 `selectedData` 변수를 통해 쿼리 결과를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-272">You create (*instantiate*) the helper object by using the `new` keyword and pass it the query results via the `selectedData` variable.</span></span> <span data-ttu-id="2ac64-273">새 `WebGrid` 개체는 데이터베이스 쿼리의 결과와 함께 `grid` 변수에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-273">The new `WebGrid` object, along with the results of the database query, are made available in the `grid` variable.</span></span> <span data-ttu-id="2ac64-274">실제로 페이지에 데이터를 표시 하는 데 시간이 조금 더 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-274">You'll need that result in a moment to actually display the data in the page.</span></span>

<span data-ttu-id="2ac64-275">이 단계에서 데이터베이스가 열리고, 원하는 데이터를 얻 었으 며, 해당 데이터를 사용 하 여 `WebGrid` 도우미를 준비 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-275">At this stage, the database has been opened, you've gotten the data you want, and you've prepared the `WebGrid` helper with that data.</span></span> <span data-ttu-id="2ac64-276">다음으로 페이지에서 태그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-276">Next is to create the markup in the page.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="2ac64-277">**SQL(구조적 쿼리 언어)**</span><span class="sxs-lookup"><span data-stu-id="2ac64-277">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="2ac64-278">SQL은 데이터베이스에서 데이터를 관리 하기 위한 대부분의 관계형 데이터베이스에 사용 되는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-278">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="2ac64-279">여기에는 데이터를 검색 하 고 업데이트 하는 데 사용할 수 있는 명령이 포함 되어 있으며,이를 통해 데이터베이스 테이블에서 데이터를 만들고 수정 하 고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-279">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage data in database tables.</span></span> <span data-ttu-id="2ac64-280">SQL은 프로그래밍 언어 (예 C#:)와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-280">SQL is different than a programming language (like C#).</span></span> <span data-ttu-id="2ac64-281">SQL을 사용 하면 데이터베이스에서 원하는 작업을 수행 하 고, 데이터를 가져오거나 작업을 수행 하는 방법을 파악 하는 데이터베이스 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-281">With SQL, you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="2ac64-282">다음은 몇 가지 SQL 명령의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-282">Here are examples of some SQL commands and what they do:</span></span>
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="2ac64-283">첫 번째 `Select` 문은 *동영상* 테이블에서 `*`로 지정 된 모든 열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-283">The first `Select` statement gets all the columns (specified by `*`) from the *Movies* table.</span></span>
> 
> <span data-ttu-id="2ac64-284">두 번째 `Select` 문은 *Product* 테이블에서 price 열 값이 10 보다 많은 레코드에서 ID, 이름 및 가격 열을 인출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-284">The second `Select` statement fetches the ID, Name, and Price columns from records in the *Product* table whose Price column value is more than 10.</span></span> <span data-ttu-id="2ac64-285">이 명령은 Name 열의 값을 기준으로 결과를 알파벳 순서로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-285">The command returns the results in alphabetical order based on the values of the Name column.</span></span> <span data-ttu-id="2ac64-286">가격 기준과 일치 하는 레코드가 없는 경우이 명령은 빈 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-286">If no records match the price criteria, the command returns an empty set.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> <span data-ttu-id="2ac64-287">이 명령은 *Product* 테이블에 새 레코드를 삽입 하 고 Name 열을 "크 라 상"로 설정 하 고 Description 열을 "a 부실 즐거움"로 설정 하 고 price를 1.99으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-287">This command inserts a new record into the *Product* table, setting the Name column to "Croissant", the Description column to "A flaky delight", and the price to 1.99.</span></span>
> 
> <span data-ttu-id="2ac64-288">숫자가 아닌 값을 지정 하는 경우이 값은에서 C#와 같이 작은따옴표로 묶여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-288">Notice that when you're specifying a non-numeric value, the value is enclosed in single quotation marks (not double quotation marks, as in C#).</span></span> <span data-ttu-id="2ac64-289">이러한 따옴표는 텍스트 또는 날짜 값에는 사용할 수 있지만 숫자 앞뒤에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-289">You use these quotation marks around text or date values, but not around numbers.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> <span data-ttu-id="2ac64-290">이 명령은 만료 날짜 열이 2008 년 1 월 1 일 이전인 *Product* 테이블의 레코드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-290">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="2ac64-291">이 명령은 *Product* 테이블에 이러한 열이 있다고 가정 합니다. 날짜는 여기에 MM/DD/YYYY 형식으로 입력 되지만 로캘에 사용 되는 형식으로 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-291">(The command assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="2ac64-292">`Insert` 및 `Delete` 명령은 결과 집합을 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-292">The `Insert` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="2ac64-293">대신 명령의 영향을 받은 레코드 수를 나타내는 숫자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-293">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="2ac64-294">이러한 작업 중 일부 (예: 레코드 삽입 및 삭제)의 경우 작업을 요청 하는 프로세스에 데이터베이스에 대 한 적절 한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-294">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="2ac64-295">따라서 프로덕션 데이터베이스의 경우 데이터베이스에 연결할 때 사용자 이름과 암호를 제공 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-295">That's why for production databases you often have to supply a user name and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="2ac64-296">수십 개의 SQL 명령이 있지만 모두 여기에 표시 되는 명령과 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-296">There are dozens of SQL commands, but they all follow a pattern like the commands you see here.</span></span> <span data-ttu-id="2ac64-297">SQL 명령을 사용 하 여 데이터베이스 테이블을 만들고, 테이블의 레코드 수를 계산 하 고, 가격을 계산 하 고, 더 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-297">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>

### <a name="adding-markup-to-display-the-data"></a><span data-ttu-id="2ac64-298">데이터를 표시 하는 태그 추가</span><span class="sxs-lookup"><span data-stu-id="2ac64-298">Adding Markup to Display the Data</span></span>

<span data-ttu-id="2ac64-299">`<head>` 요소 내에서 `<title>` 요소의 내용을 "영화"로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-299">Inside the `<head>` element, set contents of the `<title>` element to "Movies":</span></span>

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

<span data-ttu-id="2ac64-300">페이지의 `<body>` 요소 내에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-300">Inside the `<body>` element of the page, add the following:</span></span>

[!code-html[Main](displaying-data/samples/sample3.html)]

<span data-ttu-id="2ac64-301">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-301">That's it.</span></span> <span data-ttu-id="2ac64-302">`grid` 변수는 이전 코드에서 `WebGrid` 개체를 만들 때 만든 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-302">The `grid` variable is the value you created when you created the `WebGrid` object in code earlier.</span></span>

<span data-ttu-id="2ac64-303">WebMatrix 트리 보기에서 페이지를 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 시작**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-303">In the WebMatrix tree view, right-click the page and select **Launch in browser**.</span></span> <span data-ttu-id="2ac64-304">이 페이지와 유사한 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-304">You'll see something like this page:</span></span>

![동영상 테이블의 기본 WebGrid 도우미 출력](displaying-data/_static/image18.png)

<span data-ttu-id="2ac64-306">열 머리글 링크를 클릭 하 여 해당 열을 기준으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-306">Click a column heading link to sort by that column.</span></span> <span data-ttu-id="2ac64-307">제목을 클릭 하 여 정렬할 수 있는 기능은 **Webgrid** 도우미에 기본 제공 되는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-307">Being able to sort by clicking a heading is a feature that's built into the **WebGrid** helper.</span></span>

<span data-ttu-id="2ac64-308">`GetHtml` 메서드는 이름에서 알 때 데이터를 표시 하는 태그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-308">The `GetHtml` method, as its name suggests, generates markup that displays the data.</span></span> <span data-ttu-id="2ac64-309">기본적으로 `GetHtml` 메서드는 HTML `<table>` 요소를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-309">By default, the `GetHtml` method generates an HTML `<table>` element.</span></span> <span data-ttu-id="2ac64-310">(원하는 경우 브라우저에서 페이지의 원본을 확인 하 여 렌더링을 확인할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="2ac64-310">(If you want, you can verify the rendering by looking at the source of the page in the browser.)</span></span>

## <a name="modifying-the-look-of-the-grid"></a><span data-ttu-id="2ac64-311">그리드 모양 수정</span><span class="sxs-lookup"><span data-stu-id="2ac64-311">Modifying the Look of the Grid</span></span>

<span data-ttu-id="2ac64-312">방금 했던 것 처럼 `WebGrid` 도우미를 사용 하는 것은 쉽지만 결과 표시는 일반입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-312">Using the `WebGrid` helper like you just did is easy, but the resulting display is plain.</span></span> <span data-ttu-id="2ac64-313">`WebGrid` 도우미에는 데이터가 표시 되는 방식을 제어할 수 있는 모든 종류의 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-313">The `WebGrid` helper has all sorts of options that let you control how the data is displayed.</span></span> <span data-ttu-id="2ac64-314">이 자습서에서 살펴볼 수 있는 방법은 너무 많습니다 .이 섹션에서는 이러한 옵션 중 일부에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-314">There are far too many to explore in this tutorial, but this section will give you an idea of some of those options.</span></span> <span data-ttu-id="2ac64-315">몇 가지 추가 옵션은이 시리즈의 이후 자습서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-315">A few additional options will be covered in later tutorials in this series.</span></span>

### <a name="specifying-individual-columns-to-display"></a><span data-ttu-id="2ac64-316">표시할 개별 열 지정</span><span class="sxs-lookup"><span data-stu-id="2ac64-316">Specifying Individual Columns to Display</span></span>

<span data-ttu-id="2ac64-317">시작 하려면 특정 열만 표시 하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-317">To start, you can specify that you want to display only certain columns.</span></span> <span data-ttu-id="2ac64-318">기본적으로 표 형태 창에는 *동영상* 테이블의 네 열이 모두 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-318">By default, as you've seen, the grid shows all four of the columns from the *Movies* table.</span></span>

<span data-ttu-id="2ac64-319">*동영상과* 파일에서 방금 추가한 `@grid.GetHtml()` 태그를 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-319">In the *Movies.cshtml* file, replace the `@grid.GetHtml()` markup that you just added with the following:</span></span>

[!code-css[Main](displaying-data/samples/sample4.css)]

<span data-ttu-id="2ac64-320">도우미에 표시할 열을 알리기 위해 `GetHtml` 메서드에 `columns` 매개 변수를 포함 하 고 열 컬렉션을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-320">To tell the helper which columns to display, you include a `columns` parameter for the `GetHtml` method and pass in a collection of columns.</span></span> <span data-ttu-id="2ac64-321">컬렉션에서 포함할 각 열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-321">In the collection, you specify each column to include.</span></span> <span data-ttu-id="2ac64-322">`grid.Column` 개체를 포함 하 여 표시할 개별 열을 지정 하 고 원하는 데이터 열의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-322">You specify an individual column to display by including a `grid.Column` object, and pass in the name of the data column you want.</span></span> <span data-ttu-id="2ac64-323">이러한 열은 SQL 쿼리 결과에 포함 되어야 합니다. `WebGrid` 도우미가 쿼리에서 반환 되지 않은 열을 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-323">(These columns must be included in the SQL query results — the `WebGrid` helper cannot display columns that were not returned by the query.)</span></span>

<span data-ttu-id="2ac64-324">브라우저에서 *동영상과* 페이지를 다시 시작 합니다. 이번에는 다음과 같은 표시를 얻을 수 있습니다 (ID 열이 표시 되지 않음).</span><span class="sxs-lookup"><span data-stu-id="2ac64-324">Launch the *Movies.cshtml* page in the browser again, and this time you get a display like the following one (notice that no ID column is displayed):</span></span>

![선택한 열만 표시 하는 WebGrid 표시](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a><span data-ttu-id="2ac64-326">표 모양 변경</span><span class="sxs-lookup"><span data-stu-id="2ac64-326">Changing the Look of the Grid</span></span>

<span data-ttu-id="2ac64-327">열을 표시 하기 위한 몇 가지 옵션이 몇 가지 있습니다 .이 중 일부는이 집합의 이후 자습서에서 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-327">There are quite a few more options for displaying columns, some of which will be explored in later tutorials in this set.</span></span> <span data-ttu-id="2ac64-328">현재이 섹션에서는 표를 전체적으로 스타일을 지정할 수 있는 방법을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-328">For now, this section will introduce you to ways in which you can style the grid as a whole.</span></span>

<span data-ttu-id="2ac64-329">페이지의 `<head>` 섹션 내에서 닫는 `</head>` 태그 바로 앞에 다음 `<style>` 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-329">Inside the `<head>` section of the page, just before the closing `</head>` tag, add the following `<style>` element:</span></span>

[!code-css[Main](displaying-data/samples/sample5.css)]

<span data-ttu-id="2ac64-330">이 CSS 태그는 `grid`, `head`등의 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-330">This CSS markup defines classes named `grid`, `head`, and so on.</span></span> <span data-ttu-id="2ac64-331">이러한 스타일 정의를 별도의 *.css* 파일에 넣고 페이지에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-331">You could also put these style definitions in a separate *.css* file and link that to the page.</span></span> <span data-ttu-id="2ac64-332">실제로는이 자습서의 뒷부분에서이 작업을 수행 합니다. 그러나이 자습서의 작업을 쉽게 수행 하기 위해 데이터를 표시 하는 동일한 페이지 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-332">(In fact, you'll do that later in this tutorial set.) But to make things easy for this tutorial, they're inside the same page that displays the data.</span></span>

<span data-ttu-id="2ac64-333">이제 `WebGrid` 도우미를 가져와 이러한 스타일 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-333">Now you can get the `WebGrid` helper to use these style classes.</span></span> <span data-ttu-id="2ac64-334">도우미에는이 목적에 대 한 다양 한 속성 (예: `tableStyle`)이 있습니다. 여기에는 CSS 스타일 클래스 이름을 할당 하 고 해당 클래스 이름은 도우미가 렌더링 하는 태그의 일부로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-334">The helper has a number of properties (for example, `tableStyle`) for just this purpose — you assign a CSS style class name to them, and that class name is rendered as part of the markup that's rendered by the helper.</span></span>

<span data-ttu-id="2ac64-335">이제이 코드 처럼 보이도록 `grid.GetHtml` 태그를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-335">Change the `grid.GetHtml` markup so that it now looks like this code:</span></span>

[!code-css[Main](displaying-data/samples/sample6.css)]

<span data-ttu-id="2ac64-336">`tableStyle`, `headerStyle`및 `alternatingRowStyle` 매개 변수를 `GetHtml` 메서드에 추가 했으므로 여기에서 새로운 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-336">What's new here is that you've added `tableStyle`, `headerStyle`, and `alternatingRowStyle` parameters to the `GetHtml` method.</span></span> <span data-ttu-id="2ac64-337">이러한 매개 변수는 잠시 전에 추가한 CSS 스타일의 이름으로 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-337">These parameters have been set to the names of the CSS styles that you added a moment ago.</span></span>

<span data-ttu-id="2ac64-338">페이지를 실행 합니다. 이번에는 이전 보다 훨씬 단순한 표 모양의 표가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-338">Run the page, and this time you see a grid that looks much less plain than before:</span></span>

![CSS 클래스 이름으로 설정 된 매개 변수를 포함 하는 WebGrid 표시](displaying-data/_static/image20.png)

<span data-ttu-id="2ac64-340">`GetHtml` 메서드가 생성 된 것을 확인 하기 위해 브라우저에서 페이지의 소스를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-340">To see what the `GetHtml` method generated, you can look at the source of the page in the browser.</span></span> <span data-ttu-id="2ac64-341">여기서는 자세히 다루지 않지만 `tableStyle`와 같은 매개 변수를 지정 하 여 표를 통해 다음과 같은 HTML 태그를 생성 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-341">We won't go into detail here, but the important point is that by specifying parameters like `tableStyle`, you caused the grid to generate HTML tags like the following:</span></span>

`<table class="grid">`

<span data-ttu-id="2ac64-342">`<table>` 태그에는 이전에 추가한 CSS 규칙 중 하나를 참조 하는 `class` 특성이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-342">The `<table>` tag has had a `class` attribute added to it that references one of the CSS rules that you added earlier.</span></span> <span data-ttu-id="2ac64-343">이 코드는 `GetHtml` 메서드에 서로 다른 매개 변수를 &mdash; 하 여 메서드가 태그와 함께 생성 하는 CSS 클래스를 참조할 수 있도록 하는 기본 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-343">This code shows you the basic pattern &mdash; different parameters for the `GetHtml` method let you reference CSS classes that the method then generates along with the markup.</span></span> <span data-ttu-id="2ac64-344">CSS 클래스를 사용 하 여 수행 하는 작업은 사용자에 게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-344">What you do with the CSS classes is up to you.</span></span>

## <a name="adding-paging"></a><span data-ttu-id="2ac64-345">페이징 추가</span><span class="sxs-lookup"><span data-stu-id="2ac64-345">Adding Paging</span></span>

<span data-ttu-id="2ac64-346">이 자습서의 마지막 작업으로, 표에 페이징을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-346">As the last task for this tutorial, you'll add paging to the grid.</span></span> <span data-ttu-id="2ac64-347">지금은 모든 영화를 한 번에 표시 하는 것은 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-347">Right now it's no problem to display all your movies at once.</span></span> <span data-ttu-id="2ac64-348">그러나 수백 개의 영화를 추가한 경우 페이지 표시 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-348">But if you added hundreds of movies, the page display would get long.</span></span>

<span data-ttu-id="2ac64-349">페이지 코드에서 `WebGrid` 개체를 만드는 줄을 다음 코드로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-349">In the page code, change the line that creates the `WebGrid` object to the following code:</span></span>

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

<span data-ttu-id="2ac64-350">이전과의 유일한 차이점은 3으로 설정 된 `rowsPerPage` 매개 변수를 추가 했다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-350">The only difference from before is that you've added a `rowsPerPage` parameter that's set to 3.</span></span>

<span data-ttu-id="2ac64-351">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-351">Run the page.</span></span> <span data-ttu-id="2ac64-352">표는 한 번에 3 개의 행을 표시 하 고 데이터베이스의 영화를 통해 페이지를 이동할 수 있는 탐색 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-352">The grid displays 3 rows at a time, plus navigation links that let you page through the movies in your database:</span></span>

![페이징을 사용 하 여 WebGrid 표시](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a><span data-ttu-id="2ac64-354">다음에서 시작</span><span class="sxs-lookup"><span data-stu-id="2ac64-354">Coming Up Next</span></span>

<span data-ttu-id="2ac64-355">다음 자습서에서는 Razor 및 C# 코드를 사용 하 여 양식에서 사용자 입력을 가져오는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-355">In the next tutorial, you'll learn how to use Razor and C# code to get user input in a form.</span></span> <span data-ttu-id="2ac64-356">제목 또는 장르로 영화를 찾을 수 있도록 동영상 페이지에 검색 상자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac64-356">You'll add a search box to the Movies page so that you can find movies by title or genre.</span></span>

## <a name="complete-listing-for-movies-page"></a><span data-ttu-id="2ac64-357">동영상에 대 한 전체 목록 페이지</span><span class="sxs-lookup"><span data-stu-id="2ac64-357">Complete Listing for Movies Page</span></span>

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="2ac64-358">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2ac64-358">Additional Resources</span></span>

- [<span data-ttu-id="2ac64-359">Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="2ac64-359">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> <span data-ttu-id="2ac64-360">[이전](intro-to-web-pages-programming.md)
> [다음](form-basics.md)</span><span class="sxs-lookup"><span data-stu-id="2ac64-360">[Previous](intro-to-web-pages-programming.md)
[Next](form-basics.md)</span></span>
