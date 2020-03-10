---
uid: web-pages/overview/data/working-with-files
title: ASP.NET 웹 페이지 (Razor) 사이트에서 파일 작업 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 파일을 읽고, 쓰고, 추가 하 고, 삭제 하 고, 업로드 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 684c47a8a8480dc040e5144144577c94c35d39e5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521885"
---
# <a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="5197a-103">ASP.NET 웹 페이지 (Razor) 사이트에서 파일 작업</span><span class="sxs-lookup"><span data-stu-id="5197a-103">Working with Files in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="5197a-104">만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5197a-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5197a-105">이 문서에서는 Razor (ASP.NET 웹 페이지) 사이트에서 파일을 읽고, 쓰고, 추가 하 고, 삭제 하 고, 업로드 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-105">This article explains how to read, write, append, delete, and upload files in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="5197a-106">이미지를 업로드 하 고 조작 하려면 (예: 대칭 이동 또는 크기 조정) [ASP.NET 웹 페이지 사이트에서 이미지 작업](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5197a-106">If you want to upload images and manipulate them (for example, flip or resize them), see [Working with Images in an ASP.NET Web Pages Site](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images).</span></span>
> 
> 
> <span data-ttu-id="5197a-107">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="5197a-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="5197a-108">텍스트 파일을 만들고이 파일에 데이터를 쓰는 방법</span><span class="sxs-lookup"><span data-stu-id="5197a-108">How to create a text file and write data to it.</span></span>
> - <span data-ttu-id="5197a-109">기존 파일에 데이터를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5197a-109">How to append data to an existing file.</span></span>
> - <span data-ttu-id="5197a-110">파일을 읽고 파일에서 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-110">How to read a file and display from it.</span></span>
> - <span data-ttu-id="5197a-111">웹 사이트에서 파일을 삭제 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5197a-111">How to delete files from a website.</span></span>
> - <span data-ttu-id="5197a-112">사용자가 한 파일 또는 여러 파일을 업로드할 수 있도록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-112">How to let users upload one file or multiple files.</span></span>
> 
> <span data-ttu-id="5197a-113">다음은이 문서에 도입 된 ASP.NET 프로그래밍 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-113">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="5197a-114">파일을 관리 하는 방법을 제공 하는 `File` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-114">The `File` object, which provides a way to manage files.</span></span>
> - <span data-ttu-id="5197a-115">`FileUpload` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-115">The `FileUpload` helper.</span></span>
> - <span data-ttu-id="5197a-116">경로와 파일 이름을 조작할 수 있는 메서드를 제공 하는 `Path` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-116">The `Path` object, which provides methods that let you manipulate path and file names.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5197a-117">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="5197a-117">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5197a-118">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="5197a-118">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="5197a-119">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="5197a-119">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="5197a-120">이 자습서는 WebMatrix 3 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-120">This tutorial also works with WebMatrix 3.</span></span>

<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a><span data-ttu-id="5197a-121">텍스트 파일을 만들고 여기에 데이터 쓰기</span><span class="sxs-lookup"><span data-stu-id="5197a-121">Creating a Text File and Writing Data to It</span></span>

<span data-ttu-id="5197a-122">웹 사이트에서 데이터베이스를 사용 하는 것 외에도 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-122">In addition to using a database in your website, you might work with files.</span></span> <span data-ttu-id="5197a-123">예를 들어 텍스트 파일을 사이트에 대 한 데이터를 저장 하는 간단한 방법으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-123">For example, you might use text files as a simple way to store data for the site.</span></span> <span data-ttu-id="5197a-124">데이터를 저장 하는 데 사용 되는 텍스트 파일을 *플랫 파일이*라고도 합니다. 텍스트 파일은 *.txt*, *.xml*또는 *.csv* (쉼표로 구분 된 값)와 같은 다양 한 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-124">(A text file that's used to store data is sometimes called a *flat file*.) Text files can be in different formats, like *.txt*, *.xml*, or *.csv* (comma-delimited values).</span></span>

<span data-ttu-id="5197a-125">텍스트 파일에 데이터를 저장 하려는 경우 `File.WriteAllText` 메서드를 사용 하 여 만들 파일과 해당 파일에 쓸 데이터를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-125">If you want to store data in a text file, you can use the `File.WriteAllText` method to specify the file to create and the data to write to it.</span></span> <span data-ttu-id="5197a-126">이 절차에서는 3 개의 `input` 요소 (이름, 성 및 전자 메일 주소)와 **제출** 단추를 포함 하는 간단한 양식이 포함 된 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-126">In this procedure, you'll create a page that contains a simple form with three `input` elements (first name, last name, and email address) and a **Submit** button.</span></span> <span data-ttu-id="5197a-127">사용자가 양식을 제출할 때 텍스트 파일에 사용자의 입력을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-127">When the user submits the form, you'll store the user's input in a text file.</span></span>

1. <span data-ttu-id="5197a-128">이미 존재 하지 않는 경우 *App\_Data*라는 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-128">Create a new folder named *App\_Data*, if it doesn't exist already.</span></span>
2. <span data-ttu-id="5197a-129">웹 사이트의 루트에서 *UserData. cshtml*라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-129">At the root of your website, create a new file named *UserData.cshtml*.</span></span>
3. <span data-ttu-id="5197a-130">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-130">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    <span data-ttu-id="5197a-131">HTML 태그는 세 개의 텍스트 상자를 사용 하 여 폼을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-131">The HTML markup creates the form with the three text boxes.</span></span> <span data-ttu-id="5197a-132">코드에서 `IsPost` 속성을 사용 하 여 처리를 시작 하기 전에 페이지가 전송 되었는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-132">In the code, you use the `IsPost` property to determine whether the page has been submitted before you start processing.</span></span>

    <span data-ttu-id="5197a-133">첫 번째 작업은 사용자 입력을 가져와 변수에 할당 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-133">The first task is to get the user input and assign it to variables.</span></span> <span data-ttu-id="5197a-134">그런 다음 코드는 개별 변수의 값을 쉼표로 구분 된 하나의 문자열로 연결 합니다. 그러면 다른 변수에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-134">The code then concatenates the values of the separate variables into one comma-delimited string, which is then stored in a different variable.</span></span> <span data-ttu-id="5197a-135">쉼표 구분 기호는 생성 하는 큰 문자열에 쉼표를 포함 하 고 있기 때문에 따옴표 (",")에 포함 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-135">Notice that the comma separator is a string contained in quotation marks (","), because you're literally embedding a comma into the big string that you're creating.</span></span> <span data-ttu-id="5197a-136">함께 연결 하는 데이터의 끝에 `Environment.NewLine`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-136">At the end of the data that you concatenate together, you add `Environment.NewLine`.</span></span> <span data-ttu-id="5197a-137">줄 바꿈 (줄 바꿈 문자)이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-137">This adds a line break (a newline character).</span></span> <span data-ttu-id="5197a-138">이 연결을 모두 사용 하 여 만드는 작업은 다음과 같은 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-138">What you're creating with all this concatenation is a string that looks like this:</span></span>

    [!code-css[Main](working-with-files/samples/sample2.css)]

    <span data-ttu-id="5197a-139">(끝에 보이지 않는 줄 바꿈 포함)</span><span class="sxs-lookup"><span data-stu-id="5197a-139">(With an invisible line break at the end.)</span></span>

    <span data-ttu-id="5197a-140">그런 다음 데이터를 저장할 파일의 위치와 이름을 포함 하는 변수 (`dataFile`)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-140">You then create a variable (`dataFile`) that contains the location and name of the file to store the data in.</span></span> <span data-ttu-id="5197a-141">위치를 설정 하려면 특별 한 처리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-141">Setting the location requires some special handling.</span></span> <span data-ttu-id="5197a-142">웹 사이트에서는 웹 서버에서 파일의 *C:\Folder\File.txt* 와 같은 절대 경로에 대 한 코드를 참조 하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-142">In websites, it's a bad practice to refer in code to absolute paths like *C:\Folder\File.txt* for files on the web server.</span></span> <span data-ttu-id="5197a-143">웹 사이트를 이동 하는 경우 절대 경로가 잘못 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-143">If a website is moved, an absolute path will be wrong.</span></span> <span data-ttu-id="5197a-144">또한 호스트 된 사이트의 경우 (자체 컴퓨터와 반대 됨) 일반적으로 코드를 작성할 때 올바른 경로를 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-144">Moreover, for a hosted site (as opposed to on your own computer) you typically don't even know what the correct path is when you're writing the code.</span></span>

    <span data-ttu-id="5197a-145">그러나 경우에 따라 (예: 파일을 작성 하는 경우) 전체 경로가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-145">But sometimes (like now, for writing a file) you do need a complete path.</span></span> <span data-ttu-id="5197a-146">이 솔루션은 `Server` 개체의 `MapPath` 메서드를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-146">The solution is to use the `MapPath` method of the `Server` object.</span></span> <span data-ttu-id="5197a-147">그러면 웹 사이트의 전체 경로가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-147">This returns the complete path to your website.</span></span> <span data-ttu-id="5197a-148">웹 사이트 루트의 경로를 가져오려면 `~` 연산자 (사이트의 가상 루트를 represen)를 사용 하 여 `MapPath`합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-148">To get the path for the website root, you user the `~` operator (to represen the site's virtual root) to `MapPath`.</span></span> <span data-ttu-id="5197a-149">( *~/App\_Data/* 와 같이 하위 폴더 이름을 전달 하 여 해당 하위 폴더에 대 한 경로를 가져올 수도 있습니다.) 그런 다음 전체 경로를 만들기 위해 메서드가 반환 하는 항목에 대 한 추가 정보를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-149">(You can also pass a subfolder name to it, like *~/App\_Data/*, to get the path for that subfolder.) You can then concatenate additional information onto whatever the method returns in order to create a complete path.</span></span> <span data-ttu-id="5197a-150">이 예제에서는 파일 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-150">In this example, you add a file name.</span></span> <span data-ttu-id="5197a-151">[Razor 구문을 사용 하 여 ASP.NET 웹 페이지 프로그래밍](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)에 대 한 소개에서 파일 및 폴더 경로를 사용 하는 방법에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-151">(You can read more about how to work with file and folder paths in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    <span data-ttu-id="5197a-152">이 파일은 *App\_Data* 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-152">The file is saved in the *App\_Data* folder.</span></span> <span data-ttu-id="5197a-153">이 폴더는 [ASP.NET 웹 페이지 사이트의 데이터베이스 작업 소개](https://go.microsoft.com/fwlink/?LinkId=195209)에 설명 된 대로 데이터 파일을 저장 하는 데 사용 되는 ASP.NET의 특수 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-153">This folder is a special folder in ASP.NET that's used to store data files, as described in [Introduction to Working with a Database in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=195209).</span></span>

    <span data-ttu-id="5197a-154">`File` 개체의 `WriteAllText` 메서드는 파일에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-154">The `WriteAllText` method of the `File` object writes the data to the file.</span></span> <span data-ttu-id="5197a-155">이 메서드는 두 개의 매개 변수, 즉 쓸 파일의 이름 (경로 포함) 및 쓸 실제 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-155">This method takes two parameters: the name (with path) of the file to write to, and the actual data to write.</span></span> <span data-ttu-id="5197a-156">첫 번째 매개 변수의 이름에는 접두사로 `@` 문자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-156">Notice that the name of the first parameter has an `@` character as a prefix.</span></span> <span data-ttu-id="5197a-157">이는 축 자 문자열 리터럴을 제공 한다는 것을 ASP.NET 하 고, "/"와 같은 문자는 특별 한 방식으로 해석 되지 않아야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-157">This tells ASP.NET that you're providing a verbatim string literal, and that characters like "/" should not be interpreted in special ways.</span></span> <span data-ttu-id="5197a-158">자세한 내용은 [Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5197a-158">(For more information, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)</span></span>

    > [!NOTE]
    > <span data-ttu-id="5197a-159">코드에서 응용 프로그램 *\_Data* 폴더에 파일을 저장 하려면 해당 폴더에 대 한 읽기/쓰기 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-159">In order for your code to save files in the *App\_Data* folder, the application needs read-write permissions for that folder.</span></span> <span data-ttu-id="5197a-160">개발 컴퓨터에는 일반적으로 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-160">On your development computer this is not typically an issue.</span></span> <span data-ttu-id="5197a-161">그러나 호스팅 공급자의 웹 서버에 사이트를 게시 하는 경우 해당 권한을 명시적으로 설정 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-161">However, when you publish your site to a hosting provider's web server, you might need to explicitly set those permissions.</span></span> <span data-ttu-id="5197a-162">호스팅 공급자의 서버에서이 코드를 실행 하 고 오류를 수신 하는 경우 호스팅 공급자에 게 문의 하 여 이러한 권한을 설정 하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5197a-162">If you run this code on a hosting provider's server and get errors, check with the hosting provider to find out how to set those permissions.</span></span>

- <span data-ttu-id="5197a-163">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-163">Run the page in a browser.</span></span> 

    ![](working-with-files/_static/image1.jpg)
- <span data-ttu-id="5197a-164">필드에 값을 입력 한 다음 **제출**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-164">Enter values into the fields and then click **Submit**.</span></span>
- <span data-ttu-id="5197a-165">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-165">Close the browser.</span></span>
- <span data-ttu-id="5197a-166">프로젝트로 돌아가서 뷰를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-166">Return to the project and refresh the view.</span></span>
- <span data-ttu-id="5197a-167">*Data .txt* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-167">Open the *data.txt* file.</span></span> <span data-ttu-id="5197a-168">양식에서 제출한 데이터는 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-168">The data you submitted in the form is in the file.</span></span> 

    ![[이미지]](working-with-files/_static/image2.jpg)
- <span data-ttu-id="5197a-170">*Data .txt* 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-170">Close the *data.txt* file.</span></span>

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a><span data-ttu-id="5197a-171">기존 파일에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="5197a-171">Appending Data to an Existing File</span></span>

<span data-ttu-id="5197a-172">이전 예제에서는 `WriteAllText` 사용 하 여 데이터의 한 부분에만 있는 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-172">In the previous example, you used `WriteAllText` to create a text file that's got just one piece of data in it.</span></span> <span data-ttu-id="5197a-173">메서드를 다시 호출 하 고 동일한 파일 이름을 전달 하면 기존 파일을 완전히 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-173">If you call the method again and pass it the same file name, the existing file is completely overwritten.</span></span> <span data-ttu-id="5197a-174">그러나 파일을 만든 후에는 파일의 끝에 새 데이터를 추가 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-174">However, after you've created a file you often want to add new data to the end of the file.</span></span> <span data-ttu-id="5197a-175">`File` 개체의 `AppendAllText` 메서드를 사용 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-175">You can do that using the `AppendAllText` method of the `File` object.</span></span>

1. <span data-ttu-id="5197a-176">웹 사이트에서 *UserData* 파일의 복사본을 만들고 복사본의 이름을 *UserDataMultiple*로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-176">In the website, make a copy of the *UserData.cshtml* file and name the copy *UserDataMultiple.cshtml*.</span></span>
2. <span data-ttu-id="5197a-177">다음 코드 블록을 사용 하 여 여는 `<!DOCTYPE html>` 태그 앞에 코드 블록을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-177">Replace the code block before the opening `<!DOCTYPE html>` tag with the following code block:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    <span data-ttu-id="5197a-178">이 코드에는 이전 예제에서 변경 된 내용이 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-178">This code has one change in it from the previous example.</span></span> <span data-ttu-id="5197a-179">`WriteAllText`를 사용 하는 대신 `the AppendAllText` 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-179">Instead of using `WriteAllText`, it uses `the AppendAllText` method.</span></span> <span data-ttu-id="5197a-180">`AppendAllText`는 파일의 끝에 데이터를 추가 하는 것을 제외 하 고 메서드는 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-180">The methods are similar, except that `AppendAllText` adds the data to the end of the file.</span></span> <span data-ttu-id="5197a-181">`WriteAllText`와 마찬가지로 `AppendAllText` 파일이 없는 경우 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-181">As with `WriteAllText`, `AppendAllText` creates the file if it doesn't already exist.</span></span>
3. <span data-ttu-id="5197a-182">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-182">Run the page in a browser.</span></span>
4. <span data-ttu-id="5197a-183">필드에 대 한 값을 입력 한 다음 **제출**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-183">Enter values for the fields and then click **Submit**.</span></span>
5. <span data-ttu-id="5197a-184">데이터를 더 추가 하 고 양식을 다시 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-184">Add more data and submit the form again.</span></span>
6. <span data-ttu-id="5197a-185">프로젝트로 돌아가서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새로 고침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-185">Return to your project, right-click the project folder, and then click **Refresh**.</span></span>
7. <span data-ttu-id="5197a-186">*Data .txt* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-186">Open the *data.txt* file.</span></span> <span data-ttu-id="5197a-187">이제 방금 입력 한 새 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-187">It now contains the new data that you just entered.</span></span> 

    ![[이미지]](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a><span data-ttu-id="5197a-189">파일에서 데이터 읽기 및 표시</span><span class="sxs-lookup"><span data-stu-id="5197a-189">Reading and Displaying Data from a File</span></span>

<span data-ttu-id="5197a-190">텍스트 파일에 데이터를 쓸 필요가 없는 경우에도 데이터를 한 곳에서 읽어야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-190">Even if you don't need to write data to a text file, you'll probably sometimes need to read data from one.</span></span> <span data-ttu-id="5197a-191">이렇게 하려면 `File` 개체를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-191">To do this, you can again use the `File` object.</span></span> <span data-ttu-id="5197a-192">`File` 개체를 사용 하 여 각 줄을 개별적으로 읽거나 (줄 바꿈으로 구분) 개별 항목을 구분 하는 방법에 관계 없이 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-192">You can use the `File` object to read each line individually (separated by line breaks) or to read individual item no matter how they're separated.</span></span>

<span data-ttu-id="5197a-193">이 절차에서는 이전 예제에서 만든 데이터를 읽고 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-193">This procedure shows you how to read and display the data that you created in the previous example.</span></span>

1. <span data-ttu-id="5197a-194">웹 사이트의 루트에서 *Displaydata. cshtml*라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-194">At the root of your website, create a new file named *DisplayData.cshtml*.</span></span>
2. <span data-ttu-id="5197a-195">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-195">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    <span data-ttu-id="5197a-196">이 메서드 호출을 사용 하 여 앞의 예제에서 만든 파일을 `userData`라는 변수로 읽어 먼저 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-196">The code starts by reading the file that you created in the previous example into a variable named `userData`, using this method call:</span></span>

    [!code-css[Main](working-with-files/samples/sample5.css)]

    <span data-ttu-id="5197a-197">이 작업을 수행 하는 코드는 `if` 문 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-197">The code to do this is inside an `if` statement.</span></span> <span data-ttu-id="5197a-198">파일을 읽으려면 먼저 `File.Exists` 메서드를 사용 하 여 파일을 사용할 수 있는지 여부를 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-198">When you want to read a file, it's a good idea to use the `File.Exists` method to determine first whether the file is available.</span></span> <span data-ttu-id="5197a-199">또한이 코드는 파일이 비어 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-199">The code also checks whether the file is empty.</span></span>

    <span data-ttu-id="5197a-200">페이지 본문에는 서로 중첩 된 두 개의 `foreach` 루프가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-200">The body of the page contains two `foreach` loops, one nested inside the other.</span></span> <span data-ttu-id="5197a-201">외부 `foreach` 루프는 데이터 파일에서 한 번에 한 줄을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-201">The outer `foreach` loop gets one line at a time from the data file.</span></span> <span data-ttu-id="5197a-202">이 경우 줄은 파일 &#8212; 의 줄 바꿈으로 정의 됩니다. 즉, 각 데이터 항목은 별도의 줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-202">In this case, the lines are defined by line breaks in the file &#8212; that is, each data item is on its own line.</span></span> <span data-ttu-id="5197a-203">외부 루프는 정렬 된 목록 (`<ol>` 요소) 안에 새 항목 (`<li>` 요소)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-203">The outer loop creates a new item (`<li>` element) inside an ordered list (`<ol>` element).</span></span>

    <span data-ttu-id="5197a-204">내부 루프는 쉼표를 구분 기호로 사용 하 여 각 데이터 줄을 항목 (필드)으로 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-204">The inner loop splits each data line into items (fields) using a comma as a delimiter.</span></span> <span data-ttu-id="5197a-205">이전 예제를 기반으로 하 여 각 줄에는 이름, 성 및 &#8212; 전자 메일 주소 라는 세 개의 필드가 쉼표로 구분 되어 포함 되어 있음을 의미 합니다. 또한 내부 루프는 `<ul>` 목록을 만들고 데이터 줄의 각 필드에 대해 하나의 목록 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-205">(Based on the previous example, this means that each line contains three fields &#8212; the first name, last name, and email address, each separated by a comma.) The inner loop also creates a `<ul>` list and displays one list item for each field in the data line.</span></span>

    <span data-ttu-id="5197a-206">이 코드에서는 두 가지 데이터 형식, 배열 및 `char` 데이터 형식을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-206">The code illustrates how to use two data types, an array and the `char` data type.</span></span> <span data-ttu-id="5197a-207">배열은 `File.ReadAllLines` 메서드가 데이터를 배열로 반환 하기 때문에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-207">The array is required because the `File.ReadAllLines` method returns data as an array.</span></span> <span data-ttu-id="5197a-208">`char` 데이터 형식은 `Split` 메서드가 각 요소가 `char`형식인 `array`을 반환 하기 때문에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-208">The `char` data type is required because the `Split` method returns an `array` in which each element is of the type `char`.</span></span> <span data-ttu-id="5197a-209">배열에 대 한 자세한 내용은 [Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5197a-209">(For information about arrays, see [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)</span></span>
3. <span data-ttu-id="5197a-210">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-210">Run the page in a browser.</span></span> <span data-ttu-id="5197a-211">이전 예제에서 입력 한 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-211">The data you entered for the previous examples is displayed.</span></span> 

    ![[이미지]](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="5197a-213">**Microsoft Excel 쉼표로 분리 된 파일의 데이터 표시**</span><span class="sxs-lookup"><span data-stu-id="5197a-213">**Displaying Data from a Microsoft Excel Comma-Delimited File**</span></span>
> 
> <span data-ttu-id="5197a-214">Microsoft Excel을 사용 하 여 스프레드시트에 포함 된 데이터를 쉼표로 구분 된 파일 ( *.csv* 파일)로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-214">You can use Microsoft Excel to save the data contained in a spreadsheet as a comma-delimited file (*.csv* file).</span></span> <span data-ttu-id="5197a-215">이렇게 하면 파일이 Excel 형식이 아닌 일반 텍스트로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-215">When you do, the file is saved in plain text, not in Excel format.</span></span> <span data-ttu-id="5197a-216">스프레드시트의 각 행은 텍스트 파일에서 줄 바꿈으로 구분 되며, 각 데이터 항목은 쉼표로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-216">Each row in the spreadsheet is separated by a line break in the text file, and each data item is separated by a comma.</span></span> <span data-ttu-id="5197a-217">이전 예제에 표시 된 코드를 사용 하 여 코드에서 데이터 파일의 이름을 변경 하는 것 만으로 Excel 쉼표로 분리 된 파일을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-217">You can use the code shown in the previous example to read an Excel comma-delimited file just by changing the name of the data file in your code.</span></span>

<a id="Deleting_Files"></a>
## <a name="deleting-files"></a><span data-ttu-id="5197a-218">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="5197a-218">Deleting Files</span></span>

<span data-ttu-id="5197a-219">웹 사이트에서 파일을 삭제 하려면 `File.Delete` 방법을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-219">To delete files from your website, you can use the `File.Delete` method.</span></span> <span data-ttu-id="5197a-220">이 절차에서는 사용자가 파일 이름을 알고 있는 경우 *이미지 폴더에서 이미지 (* *.jpg* 파일)를 삭제할 수 있도록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-220">This procedure shows how to let users delete an image (*.jpg* file) from an *images* folder if they know the name of the file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5197a-221">**중요** 프로덕션 웹 사이트에서는 일반적으로 데이터를 변경할 수 있는 사용자를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-221">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="5197a-222">멤버 자격을 설정 하는 방법과 사용자에 게 사이트에서 작업을 수행할 수 있는 권한을 부여 하는 방법에 대 한 자세한 내용은 [ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격 추가](https://go.microsoft.com/fwlink/?LinkId=202904)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5197a-222">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="5197a-223">웹 사이트에서 이름이 *images*인 하위 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-223">In the website, create a subfolder named *images*.</span></span>
2. <span data-ttu-id="5197a-224">하나 이상의 *.jpg* 파일을 *images* 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-224">Copy one or more *.jpg* files into the *images* folder.</span></span>
3. <span data-ttu-id="5197a-225">웹 사이트의 루트에서 *Filedelete. cshtml*라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-225">In the root of the website, create a new file named *FileDelete.cshtml*.</span></span>
4. <span data-ttu-id="5197a-226">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-226">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    <span data-ttu-id="5197a-227">이 페이지에는 사용자가 이미지 파일의 이름을 입력할 수 있는 양식이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-227">This page contains a form where users can enter the name of an image file.</span></span> <span data-ttu-id="5197a-228">.Jpg 파일 이름 확장명을 입력 하지 않습니다 *.* 이와 같이 파일 이름을 제한 하면 사용자가 사이트에서 임의의 파일을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-228">They don't enter the *.jpg* file-name extension; by restricting the file name like this, you help prevents users from deleting arbitrary files on your site.</span></span>

    <span data-ttu-id="5197a-229">이 코드는 사용자가 입력 한 파일 이름을 읽은 다음 전체 경로를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-229">The code reads the file name that the user has entered and then constructs a complete path.</span></span> <span data-ttu-id="5197a-230">경로를 만들기 위해 코드는 현재 웹 사이트 경로 (`Server.MapPath` 메서드에서 반환), *이미지* 폴더 이름, 사용자가 제공한 이름 및 ".jpg"를 리터럴 문자열로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-230">To create the path, the code uses the current website path (as returned by the `Server.MapPath` method), the *images* folder name, the name that the user has provided, and ".jpg" as a literal string.</span></span>

    <span data-ttu-id="5197a-231">이 파일을 삭제 하기 위해 코드는 `File.Delete` 메서드를 호출 하 여 방금 만든 전체 경로를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-231">To delete the file, the code calls the `File.Delete` method, passing it the full path that you just constructed.</span></span> <span data-ttu-id="5197a-232">태그의 끝에서 코드는 파일이 삭제 되었다는 확인 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-232">At the end of the markup, code displays a confirmation message that the file was deleted.</span></span>
5. <span data-ttu-id="5197a-233">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-233">Run the page in a browser.</span></span> 

    ![[이미지]](working-with-files/_static/image5.jpg)
6. <span data-ttu-id="5197a-235">삭제할 파일의 이름을 입력 한 다음 **제출**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-235">Enter the name of the file to delete and then click **Submit**.</span></span> <span data-ttu-id="5197a-236">파일이 삭제 된 경우 페이지의 맨 아래에 파일 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-236">If the file was deleted, the name of the file is displayed at the bottom of the page.</span></span>

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a><span data-ttu-id="5197a-237">사용자가 파일 업로드 허용</span><span class="sxs-lookup"><span data-stu-id="5197a-237">Letting Users Upload a File</span></span>

<span data-ttu-id="5197a-238">사용자는 `FileUpload` 도우미를 사용 하 여 웹 사이트에 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-238">The `FileUpload` helper lets users upload files to your website.</span></span> <span data-ttu-id="5197a-239">다음 절차에서는 사용자가 단일 파일을 업로드할 수 있도록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-239">The procedure below shows you how to let users upload a single file.</span></span>

1. <span data-ttu-id="5197a-240">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)의 설명에 따라 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가 합니다 (이전에 추가 하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="5197a-240">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you didn't add it previously.</span></span>
2. <span data-ttu-id="5197a-241">*App\_Data* 폴더에서 새 폴더를 만들고 이름을 *UploadedFiles*로 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-241">In the *App\_Data* folder, create a new a folder and name it *UploadedFiles*.</span></span>
3. <span data-ttu-id="5197a-242">루트에서 *FileUpload*라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-242">In the root, create a new file named *FileUpload.cshtml*.</span></span>
4. <span data-ttu-id="5197a-243">페이지의 기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-243">Replace the existing content in the page with the following:</span></span> 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    <span data-ttu-id="5197a-244">페이지의 본문 부분은 `FileUpload` 도우미를 사용 하 여 친숙 한 업로드 상자와 단추를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-244">The body portion of the page uses the `FileUpload` helper to create the upload box and buttons that you're probably familiar with:</span></span>

    ![[이미지]](working-with-files/_static/image6.jpg)

    <span data-ttu-id="5197a-246">`FileUpload` 도우미에 대해 설정한 속성은 파일에 대 한 단일 상자를 선택 하 고 제출 단추를 클릭 하 여 **업로드**를 읽도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-246">The properties that you set for the `FileUpload` helper specify that you want a single box for the file to upload and that you want the submit button to read **Upload**.</span></span> <span data-ttu-id="5197a-247">(이 문서의 뒷부분에서 더 많은 상자를 추가 합니다.)</span><span class="sxs-lookup"><span data-stu-id="5197a-247">(You'll add more boxes later in the article.)</span></span>

    <span data-ttu-id="5197a-248">사용자가 **업로드**를 클릭 하면 페이지 맨 위에 있는 코드에서 파일을 가져와 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-248">When the user clicks **Upload**, the code at the top of the page gets the file and saves it.</span></span> <span data-ttu-id="5197a-249">양식 필드에서 값을 가져오는 데 일반적으로 사용 하는 `Request` 개체에는 업로드 된 파일 (또는 파일)을 포함 하는 `Files` 배열도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-249">The `Request` object that you normally use to get values from form fields also has a `Files` array that contains the file (or files) that have been uploaded.</span></span> <span data-ttu-id="5197a-250">배열의 &#8212; 특정 위치에서 개별 파일을 가져올 수 있습니다. 예를 들어 첫 번째 업로드 된 파일을 가져오기 위해 `Request.Files[0]`를 가져오고 두 번째 파일을 가져오고 `Request.Files[1]`를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-250">You can get individual files out of specific positions in the array &#8212; for example, to get the first uploaded file, you get `Request.Files[0]`, to get the second file, you get `Request.Files[1]`, and so on.</span></span> <span data-ttu-id="5197a-251">프로그래밍에서 계산은 일반적으로 0부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-251">(Remember that in programming, counting usually starts at zero.)</span></span>

    <span data-ttu-id="5197a-252">업로드 된 파일을 페치할 때 해당 파일을 조작할 수 있도록 변수에 저장 합니다 (여기 `uploadedFile`).</span><span class="sxs-lookup"><span data-stu-id="5197a-252">When you fetch an uploaded file, you put it in a variable (here, `uploadedFile`) so that you can manipulate it.</span></span> <span data-ttu-id="5197a-253">업로드 된 파일의 이름을 확인 하려면 해당 `FileName` 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-253">To determine the name of the uploaded file, you just get its `FileName` property.</span></span> <span data-ttu-id="5197a-254">그러나 사용자가 파일을 업로드 하면 전체 경로를 포함 하는 사용자의 원래 이름이 `FileName`에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-254">However, when the user uploads a file, `FileName` contains the user's original name, which includes the entire path.</span></span> <span data-ttu-id="5197a-255">다음과 같이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-255">It might look like this:</span></span>

    <span data-ttu-id="5197a-256">*C:\Users\Public\Sample.txt*</span><span class="sxs-lookup"><span data-stu-id="5197a-256">*C:\Users\Public\Sample.txt*</span></span>

    <span data-ttu-id="5197a-257">그러나 서버에 대 한 것이 아니라 사용자 컴퓨터의 경로 이기 때문에 모든 경로 정보를 원하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-257">You don't want all that path information, though, because that's the path on the user's computer, not for your server.</span></span> <span data-ttu-id="5197a-258">실제 파일 이름 (*샘플 .txt*)만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-258">You just want the actual file name (*Sample.txt*).</span></span> <span data-ttu-id="5197a-259">다음과 같이 `Path.GetFileName` 메서드를 사용 하 여 경로에서 파일만 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-259">You can strip out just the file from a path by using the `Path.GetFileName` method, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    <span data-ttu-id="5197a-260">`Path` 개체는 경로를 제거 하 고 경로를 결합 하는 데 사용할 수 있는 다음과 같은 여러 메서드가 있는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-260">The `Path` object is a utility that has a number of methods like this that you can use to strip paths, combine paths, and so on.</span></span>

    <span data-ttu-id="5197a-261">업로드 된 파일의 이름을 지정한 후에는 업로드 된 파일을 웹 사이트에 저장 하려는 새 경로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-261">Once you've gotten the name of the uploaded file, you can build a new path for where you want to store the uploaded file in your website.</span></span> <span data-ttu-id="5197a-262">이 경우 `Server.MapPath`, 폴더 이름 (*앱\_데이터/UploadedFiles*) 및 새로 제거 된 파일 이름을 결합 하 여 새 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-262">In this case, you combine `Server.MapPath`, the folder names (*App\_Data/UploadedFiles*), and the newly stripped file name to create a new path.</span></span> <span data-ttu-id="5197a-263">그런 다음 업로드 된 파일의 `SaveAs` 메서드를 호출 하 여 실제로 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-263">You can then call the uploaded file's `SaveAs` method to actually save the file.</span></span>
5. <span data-ttu-id="5197a-264">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-264">Run the page in a browser.</span></span> 

    ![[이미지]](working-with-files/_static/image7.jpg)
6. <span data-ttu-id="5197a-266">**찾아보기** 를 클릭 한 다음 업로드할 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-266">Click **Browse** and then select a file to upload.</span></span> 

    ![[이미지]](working-with-files/_static/image8.jpg)

    <span data-ttu-id="5197a-268">**찾아보기** 단추 옆의 텍스트 상자에는 경로와 파일 위치가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-268">The text box next to the **Browse** button will contain the path and file location.</span></span>

    ![[이미지]](working-with-files/_static/image9.jpg)
7. <span data-ttu-id="5197a-270">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-270">Click **Upload**.</span></span>
8. <span data-ttu-id="5197a-271">웹 사이트에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새로 고침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-271">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="5197a-272">*UploadedFiles* 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-272">Open the *UploadedFiles* folder.</span></span> <span data-ttu-id="5197a-273">업로드 한 파일은 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-273">The file that you uploaded is in the folder.</span></span> 

    ![[이미지]](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a><span data-ttu-id="5197a-275">사용자가 여러 파일 업로드 허용</span><span class="sxs-lookup"><span data-stu-id="5197a-275">Letting Users Upload Multiple Files</span></span>

<span data-ttu-id="5197a-276">이전 예제에서는 사용자가 파일 하나를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-276">In the previous example, you let users upload one file.</span></span> <span data-ttu-id="5197a-277">하지만 `FileUpload` 도우미를 사용 하 여 한 번에 두 개 이상의 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-277">But you can use the `FileUpload` helper to upload more than one file at a time.</span></span> <span data-ttu-id="5197a-278">이는 한 번에 한 파일을 업로드 하는 것이 지루한 사진 업로드와 같은 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-278">This is handy for scenarios like uploading photos, where uploading one file at a time is tedious.</span></span> <span data-ttu-id="5197a-279">[ASP.NET 웹 페이지 사이트에서 이미지를 사용 하 여 작업 하는](https://go.microsoft.com/fwlink/?LinkId=202897)사진을 업로드 하는 방법에 대해 알아볼 수 있습니다. 이 예제에서는 동일한 기술을 사용 하 여 둘 이상의를 업로드할 수 있지만 사용자가 한 번에 2를 업로드할 수 있게 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-279">(You can read about uploading photos in [Working with Images in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202897).) This example shows how to let users upload two at a time, although you can use the same technique to upload more than that.</span></span>

1. <span data-ttu-id="5197a-280">[ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="5197a-280">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="5197a-281">*FileUploadMultiple*라는 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-281">Create a new page named *FileUploadMultiple.cshtml*.</span></span>
3. <span data-ttu-id="5197a-282">페이지의 기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-282">Replace the existing content in the page with the following:</span></span>  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    <span data-ttu-id="5197a-283">이 예제에서는 사용자가 기본적으로 두 파일을 업로드할 수 있도록 페이지 본문의 `FileUpload` 도우미가 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-283">In this example, the `FileUpload` helper in the body of the page is configured to let users upload two files by default.</span></span> <span data-ttu-id="5197a-284">`allowMoreFilesToBeAdded`이 `true`으로 설정 되어 있으므로 도우미가 사용자가 더 많은 업로드 상자를 추가할 수 있는 링크를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-284">Because `allowMoreFilesToBeAdded` is set to `true`, the helper renders a link that lets user add more upload boxes:</span></span>

    ![[이미지]](working-with-files/_static/image11.jpg)

    <span data-ttu-id="5197a-286">사용자가 업로드 하는 파일을 처리 하기 위해 코드는 이전 예제 &#8212; 에서 사용한 것과 동일한 기본 기술을 사용 하 여 `Request.Files` 파일을 가져온 다음 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-286">To process the files that the user uploads, the code uses the same basic technique that you used in the previous example &#8212; get a file from `Request.Files` and then save it.</span></span> <span data-ttu-id="5197a-287">(올바른 파일 이름 및 경로를 가져오기 위해 수행 해야 하는 다양 한 작업 포함) 이 시간을 혁신 하는 것은 사용자가 여러 파일을 업로드할 수 있고 많은 것을 알 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-287">(Including the various things you need to do to get the right file name and path.) The innovation this time is that the user might be uploading multiple files and you don't know many.</span></span> <span data-ttu-id="5197a-288">`Request.Files.Count`를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-288">To find out, you can get `Request.Files.Count`.</span></span>

    <span data-ttu-id="5197a-289">이 번호를 사용 하면 `Request.Files`를 반복 하 고 각 파일을 차례로 가져와 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-289">With this number in hand, you can loop through `Request.Files`, fetch each file in turn, and save it.</span></span> <span data-ttu-id="5197a-290">컬렉션을 통해 알려진 횟수를 반복 하려는 경우 다음과 같이 `for` 루프를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-290">When you want to loop a known number of times through a collection, you can use a `for` loop, like this:</span></span>

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    <span data-ttu-id="5197a-291">`i` 변수는 0에서 설정 하는 상한에 해당 하는 임시 카운터 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-291">The variable `i` is just a temporary counter that will go from zero to whatever upper limit you set.</span></span> <span data-ttu-id="5197a-292">이 경우 상한 값은 파일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-292">In this case, the upper limit is the number of files.</span></span> <span data-ttu-id="5197a-293">하지만 카운터는 ASP.NET에서 계산 시나리오에 일반적으로 발생 하는 것 처럼 0에서 시작 되므로 상한 값은 실제로 파일 수보다 하나 미만입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-293">But because the counter starts at zero, as is typical for counting scenarios in ASP.NET, the upper limit is actually one less than the file count.</span></span> <span data-ttu-id="5197a-294">3 개의 파일을 업로드 하는 경우 수는 0에서 2 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-294">(If three files are uploaded, the count is zero to 2.)</span></span>

    <span data-ttu-id="5197a-295">`uploadedCount` 변수는 성공적으로 업로드 되 고 저장 된 모든 파일의 합계를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-295">The `uploadedCount` variable totals all the files that are successfully uploaded and saved.</span></span> <span data-ttu-id="5197a-296">이 코드는 예상 되는 파일을 업로드 하지 못할 수 있는 가능성을 계정으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-296">This code accounts for the possibility that an expected file may not be able to be uploaded.</span></span>
4. <span data-ttu-id="5197a-297">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-297">Run the page in a browser.</span></span> <span data-ttu-id="5197a-298">브라우저에 페이지와 두 개의 업로드 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-298">The browser displays the page and its two upload boxes.</span></span>
5. <span data-ttu-id="5197a-299">업로드할 파일 두 개를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-299">Select two files to upload.</span></span>
6. <span data-ttu-id="5197a-300">**다른 파일 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-300">Click **Add another file**.</span></span> <span data-ttu-id="5197a-301">이 페이지에는 새 업로드 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-301">The page displays a new upload box.</span></span> 

    ![[이미지]](working-with-files/_static/image12.jpg)
7. <span data-ttu-id="5197a-303">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-303">Click **Upload**.</span></span>
8. <span data-ttu-id="5197a-304">웹 사이트에서 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새로 고침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-304">In the website, right-click the project folder and then click **Refresh**.</span></span>
9. <span data-ttu-id="5197a-305">*UploadedFiles* 폴더를 열어서 성공적으로 업로드 된 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5197a-305">Open the *UploadedFiles* folder to see the successfully uploaded files.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="5197a-306">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5197a-306">Additional Resources</span></span>

[<span data-ttu-id="5197a-307">ASP.NET 웹 페이지 사이트에서 이미지 작업</span><span class="sxs-lookup"><span data-stu-id="5197a-307">Working with Images in an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkId=202897)

[<span data-ttu-id="5197a-308">CSV 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="5197a-308">Exporting to a CSV File</span></span>](https://msdn.microsoft.com/library/ms155919.aspx)
