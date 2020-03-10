---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: ASP.NET 웹 페이지 소개-폼을 사용 하 여 데이터베이스 데이터 입력 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 ASP.NET 웹 페이지 (...)를 사용할 때 양식에서 가져온 데이터를 데이터베이스 테이블에 입력 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 05/28/2015
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: b9354a7b97a7df9020a681f709e16a92650cfcf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506603"
---
# <a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a><span data-ttu-id="ffcdf-103">ASP.NET 웹 페이지 소개-폼을 사용 하 여 데이터베이스 데이터 입력</span><span class="sxs-lookup"><span data-stu-id="ffcdf-103">Introducing ASP.NET Web Pages - Entering Database Data by Using Forms</span></span>

<span data-ttu-id="ffcdf-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ffcdf-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="ffcdf-105">이 자습서에서는 ASP.NET 웹 페이지 (Razor)를 사용할 때 입력 양식을 만들고 폼에서 데이터베이스 테이블로 가져오는 데이터를 입력 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-105">This tutorial shows you how to create an entry form and then enter the data that you get from the form into a database table when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="ffcdf-106">[ASP.NET 웹 페이지에서 HTML 폼의 기본 사항을](https://go.microsoft.com/fwlink/?LinkId=251581)통해 계열을 완료 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-106">It assumes you have completed the series through [Basics of HTML Forms in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581).</span></span>
> 
> <span data-ttu-id="ffcdf-107">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="ffcdf-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="ffcdf-108">항목 양식을 처리 하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-108">More about how to process entry forms.</span></span>
> - <span data-ttu-id="ffcdf-109">데이터베이스에서 데이터를 추가 (삽입) 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ffcdf-109">How to add (insert) data in a database.</span></span>
> - <span data-ttu-id="ffcdf-110">사용자가 양식에 필수 값을 입력 했는지 확인 하는 방법 (사용자 입력의 유효성을 검사 하는 방법)</span><span class="sxs-lookup"><span data-stu-id="ffcdf-110">How to make sure that users have entered a required value in a form (how to validate user input).</span></span>
> - <span data-ttu-id="ffcdf-111">유효성 검사 오류를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-111">How to display validation errors.</span></span>
> - <span data-ttu-id="ffcdf-112">현재 페이지에서 다른 페이지로 이동 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-112">How to jump to another page from the current page.</span></span>
>   
> 
> <span data-ttu-id="ffcdf-113">설명 하는 기능/기술:</span><span class="sxs-lookup"><span data-stu-id="ffcdf-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="ffcdf-114">`Database.Execute` 메서드</span><span class="sxs-lookup"><span data-stu-id="ffcdf-114">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="ffcdf-115">SQL `Insert Into` 문</span><span class="sxs-lookup"><span data-stu-id="ffcdf-115">The SQL `Insert Into` statement</span></span>
> - <span data-ttu-id="ffcdf-116">`Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-116">The `Validation` helper.</span></span>
> - <span data-ttu-id="ffcdf-117">`Response.Redirect` 메서드</span><span class="sxs-lookup"><span data-stu-id="ffcdf-117">The `Response.Redirect` method.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="ffcdf-118">만들 내용</span><span class="sxs-lookup"><span data-stu-id="ffcdf-118">What You'll Build</span></span>

<span data-ttu-id="ffcdf-119">앞의 자습서에서는 데이터베이스를 만드는 방법을 보여 주었습니다 **. 데이터베이스 작업 영역에서** 작업 하는 WebMatrix에서 직접 데이터베이스를 편집 하 여 데이터베이스 데이터를 입력 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-119">In the tutorial earlier that showed you how to create a database, you entered database data by editing the database directly in WebMatrix, working in the **Database** workspace.</span></span> <span data-ttu-id="ffcdf-120">그러나 대부분의 앱에서 데이터를 데이터베이스에 저장 하는 것은 실용적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-120">In most apps, that's not a practical way to put data into the database, though.</span></span> <span data-ttu-id="ffcdf-121">따라서이 자습서에서는 사용자가 데이터를 입력 하 고 데이터베이스에 저장 하는 데 사용할 수 있는 웹 기반 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-121">So in this tutorial, you'll create a web-based interface that lets you or anyone enter data and save it to the database.</span></span>

<span data-ttu-id="ffcdf-122">새 영화를 입력할 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-122">You'll create a page where you can enter new movies.</span></span> <span data-ttu-id="ffcdf-123">이 페이지에는 영화 제목, 장르 및 연도를 입력할 수 있는 필드 (텍스트 상자)가 있는 항목 양식이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-123">The page will contain an entry form that has fields (text boxes) where you can enter a movie title, genre, and year.</span></span> <span data-ttu-id="ffcdf-124">페이지는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-124">The page will look like this page:</span></span>

![브라우저의 ' 동영상 추가 ' 페이지](entering-data/_static/image1.png)

<span data-ttu-id="ffcdf-126">텍스트 상자는 다음과 같이 표시 되는 HTML `<input>` 요소가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-126">The text boxes will be HTML `<input>` elements that will look like this markup:</span></span>

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a><span data-ttu-id="ffcdf-127">기본 항목 폼 만들기</span><span class="sxs-lookup"><span data-stu-id="ffcdf-127">Creating the Basic Entry Form</span></span>

<span data-ttu-id="ffcdf-128">*Addmovie. cshtml*라는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-128">Create a page named *AddMovie.cshtml*.</span></span>

<span data-ttu-id="ffcdf-129">파일의 내용을 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-129">Replace what's in the file with the following markup.</span></span> <span data-ttu-id="ffcdf-130">모든 항목 덮어쓰기 잠시 후에 코드 블록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-130">Overwrite everything; you'll add a code block at the top shortly.</span></span>

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

<span data-ttu-id="ffcdf-131">이 예제에서는 폼을 만드는 일반적인 HTML을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-131">This example shows typical HTML for creating a form.</span></span> <span data-ttu-id="ffcdf-132">텍스트 상자 및 전송 단추에 대 한 `<input>` 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-132">It uses `<input>` elements for the text boxes and for the submit button.</span></span> <span data-ttu-id="ffcdf-133">텍스트 상자에 대 한 캡션은 표준 `<label>` 요소를 사용 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-133">The captions for the text boxes are created by using standard `<label>` elements.</span></span> <span data-ttu-id="ffcdf-134">`<fieldset>` 및 `<legend>` 요소는 폼 주위에 멋진 상자를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-134">The `<fieldset>` and `<legend>` elements put a nice box around the form.</span></span>

<span data-ttu-id="ffcdf-135">이 페이지에서 `<form>` 요소는 `post`를 `method` 특성의 값으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-135">Notice that in this page, the `<form>` element uses `post` as the value for the `method` attribute.</span></span> <span data-ttu-id="ffcdf-136">이전 자습서에서는 `get` 메서드를 사용 하는 양식을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-136">In the previous tutorial, you created a form that used the `get` method.</span></span> <span data-ttu-id="ffcdf-137">이는 양식이 서버에 값을 전송 하더라도 요청은 변경 하지 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-137">That was correct, because although the form submitted values to the server, the request did not make any changes.</span></span> <span data-ttu-id="ffcdf-138">모든 것이 다른 방법으로 데이터를 인출 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-138">All it did was fetch data in different ways.</span></span> <span data-ttu-id="ffcdf-139">그러나이 페이지에서는 새 데이터베이스 레코드를 추가 하 여 *변경 작업을 수행 합니다.*</span><span class="sxs-lookup"><span data-stu-id="ffcdf-139">However, in this page you *will* make changes—you're going to add new database records.</span></span> <span data-ttu-id="ffcdf-140">따라서이 폼은 `post` 메서드를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-140">Therefore, this form should use the `post` method.</span></span> <span data-ttu-id="ffcdf-141">`GET`와 `POST` 작업 간의 차이점에 대 한 자세한 내용은 이전 자습서의[GET, POST 및 HTTP Verb Safety](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) 사이드바를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-141">(For more about the difference between `GET` and `POST` operations, see the[GET, POST, and HTTP Verb Safety](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the previous tutorial.)</span></span>

<span data-ttu-id="ffcdf-142">각 텍스트 상자에는 `name` 요소 (`title`, `genre`, `year`)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-142">Note that each text box has a `name` element (`title`, `genre`, `year`).</span></span> <span data-ttu-id="ffcdf-143">이전 자습서에서 살펴본 것 처럼 이러한 이름은 나중에 사용자의 입력을 받을 수 있도록 이러한 이름이 있어야 하기 때문에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-143">As you saw in the previous tutorial, these names are important because you must have those names so you can get the user's input later.</span></span> <span data-ttu-id="ffcdf-144">임의의 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-144">You can use any names.</span></span> <span data-ttu-id="ffcdf-145">작업 하는 데이터를 기억할 수 있도록 하는 의미 있는 이름을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-145">It's helpful to use meaningful names that help you remember what data you're working with.</span></span>

<span data-ttu-id="ffcdf-146">각 `<input>` 요소의 `value` 특성에는 약간의 Razor 코드 (예: `Request.Form["title"]`)가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-146">The `value` attribute of each `<input>` element contains a bit of Razor code (for example, `Request.Form["title"]`).</span></span> <span data-ttu-id="ffcdf-147">이전 자습서에서이 트릭의 버전을 학습 하 여 양식이 제출 된 후 입력란에 입력 된 값 (있는 경우)을 유지 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-147">You learned a version of this trick in the previous tutorial to preserve the value entered into the text box (if any) after the form has been submitted.</span></span>

## <a name="getting-the-form-values"></a><span data-ttu-id="ffcdf-148">양식 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="ffcdf-148">Getting the Form Values</span></span>

<span data-ttu-id="ffcdf-149">그런 다음 폼을 처리 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-149">Next, you add code that processes the form.</span></span> <span data-ttu-id="ffcdf-150">개요에서는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-150">In outline, you'll do the following:</span></span>

1. <span data-ttu-id="ffcdf-151">페이지가 게시 되었는지 (제출 되었는지) 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-151">Check whether the page is being posted (was submitted).</span></span> <span data-ttu-id="ffcdf-152">사용자가 단추를 클릭 한 경우에만 페이지가 처음으로 실행 되는 경우에만 코드를 실행 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-152">You want to your code to run only when users have clicked the button, not when the page first runs.</span></span>
2. <span data-ttu-id="ffcdf-153">사용자가 텍스트 상자에 입력 한 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-153">Get the values that the user entered into the text boxes.</span></span> <span data-ttu-id="ffcdf-154">이 경우 폼이 `POST` 동사를 사용 하기 때문에 `Request.Form` 컬렉션에서 폼 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-154">In this case, because the form is using the `POST` verb, you get the form values from the `Request.Form` collection.</span></span>
3. <span data-ttu-id="ffcdf-155">*동영상* 데이터베이스 테이블에 새 레코드로 값을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-155">Insert the values as a new record in the *Movies* database table.</span></span>

<span data-ttu-id="ffcdf-156">파일 맨 위에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-156">At the top of the file, add the following code:</span></span>

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

<span data-ttu-id="ffcdf-157">처음 몇 줄은 텍스트 상자의 값을 포함 하는 변수 (`title`, `genre`및 `year`)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-157">The first few lines create variables (`title`, `genre`, and `year`) to hold the values from the text boxes.</span></span> <span data-ttu-id="ffcdf-158">줄 `if(IsPost)`은 사용자가 **동영상 추가** 단추를 클릭할 때 (즉, 폼이 게시 된 경우)에 *만* 변수가 설정 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-158">The line `if(IsPost)` makes sure that the variables are set *only* when users click the **Add Movie** button — that is, when the form has been posted.</span></span>

<span data-ttu-id="ffcdf-159">이전 자습서에서 살펴본 것 처럼 `Request.Form["name"]`와 같은 식을 사용 하 여 텍스트 상자의 값을 가져옵니다. 여기서 *name* 은 `<input>` 요소의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-159">As you saw in an earlier tutorial, you get the value of a text box by using an expression like `Request.Form["name"]`, where *name* is the name of the `<input>` element.</span></span>

<span data-ttu-id="ffcdf-160">변수 이름 (`title`, `genre`및 `year`)은 임의로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-160">The names of the variables (`title`, `genre`, and `year`) are arbitrary.</span></span> <span data-ttu-id="ffcdf-161">`<input>` 요소에 할당 하는 이름과 마찬가지로 원하는 모든 항목을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-161">Like the names that you assign to `<input>` elements, you can call them anything you like.</span></span> <span data-ttu-id="ffcdf-162">(변수의 이름이 폼에 있는 `<input>` 요소의 이름 특성과 일치 하지 않아도 됩니다.) 그러나 `<input>` 요소와 마찬가지로 포함 된 데이터를 반영 하는 변수 이름을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-162">(The names of the variables don't have to match the name attributes of `<input>` elements on the form.) But as with the `<input>` elements, it's a good idea to use variable names that reflect the data that they contain.</span></span> <span data-ttu-id="ffcdf-163">코드를 작성할 때 일관 된 이름을 사용 하면 작업 중인 데이터를 쉽게 기억할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-163">When you write code, consistent names make it easier for you to remember what data you're working with.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="ffcdf-164">데이터베이스에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="ffcdf-164">Adding Data to the Database</span></span>

<span data-ttu-id="ffcdf-165">방금 추가한 코드 블록의 닫는 중괄호 (`}` `if`) *내* 에서 (코드 블록 내부 뿐만 아니라) 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-165">In the code block you just added, just *inside* the closing brace ( `}` ) of the `if` block (not just inside the code block), add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample3.cs)]

<span data-ttu-id="ffcdf-166">이 예제는 데이터를 가져오고 표시 하기 위해 이전 자습서에서 사용한 코드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-166">This example is similar to the code you used in a previous tutorial to fetch and display data.</span></span> <span data-ttu-id="ffcdf-167">`db =` 시작 하는 줄은 이전과 같이 데이터베이스를 열고 앞에서 살펴본 대로 다음 줄은 SQL 문을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-167">The line that starts with `db =` opens the database, like before, and the next line defines a SQL statement, again as you saw before.</span></span> <span data-ttu-id="ffcdf-168">그러나 이번에는 SQL `Insert Into` 문을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-168">However, this time it defines a SQL `Insert Into` statement.</span></span> <span data-ttu-id="ffcdf-169">다음 예에서는 `Insert Into` 문의 일반적인 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-169">The following example shows the general syntax of the `Insert Into` statement:</span></span>

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

<span data-ttu-id="ffcdf-170">즉, 삽입할 테이블을 지정한 다음 삽입할 열을 나열 하 고 삽입할 값을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-170">In other words, you specify the table to insert into, then list the columns to insert into, and then list the values to insert.</span></span> <span data-ttu-id="ffcdf-171">앞에서 설명한 것 처럼 SQL은 대/소문자를 구분 하지 않지만 일부 사용자는 키워드를 사용 하 여 명령을 더 쉽게 읽을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-171">(As noted before, SQL is not case sensitive but some people capitalize the keywords to make it easier to read the command.)</span></span>

<span data-ttu-id="ffcdf-172">삽입 하는 열은 명령에 이미 나열 되어 `(Title, Genre, Year)`합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-172">The columns that you're inserting into are already listed in the command — `(Title, Genre, Year)`.</span></span> <span data-ttu-id="ffcdf-173">흥미로운 부분은 텍스트 상자의 값을 명령의 `VALUES` 부분으로 가져오는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-173">The interesting part is how you get the values from the text boxes into the `VALUES` part of the command.</span></span> <span data-ttu-id="ffcdf-174">실제 값 대신 자리 표시자 인 `@0`, `@1`및 `@2`표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-174">Instead of actual values, you see `@0`, `@1`, and `@2`, which are of course placeholders.</span></span> <span data-ttu-id="ffcdf-175">`db.Execute` 줄에서 명령을 실행할 때 텍스트 상자에서 가져온 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-175">When you run the command (on the `db.Execute` line), you pass the values that you got from the text boxes.</span></span>

<span data-ttu-id="ffcdf-176">**중요!**</span><span class="sxs-lookup"><span data-stu-id="ffcdf-176">**Important!**</span></span> <span data-ttu-id="ffcdf-177">SQL 문에 사용자가 온라인으로 입력 한 데이터를 포함 하는 유일한 방법은 여기에 표시 된 대로 자리 표시자를 사용 하는 것입니다 (`VALUES(@0, @1, @2)`).</span><span class="sxs-lookup"><span data-stu-id="ffcdf-177">Remember that the only way you should ever include data entered online by a user in a SQL statement is to use placeholders, as you see here (`VALUES(@0, @1, @2)`).</span></span> <span data-ttu-id="ffcdf-178">사용자 입력을 SQL 문에 연결 하는 경우 [ASP.NET 웹 페이지의 양식 기본 사항](https://go.microsoft.com/fwlink/?LinkId=251581) (이전 자습서)에 설명 된 대로 sql 삽입 공격을 직접 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-178">If you concatenate user input into a SQL statement, you open yourself to a SQL injection attack, as explained in [Form Basics in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581) (the previous tutorial).</span></span>

<span data-ttu-id="ffcdf-179">`if` 블록 내에서 `db.Execute` 줄 뒤에 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-179">Still inside the `if` block, add the following line after the `db.Execute` line:</span></span>

[!code-css[Main](entering-data/samples/sample4.css)]

<span data-ttu-id="ffcdf-180">새 동영상이 데이터베이스에 삽입 된 후이 줄은 사용자 (리디렉션)를 *동영상* 페이지로 이동 하 여 방금 입력 한 동영상을 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-180">After the new movie has been inserted into the database, this line jumps you (redirects) to the *Movies* page so you can see the movie you just entered.</span></span> <span data-ttu-id="ffcdf-181">`~` 연산자는 "웹 사이트의 루트"를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-181">The `~` operator means "root of the website."</span></span> <span data-ttu-id="ffcdf-182">`~` 연산자는 일반적으로 HTML이 아닌 ASP.NET 페이지 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-182">(The `~` operator works only in ASP.NET pages, not in HTML generally.)</span></span>

<span data-ttu-id="ffcdf-183">전체 코드 블록은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-183">The complete code block looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a><span data-ttu-id="ffcdf-184">삽입 명령 테스트 (지금까지)</span><span class="sxs-lookup"><span data-stu-id="ffcdf-184">Testing the Insert Command (So Far)</span></span>

<span data-ttu-id="ffcdf-185">아직 완료 되지 않았지만 지금 테스트 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-185">You're not done yet, but now is a good time to test.</span></span>

<span data-ttu-id="ffcdf-186">WebMatrix의 파일 트리 뷰에서 *Addmovie. cshtml* 페이지를 마우스 오른쪽 단추로 클릭 한 다음 **브라우저에서 시작**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-186">In the tree view of files in WebMatrix, right-click the *AddMovie.cshtml* page and then click **Launch in browser**.</span></span>

![브라우저의 ' 동영상 추가 ' 페이지](entering-data/_static/image2.png)

<span data-ttu-id="ffcdf-188">(브라우저에서 다른 페이지가 표시 되 면 URL이 `http://localhost:nnnnn/AddMovie`) 인지 확인 합니다. 여기서 *nnnnn* 은 사용 중인 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-188">(If you end up with a different page in the browser, make sure that the URL is `http://localhost:nnnnn/AddMovie`), where *nnnnn* is the port number that you're using.)</span></span>

<span data-ttu-id="ffcdf-189">오류 페이지가 있나요?</span><span class="sxs-lookup"><span data-stu-id="ffcdf-189">Did you get an error page?</span></span> <span data-ttu-id="ffcdf-190">그렇다면, 신중 하 게 읽고 코드가 앞에서 설명한 것과 정확히 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-190">If so, read it carefully and make sure that the code looks exactly what was listed earlier.</span></span>

<span data-ttu-id="ffcdf-191">예를 들어 "Kane", "드라마" 및 "1941"를 사용 하 여 &mdash; 양식에 영화를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-191">Enter a movie in the form &mdash; for example, use "Citizen Kane", "Drama", and "1941".</span></span> <span data-ttu-id="ffcdf-192">(또는 모든 항목) 그런 다음 **동영상 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-192">(Or whatever.) Then click **Add Movie**.</span></span>

<span data-ttu-id="ffcdf-193">모든 작업이 제대로 진행 되 면 *동영상* 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-193">If all goes well, you're redirected to the *Movies* page.</span></span> <span data-ttu-id="ffcdf-194">새 동영상이 나열 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-194">Make sure that your new movie is listed.</span></span>

![새로 추가 된 동영상을 보여 주는 동영상 페이지](entering-data/_static/image3.png)

## <a name="validating-user-input"></a><span data-ttu-id="ffcdf-196">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="ffcdf-196">Validating User Input</span></span>

<span data-ttu-id="ffcdf-197">*Addmovie* 페이지로 돌아가서 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-197">Go back to the *AddMovie* page, or run it again.</span></span> <span data-ttu-id="ffcdf-198">다른 영화를 입력 합니다. 그러나 이번에는 &mdash; 제목만 입력 합니다. 예를 들어 "Singin'"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-198">Enter another movie, but this time, enter only the title &mdash; for example, enter "Singin' in the Rain".</span></span> <span data-ttu-id="ffcdf-199">그런 다음 **동영상 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-199">Then click **Add Movie**.</span></span>

<span data-ttu-id="ffcdf-200">*동영상* 페이지로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-200">You're redirected to the *Movies* page again.</span></span> <span data-ttu-id="ffcdf-201">새 동영상을 찾을 수 있지만 불완전 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-201">You can find the new movie, but it's incomplete.</span></span>

![일부 값이 누락 된 새 동영상을 보여 주는 동영상 페이지](entering-data/_static/image4.png)

<span data-ttu-id="ffcdf-203">*동영상* 테이블을 만들 때 null 일 수 있는 필드는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-203">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="ffcdf-204">새 영화에 대 한 입력 양식이 있고 필드를 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-204">Here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="ffcdf-205">오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-205">That's an error.</span></span>

<span data-ttu-id="ffcdf-206">이 경우 데이터베이스는 실제로 오류를 발생 시키거나 *throw*하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-206">In this case, the database didn't actually raise (or *throw*) an error.</span></span> <span data-ttu-id="ffcdf-207">장르 또는 연도를 제공 하지 않았으므로 *Addmovie* 페이지의 코드는 이러한 값을 *빈 문자열로*처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-207">You didn't supply a genre or year, so the code in the *AddMovie* page treated those values as so-called *empty strings*.</span></span> <span data-ttu-id="ffcdf-208">SQL `Insert Into` 명령이 실행 될 때 장르 및 연도 필드에는 유용한 데이터가 없지만 null은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-208">When the SQL `Insert Into` command ran, the genre and year fields didn't have useful data in them, but they weren't null.</span></span>

<span data-ttu-id="ffcdf-209">사용자가 데이터베이스에 절반의 영화 정보를 입력할 수 없도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-209">Obviously, you don't want to let users enter half-empty movie information into the database.</span></span> <span data-ttu-id="ffcdf-210">이 솔루션은 사용자 입력의 유효성을 검사 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-210">The solution is to validate the user's input.</span></span> <span data-ttu-id="ffcdf-211">처음에는 유효성 검사를 통해 사용자가 모든 필드 (즉, 빈 문자열은 포함 하지 않음)에 대 한 값을 입력 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-211">Initially, the validation will simply make sure that the user has entered a value for all of the fields (that is, that none of them contains an empty string).</span></span>

> [!TIP]
> 
> <span data-ttu-id="ffcdf-212">**Null 및 빈 문자열**</span><span class="sxs-lookup"><span data-stu-id="ffcdf-212">**Null and Empty Strings**</span></span>
> 
> <span data-ttu-id="ffcdf-213">프로그래밍에서는 서로 다른 개념 "no value"를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-213">In programming, there's a distinction between different notions of "no value."</span></span> <span data-ttu-id="ffcdf-214">일반적으로 값은 설정 되거나 초기화 되지 않은 경우 *null* 입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-214">In general, a value is *null* if it has never been set or initialized in any way.</span></span> <span data-ttu-id="ffcdf-215">반대로 문자 데이터 (문자열)를 필요로 하는 변수를 *빈 문자열로*설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-215">In contrast, a variable that expects character data (strings) can be set to an *empty string*.</span></span> <span data-ttu-id="ffcdf-216">이 경우 값은 null이 아닙니다. 길이가 0 인 문자 문자열로 명시적으로 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-216">In that case, the value is not null; it's just been explicitly set to a string of characters whose length is zero.</span></span> <span data-ttu-id="ffcdf-217">이 두 문은 다음과 같은 차이점을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-217">These two statements show the difference:</span></span>
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> <span data-ttu-id="ffcdf-218">보다 다소 복잡 하지만 `null`는 결정 되지 않은 상태를 나타내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-218">It's a little more complicated than that, but the important point is that `null` represents a sort of undetermined state.</span></span>
> 
> <span data-ttu-id="ffcdf-219">이제 값이 null 인 경우와 빈 문자열일 때를 정확 하 게 이해 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-219">Now and then it's important to understand exactly when a value is null and when it's just an empty string.</span></span> <span data-ttu-id="ffcdf-220">*Addmovie* 의 코드 페이지에서 `Request.Form["title"]`를 사용 하 여 텍스트 상자의 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-220">In the code for the *AddMovie* page, you get the values of the text boxes by using `Request.Form["title"]` and so on.</span></span> <span data-ttu-id="ffcdf-221">단추를 클릭 하기 전에 페이지를 처음 실행 하면 `Request.Form["title"]`의 값이 null입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-221">When the page first runs (before you click the button), the value of `Request.Form["title"]` is null.</span></span> <span data-ttu-id="ffcdf-222">그러나 양식을 제출할 때 `title` 텍스트 상자의 값을 `Request.Form["title"]` 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-222">But when you submit the form, `Request.Form["title"]` gets the value of the `title` text box.</span></span> <span data-ttu-id="ffcdf-223">분명 한 것은 아니지만 빈 텍스트 상자는 null이 아닙니다. 빈 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-223">It's not obvious, but an empty text box is not null; it just has an empty string in it.</span></span> <span data-ttu-id="ffcdf-224">그러면 단추 클릭에 대 한 응답으로 코드가 실행 될 때 `Request.Form["title"]`에 빈 문자열이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-224">So when the code runs in response to the button click, `Request.Form["title"]` has an empty string in it.</span></span>
> 
> <span data-ttu-id="ffcdf-225">이러한 차이점이 중요 한 이유는 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="ffcdf-225">Why is this distinction important?</span></span> <span data-ttu-id="ffcdf-226">*동영상* 테이블을 만들 때 null 일 수 있는 필드는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-226">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="ffcdf-227">하지만 여기서는 새 영화에 대 한 입력 양식이 있고 필드를 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-227">But here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="ffcdf-228">장르 또는 연도에 대 한 값이 없는 새 영화를 저장 하려고 하면 데이터베이스가 정상적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-228">You would reasonably expect the database to complain when you tried to save new movies that didn't have values for genre or year.</span></span> <span data-ttu-id="ffcdf-229">&mdash; 단, 해당 텍스트 상자를 비워 두는 경우에도 해당 값은 null이 아닙니다. 빈 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-229">But that's the point &mdash; even if you leave those text boxes blank, the values aren't null; they're empty strings.</span></span> <span data-ttu-id="ffcdf-230">결과적으로, 이러한 열이 비어 &mdash; 있지만 null이 아닌 새 동영상을 데이터베이스에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-230">As a result, you're able to save new movies to the database with these columns empty &mdash; but not null!</span></span> <span data-ttu-id="ffcdf-231">&mdash; 값</span><span class="sxs-lookup"><span data-stu-id="ffcdf-231">&mdash; values.</span></span> <span data-ttu-id="ffcdf-232">따라서 사용자가 입력의 유효성을 검사 하 여 수행할 수 있는 빈 문자열을 제출 하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-232">Therefore, you have to make sure that users don't submit an empty string, which you can do by validating the user's input.</span></span>

### <a name="the-validation-helper"></a><span data-ttu-id="ffcdf-233">유효성 검사 도우미</span><span class="sxs-lookup"><span data-stu-id="ffcdf-233">The Validation Helper</span></span>

<span data-ttu-id="ffcdf-234">ASP.NET 웹 페이지에는 사용자가 요구 사항을 충족 하는 데이터를 입력 하는지 확인 하는 데 사용할 수 있는 도우미 &mdash; `Validation` 도우미 &mdash; 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-234">ASP.NET Web Pages includes a helper &mdash; the `Validation` helper &mdash; that you can use to make sure that users enter data that meets your requirements.</span></span> <span data-ttu-id="ffcdf-235">`Validation` 도우미는 ASP.NET 웹 페이지에 기본 제공 되는 도우미 중 하나 이며, 이전 자습서에서 Gravatar 도우미를 설치 하는 방식으로 NuGet을 사용 하 여 패키지로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-235">The `Validation` helper is one of the helpers that's built in to ASP.NET Web Pages, so you don't have to install it as a package by using NuGet, the way you installed the Gravatar helper in an earlier tutorial.</span></span>

<span data-ttu-id="ffcdf-236">사용자 입력의 유효성을 검사 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-236">To validate the user's input, you'll do the following:</span></span>

- <span data-ttu-id="ffcdf-237">코드를 사용 하 여 페이지의 텍스트 상자에 값을 요구 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-237">Use code to specify that you want to require values in the text boxes on the page.</span></span>
- <span data-ttu-id="ffcdf-238">모든 것이 제대로 유효성을 검사 하는 경우에만 데이터베이스에 동영상 정보가 추가 되도록 테스트를 코드에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-238">Put a test into the code so that the movie information is added to the database only if everything validates properly.</span></span>
- <span data-ttu-id="ffcdf-239">태그에 오류 메시지를 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-239">Add code into the markup to display error messages.</span></span>

<span data-ttu-id="ffcdf-240">*Addmovie* 페이지의 코드 블록에서 변수 선언 앞의 위쪽에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-240">In the code block in the *AddMovie* page, right up at the top before the variable declarations, add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample7.cs)]

<span data-ttu-id="ffcdf-241">항목을 요구 하려는 각 필드 (`<input>` 요소)에 대해 `Validation.RequireField`를 한 번씩 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-241">You call `Validation.RequireField` once for each field (`<input>` element) where you want to require an entry.</span></span> <span data-ttu-id="ffcdf-242">여기에 표시 된 것 처럼 각 호출에 대 한 사용자 지정 오류 메시지를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-242">You can also add a custom error message for each call, like you see here.</span></span> <span data-ttu-id="ffcdf-243">(원하는 모든 항목을 배치할 수 있다는 것을 보여 주기 위해 메시지를 다양 하 게 설명 합니다.)</span><span class="sxs-lookup"><span data-stu-id="ffcdf-243">(We varied the messages just to show that you can put anything you like there.)</span></span>

<span data-ttu-id="ffcdf-244">문제가 있는 경우 새 동영상 정보가 데이터베이스에 삽입 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-244">If there's a problem, you want to prevent the new movie information from being inserted into the database.</span></span> <span data-ttu-id="ffcdf-245">`if(IsPost)` 블록에서 `&&` (논리적 AND)를 사용 하 여 `Validation.IsValid()`테스트 하는 다른 조건을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-245">In the `if(IsPost)` block, use `&&` (logical AND) to add another condition that tests `Validation.IsValid()`.</span></span> <span data-ttu-id="ffcdf-246">완료 되 면 전체 `if(IsPost)` 블록은 다음 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-246">When you're done, the whole `if(IsPost)` block looks like this code:</span></span>

[!code-csharp[Main](entering-data/samples/sample8.cs)]

<span data-ttu-id="ffcdf-247">`Validation` 도우미를 사용 하 여 등록 한 필드에 유효성 검사 오류가 있는 경우 `Validation.IsValid` 메서드에서 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-247">If there's a validation error with any of the fields that you registered by using the `Validation` helper, the `Validation.IsValid` method returns false.</span></span> <span data-ttu-id="ffcdf-248">이 경우 해당 블록의 코드는 실행 되지 않으므로 잘못 된 영화 항목이 데이터베이스에 삽입 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-248">And in that case, none of the code in that block will run, so no invalid movie entries will be inserted into the database.</span></span> <span data-ttu-id="ffcdf-249">물론 *동영상* 페이지로 리디렉션되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-249">And of course you're not redirected to the *Movies* page.</span></span>

<span data-ttu-id="ffcdf-250">유효성 검사 코드를 비롯 한 전체 코드 블록은 이제 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-250">The complete code block, including the validation code, now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a><span data-ttu-id="ffcdf-251">유효성 검사 오류 표시</span><span class="sxs-lookup"><span data-stu-id="ffcdf-251">Displaying Validation Errors</span></span>

<span data-ttu-id="ffcdf-252">마지막 단계는 오류 메시지를 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-252">The last step is to display any error messages.</span></span> <span data-ttu-id="ffcdf-253">각 유효성 검사 오류에 대 한 개별 메시지를 표시 하거나 요약 또는 둘 다를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-253">You can display individual messages for each validation error, or you can display a summary, or both.</span></span> <span data-ttu-id="ffcdf-254">이 자습서에서는 작동 방식을 확인할 수 있도록 두 작업을 모두 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-254">For this tutorial, you'll do both so that you can see how it works.</span></span>

<span data-ttu-id="ffcdf-255">유효성을 검사 하는 각 `<input>` 요소 옆의 `Html.ValidationMessage` 메서드를 호출 하 고 유효성을 검사 하는 `<input>` 요소의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-255">Next to each `<input>` element that you're validating, call the `Html.ValidationMessage` method and pass it the name of the `<input>` element you're validating.</span></span> <span data-ttu-id="ffcdf-256">오류 메시지를 표시할 위치에 `Html.ValidationMessage` 메서드를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-256">You put the `Html.ValidationMessage` method right where you want the error message to appear.</span></span> <span data-ttu-id="ffcdf-257">페이지가 실행 될 때 `Html.ValidationMessage` 메서드는 유효성 검사 오류가 발생 하는 `<span>` 요소를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-257">When the page runs, the `Html.ValidationMessage` method renders a `<span>` element where the validation error will go.</span></span> <span data-ttu-id="ffcdf-258">오류가 없는 경우에는 `<span>` 요소가 렌더링 되지만 텍스트는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-258">(If there's no error, the `<span>` element is rendered, but there's no text in it.)</span></span>

<span data-ttu-id="ffcdf-259">페이지에서 다음 예제와 같이 세 개의 `<input>` 요소 각각에 대 한 `Html.ValidationMessage` 메서드를 포함 하도록 페이지의 태그를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-259">Change the markup in the page so that it includes an `Html.ValidationMessage` method for each of the three `<input>` elements on the page, like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

<span data-ttu-id="ffcdf-260">요약이 어떻게 작동 하는지 확인 하려면 페이지의 `<h1>Add a Movie</h1>` 요소 바로 뒤에 다음 태그와 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-260">To see how the summary works, also add the following markup and code right after the `<h1>Add a Movie</h1>` element on the page:</span></span>

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

<span data-ttu-id="ffcdf-261">기본적으로 `Html.ValidationSummary` 메서드는 목록에 모든 유효성 검사 메시지를 표시 합니다 (`<div>` 요소 내에 있는 `<ul>` 요소).</span><span class="sxs-lookup"><span data-stu-id="ffcdf-261">By default, the `Html.ValidationSummary` method displays all the validation messages in a list (a `<ul>` element that's inside a `<div>` element).</span></span> <span data-ttu-id="ffcdf-262">`Html.ValidationMessage` 메서드와 마찬가지로 유효성 검사 요약에 대 한 태그는 항상 렌더링 됩니다. 오류가 없으면 목록 항목이 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-262">As with the `Html.ValidationMessage` method, the markup for the validation summary is always rendered; if there are no errors, no list items are rendered.</span></span>

<span data-ttu-id="ffcdf-263">요약은 `Html.ValidationMessage` 메서드를 사용 하 여 각 필드별 오류를 표시 하는 대신 유효성 검사 메시지를 표시 하는 대체 방법이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-263">The summary can be an alternative way to display validation messages instead of by using the `Html.ValidationMessage` method to display each field-specific error.</span></span> <span data-ttu-id="ffcdf-264">또는 요약 및 세부 정보를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-264">Or you can use both a summary and the details.</span></span> <span data-ttu-id="ffcdf-265">또는 `Html.ValidationSummary` 메서드를 사용 하 여 일반 오류를 표시 한 다음 개별 `Html.ValidationMessage` 호출을 사용 하 여 세부 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-265">Or you can use the `Html.ValidationSummary` method to display a generic error and then use individual `Html.ValidationMessage` calls to display details.</span></span>

<span data-ttu-id="ffcdf-266">이제 전체 페이지는 다음 예와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-266">The complete page now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

<span data-ttu-id="ffcdf-267">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-267">That's it.</span></span> <span data-ttu-id="ffcdf-268">이제 영화를 추가 하 고 하나 이상의 필드를 남기고 페이지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-268">You can now test the page by adding a movie but leaving out one or more of the fields.</span></span> <span data-ttu-id="ffcdf-269">이렇게 하면 다음과 같은 오류 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-269">When you do, you see the following error display:</span></span>

![유효성 검사 오류 메시지를 보여 주는 동영상 추가](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a><span data-ttu-id="ffcdf-271">유효성 검사 오류 메시지의 스타일 지정</span><span class="sxs-lookup"><span data-stu-id="ffcdf-271">Styling the Validation Error Messages</span></span>

<span data-ttu-id="ffcdf-272">오류 메시지가 표시 되는 것을 확인할 수 있지만,이는 정말 잘 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-272">You can see that there are error messages, but they don't really stand out very well.</span></span> <span data-ttu-id="ffcdf-273">그러나 오류 메시지의 스타일을 쉽게 적용할 수 있는 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-273">There's an easy way to style the error messages, though.</span></span>

<span data-ttu-id="ffcdf-274">`Html.ValidationMessage`표시 되는 개별 오류 메시지의 스타일을 지정 하려면 `field-validation-error`라는 CSS 스타일 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-274">To style the individual error messages that are displayed by `Html.ValidationMessage`, create a CSS style class named `field-validation-error`.</span></span> <span data-ttu-id="ffcdf-275">유효성 검사 요약에 대 한 검색을 정의 하려면 `validation-summary-errors`라는 CSS 스타일 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-275">To define the look for the validation summary, create a CSS style class named `validation-summary-errors`.</span></span>

<span data-ttu-id="ffcdf-276">이 기술의 작동 방식을 확인 하려면 페이지의 `<head>` 섹션 내에 `<style>` 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-276">To see how this technique works, add a `<style>` element inside the `<head>` section of the page.</span></span> <span data-ttu-id="ffcdf-277">그런 다음 다음 규칙을 포함 하는 `field-validation-error` 및 `validation-summary-errors` 이라는 스타일 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-277">Then define style classes named `field-validation-error` and `validation-summary-errors` that contain the following rules:</span></span>

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

<span data-ttu-id="ffcdf-278">일반적으로 별도의 *.css* 파일에 스타일 정보를 저장 하는 것이 좋습니다. 편의상 페이지에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-278">Normally you'd probably put style information into a separate *.css* file, but for simplicity you can put them in the page for now.</span></span> <span data-ttu-id="ffcdf-279">이 자습서의 뒷부분에서는 CSS 규칙을 별도 *.css* 파일로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-279">(Later in this tutorial set, you'll move the CSS rules to a separate *.css* file.)</span></span>

<span data-ttu-id="ffcdf-280">유효성 검사 오류가 있는 경우 `Html.ValidationMessage` 메서드는 `class="field-validation-error"`를 포함 하는 `<span>` 요소를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-280">If there's a validation error, the `Html.ValidationMessage` method renders a `<span>` element that includes `class="field-validation-error"`.</span></span> <span data-ttu-id="ffcdf-281">해당 클래스에 대 한 스타일 정의를 추가 하 여 메시지가 표시 되는 모양을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-281">By adding a style definition for that class, you can configure what the message looks like.</span></span> <span data-ttu-id="ffcdf-282">오류가 있는 경우 `ValidationSummary` 메서드는 마찬가지로 특성 `class="validation-summary-errors"`를 동적으로 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-282">If there are errors, the `ValidationSummary` method likewise dynamically renders the attribute `class="validation-summary-errors"`.</span></span>

<span data-ttu-id="ffcdf-283">페이지를 다시 실행 하 고, 두 필드를 의도적으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-283">Run the page again and deliberately leave out a couple of the fields.</span></span> <span data-ttu-id="ffcdf-284">이제 오류가 더 두드러집니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-284">The errors are now more noticeable.</span></span> <span data-ttu-id="ffcdf-285">실제로는이 작업을 수행할 수 있는 작업을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-285">(In fact, they're overdone, but that's just to show what you can do.)</span></span>

![스타일이 지정 된 유효성 검사 오류를 보여 주는 동영상 추가 페이지](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a><span data-ttu-id="ffcdf-287">동영상 페이지에 링크 추가</span><span class="sxs-lookup"><span data-stu-id="ffcdf-287">Adding a Link to the Movies Page</span></span>

<span data-ttu-id="ffcdf-288">최종 단계 중 하나는 원래 동영상 목록에서 *addmovie* 페이지로 이동 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-288">One final step is to make it convenient to get to the *AddMovie* page from the original movie listing.</span></span>

<span data-ttu-id="ffcdf-289">*동영상* 페이지를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-289">Open the *Movies* page again.</span></span> <span data-ttu-id="ffcdf-290">`WebGrid` 도우미 뒤에 오는 closing `</div>` 태그 뒤에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-290">After the closing `</div>` tag that follows the `WebGrid` helper, add the following markup:</span></span>

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

<span data-ttu-id="ffcdf-291">앞서 살펴본 것 처럼 ASP.NET는 `~` 연산자를 웹 사이트의 루트로 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-291">As you saw before, ASP.NET interprets the `~` operator as the root of the website.</span></span> <span data-ttu-id="ffcdf-292">`~` 연산자를 사용할 필요가 없습니다. 태그 `<a href="./AddMovie">Add a movie</a>` 또는 다른 방법을 사용 하 여 HTML에서 인식 하는 경로를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-292">You don't have to use the `~` operator; you could use the markup `<a href="./AddMovie">Add a movie</a>` or some other way to define the path that HTML understands.</span></span> <span data-ttu-id="ffcdf-293">그러나 `~` 연산자는 Razor 페이지에 대 한 링크를 만들 때 적절 한 일반적인 방법입니다 .이는 사이트의 유연성을 향상 시킬 수 있기 때문입니다. 현재 페이지를 하위 폴더로 이동 하면 링크가 여전히 *Addmovie* 페이지로 이동 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-293">But the `~` operator is a good general approach when you create links for Razor pages, because it makes the site more flexible — if you move the current page to a subfolder, the link will still go to the *AddMovie* page.</span></span> <span data-ttu-id="ffcdf-294">`~` 연산자는 *. cshtml* 페이지 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-294">(Remember that the `~` operator only works in *.cshtml* pages.</span></span> <span data-ttu-id="ffcdf-295">ASP.NET는이를 이해 하지만 표준 HTML은 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="ffcdf-295">ASP.NET understands it, but it's not standard HTML.)</span></span>

<span data-ttu-id="ffcdf-296">완료 되 면 *동영상* 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-296">When you're done, run the *Movies* page.</span></span> <span data-ttu-id="ffcdf-297">이 페이지가 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-297">It will look like this page:</span></span>

![' 동영상 추가 ' 페이지에 대 한 링크가 있는 동영상 페이지](entering-data/_static/image7.png)

<span data-ttu-id="ffcdf-299">**동영상 추가** 링크를 클릭 하 여 *addmovie* 페이지로 이동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-299">Click the **Add a movie** link to make sure that it goes to the *AddMovie* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="ffcdf-300">다음에서 시작</span><span class="sxs-lookup"><span data-stu-id="ffcdf-300">Coming Up Next</span></span>

<span data-ttu-id="ffcdf-301">다음 자습서에서는 데이터베이스에 이미 있는 데이터를 사용자가 편집할 수 있도록 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-301">In the next tutorial, you'll learn how to let users edit data that's already in the database.</span></span>

## <a name="complete-listing-for-addmovie-page"></a><span data-ttu-id="ffcdf-302">AddMovie 페이지의 전체 목록</span><span class="sxs-lookup"><span data-stu-id="ffcdf-302">Complete Listing for AddMovie Page</span></span>

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="ffcdf-303">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ffcdf-303">Additional Resources</span></span>

- [<span data-ttu-id="ffcdf-304">Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="ffcdf-304">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="ffcdf-305">W3Schools 사이트의 [SQL INSERT INTO 문](http://www.w3schools.com/sql/sql_insert.asp)</span><span class="sxs-lookup"><span data-stu-id="ffcdf-305">[SQL INSERT INTO Statement](http://www.w3schools.com/sql/sql_insert.asp) on the W3Schools site</span></span>
- <span data-ttu-id="ffcdf-306">[ASP.NET 웹 페이지 사이트에서 사용자 입력의 유효성을 검사](https://go.microsoft.com/fwlink/?LinkId=253002)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-306">[Validating User Input in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=253002).</span></span> <span data-ttu-id="ffcdf-307">`Validation` 도우미를 사용 하는 방법에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="ffcdf-307">More information about working with the `Validation` helper.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ffcdf-308">[이전](form-basics.md)
> [다음](updating-data.md)</span><span class="sxs-lookup"><span data-stu-id="ffcdf-308">[Previous](form-basics.md)
[Next](updating-data.md)</span></span>
