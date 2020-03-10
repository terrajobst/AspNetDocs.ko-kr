---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Razor 및 비-JavaScript를 사용 하 여 MVC 3 응용 프로그램 만들기 | Microsoft Docs
author: microsoft
description: 사용자 목록 샘플 웹 응용 프로그램은 Razor 뷰 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 간단한 방법을 보여 줍니다. 응용 프로그램 샘플 ...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434999"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="e8491-104">Razor 및 비간섭 JavaScript를 사용해 MVC 3 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e8491-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="e8491-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="e8491-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e8491-106">사용자 목록 샘플 웹 응용 프로그램은 Razor 뷰 엔진을 사용 하 여 ASP.NET MVC 3 응용 프로그램을 만드는 간단한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="e8491-107">샘플 응용 프로그램은 ASP.NET MVC 버전 3 및 Visual Studio 2010에서 새 Razor 뷰 엔진을 사용 하 여 사용자 만들기, 표시, 편집 및 삭제와 같은 기능을 포함 하는 가상의 사용자 목록 웹 사이트를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="e8491-108">이 자습서에서는 사용자 목록 샘플 ASP.NET MVC 3 응용 프로그램을 빌드하기 위해 수행 된 단계에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="e8491-109">및 VB 소스 코드를 C# 포함 하는 Visual Studio 프로젝트를 다운로드 하 여 [다운로드할](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="e8491-110">이 자습서에 대 한 질문이 있는 경우 [MVC 포럼](https://forums.asp.net/1146.aspx)에 게시 해 주세요.</span><span class="sxs-lookup"><span data-stu-id="e8491-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="e8491-111">개요</span><span class="sxs-lookup"><span data-stu-id="e8491-111">Overview</span></span>

<span data-ttu-id="e8491-112">빌드할 응용 프로그램은 간단한 사용자 목록 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="e8491-113">사용자는 사용자 정보를 입력 하 고, 확인 하 고, 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-113">Users can enter, view, and update user information.</span></span>

![샘플 사이트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="e8491-115">C# [여기](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)에서 VB 및 완료 된 프로젝트를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="e8491-116">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e8491-116">Creating the Web Application</span></span>

<span data-ttu-id="e8491-117">자습서를 시작 하려면 Visual Studio 2010을 열고 *ASP.NET MVC 3 웹 응용 프로그램* 템플릿을 사용 하 여 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="e8491-118">응용 프로그램의 이름을 Mvc3Razor&quot;로 &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="e8491-119">[새 MVC 3 프로젝트 ![](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="e8491-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="e8491-120">**새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**을 선택 하 고 Razor 뷰 엔진을 선택한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![새 ASP.NET MVC 3 프로젝트 대화 상자](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="e8491-122">이 자습서에서는 ASP.NET 멤버 자격 공급자를 사용 하지 않으므로 로그온 및 멤버 자격과 관련 된 모든 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="e8491-123">**솔루션 탐색기**에서 다음 파일 및 디렉터리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="e8491-124">*Controllers\AccountController*</span><span class="sxs-lookup"><span data-stu-id="e8491-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="e8491-125">*Models\AccountModels*</span><span class="sxs-lookup"><span data-stu-id="e8491-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="e8491-126">*Views\Shared\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="e8491-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="e8491-127">*Views\Account* (및이 디렉터리의 모든 파일)</span><span class="sxs-lookup"><span data-stu-id="e8491-127">*Views\Account* (and all the files in this directory)</span></span>

![고 개 Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="e8491-129"><em>\_Layout</em> 파일을 편집 하 고 `logindisplay` 이라는 `<div>` 요소 내부의 태그를 로그인 사용 안 함&quot;<em>&quot;</em>메시지로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="e8491-130">다음 예제에서는 새 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="e8491-131">모델 추가</span><span class="sxs-lookup"><span data-stu-id="e8491-131">Adding the Model</span></span>

<span data-ttu-id="e8491-132">**솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **클래스**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![새 사용자 Mdl 클래스](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="e8491-134">클래스 `UserModel` 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-134">Name the class `UserModel`.</span></span> <span data-ttu-id="e8491-135">*Usermodel* 파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="e8491-136">`UserModel` 클래스는 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="e8491-137">클래스의 각 멤버에는 [dataannotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스의 [필수](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 특성으로 주석이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="e8491-138">[Dataannotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스의 특성은 웹 응용 프로그램에 대 한 자동 클라이언트 및 서버 쪽 유효성 검사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="e8491-139">`HomeController` 클래스를 열고 `UserModel` 및 `Users` 클래스에 액세스할 수 있도록 `using` 지시문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="e8491-140">`HomeController` 선언 바로 뒤에 다음 주석과 `Users` 클래스에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="e8491-141">`Users` 클래스는이 자습서에서 사용할 수 있는 간소화 된 메모리 내 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="e8491-142">실제 응용 프로그램에서는 데이터베이스를 사용 하 여 사용자 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="e8491-143">다음 예제에서는 `HomeController` 파일의 처음 몇 줄을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="e8491-144">사용자 모델을 다음 단계에서 스 캐 폴딩 마법사에서 사용할 수 있도록 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="e8491-145">기본 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="e8491-145">Creating the Default View</span></span>

<span data-ttu-id="e8491-146">다음 단계는 사용자를 표시 하는 작업 메서드와 뷰를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="e8491-147">기존 *Views\Home\Index* 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="e8491-148">사용자를 표시 하는 새 *인덱스* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="e8491-149">`HomeController` 클래스에서 `Index` 메서드의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="e8491-150">`Index` 메서드 내부를 마우스 오른쪽 단추로 클릭 한 다음 **뷰 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="e8491-152">**강력한 형식의 뷰 만들기** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="e8491-153">**뷰 데이터 클래스**에 대해 **Mvc3Razor**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="e8491-154">( **데이터 클래스 보기** 상자에 **Mvc3Razor** 가 표시 되지 않으면 프로젝트를 빌드해야 합니다.) 뷰 엔진이 **Razor**로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="e8491-155">**콘텐츠 보기** 를 **목록** 으로 설정 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-155">Set **View content** to **List** and then click **Add**.</span></span>

![인덱스 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="e8491-157">새 뷰는 `Index` 뷰에 전달 되는 사용자 데이터를 자동으로 스 캐 폴드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="e8491-158">새로 생성 된 *Views\Home\Index* 파일을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="e8491-159">**새로 만들기**, **편집**, **세부 정보**및 **삭제** 링크가 작동 하지 않지만 페이지의 나머지 부분은 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="e8491-160">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-160">Run the page.</span></span> <span data-ttu-id="e8491-161">사용자 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-161">You see a list of users.</span></span>

![인덱스 페이지](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="e8491-163">다음 코드를 사용 하 여 *인덱스 cshtml* 파일을 열고 **편집**, **세부 정보**및 **삭제** 에 대 한 `ActionLink` 태그를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="e8491-164">사용자 이름은 **편집**, **세부 정보**및 **삭제** 링크에서 선택한 레코드를 찾는 ID로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="e8491-165">세부 정보 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="e8491-165">Creating the Details View</span></span>

<span data-ttu-id="e8491-166">다음 단계는 사용자 세부 정보를 표시 하기 위해 `Details` 작업 메서드 및 보기를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![세부 정보](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="e8491-168">다음 `Details` 메서드를 홈 컨트롤러에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="e8491-169">`Details` 메서드 내부를 마우스 오른쪽 단추로 클릭 한 다음 <strong>뷰 추가</strong>를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="e8491-170"><strong>데이터 클래스 보기</strong> 상자에 <strong>Mvc3Razor 모델이</strong>포함 되어 있는지<em>확인 합니다.</em></span><span class="sxs-lookup"><span data-stu-id="e8491-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="e8491-171"><strong>콘텐츠 보기</strong> 를 <strong>자세히</strong> 로 설정 하 고 <strong>추가</strong>를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![세부 정보 보기 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="e8491-173">응용 프로그램을 실행 하 고 세부 정보 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-173">Run the application and select a details link.</span></span> <span data-ttu-id="e8491-174">자동 스 캐 폴딩은 모델의 각 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-174">The automatic scaffolding shows each property in the model.</span></span>

![세부 정보](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="e8491-176">편집 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="e8491-176">Creating the Edit View</span></span>

<span data-ttu-id="e8491-177">다음 `Edit` 메서드를 home 컨트롤러에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="e8491-178">이전 단계에서와 같이 뷰를 추가 하지만 **뷰 콘텐츠** 를 **편집**으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![편집 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="e8491-180">응용 프로그램을 실행 하 고 사용자 중 하나의 성과 이름을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="e8491-181">`UserModel` 클래스에 적용 된 `DataAnnotation` 제약 조건을 위반 하는 경우 폼을 제출할 때 서버 코드에서 생성 된 유효성 검사 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="e8491-182">예를 들어 Ann&quot; &quot;이름을 변경 하 여&quot;을 &quot;경우 양식을 제출할 때 다음 오류가 폼에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="e8491-183">이 자습서에서는 사용자 이름을 기본 키로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="e8491-184">따라서 사용자 이름 속성은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="e8491-185">*편집. cshtml* 파일에서 `Html.BeginForm` 문 바로 뒤에 사용자 이름을 숨겨진 필드로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="e8491-186">이렇게 하면 속성이 모델에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="e8491-187">다음 코드 조각에서는 `Hidden` 문을 배치 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="e8491-188">사용자 이름에 대 한 `TextBoxFor` 및 `ValidationMessageFor` 태그를 `DisplayFor` 호출로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="e8491-189">`DisplayFor` 메서드는 속성을 읽기 전용 요소로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="e8491-190">다음 예제에서는 전체 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-190">The following example shows the completed markup.</span></span> <span data-ttu-id="e8491-191">원래 `TextBoxFor` 및 `ValidationMessageFor` 호출은 Razor 시작-주석 및 끝 주석 문자 (`@* *@`)로 주석 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="e8491-192">클라이언트 쪽 유효성 검사 사용</span><span class="sxs-lookup"><span data-stu-id="e8491-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="e8491-193">ASP.NET MVC 3에서 클라이언트 쪽 유효성 검사를 사용 하도록 설정 하려면 두 개의 플래그를 설정 하 고 세 개의 JavaScript 파일을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="e8491-194">응용 프로그램의 *web.config* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="e8491-195">응용 프로그램 설정에서 `that ClientValidationEnabled` 및 `UnobtrusiveJavaScriptEnabled`이 true로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="e8491-196">루트 web.config 파일의 다음 조각은 올바른 설정을 보여 *줍니다.*</span><span class="sxs-lookup"><span data-stu-id="e8491-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="e8491-197">`UnobtrusiveJavaScriptEnabled`를 true로 설정 하면 Ajax와 클라이언트의 유효성을 검사 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="e8491-198">비 표시 유효성 검사를 사용 하는 경우 유효성 검사 규칙이 HTML5 특성으로 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="e8491-199">HTML5 특성 이름은 소문자, 숫자 및 대시로만 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="e8491-200">`ClientValidationEnabled`를 true로 설정 하면 클라이언트 쪽 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="e8491-201">응용 프로그램 *web.config* 파일에서 이러한 키를 설정 하 여 전체 응용 프로그램에 대 한 클라이언트 유효성 검사 및 비 표시 JavaScript를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="e8491-202">다음 코드를 사용 하 여 개별 뷰나 컨트롤러 메서드에서 이러한 설정을 사용 하거나 사용 하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="e8491-203">또한 렌더링 된 뷰에 여러 JavaScript 파일을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="e8491-204">모든 뷰에 JavaScript를 포함 하는 쉬운 방법은 *Views\Shared\\_Layout* 파일에 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="e8491-205">*\_Layout. cshtml* 파일의 `<head>` 요소를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="e8491-206">처음 두 jQuery 스크립트는 Microsoft Ajax Content Delivery Network (CDN)에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="e8491-207">Microsoft Ajax CDN을 활용 하 여 응용 프로그램의 첫 번째 적중 성능을 크게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="e8491-208">응용 프로그램을 실행 하 고 편집 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-208">Run the application and click an edit link.</span></span> <span data-ttu-id="e8491-209">브라우저에서 페이지의 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-209">View the page's source in the browser.</span></span> <span data-ttu-id="e8491-210">브라우저 소스는 데이터 유효성 검사를 위해 `data-val` 폼의 많은 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="e8491-211">클라이언트 유효성 검사 및 문제가 없는 JavaScript를 사용 하는 경우 클라이언트 유효성 검사 규칙을 사용 하는 입력 필드에 `data-val="true"` 특성이 포함 되어 문제가 없는 클라이언트 유효성 검사를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="e8491-212">예를 들어 모델의 `City` 필드가 [필수](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 특성으로 데코레이팅 되었으므로 다음 예제에 표시 된 HTML이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="e8491-213">각 클라이언트 유효성 검사 규칙에 대해 양식이 `data-val-rulename="message"`된 특성이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="e8491-214">앞에 표시 된 `City` 필드 예제를 사용 하 여 필요한 클라이언트 유효성 검사 규칙은 `data-val-required` 특성을 생성 하 고 City 필드 &quot;메시지는&quot;필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="e8491-215">응용 프로그램을 실행 하 고, 사용자 중 하나를 편집 하 고, `City` 필드의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="e8491-216">필드에서 tab 키를 누르면 클라이언트 쪽 유효성 검사 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![도시 필요](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="e8491-218">마찬가지로, 클라이언트 유효성 검사 규칙의 각 매개 변수에 대해 양식이 `data-val-rulename-paramname=paramvalue`된 특성이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="e8491-219">예를 들어 `FirstName` 속성은 [Stringlength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성으로 주석이 지정 되 고 최소 길이는 3이 고 최대 길이는 8입니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="e8491-220">`length` 이라는 데이터 유효성 검사 규칙에는 매개 변수 이름 `max`와 매개 변수 값 8이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="e8491-221">다음은 사용자 중 하나를 편집할 때 `FirstName` 필드에 대해 생성 되는 HTML을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="e8491-222">클라이언트 유효성 검사에 대 한 자세한 내용은 ASP.NET MVC 3의 Wilson의 블로그 [에서 조심 스럽게 클라이언트 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e8491-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="e8491-223">ASP.NET MVC 3 Beta에서는 때때로 클라이언트 쪽 유효성 검사를 시작 하기 위해 양식을 제출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="e8491-224">최종 릴리스에서 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="e8491-225">만들기 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="e8491-225">Creating the Create View</span></span>

<span data-ttu-id="e8491-226">다음 단계는 사용자가 새 사용자를 만들 수 있도록 하기 위해 `Create` 작업 메서드와 보기를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="e8491-227">다음 `Create` 메서드를 홈 컨트롤러에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="e8491-228">이전 단계에서와 같이 뷰를 추가 하지만 **뷰 콘텐츠** 를 **Create**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![Create View](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="e8491-230">응용 프로그램을 실행 하 고, **만들기** 링크를 선택 하 고, 새 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="e8491-231">`Create` 메서드는 클라이언트 쪽 및 서버 쪽 유효성 검사를 자동으로 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="e8491-232">&quot;이혜준 X&quot;와 같이 공백을 포함 하는 사용자 이름을 입력 해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="e8491-233">사용자 이름 필드에서 tab 키를 누르면 클라이언트 쪽 유효성 검사 오류 (`White space is not allowed`)가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="e8491-234">Delete 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="e8491-234">Add the Delete method</span></span>

<span data-ttu-id="e8491-235">자습서를 완료 하려면 home 컨트롤러에 다음 `Delete` 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="e8491-236">이전 단계에서와 같이 `Delete` 뷰를 추가 하 여 **뷰 콘텐츠** 를 **삭제**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![보기 삭제](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="e8491-238">이제 유효성 검사를 사용 하는 간단 하지만 완전 한 기능의 ASP.NET MVC 3 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8491-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
