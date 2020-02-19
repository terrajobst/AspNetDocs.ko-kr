---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: JQuery UI를 사용 하 여 DropDownList에 새 범주 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 3207079ee468232e5f75b081421241c232936baf
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455726"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="4ccc5-102">jQuery UI를 사용하여 DropDownList에 새 범주 추가</span><span class="sxs-lookup"><span data-stu-id="4ccc5-102">Adding a New Category to the DropDownList using jQuery UI</span></span>

<span data-ttu-id="4ccc5-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="4ccc5-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="4ccc5-104">HTML `Select` 태그는 고정 된 범주 데이터의 목록을 제공 하는 데 이상적 이지만 새 범주를 추가 해야 하는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="4ccc5-105">데이터베이스의 범주에 "Opera" 장르를 추가 하려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="4ccc5-106">이 섹션에서는 jQuery UI를 사용 하 여 새 범주를 추가 하는 데 사용할 수 있는 대화 상자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="4ccc5-107">아래 이미지는 브라우저에서 UI가 표시 되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="4ccc5-108">사용자가 **새 장르 추가** 링크를 선택 하면 팝업 대화 상자에 사용자에 게 새 장르 이름과 설명 (선택 사항)을 입력 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="4ccc5-109">아래 이미지는 **장르 추가** 팝업 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="4ccc5-110">새 장르 이름을 입력 하면 **저장** 단추가 푸시되 면 다음과 같은 상황이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="4ccc5-111">AJAX 호출은 장르 컨트롤러의 Create 메서드에 데이터를 게시 합니다. 그러면 새 장르를 데이터베이스에 저장 하 고 새 장르 정보 (장르 이름 및 ID)를 JSON으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="4ccc5-112">JavaScript는 새 장르 데이터를 선택 목록에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="4ccc5-113">JavaScript는 새 장르를 선택한 항목으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-113">JavaScript makes the new genre the selected item.</span></span>

   <span data-ttu-id="4ccc5-114">아래 이미지에서 **Opera** 는 데이터베이스에 추가 되 고 **장르** 드롭다운 목록에서 선택 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="4ccc5-115">*Views\StoreManager\Create.cshtml* 파일을 열고 장르 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="4ccc5-116">`_ChooseGenre` 부분 보기에는 새 장르 추가 기능을 구현 하는 데 사용 되는 JavaScript 및 jQuery를 연결 하는 모든 논리가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="4ccc5-117">코드를 완료 한 후에는 음악가 UI를 사용 하 여 동일한 작업을 수행 하는 것이 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="4ccc5-118">솔루션 탐색기에서 *Views\StoreManager* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **보기**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="4ccc5-119">**보기 이름** 입력에 `_ChooseGenre`를 입력 하 고 **추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="4ccc5-120">*Views\StoreManager\\_ChooseGenre* 의 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="4ccc5-121">첫 번째 줄은 모델 처럼 `Album`를 전달 한다는 것을 선언 하 고, Create view에 있는 동일한 모델 문을 정확히 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="4ccc5-122">다음 줄은 **레이블** 도우미 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="4ccc5-123">다음 줄은 원래 Create view와 정확히 같은 **DropDownList** 도우미 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="4ccc5-124">다음 줄은 `Add New Genre`이름이 있는 링크를 추가 하 고 단추 처럼 스타일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="4ccc5-125">`ValidationMessageFor`를 포함 하는 줄은 Create view에서 직접 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="4ccc5-126">다음 줄:</span><span class="sxs-lookup"><span data-stu-id="4ccc5-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="4ccc5-127">ID가 `genreDialog`인 숨겨진 div를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="4ccc5-128">JQuery를 사용 하 여이 div의 ID `genreDialog`를 사용 하 여 **장르 추가** 대화 상자를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="4ccc5-129">마지막 두 스크립트 태그에는 새 장르 추가 기능을 구현 하는 데 사용할 JavaScript 파일에 대 한 링크가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="4ccc5-130">*/Scripts/chooseGenre.js* 파일은 프로젝트에 제공 되며 자습서의 뒷부분에서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="4ccc5-131">응용 프로그램을 실행 하 고 **새 장르 추가** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="4ccc5-132">**장르 추가** 대화 상자에서 **이름** 입력 상자에 **Opera** 를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="4ccc5-133">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-133">Click the **Save** button.</span></span> <span data-ttu-id="4ccc5-134">AJAX 호출은 Opera 범주를 만든 다음 Opera를 사용 하 여 드롭다운 목록을 채우고 Opera를 선택 된 장르로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="4ccc5-135">음악가, 제목 및 가격을 입력 한 다음 **만들기** 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="4ccc5-136">$8.99 보다 작은 가격을 입력 하면 새 앨범이 인덱스 보기의 맨 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="4ccc5-137">새 앨범 항목이 데이터베이스에 저장 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="4ccc5-138">한 문자만 사용 하 여 새 장르를 만들어 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="4ccc5-139">*Models\genre.cs* 파일의 다음 코드는 장르 이름의 최소 및 최대 길이를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="4ccc5-140">클라이언트 쪽 유효성 검사 보고서 2 ~ 007e; 20 자 사이의 문자열을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="4ccc5-141">데이터베이스 및 선택 목록에 새 장르를 추가 하는 방법을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="4ccc5-142">*Scripts\chooseGenre.js* 파일을 열고 코드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="4ccc5-143">두 번째 줄은 ID `genreDialog`를 사용 하 여 *Views\StoreManager\\_ChooseGenre. cshtml* 파일의 div 태그에 대화 상자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="4ccc5-144">대부분의 명명 된 매개 변수는 자체 설명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="4ccc5-145">`autoOpen` 매개 변수는 false로 설정 되 고, **장르 만들기** 단추를 선택 하면 대화 상자가 명시적으로 열립니다 (이에 대 한 뒷부분에서 설명).</span><span class="sxs-lookup"><span data-stu-id="4ccc5-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="4ccc5-146">대화 상자에는 **저장** 및 **취소**단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="4ccc5-147">**취소** 단추를 클릭 하면 대화 상자가 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="4ccc5-148">다음 코드에서는 **저장** 단추 함수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="4ccc5-149">`var createGenreForm` `createGenreForm` ID에서 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="4ccc5-150">`createGenreForm` ID는 *Views\Genre\\_CreateGenre. cshtml* 파일에 있는 다음 코드에서 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="4ccc5-151">*Views\Genre\\_CreateGenre* 에서 사용 되는 [html. html.beginform](https://msdn.microsoft.com/library/dd492714.aspx) 도우미 오버 로드는 폼을 전송 하기 위한 URL이 포함 된 action 특성으로 html을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="4ccc5-152">브라우저에서 앨범 만들기 페이지를 표시 하 고 브라우저에서 소스 표시를 선택 하 여이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="4ccc5-153">다음 태그는 form 태그를 포함 하는 생성 된 HTML을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="4ccc5-154">JQuery `$.post` 줄은 작업 특성 (`/StoreManager/Create`)에 대 한 AJAX 호출을 수행 하 고 **장르 만들기** 대화 상자에서 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="4ccc5-155">데이터는 새 장르 이름과 설명 (선택 사항)으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="4ccc5-156">AJAX 호출에 성공 하면 새 장르 이름과 값이 선택 태그에 추가 되 고 새 장르는 선택한 값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="4ccc5-157">이는 동적으로 생성 된 태그 이므로 브라우저에서 소스를 확인 하 여 새 선택 옵션을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="4ccc5-158">IE 9 F12 개발자 도구를 사용 하 여 새 HTML을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="4ccc5-159">새 선택 옵션을 보려면 Internet Explorer 9에서 F12 키를 눌러 F12 개발자 도구를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="4ccc5-160">만들기 페이지로 이동 하 고 새 장르를 추가 하 여 장르 선택 목록에서 새 장르를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="4ccc5-161">F12 개발자 도구:</span><span class="sxs-lookup"><span data-stu-id="4ccc5-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="4ccc5-162">HTML 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="4ccc5-163">새로 고침 아이콘을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="4ccc5-164">검색 상자에 GenreID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="4ccc5-165">다음 아이콘을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4ccc5-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   <span data-ttu-id="4ccc5-166">다음 select 태그로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="4ccc5-167">마지막 옵션 값을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="4ccc5-168">*Scripts\chooseGenre.js* 파일의 다음 코드는 **새 장르 추가** 단추가 클릭 이벤트에 연결 되는 방법 및 **새 장르 추가** 대화 상자를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="4ccc5-169">첫 번째 줄에서는 **새 장르 추가** 단추에 연결 된 클릭 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="4ccc5-170">Views\StoreManager\\_ChooseGenre 파일의 다음 태그는 **새 장르 추가** 단추가 만들어지는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="4ccc5-171">Load 메서드는 장르 추가 대화 상자를 만들고 열고 jQuery `parse` 메서드를 호출 하 여 대화 상자에 입력 한 데이터에서 클라이언트 유효성 검사가 수행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="4ccc5-172">이 섹션에서는 선택 목록에 새 범주 데이터를 추가 하는 데 사용할 수 있는 대화 상자를 만드는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="4ccc5-173">동일한 절차에 따라 새 음악가를 음악가 선택 목록에 추가 하는 UI를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="4ccc5-174">이 자습서에서는 ASP.NET MVC HTML 도우미 **DropDownList**사용에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="4ccc5-175">**DropDownList**사용에 대 한 자세한 내용은 아래의 추가 참조 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="4ccc5-176">이 자습서를 통해 도움이 되는 경우 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="4ccc5-177">Rick.Anderson[at]Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="4ccc5-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="4ccc5-178">추가 참조</span><span class="sxs-lookup"><span data-stu-id="4ccc5-178">Additional References</span></span>

- <span data-ttu-id="4ccc5-179">[ASP.NET MVC – 계단식 드롭다운 목록](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) [Radu Enuca의](https://weblogs.asp.net/raduenuca/default.aspx) 자습서</span><span class="sxs-lookup"><span data-stu-id="4ccc5-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="4ccc5-180">[선택](https://harvesthq.github.com/chosen/) 다중 선택 및 필터링을 지 원하는 JavaScript 플러그 인입니다.</span><span class="sxs-lookup"><span data-stu-id="4ccc5-180">[Chosen](https://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="4ccc5-181">참가자</span><span class="sxs-lookup"><span data-stu-id="4ccc5-181">Contributors</span></span>

- [<span data-ttu-id="4ccc5-182">Radu Ena</span><span class="sxs-lookup"><span data-stu-id="4ccc5-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="4ccc5-183">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="4ccc5-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="4ccc5-184">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="4ccc5-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="4ccc5-185">검토자</span><span class="sxs-lookup"><span data-stu-id="4ccc5-185">Reviewers</span></span>

- <span data-ttu-id="4ccc5-186">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="4ccc5-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="4ccc5-187">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="4ccc5-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="4ccc5-188">Mike Pope</span><span class="sxs-lookup"><span data-stu-id="4ccc5-188">Mike Pope</span></span>
- <span data-ttu-id="4ccc5-189">Tom Dykstra</span><span class="sxs-lookup"><span data-stu-id="4ccc5-189">Tom Dykstra</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4ccc5-190">이전</span><span class="sxs-lookup"><span data-stu-id="4ccc5-190">Previous</span></span>](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
