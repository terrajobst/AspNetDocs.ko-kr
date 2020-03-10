---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 모델에 열 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437225"
---
# <a name="adding-a-column-to-the-model"></a><span data-ttu-id="06af9-104">모델에 열 추가</span><span class="sxs-lookup"><span data-stu-id="06af9-104">Adding a Column to the Model</span></span>

<span data-ttu-id="06af9-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="06af9-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="06af9-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="06af9-107">데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="06af9-108">[ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="06af9-109">이 섹션에서는 데이터베이스의 스키마를 변경 하 고 응용 프로그램 내에서 변경 내용을 처리 하는 방법을 단계별로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="06af9-110">동영상 테이블에 "등급" 열을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-110">Let's add a "Rating" Column to the Movie table.</span></span> <span data-ttu-id="06af9-111">IDE로 돌아가서 데이터베이스 탐색기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="06af9-112">동영상 테이블을 마우스 오른쪽 단추로 클릭 하 고 테이블 정의 열기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="06af9-113">아래 표시 된 것 처럼 "등급" 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="06af9-114">지금은 등급이 없으므로 열에서 null을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="06af9-115">저장을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-115">Click Save.</span></span>

<span data-ttu-id="06af9-116">[동영상 테이블 편집 ![](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="06af9-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="06af9-117">그런 다음 솔루션 탐색기로 돌아가서 영화 .edmx 파일 (\Stoml 폴더에 있습니다)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="06af9-118">디자인 화면 (흰색 영역)을 마우스 오른쪽 단추로 클릭 하 고 데이터베이스에서 모델 업데이트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="06af9-119">[![영화-Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="06af9-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="06af9-120">그러면 "업데이트 마법사"가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="06af9-121">내 새로 고침 탭을 클릭 하 고 마침을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="06af9-122">그런 다음 새 열을 사용 하 여 동영상 모델 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-122">Our Movie model class will then be updated with the new column.</span></span>

![업데이트 마법사 (2)](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="06af9-124">마침을 클릭 하면 모델의 영화 엔터티에 새 등급 열이 추가 된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="06af9-125">[![Movie 엔터티](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="06af9-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="06af9-126">데이터베이스 모델에 열을 추가 했지만 뷰에서는 열을 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="06af9-127">모델 변경 내용으로 뷰 업데이트</span><span class="sxs-lookup"><span data-stu-id="06af9-127">Update Views with Model Changes</span></span>

<span data-ttu-id="06af9-128">몇 가지 방법으로 보기 템플릿을 업데이트 하 여 새 등급 열을 반영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="06af9-129">뷰 추가 대화 상자를 통해 이러한 뷰를 생성 했으므로 삭제 하 고 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="06af9-130">그러나 일반적으로 사용자는 초기 스 캐 폴드 생성에서 보기 템플릿을 수정 했으며 Create에 대 한 ID 필드와 마찬가지로 필드를 수동으로 추가 하거나 삭제 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="06af9-131">\Views\Movies\Index.aspx 템플릿을 열고 &lt;번째&gt;등급&lt;/th&gt;를 동영상 테이블의 헤드에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="06af9-132">장르 뒤에 광산을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-132">I added mine after Genre.</span></span> <span data-ttu-id="06af9-133">그런 다음 동일한 열 위치에서 아래쪽으로 줄을 추가 하 여 새 등급을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="06af9-134">최종 Index .aspx 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="06af9-135">\Views\Movies\Create.aspx 템플릿을 열고 새 등급 속성에 대 한 레이블 및 텍스트 상자를 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="06af9-136">최종 .aspx 템플릿은 다음과 같이 표시 되 고 여기에 있는 동안 브라우저의 제목 및 보조 &lt;h2&gt; 제목을 "동영상 만들기"와 같이 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="06af9-137">앱을 실행 하면 데이터베이스에서 만들기 페이지에 추가 된 새 필드가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="06af9-138">새 영화 (이번에는 등급)를 추가 하 고 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="06af9-139">[동영상 ![만들기-Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="06af9-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="06af9-140">만들기를 클릭 하면 새 동영상이 데이터베이스의 새 등급 열로 나열 된 인덱스 페이지로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="06af9-141">[![동영상 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="06af9-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="06af9-142">이 기본 자습서에서는 컨트롤러를 만들어 뷰와 연결 하 고 하드 코드 된 데이터를 전달 하기 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="06af9-143">그런 다음 데이터베이스를 만들고 디자인 하 고 일부 데이터를 저장 했습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="06af9-144">데이터베이스에서 데이터를 검색 하 여 HTML 테이블에 표시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="06af9-145">그런 다음 사용자가 웹 응용 프로그램 내에서 데이터베이스 자체에 데이터를 추가할 수 있는 만들기 폼을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="06af9-146">유효성 검사를 추가 하 고 클라이언트 쪽에서 JavaScript를 사용 하 여 유효성 검사를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="06af9-147">마지막으로 새 데이터 열을 포함 하도록 데이터베이스를 변경 하 고 두 페이지를 업데이트 하 여 새 데이터를 만들고 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="06af9-148">이제 ASP.NET MVC에 대해 자세히 학습할 수 있는 많은 비디오와 [https://asp.net/mvc](https://asp.net/mvc) 리소스 뿐만 아니라 중간 수준 자습서 "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)"로 이동 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="06af9-149">마음껏 즐기세요!</span><span class="sxs-lookup"><span data-stu-id="06af9-149">Enjoy!</span></span>

- <span data-ttu-id="06af9-150">Twitter의 Scott Hanselman [http://hanselman.com](http://hanselman.com) 및 [@shanselman](http://twitter.com/shanselman) 입니다.</span><span class="sxs-lookup"><span data-stu-id="06af9-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="06af9-151">이전</span><span class="sxs-lookup"><span data-stu-id="06af9-151">Previous</span></span>](getting-started-with-mvc-part7.md)
