---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: ASP.NET MVC가 DropDownList 도우미를 스 캐 폴드 하는 방식 검사 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498359"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a><span data-ttu-id="6745c-102">ASP.NET MVC가 DropDownList 도우미를 스캐폴드하는 방법 검사</span><span class="sxs-lookup"><span data-stu-id="6745c-102">Examining  how  ASP.NET MVC scaffolds the DropDownList Helper</span></span>

<span data-ttu-id="6745c-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6745c-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="6745c-104">**솔루션 탐색기**에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **컨트롤러 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-104">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span> <span data-ttu-id="6745c-105">컨트롤러 이름을 **StoreManagerController**로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-105">Name the controller **StoreManagerController**.</span></span> <span data-ttu-id="6745c-106">아래 이미지에 표시 된 것 처럼 **컨트롤러 추가** 대화 상자에 대 한 옵션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-106">Set the options for the **Add Controller** dialog as shown in the image below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

<span data-ttu-id="6745c-107">*StoreManager\Index.cshtml* view를 편집 하 고 `AlbumArtUrl`를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-107">Edit the *StoreManager\Index.cshtml* view and remove `AlbumArtUrl`.</span></span> <span data-ttu-id="6745c-108">`AlbumArtUrl` 제거 하면 프레젠테이션을 더 쉽게 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-108">Removing `AlbumArtUrl` will make the presentation more readable.</span></span> <span data-ttu-id="6745c-109">완성된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-109">The completed code is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

<span data-ttu-id="6745c-110">*Controllers\StoreManagerController.cs* 파일을 열고 `Index` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-110">Open the *Controllers\StoreManagerController.cs* file and find the `Index` method.</span></span> <span data-ttu-id="6745c-111">`OrderBy` 절을 추가 하 여 앨범이 가격을 기준으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-111">Add the `OrderBy` clause so the albums will be sorted by price.</span></span> <span data-ttu-id="6745c-112">전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-112">The complete code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

<span data-ttu-id="6745c-113">가격을 기준으로 정렬 하면 데이터베이스의 변경 내용을 보다 쉽게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-113">Sorting by price will make it easier to test changes to the database.</span></span> <span data-ttu-id="6745c-114">편집 및 만들기 메서드를 테스트할 때 낮은 가격을 사용 하 여 저장 된 데이터가 먼저 표시 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-114">When you are testing the edit and create methods, you can use a low price so the saved data will appear first.</span></span>

<span data-ttu-id="6745c-115">*StoreManager\Edit.cshtml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-115">Open the *StoreManager\Edit.cshtml* file.</span></span> <span data-ttu-id="6745c-116">범례 태그 바로 뒤에 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-116">Add the following line just after the legend tag.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

<span data-ttu-id="6745c-117">다음 코드는이 변경 내용의 컨텍스트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-117">The following code shows the context of this change:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

<span data-ttu-id="6745c-118">앨범 레코드를 변경 하려면 `AlbumId` 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-118">The `AlbumId` is required to make changes to an album record.</span></span>

<span data-ttu-id="6745c-119">Ctrl+F5를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-119">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="6745c-120">**관리자** 링크를 선택 하 고 **새로 만들기** 링크를 선택 하 여 새 앨범을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-120">Select to the **Admin** link, then select the **Create New** link to create a new album.</span></span> <span data-ttu-id="6745c-121">앨범 정보가 저장 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-121">Verify the album information was saved.</span></span> <span data-ttu-id="6745c-122">앨범을 편집 하 고 변경한 내용이 유지 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-122">Edit an album and verify the changes you made are persisted.</span></span>

### <a name="the-album-schema"></a><span data-ttu-id="6745c-123">앨범 스키마</span><span class="sxs-lookup"><span data-stu-id="6745c-123">The Album Schema</span></span>

<span data-ttu-id="6745c-124">MVC 스 캐 폴딩 메커니즘을 사용 하 여 만든 `StoreManager` 컨트롤러는 music 저장소 데이터베이스의 앨범에 대 한 CRUD (만들기, 읽기, 업데이트, 삭제) 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-124">The `StoreManager` controller created by the MVC scaffolding mechanism allows CRUD (Create, Read, Update, Delete) access to the albums in the music store database.</span></span> <span data-ttu-id="6745c-125">앨범 정보에 대 한 스키마는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-125">The schema for album information is shown below:</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

<span data-ttu-id="6745c-126">`Albums` 테이블은 앨범 장르 및 설명을 저장 하지 않으며 `Genres` 테이블에 외래 키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-126">The `Albums` table does not store the album genre and description, it stores a foreign key to the `Genres` table.</span></span> <span data-ttu-id="6745c-127">`Genres` 테이블에는 장르 이름 및 설명이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-127">The `Genres` table contains the genre name and description.</span></span> <span data-ttu-id="6745c-128">마찬가지로 `Albums` 테이블에는 앨범 아티스트 이름 뿐만 아니라 `Artists` 테이블에 대 한 외래 키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-128">Likewise, the `Albums` table doesn't contain the album artists name, but a foreign key to the `Artists` table.</span></span> <span data-ttu-id="6745c-129">`Artists` 테이블은 음악가의 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-129">The `Artists` table contains the artist's name.</span></span> <span data-ttu-id="6745c-130">`Albums` 테이블의 데이터를 검사 하는 경우 각 행에 `Genres` 테이블에 대 한 외래 키와 `Artists` 테이블에 대 한 외래 키가 포함 되어 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-130">If you examine the data in the `Albums` table, you can see each row contains a foreign key to the `Genres` table and a foreign key to the `Artists` table.</span></span> <span data-ttu-id="6745c-131">아래 이미지는 `Albums` 테이블의 일부 테이블 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-131">The image below show some table data from the `Albums` table.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a><span data-ttu-id="6745c-132">HTML Select 태그</span><span class="sxs-lookup"><span data-stu-id="6745c-132">The HTML Select Tag</span></span>

<span data-ttu-id="6745c-133">Html [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 도우미에서 만든 html `<select>` 요소는 전체 값 목록 (예: 장르 목록)을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-133">The HTML `<select>` element (created by the HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper) is used to display a complete list of values (such as the list of genres).</span></span> <span data-ttu-id="6745c-134">편집 폼의 경우 현재 값을 알고 있는 경우 선택 목록에 현재 값이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-134">For edit forms, when the current value is known, the select list can display the current value.</span></span> <span data-ttu-id="6745c-135">이전에 선택한 값을 **코미디**로 설정 하는 경우이에 대해 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-135">We saw this previously when we set the selected value to **Comedy**.</span></span> <span data-ttu-id="6745c-136">Select 목록은 범주 또는 외래 키 데이터를 표시 하는 데 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-136">The select list is ideal for displaying category or foreign key data.</span></span> <span data-ttu-id="6745c-137">장르 외래 키에 대 한 `<select>` 요소는 가능한 장르 이름 목록을 표시 하지만 양식을 저장할 때 장르 속성은 표시 된 장르 이름이 아니라 장르 외래 키 값으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-137">The `<select>` element for the Genre foreign key displays the list of possible genre names, but when you save the form the Genre property is updated with the Genre foreign key value, not the displayed genre name.</span></span> <span data-ttu-id="6745c-138">아래 이미지에서 선택 된 장르는 **Disco** 이며 음악가는 **Donna 여름**입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-138">In the image below, the genre selected is **Disco** and the artist is **Donna Summer**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a><span data-ttu-id="6745c-139">ASP.NET MVC 스 캐 폴드 코드 검사</span><span class="sxs-lookup"><span data-stu-id="6745c-139">Examining the ASP.NET MVC Scaffolded Code</span></span>

<span data-ttu-id="6745c-140">*Controllers\StoreManagerController.cs* 파일을 열고 `HTTP GET Create` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-140">Open the *Controllers\StoreManagerController.cs* file and find the `HTTP GET Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

<span data-ttu-id="6745c-141">`Create` 메서드는 두 개의 [Selectlist](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) 개체를 `ViewBag`에 추가 하 고 하나는 장르 정보를 포함 하 고 다른 하나는 음악가 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-141">The `Create` method adds two [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) objects to the `ViewBag`, one to contain the genre information, and one to contain the artist information.</span></span> <span data-ttu-id="6745c-142">위에서 사용 된 [Selectlist](https://msdn.microsoft.com/library/dd505286.aspx) 생성자 오버 로드에는 세 개의 인수가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-142">The [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) constructor overload used above takes three arguments:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. <span data-ttu-id="6745c-143">*items*: 목록의 항목을 포함 하는 [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-143">*items*: An [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) containing the items in the list.</span></span> <span data-ttu-id="6745c-144">위의 예제에서는 `db.Genres`에서 반환 된 장르 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-144">In the example above, the list of genres returned by `db.Genres`.</span></span>
2. <span data-ttu-id="6745c-145">*Datavaluefield*: 키 값을 포함 하는 **IEnumerable** 목록의 속성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-145">*dataValueField*: The name of the property in the **IEnumerable** list that contains the key value.</span></span> <span data-ttu-id="6745c-146">위의 예제에서 `GenreId` 하 고 `ArtistId`합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-146">In the example above, `GenreId` and `ArtistId`.</span></span>
3. <span data-ttu-id="6745c-147">*dataTextField*: 표시할 정보를 포함 하는 **IEnumerable** 목록의 속성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-147">*dataTextField*: The name of the property in the **IEnumerable** list that contains the information to display.</span></span> <span data-ttu-id="6745c-148">음악가와 장르 테이블 모두에 `name` 필드가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-148">In both the artists and genre table, the `name` field is used.</span></span>

<span data-ttu-id="6745c-149">*Views\StoreManager\Create.cshtml* 파일을 열고 장르 필드에 대 한 `Html.DropDownList` 도우미 태그를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-149">Open the *Views\StoreManager\Create.cshtml* file and examine the `Html.DropDownList` helper markup for the genre field.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

<span data-ttu-id="6745c-150">첫 번째 줄에서는 create view가 `Album` 모델을 사용 하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-150">The first line shows that the create view takes an `Album` model.</span></span> <span data-ttu-id="6745c-151">위에 표시 된 `Create` 메서드에서는 모델이 전달 되지 않으므로 뷰가 **null** `Album` 모델을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-151">In the `Create` method shown above, no model was passed, so the view gets a **null** `Album` model.</span></span> <span data-ttu-id="6745c-152">이 시점에서 새로운 앨범을 만드는 중 이므로 `Album` 데이터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-152">At this point we are creating a new album so we don't have any `Album` data for it.</span></span>

<span data-ttu-id="6745c-153">위에 표시 된 [Html DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 오버 로드는 모델에 바인딩할 필드의 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-153">The [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) overload shown above takes the name of the field to bind to the model.</span></span> <span data-ttu-id="6745c-154">또한이 이름을 사용 하 여 [Selectlist](https://msdn.microsoft.com/library/dd505286.aspx) 개체를 포함 하는 **viewbag** 개체를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-154">It also uses this name to look for a **ViewBag** object containing a [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) object.</span></span> <span data-ttu-id="6745c-155">이 오버 로드를 사용 하 여 `GenreId`**Viewbag SelectList** 개체의 이름을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-155">Using this overload, you are required to name the **ViewBag SelectList** object `GenreId`.</span></span> <span data-ttu-id="6745c-156">두 번째 매개 변수 (`String.Empty`)는 선택 된 항목이 없을 때 표시 되는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-156">The second parameter (`String.Empty`) is the text to display when no item is selected.</span></span> <span data-ttu-id="6745c-157">새 앨범을 만들 때이 작업을 수행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-157">This is exactly what we want when creating a new album.</span></span> <span data-ttu-id="6745c-158">두 번째 매개 변수를 제거 하 고 다음 코드를 사용 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="6745c-158">If you removed the second parameter and used the following code:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

<span data-ttu-id="6745c-159">Select 목록은 기본적으로 첫 번째 요소 또는 샘플에서 록 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-159">The select list would default to the first element, or Rock in our sample.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

<span data-ttu-id="6745c-160">`HTTP POST Create` 메서드 검사</span><span class="sxs-lookup"><span data-stu-id="6745c-160">Examining the `HTTP POST Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

<span data-ttu-id="6745c-161">`Create` 메서드의이 오버 로드는 게시 된 양식 값에서 ASP.NET MVC 모델 바인딩 시스템에 의해 생성 되는 `album` 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-161">This overload of the `Create` method takes an `album` object, created by the ASP.NET MVC model binding system from the form values posted.</span></span> <span data-ttu-id="6745c-162">새 앨범을 제출할 때 모델 상태가 올바르지만 데이터베이스 오류가 없으면 새 앨범이 데이터베이스에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-162">When you submit a new album, if model state is valid and there are no database errors, the new album is added the database.</span></span> <span data-ttu-id="6745c-163">다음 이미지는 새 앨범을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-163">The following image shows the creation of a new album.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

<span data-ttu-id="6745c-164">[Fiddler 도구](http://www.fiddler2.com/fiddler2/) 를 사용 하 여 ASP.NET MVC 모델 바인딩에서 앨범 개체를 만드는 데 사용 하는 게시 된 양식 값을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-164">You can use the [fiddler tool](http://www.fiddler2.com/fiddler2/) to examine the posted form values that ASP.NET MVC model binding uses to create the album object.</span></span>

<span data-ttu-id="6745c-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png)입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span></span>

### <a name="refactoring-the-viewbag-selectlist-creation"></a><span data-ttu-id="6745c-166">ViewBag SelectList 만들기를 리팩터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-166">Refactoring the ViewBag SelectList Creation</span></span>

<span data-ttu-id="6745c-167">`Edit` 메서드와 `HTTP POST Create` 메서드는 모두 **Viewbag**에서 **selectlist** 를 설정 하는 동일한 코드를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-167">Both the `Edit` methods and the `HTTP POST Create` method have identical code to set up the **SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="6745c-168">이 [연습](http://en.wikipedia.org/wiki/Don't_repeat_yourself)에서는이 코드를 리팩터링할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-168">In the spirit of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), we will refactor this code.</span></span> <span data-ttu-id="6745c-169">이 리팩터링 코드는 나중에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-169">We'll make use of this refactored code later.</span></span>

<span data-ttu-id="6745c-170">새 메서드를 만들어 장르 및 음악가 **Selectlist** 를 **viewbag**에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-170">Create a new method to add a genre and artist **SelectList** to the **ViewBag**.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

<span data-ttu-id="6745c-171">각 `Create`의 `ViewBag` 설정 하 고 `SetGenreArtistViewBag` 메서드를 호출 하는 `Edit` 메서드를 설정 하는 두 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-171">Replace the two lines setting the `ViewBag` in each of the `Create` and `Edit` methods with a call to the `SetGenreArtistViewBag` method.</span></span> <span data-ttu-id="6745c-172">완성된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-172">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

<span data-ttu-id="6745c-173">새 앨범을 만들고 앨범을 편집 하 여 변경 내용이 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-173">Create a new album and edit an album to verify the changes work.</span></span>

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a><span data-ttu-id="6745c-174">SelectList를 DropDownList에 명시적으로 전달</span><span class="sxs-lookup"><span data-stu-id="6745c-174">Explicitly Passing the SelectList to the DropDownList</span></span>

<span data-ttu-id="6745c-175">ASP.NET MVC 스 캐 폴딩에서 만든 만들기 및 편집 뷰는 다음과 같은 **DropDownList** 오버 로드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-175">The create and edit views created by the ASP.NET MVC scaffolding use the following **DropDownList** overload:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

<span data-ttu-id="6745c-176">Create view의 `DropDownList` 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-176">The `DropDownList` markup for the create view is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

<span data-ttu-id="6745c-177">`SelectList`에 대 한 `ViewBag` 속성의 이름은 `GenreId`이므로 **DropDownList** 도우미는 **viewbag**의 `GenreId`**selectlist** 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-177">Because the `ViewBag` property for the `SelectList` is named `GenreId`, the **DropDownList** helper will use the `GenreId`**SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="6745c-178">다음 **DropDownList** 오버 로드에서 `SelectList`은 명시적으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-178">In the following **DropDownList** overload, the `SelectList` is explicitly passed in.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

<span data-ttu-id="6745c-179">*Views\StoreManager\Edit.cshtml* 파일을 열고 위의 오버 로드를 사용 하 여 **selectlist**를 명시적으로 전달 하도록 **DropDownList** 호출을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-179">Open the *Views\StoreManager\Edit.cshtml* file, and change the **DropDownList** call to explicitly pass in the **SelectList**, using the overload above.</span></span> <span data-ttu-id="6745c-180">장르 범주에 대해이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-180">Do this for the Genre category.</span></span> <span data-ttu-id="6745c-181">완성 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-181">The completed code is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

<span data-ttu-id="6745c-182">응용 프로그램을 실행 하 고 **관리자** 링크를 클릭 한 다음 재즈 앨범으로 이동 하 여 **편집** 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-182">Run the application and click the **Admin** link, then navigate to a Jazz album and select the **Edit** link.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

<span data-ttu-id="6745c-183">현재 선택 된 장르로 재즈를 표시 하는 대신 바위가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-183">Instead of showing Jazz as the currently selected genre, Rock is displayed.</span></span> <span data-ttu-id="6745c-184">문자열 인수 (바인딩할 속성)와 **Selectlist** 개체의 이름이 같은 경우에는 선택한 값이 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-184">When the string argument (the property to bind) and the **SelectList** object have the same name, the selected value is not used.</span></span> <span data-ttu-id="6745c-185">선택한 값이 없는 경우 브라우저는 기본적으로 **Selectlist**의 첫 번째 요소 (위 예제의 경우 **바위** )로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-185">When there is no selected value provided, browsers default to the first element in the **SelectList**(which is **Rock** in the example above).</span></span> <span data-ttu-id="6745c-186">이는 **DropDownList** 도우미의 알려진 제한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-186">This is a known limitation of the **DropDownList** helper.</span></span>

<span data-ttu-id="6745c-187">*Controllers\StoreManagerController.cs* 파일을 열고 **selectlist** 개체 이름을 `Genres`로 변경 하 고 `Artists`합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-187">Open the *Controllers\StoreManagerController.cs* file and change the **SelectList** object names to `Genres` and `Artists`.</span></span> <span data-ttu-id="6745c-188">완성 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-188">The completed code is shown below:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

<span data-ttu-id="6745c-189">장르 이름 및 음악가 이름에는 각 범주의 ID 외에도 더 많은 범주가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-189">The names Genres and Artists are better names for the categories, as they contain more than just the ID of each category.</span></span> <span data-ttu-id="6745c-190">앞서 지불 했던 리팩터링</span><span class="sxs-lookup"><span data-stu-id="6745c-190">The refactoring we did earlier paid off.</span></span> <span data-ttu-id="6745c-191">네 가지 방법으로 **Viewbag** 를 변경 하는 대신 변경 내용을 `SetGenreArtistViewBag` 메서드로 격리 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-191">Instead of changing the **ViewBag** in four methods, our changes were isolated to the `SetGenreArtistViewBag` method.</span></span>

<span data-ttu-id="6745c-192">Create 및 edit 뷰에서 **DropDownList** 호출을 변경 하 여 새 **selectlist** 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-192">Change the **DropDownList** call in the create and edit views to use the new **SelectList** names.</span></span> <span data-ttu-id="6745c-193">편집 뷰의 새 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-193">The new markup for the edit view is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

<span data-ttu-id="6745c-194">SelectList의 첫 번째 항목이 표시 되지 않도록 하려면 Create view에 빈 문자열이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-194">The Create view requires an empty string to prevent the first item in the SelectList from being displayed.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

<span data-ttu-id="6745c-195">새 앨범을 만들고 앨범을 편집 하 여 변경 내용이 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-195">Create a new album and edit an album to verify the changes work.</span></span> <span data-ttu-id="6745c-196">바위 이외의 장르를 사용 하 여 앨범을 선택 하 여 편집 코드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-196">Test the edit code by selecting an album with a genre other than Rock.</span></span>

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a><span data-ttu-id="6745c-197">DropDownList 도우미와 함께 뷰 모델 사용</span><span class="sxs-lookup"><span data-stu-id="6745c-197">Using a View Model with the DropDownList Helper</span></span>

<span data-ttu-id="6745c-198">ViewModels 폴더에 `AlbumSelectListViewModel`라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-198">Create a new class in the ViewModels folder named `AlbumSelectListViewModel`.</span></span> <span data-ttu-id="6745c-199">`AlbumSelectListViewModel` 클래스의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-199">Replace the code in the `AlbumSelectListViewModel` class with the following:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

<span data-ttu-id="6745c-200">`AlbumSelectListViewModel` 생성자는 앨범 및 음악가의 목록을 사용 하 고 장르 및 음악가의 앨범 및 `SelectList` 포함 된 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-200">The `AlbumSelectListViewModel` constructor takes an album, a list of artists and genres and creates an object containing the album and a `SelectList` for genres and artists.</span></span>

<span data-ttu-id="6745c-201">다음 단계에서 뷰를 만들 때 `AlbumSelectListViewModel`를 사용할 수 있도록 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-201">Build the project so the `AlbumSelectListViewModel` is available when we create a view in the next step.</span></span>

<span data-ttu-id="6745c-202">`StoreManagerController`에 `EditVM` 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-202">Add an `EditVM` method to the `StoreManagerController`.</span></span> <span data-ttu-id="6745c-203">완성된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-203">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

<span data-ttu-id="6745c-204">`AlbumSelectListViewModel`를 마우스 오른쪽 단추로 클릭 하 고 **해결**을 선택한 다음 **MvcMusicStore를 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-204">Right click `AlbumSelectListViewModel`, select **Resolve**, then **using MvcMusicStore.ViewModels;**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

<span data-ttu-id="6745c-205">또는 다음 using 문을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-205">Alternatively, you can add the following using statement:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

<span data-ttu-id="6745c-206">`EditVM`를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-206">Right click `EditVM` and select **Add View**.</span></span> <span data-ttu-id="6745c-207">아래에 표시 된 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-207">Use the options shown below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

<span data-ttu-id="6745c-208">**추가**를 선택 하 고 *Views\StoreManager\EditVM.cshtml* 파일의 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-208">Select **Add**, then replace the contents of the *Views\StoreManager\EditVM.cshtml* file with the following:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

<span data-ttu-id="6745c-209">`EditVM` 태그는 다음과 같은 예외를 제외 하 고 원래 `Edit` 태그와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-209">The `EditVM` markup is very similar to the original `Edit` markup with the following exceptions.</span></span>

- <span data-ttu-id="6745c-210">`Edit` 뷰의 모델 속성은 `model.property`형식 (예: `model.Title`)입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-210">Model properties in the `Edit` view are of the form `model.property`(for example, `model.Title` ).</span></span> <span data-ttu-id="6745c-211">`EditVm` 뷰의 모델 속성은 `model.Album.property`형식 (예: `model.Album.Title`)입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-211">Model properties in the `EditVm` view are of the form `model.Album.property`(for example, `model.Album.Title`).</span></span> <span data-ttu-id="6745c-212">이는 `EditVM` 뷰에 `Edit` 뷰에서와 `Album` 아닌 `Album`에 대 한 컨테이너가 전달 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-212">That's because the `EditVM` view is passed a container for an `Album`, not an `Album` as in the `Edit` view.</span></span>
- <span data-ttu-id="6745c-213">**DropDownList** 두 번째 매개 변수는 **viewbag**아닌 뷰 모델에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-213">The **DropDownList** second parameter comes from the view model, not the **ViewBag**.</span></span>
- <span data-ttu-id="6745c-214">`EditVM` 뷰의 **html.beginform** 도우미는 `Edit` 작업 메서드에 명시적으로 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-214">The **BeginForm** helper in the `EditVM` view explicitly posts back to the `Edit` action method.</span></span> <span data-ttu-id="6745c-215">`Edit` 작업에 다시 게시 하면 `HTTP POST EditVM` 작업을 작성할 필요가 없으며 `HTTP POST` `Edit` 작업을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-215">By posting back to the `Edit` action, we don't have to write an `HTTP POST EditVM` action and can reuse the `HTTP POST` `Edit` action.</span></span>

<span data-ttu-id="6745c-216">응용 프로그램을 실행 하 고 앨범을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-216">Run the application and edit an album.</span></span> <span data-ttu-id="6745c-217">`EditVM`사용 하도록 URL을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-217">Change the URL to use `EditVM`.</span></span> <span data-ttu-id="6745c-218">필드를 변경 하 고 **저장** 단추를 눌러 코드가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-218">Change a field and hit the **Save** button to verify the code is working.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a><span data-ttu-id="6745c-219">어떤 방법을 사용 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="6745c-219">Which Approach Should You Use?</span></span>

<span data-ttu-id="6745c-220">표시 되는 세 가지 방법을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-220">All three approaches shown are acceptable.</span></span> <span data-ttu-id="6745c-221">대부분의 개발자는 `ViewBag`를 사용 하 여 `SelectList`를 `DropDownList`에 명시적으로 전달 하는 것을 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-221">Many developers prefer to explicitly pass the `SelectList` to the `DropDownList` using the `ViewBag`.</span></span> <span data-ttu-id="6745c-222">이 방법에는 컬렉션에 보다 적절 한 이름을 사용 하는 유연성을 제공 하는 추가적인 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-222">This approach has the added advantage of giving you the flexibility of using a more appropriate name for the collection.</span></span> <span data-ttu-id="6745c-223">한 가지 주의할 점은 `ViewBag SelectList` 개체의 이름을 모델 속성과 같은 이름으로 지정할 수 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-223">The one caveat is you cannot name the `ViewBag SelectList` object the same name as the model property.</span></span>

<span data-ttu-id="6745c-224">일부 개발자는 ViewModel 접근 방식을 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-224">Some developers prefer the ViewModel approach.</span></span> <span data-ttu-id="6745c-225">다른 방법으로는 더 자세한 태그를 고려 하 고 ViewModel의 생성 된 HTML을 사용 하는 것이 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-225">Others consider the more verbose markup and generated HTML of the ViewModel approach a disadvantage.</span></span>

<span data-ttu-id="6745c-226">이 섹션에서는 범주 데이터와 함께 **DropDownList** 을 사용 하는 세 가지 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-226">In this section we have learned three approaches to using the **DropDownList** with category data.</span></span> <span data-ttu-id="6745c-227">다음 섹션에서는 새 범주를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6745c-227">In the next section, we'll show how to add a new category.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6745c-228">[이전](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [다음](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="6745c-228">[Previous](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[Next](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span></span>
