---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: 영화 모델 및 테이블에 새 필드 추가 (C#) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 40b02a2f608f07091ce6b5339688a1e6290e2e37
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457456"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table-c"></a><span data-ttu-id="64c64-103">영화 모델 및 테이블에 새 필드 추가(C#)</span><span class="sxs-lookup"><span data-stu-id="64c64-103">Adding a New Field to the Movie Model and Table (C#)</span></span>

<span data-ttu-id="64c64-104">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="64c64-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="64c64-105">ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../../getting-started/introduction/getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="64c64-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="64c64-106">더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="64c64-107">이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="64c64-108">시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="64c64-109">[웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="64c64-110">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="64c64-111">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="64c64-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="64c64-112">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="64c64-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="64c64-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="64c64-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="64c64-114">Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="64c64-115">이 항목과 함께 사용할 수 있는 C# 소스 코드가 포함 된 Visual Web Developer 프로젝트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="64c64-116">[버전을 C# 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="64c64-117">Visual Basic 선호 하는 경우이 자습서의 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="64c64-118">이 섹션에서는 모델 클래스를 몇 가지 변경 하 고 모델 변경 내용과 일치 하도록 데이터베이스 스키마를 업데이트 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-118">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="64c64-119">동영상 모델에 등급 속성 추가</span><span class="sxs-lookup"><span data-stu-id="64c64-119">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="64c64-120">기존 `Movie` 클래스에 새 `Rating` 속성을 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-120">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="64c64-121">*Movie.cs* 파일을 열고 다음과 같은 `Rating` 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-121">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="64c64-122">이제 전체 `Movie` 클래스는 다음 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-122">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

<span data-ttu-id="64c64-123">**디버그** &gt;**동영상 빌드** 메뉴 명령을 사용 하 여 응용 프로그램을 다시 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-123">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="64c64-124">`Model` 클래스를 업데이트 했으므로 이제 새 `Rating` 속성을 지원 하기 위해 *\Views\Movies\Index.cshtml* 및 *\Views\Movies\Create.cshtml* 뷰 템플릿을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-124">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="64c64-125">*\Views\Movies\Index.cshtml* 파일을 열고 **Price** 열 바로 뒤에 `<th>Rating</th>` 열 머리글을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-125">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="64c64-126">그런 다음 템플릿 끝 근처에 `<td>` 열을 추가 하 여 `@item.Rating` 값을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-126">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="64c64-127">다음은 업데이트 된 *인덱스입니다. cshtml* 뷰 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-127">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

<span data-ttu-id="64c64-128">그런 다음 *\Views\Movies\Create.cshtml* 파일을 열고 폼의 끝 부분에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-128">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="64c64-129">그러면 새 동영상이 생성 될 때 등급을 지정할 수 있도록 텍스트 상자가 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-129">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="64c64-130">모델 및 데이터베이스 스키마 차이점 관리</span><span class="sxs-lookup"><span data-stu-id="64c64-130">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="64c64-131">이제 새 `Rating` 속성을 지원 하도록 응용 프로그램 코드를 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-131">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="64c64-132">이제 응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-132">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="64c64-133">그러나이 작업을 수행 하면 다음과 같은 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-133">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="64c64-134">응용 프로그램의 업데이트 된 `Movie` 모델 클래스가 이제 기존 데이터베이스의 `Movie` 테이블의 스키마와 다르기 때문에이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-134">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="64c64-135">(데이터베이스 테이블에 `Rating` 열이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="64c64-135">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="64c64-136">기본적으로이 Code First 자습서의 앞부분에서와 같이 Entity Framework Code First를 사용 하 여 데이터베이스를 자동으로 만드는 경우 데이터베이스에 테이블을 추가 하 여 데이터베이스의 스키마가 생성 된 모델 클래스와 동기화 되어 있는지 여부를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-136">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="64c64-137">동기화 되지 않은 경우 Entity Framework에서 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-137">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="64c64-138">이렇게 하면 런타임에 발생 하는 문제를 쉽게 추적할 수 있습니다. 단, 런타임에는 명확 하지 않은 오류를 통해서만 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-138">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="64c64-139">동기화 검사 기능은 오류 메시지를 표시 하 여 방금 본 것으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-139">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="64c64-140">오류를 해결 하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-140">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="64c64-141">Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-141">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="64c64-142">이 방법은 모델 및 데이터베이스 스키마를 함께 신속 하 게 진화 시킬 수 있으므로 테스트 데이터베이스에 대 한 활성 개발을 수행할 때 매우 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-142">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="64c64-143">그러나 단점은 데이터베이스의 기존 데이터를 잃지 않으므로 프로덕션 데이터베이스에서이 방법을 사용 *하지* 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-143">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="64c64-144">모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-144">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="64c64-145">이 방법의 장점은 데이터가 유지된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-145">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="64c64-146">이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-146">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="64c64-147">이 자습서에서는 첫 번째 방법을 사용 합니다. 모델이 변경 될 때마다 Entity Framework Code First 자동으로 데이터베이스를 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-147">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="64c64-148">모델 변경 시 데이터베이스 자동으로 다시 만들기</span><span class="sxs-lookup"><span data-stu-id="64c64-148">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="64c64-149">응용 프로그램에 대 한 모델을 변경할 때마다 데이터베이스를 자동으로 삭제 하 고 다시 만들도록 응용 Code First 프로그램을 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-149">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="64c64-150">**경고** 개발 또는 테스트 데이터베이스를 사용 중이 고 실제 데이터를 포함 하는 프로덕션 데이터베이스가 아닌 *경우에만* 데이터베이스를 자동으로 삭제 하 고 다시 생성 하는이 방법을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-150">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="64c64-151">프로덕션 서버에서이를 사용 하면 데이터가 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-151">Using it on a production server can lead to data loss.</span></span>

<span data-ttu-id="64c64-152">**솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-152">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="64c64-153">클래스 이름을 "MovieInitializer"로 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-153">Name the class "MovieInitializer".</span></span> <span data-ttu-id="64c64-154">다음 코드를 포함 하도록 `MovieInitializer` 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-154">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="64c64-155">`MovieInitializer` 클래스는 모델 클래스를 변경 하는 경우 모델에서 사용 하는 데이터베이스를 삭제 하 고 자동으로 다시 만들도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-155">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="64c64-156">코드에는 생성 (또는 다시 생성) 될 때마다 데이터베이스에 자동으로 추가 되는 일부 기본 데이터를 지정 하는 `Seed` 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-156">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="64c64-157">이렇게 하면 모델을 변경할 때마다 데이터베이스를 수동으로 채우지 않고도 일부 샘플 데이터로 데이터베이스를 채우는 데 유용한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-157">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="64c64-158">이제 `MovieInitializer` 클래스를 정의 했으므로 응용 프로그램이 실행 될 때마다 모델 클래스가 데이터베이스의 스키마와 다른 지 확인 하기 위해 연결 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-158">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="64c64-159">이러한 항목이 있는 경우 이니셜라이저를 실행 하 여 데이터베이스를 모델에 맞게 다시 만든 다음, 데이터베이스를 샘플 데이터로 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-159">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="64c64-160">`MvcMovies` 프로젝트의 루트에 있는 *global.asax* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-160">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

<span data-ttu-id="64c64-161">*Global.asax* 파일에는 프로젝트에 대 한 전체 응용 프로그램을 정의 하는 클래스가 포함 되어 있으며, 응용 프로그램을 처음 시작할 때 실행 되는 `Application_Start` 이벤트 처리기가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-161">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="64c64-162">파일의 맨 위에 두 개의 using 문을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-162">Let's add two using statements to the top of the file.</span></span> <span data-ttu-id="64c64-163">첫 번째는 Entity Framework 네임 스페이스를 참조 하 고, 두 번째는 `MovieInitializer` 클래스가 있는 네임 스페이스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-163">The first references the Entity Framework namespace, and the second references the namespace where our `MovieInitializer` class lives:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

<span data-ttu-id="64c64-164">그런 다음 `Application_Start` 메서드를 찾고 아래와 같이 메서드 시작 부분에 `Database.SetInitializer`에 대 한 호출을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-164">Then find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

<span data-ttu-id="64c64-165">방금 추가한 `Database.SetInitializer` 문은 스키마와 데이터베이스가 일치 하지 않는 경우 `MovieDBContext` 인스턴스에서 사용 하는 데이터베이스를 자동으로 삭제 하 고 다시 생성 해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-165">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="64c64-166">또한 사용자가 확인 한 대로 데이터베이스를 `MovieInitializer` 클래스에 지정 된 샘플 데이터로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-166">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="64c64-167">*Global.asax* 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-167">Close the *Global.asax* file.</span></span>

<span data-ttu-id="64c64-168">응용 프로그램을 다시 실행 하 고/또는 *비디오* URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-168">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="64c64-169">응용 프로그램이 시작 되 면 모델 구조가 더 이상 데이터베이스 스키마와 일치 하지 않는 것을 감지 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-169">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="64c64-170">새 모델 구조와 일치 하는 데이터베이스를 자동으로 다시 만들고 샘플 영화를 사용 하 여 데이터베이스를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-170">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

<span data-ttu-id="64c64-172">새 동영상을 추가 하려면 **새로 만들기** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-172">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="64c64-173">등급을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-173">Note that you can add a rating.</span></span>

<span data-ttu-id="64c64-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="64c64-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span></span>

<span data-ttu-id="64c64-175">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-175">Click **Create**.</span></span> <span data-ttu-id="64c64-176">이제 등급을 포함 하 여 새 동영상이 영화 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-176">The new movie, including the rating, now shows up in the movies listing:</span></span>

<span data-ttu-id="64c64-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="64c64-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span></span>

<span data-ttu-id="64c64-178">이 섹션에서는 모델 개체를 수정 하 고 데이터베이스를 변경 내용과 동기화 된 상태로 유지 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-178">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="64c64-179">시나리오를 시험해 볼 수 있도록 새로 만든 데이터베이스를 샘플 데이터로 채우는 방법도 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-179">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="64c64-180">다음으로 모델 클래스에 더 다양 한 유효성 검사 논리를 추가 하 고 일부 비즈니스 규칙을 적용할 수 있도록 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="64c64-180">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="64c64-181">[이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="64c64-181">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
