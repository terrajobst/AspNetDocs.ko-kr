---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 모델에 유효성 검사 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437279"
---
# <a name="adding-validation-to-the-model"></a><span data-ttu-id="a5a0c-104">모델에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="a5a0c-104">Adding Validation to the Model</span></span>

<span data-ttu-id="a5a0c-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="a5a0c-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="a5a0c-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="a5a0c-107">데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="a5a0c-108">[ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="a5a0c-109">이 섹션에서는 응용 프로그램 내에서 입력 유효성 검사를 사용 하도록 설정 하는 데 필요한 지원을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="a5a0c-110">데이터베이스 콘텐츠가 항상 정확한 지 확인 하 고, 유효 하지 않은 영화 데이터를 입력 하는 경우 최종 사용자에 게 유용한 오류 메시지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="a5a0c-111">먼저 Movie 클래스에 약간의 유효성 검사 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="a5a0c-112">모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 클래스 추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="a5a0c-113">클래스 이름을 Movie로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-113">Name your class Movie.</span></span>

<span data-ttu-id="a5a0c-114">이전에 영화 엔터티 모델을 만들 때 IDE는 Movie 클래스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="a5a0c-115">실제로 Movie 클래스의 일부는 한 파일에 있을 수 있고 다른 파일에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="a5a0c-116">이를 Partial 클래스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-116">This is called a Partial Class.</span></span> <span data-ttu-id="a5a0c-117">다른 파일에서 Movie 클래스를 확장할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="a5a0c-118">시스템에 유효성 검사 힌트를 제공 하는 일부 특성을 가진 "버디 클래스"를 가리키는 부분 영화 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="a5a0c-119">필요에 따라 제목 및 가격을 표시 하 고 가격이 특정 범위 내에 포함 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="a5a0c-120">모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 클래스 추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="a5a0c-121">클래스 이름을 Movie로 하 고 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="a5a0c-122">부분 동영상 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="a5a0c-123">응용 프로그램을 다시 실행 하 고 가격이 100 보다 낮은 영화를 입력 해 보세요.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="a5a0c-124">양식을 제출 하면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="a5a0c-125">이 오류는 서버 쪽에서 catch 되며 폼이 게시 된 후에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="a5a0c-126">ASP.NET MVC의 기본 제공 HTML 도우미는 오류 메시지를 표시 하 고 텍스트 상자 요소 내에서 값을 유지 하는 데 충분 한지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="a5a0c-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a5a0c-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="a5a0c-128">이는 잘 작동 하지만 서버가 포함 되기 전에 클라이언트 쪽에서 즉시 사용자에 게 알릴 수 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="a5a0c-129">JavaScript를 사용 하 여 클라이언트 쪽 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="a5a0c-130">클라이언트측 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="a5a0c-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="a5a0c-131">Movie 클래스에는 이미 일부 유효성 검사 특성이 있기 때문에 몇 가지 JavaScript 파일을 Create .aspx 뷰 템플릿에 추가 하 고 클라이언트 쪽 유효성 검사를 수행할 수 있도록 코드 줄을 추가 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="a5a0c-132">VWD 내에서 Views/Movie 폴더로 이동 하 여 Create .aspx를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="a5a0c-133">솔루션 탐색기에서 Scripts 폴더를 열고 다음 세 개의 스크립트를 &lt;head&gt; 태그 내에 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="a5a0c-134">MicrosoftAjax.js</span><span class="sxs-lookup"><span data-stu-id="a5a0c-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="a5a0c-135">MicrosoftMvcValidation.js</span><span class="sxs-lookup"><span data-stu-id="a5a0c-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="a5a0c-136">이러한 스크립트 파일이이 순서 대로 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="a5a0c-137">또한이 한 줄을 Html.beginform 위에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="a5a0c-138">IDE 내에 표시 되는 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="a5a0c-139">[![영화-Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="a5a0c-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="a5a0c-140">응용 프로그램을 실행 하 고/Movies/Create를 다시 방문 하 고 데이터를 입력 하지 않고 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="a5a0c-141">오류 메시지는 서버에 대 한 모든 방식으로 데이터를 전송 하는 데 연결 하는 페이지 플래시 없이 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="a5a0c-142">ASP.NET MVC는 이제 JavaScript를 사용 하 여 클라이언트와 서버에서 입력의 유효성을 검사 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="a5a0c-143">[![만들기-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="a5a0c-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="a5a0c-144">좋은 방법입니다!</span><span class="sxs-lookup"><span data-stu-id="a5a0c-144">This is looking good!</span></span> <span data-ttu-id="a5a0c-145">이제 데이터베이스에 열을 하나 더 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a5a0c-145">Let's now add one additional column to the database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a5a0c-146">[이전](getting-started-with-mvc-part6.md)
> [다음](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="a5a0c-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>
