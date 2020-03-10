---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: ASP.NET 웹 페이지-데이터베이스 데이터 삭제 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다. ASP.NET 웹 Pa에서 데이터베이스 데이터를 업데이트 하 여 시리즈를 완료 했다고 가정 합니다.
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510461"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="65387-104">ASP.NET 웹 페이지 소개-데이터베이스 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="65387-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>

<span data-ttu-id="65387-105">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="65387-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="65387-106">이 자습서에서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65387-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="65387-107">[ASP.NET 웹 페이지에서 데이터베이스 데이터를 업데이트](updating-data.md)하 여 계열을 완료 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="65387-108">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="65387-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="65387-109">레코드 목록에서 개별 레코드를 선택 하는 방법</span><span class="sxs-lookup"><span data-stu-id="65387-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="65387-110">데이터베이스에서 단일 레코드를 삭제 하는 방법</span><span class="sxs-lookup"><span data-stu-id="65387-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="65387-111">특정 단추를 폼에서 클릭 했는지 확인 하는 방법</span><span class="sxs-lookup"><span data-stu-id="65387-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="65387-112">설명 하는 기능/기술:</span><span class="sxs-lookup"><span data-stu-id="65387-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="65387-113">`WebGrid` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="65387-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="65387-114">SQL `Delete` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="65387-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="65387-115">SQL `Delete` 명령을 실행 하는 `Database.Execute` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="65387-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="65387-116">만들 내용</span><span class="sxs-lookup"><span data-stu-id="65387-116">What You'll Build</span></span>

<span data-ttu-id="65387-117">이전 자습서에서는 기존 데이터베이스 레코드를 업데이트 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="65387-118">이 자습서는 레코드를 업데이트 하는 대신 삭제 하는 것을 제외 하 고는 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="65387-119">이러한 프로세스는 거의 동일 합니다. 단, 삭제가 더 간단 하기 때문에이 자습서는 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="65387-120">*동영상* 페이지에서 이전에 추가한 **편집** 링크와 함께 각 동영상 옆에 있는 **삭제** 링크를 표시 하도록 `WebGrid` 도우미를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![각 영화에 대 한 삭제 링크를 보여 주는 동영상 페이지](deleting-data/_static/image1.png)

<span data-ttu-id="65387-122">편집과 마찬가지로, **삭제** 링크를 클릭 하면 동영상 정보가 이미 양식에 있는 다른 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![동영상이 표시 된 동영상 페이지 삭제](deleting-data/_static/image2.png)

<span data-ttu-id="65387-124">그런 다음 단추를 클릭 하 여 레코드를 영구적으로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="65387-125">동영상 목록에 삭제 링크 추가</span><span class="sxs-lookup"><span data-stu-id="65387-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="65387-126">먼저 `WebGrid` 도우미에 **삭제** 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="65387-127">이 링크는 이전 자습서에서 추가한 **편집** 링크와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="65387-128">*영화 cshtml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="65387-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="65387-129">열을 추가 하 여 페이지 본문의 `WebGrid` 태그를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="65387-130">수정 된 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="65387-131">새 열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="65387-132">표를 구성 하는 방법은 **편집** 열이 표의 맨 위에 있고 **삭제** 열은 가장 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="65387-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="65387-133">(현재는 `Year` 열 뒤에 쉼표가 있습니다. 이러한 링크 열이 이동 하는 위치에 대 한 특별 한 사항은 없으며, 서로에 게 쉽게 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="65387-134">이 경우 혼합 하는 것이 더 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="65387-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![편집 및 세부 정보 링크가 있는 동영상 페이지는 서로 옆에 있지 않은 것으로 표시 됩니다.](deleting-data/_static/image3.png)

<span data-ttu-id="65387-136">새 열은 텍스트가 "Delete" 라고 표시 된 링크 (`<a>` 요소)를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="65387-137">링크의 대상 (`href` 특성)은 다음 URL과 같이 궁극적으로 확인 되는 코드로, 각 동영상 마다 `id` 값이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="65387-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="65387-138">이 링크는 *DeleteMovie* 라는 페이지를 호출 하 고 선택한 영화 ID를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="65387-139">이 자습서는 이전 자습서의 **편집** 링크와 거의 동일 하기 때문에이 링크를 생성 하는 방법에 대해서는 자세히 다루지 않습니다 ([ASP.NET 웹 페이지의 데이터베이스 데이터 업데이트](updating-data.md)).</span><span class="sxs-lookup"><span data-stu-id="65387-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="65387-140">삭제 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="65387-140">Creating the Delete Page</span></span>

<span data-ttu-id="65387-141">이제 표에서 **삭제** 링크의 대상이 될 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="65387-142">**중요** 먼저 삭제할 레코드를 선택 하 고 별도의 페이지 및 단추를 사용 하 여 프로세스를 확인 하는 방법은 보안에 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="65387-143">이전 자습서에서 읽은 것 처럼 웹 사이트를 변경 하는 것은 *항상* HTTP POST 작업을 사용 하는 양식 &mdash;를 사용 하 여 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="65387-144">링크를 클릭 하 여 사이트를 변경 (즉, 가져오기 작업 사용) 할 수 있는 경우 사용자가 사이트에 대 한 간단한 요청을 만들고 데이터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="65387-145">사이트를 인덱싱하는 검색 엔진 크롤러도 다음 링크를 통해 실수로 데이터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="65387-146">앱에서 사용자가 레코드를 변경할 수 있는 경우 편집을 위해 사용자에 게 레코드를 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="65387-147">그러나 레코드를 삭제 하는 경우이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="65387-148">그러나이 단계를 건너뛰지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="65387-148">Don't skip that step, though.</span></span> <span data-ttu-id="65387-149">사용자가 레코드를 확인 하 고 의도 한 레코드를 삭제 하 고 있는지 확인 하는 것도 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="65387-150">이후 자습서 집합에서 사용자가 레코드를 삭제 하기 전에 로그인 해야 하는 로그인 기능을 추가 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>

<span data-ttu-id="65387-151">*DeleteMovie* 라는 페이지를 만들고 파일의 내용을 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="65387-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="65387-152">이 태그는 텍스트 상자 (`<input type="text">`)를 사용 하는 대신 `<span>` 요소를 포함 하는 것을 제외 하 고는 *Editmovie* 페이지와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="65387-153">편집할 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-153">There's nothing here to edit.</span></span> <span data-ttu-id="65387-154">사용자가 오른쪽 동영상을 삭제 하 고 있는지 확인할 수 있도록 영화 세부 정보를 표시 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65387-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="65387-155">태그에는 사용자가 동영상 목록 페이지로 돌아갈 수 있는 링크가 이미 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="65387-156">*Editmovie* 페이지에서와 같이 선택한 동영상의 ID는 숨겨진 필드에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65387-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="65387-157">이는 첫 번째 위치의 페이지에 쿼리 문자열 값으로 전달 됩니다. 유효성 검사 오류를 표시 하는 `Html.ValidationSummary` 호출이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="65387-158">이 경우 페이지에 전달 된 영화 ID가 없거나 동영상 ID가 잘못 된 경우 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="65387-159">이 상황은 다른 사람이 *영화* 페이지에서 영화를 먼저 선택 하지 않고이 페이지를 실행 한 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="65387-160">단추 캡션은 **동영상 삭제**이며 해당 name 특성은 `buttonDelete`로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65387-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="65387-161">`name` 특성은 폼을 전송한 단추를 식별 하기 위해 코드에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65387-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="65387-162">1\) 코드를 작성 해야 합니다. 페이지가 처음 표시 될 때 영화 세부 정보를 읽고 사용자가 단추를 클릭 하면 동영상이 실제로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65387-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="65387-163">단일 영화를 읽기 위한 코드 추가</span><span class="sxs-lookup"><span data-stu-id="65387-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="65387-164">*DeleteMovie* 페이지 위쪽에 다음 코드 블록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="65387-165">이 태그는 *Editmovie* 페이지의 해당 코드와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="65387-166">쿼리 문자열에서 영화 ID를 가져오고 ID를 사용 하 여 데이터베이스에서 레코드를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="65387-167">이 코드는 페이지에 전달 되는 영화 ID가 유효한 지 확인 하기 위해 유효성 검사 테스트 (`IsInt()` 및 `row != null`)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="65387-168">이 코드는 페이지가 처음 실행 될 때만 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="65387-169">사용자가 **동영상 삭제** 단추를 클릭할 때 데이터베이스에서 동영상 레코드를 다시 읽지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="65387-170">따라서 영화를 읽는 코드는 *요청이 post 작업 (양식 전송)이 아닌 경우*에 `if(!IsPost)` &mdash; 있음을 나타내는 테스트 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="65387-171">선택한 동영상을 삭제 하는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="65387-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="65387-172">사용자가 단추를 클릭할 때 동영상을 삭제 하려면 `@` 블록의 닫는 중괄호 바로 안에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="65387-173">이 코드는 기존 레코드를 업데이트 하는 코드와 유사 하지만 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="65387-174">이 코드는 기본적으로 SQL `Delete` 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="65387-175">*Editmovie* 페이지에서와 같이 코드는 `if(IsPost)` 블록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="65387-176">이번에는 `if()` 조건이 약간 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="65387-177">여기에는 두 가지 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-177">There are two conditions here.</span></span> <span data-ttu-id="65387-178">첫 번째는 `if(IsPost)`&mdash; 하기 전에 표시 된 페이지를 전송 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65387-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="65387-179">두 번째 조건은 `!Request["buttonDelete"].IsEmpty()`이며,이는 요청에 `buttonDelete`라는 개체가 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="65387-180">이는 폼을 제출한 단추를 간접적으로 테스트 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65387-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="65387-181">양식에 여러 전송 단추가 있는 경우 클릭 한 단추의 이름만 요청에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65387-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="65387-182">따라서 논리적으로 특정 단추의 이름이 요청 &mdash;에 표시 되거나 코드에 명시 된 대로 표시 되는 경우 해당 단추가 비어 있지 않으면 폼을 전송한 단추 &mdash;.</span><span class="sxs-lookup"><span data-stu-id="65387-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="65387-183">`&&` 연산자는 "and" (논리적 AND)를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="65387-184">따라서 전체 `if` 조건은 ...입니다.</span><span class="sxs-lookup"><span data-stu-id="65387-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="65387-185">*이 요청은 post (첫 번째 시간 요청이 아님)입니다.*</span><span class="sxs-lookup"><span data-stu-id="65387-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="65387-186">AND</span><span class="sxs-lookup"><span data-stu-id="65387-186">AND</span></span>  
  
<span data-ttu-id="65387-187">`buttonDelete`단추 *는* *폼을 전송 하는 단추입니다.*</span><span class="sxs-lookup"><span data-stu-id="65387-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="65387-188">이 폼에는 하나의 단추만 포함 되어 있으므로 `buttonDelete`에 대 한 추가 테스트는 기술적으로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="65387-189">계속 해 서 데이터를 영구적으로 제거 하는 작업을 수행 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="65387-190">사용자가 명시적으로 요청한 경우에만 작업을 수행 하는 것이 가능한 지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="65387-191">예를 들어이 페이지를 나중에 확장 하 고 다른 단추를 추가 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="65387-192">이 경우에도 `buttonDelete` 단추를 클릭 한 경우에만 동영상을 삭제 하는 코드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65387-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="65387-193">*Editmovie* 페이지에서와 같이 hidden 필드에서 ID를 가져온 다음 SQL 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="65387-194">`Delete` 문의 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="65387-195">`WHERE` 절과 ID를 포함 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="65387-196">WHERE 절을 생략 하면 *테이블의 모든 레코드가 삭제*됩니다.</span><span class="sxs-lookup"><span data-stu-id="65387-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="65387-197">표시 된 대로 자리 표시자를 사용 하 여 ID 값을 SQL 명령에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="65387-198">동영상 삭제 프로세스 테스트</span><span class="sxs-lookup"><span data-stu-id="65387-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="65387-199">이제를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-199">Now you can test.</span></span> <span data-ttu-id="65387-200">동영상 페이지 *를* 실행 하 고 동영상 옆의 **삭제** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="65387-201">*DeleteMovie* 페이지가 표시 되 면 **동영상 삭제**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65387-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![동영상 삭제 단추가 강조 표시 된 동영상 삭제](deleting-data/_static/image4.png)

<span data-ttu-id="65387-203">이 단추를 클릭 하면 코드가 영화를 삭제 하 고 동영상 목록으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="65387-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="65387-204">여기에서 삭제 된 동영상을 검색 하 고 삭제 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65387-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="65387-205">다음에서 시작</span><span class="sxs-lookup"><span data-stu-id="65387-205">Coming Up Next</span></span>

<span data-ttu-id="65387-206">다음 자습서에서는 사이트의 모든 페이지에 공통적인 모양과 레이아웃을 제공 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65387-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="65387-207">동영상에 대 한 목록 완료 페이지 (Delete 링크로 업데이트 됨)</span><span class="sxs-lookup"><span data-stu-id="65387-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="65387-208">DeleteMovie 페이지에 대 한 전체 목록</span><span class="sxs-lookup"><span data-stu-id="65387-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="65387-209">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="65387-209">Additional Resources</span></span>

- [<span data-ttu-id="65387-210">Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="65387-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="65387-211">W3Schools 사이트의 [SQL DELETE 문](http://www.w3schools.com/sql/sql_delete.asp)</span><span class="sxs-lookup"><span data-stu-id="65387-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="65387-212">[이전](updating-data.md)
> [다음](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="65387-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
