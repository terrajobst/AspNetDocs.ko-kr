---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: 폼 인증으로 사용자 인증 (C#) | Microsoft Docs
author: microsoft
description: '[권한 부여] 특성을 사용 하 여 MVC 응용 프로그램에서 특정 페이지를 암호로 보호 하는 방법에 대해 알아봅니다. 웹 사이트 관리를 사용 하는 방법에 대해 알아봅니다.'
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: bed2eafa47fec25ac04cb07e0037f596494bb7d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435449"
---
# <a name="authenticating-users-with-forms-authentication-c"></a><span data-ttu-id="823f1-104">폼 인증으로 사용자 인증(C#)</span><span class="sxs-lookup"><span data-stu-id="823f1-104">Authenticating Users with Forms Authentication (C#)</span></span>

<span data-ttu-id="823f1-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="823f1-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="823f1-106">[권한 부여] 특성을 사용 하 여 MVC 응용 프로그램에서 특정 페이지를 암호로 보호 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-106">Learn how to use the [Authorize] attribute to password protect particular pages in your MVC application.</span></span> <span data-ttu-id="823f1-107">웹 사이트 관리 도구를 사용 하 여 사용자 및 역할을 만들고 관리 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-107">You learn how to use the Web Site Administration Tool to create and manage users and roles.</span></span> <span data-ttu-id="823f1-108">또한 사용자 계정 및 역할 정보가 저장 되는 위치를 구성 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-108">You also learn how to configure where user account and role information is stored.</span></span>

<span data-ttu-id="823f1-109">이 자습서의 목표는 폼 인증을 사용 하 여 ASP.NET MVC 응용 프로그램에서 뷰를 암호로 보호 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-109">The goal of this tutorial is to explain how you can use Forms authentication to password protect the views in your ASP.NET MVC applications.</span></span> <span data-ttu-id="823f1-110">웹 사이트 관리 도구를 사용 하 여 사용자 및 역할을 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-110">You learn how to use the Web Site Administration Tool to create users and roles.</span></span> <span data-ttu-id="823f1-111">또한 권한이 없는 사용자가 컨트롤러 작업을 호출 하지 못하도록 방지 하는 방법도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-111">You also learn how to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="823f1-112">마지막으로 사용자 이름 및 암호를 저장 하는 위치를 구성 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-112">Finally, you learn how to configure where user names and passwords are stored.</span></span>

#### <a name="using-the-web-site-administration-tool"></a><span data-ttu-id="823f1-113">웹 사이트 관리 도구 사용</span><span class="sxs-lookup"><span data-stu-id="823f1-113">Using the Web Site Administration Tool</span></span>

<span data-ttu-id="823f1-114">다른 작업을 수행 하기 전에 먼저 일부 사용자 및 역할을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-114">Before we do anything else, we should start by creating some users and roles.</span></span> <span data-ttu-id="823f1-115">새 사용자 및 역할을 만드는 가장 쉬운 방법은 Visual Studio 2008 웹 사이트 관리 도구를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-115">The easiest way to create new users and roles is to take advantage of the Visual Studio 2008 Web Site Administration Tool.</span></span> <span data-ttu-id="823f1-116">메뉴 옵션 **프로젝트, ASP.NET 구성**을 선택 하 여이 도구를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-116">You can launch this tool by selecting the menu option **Project, ASP.NET Configuration**.</span></span> <span data-ttu-id="823f1-117">또는 솔루션 탐색기 창의 맨 위에 표시 되는 전 세계에 있는 해머의 (약간의) 아이콘을 클릭 하 여 웹 사이트 관리 도구를 시작할 수 있습니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="823f1-117">Alternatively, you can launch the Web Site Administration Tool by clicking the (somewhat scary) icon of the hammer hitting the world that appears at the top of the Solution Explorer window (see Figure 1).</span></span>

<span data-ttu-id="823f1-118">**그림 1-웹 사이트 관리 도구 시작**</span><span class="sxs-lookup"><span data-stu-id="823f1-118">**Figure 1 – Launching the Web Site Administration Tool**</span></span>

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

<span data-ttu-id="823f1-120">웹 사이트 관리 도구에서 보안 탭을 선택 하 여 새 사용자 및 역할을 만듭니다. **사용자 만들기** 링크를 클릭 하 여 Stephen 라는 새 사용자를 만듭니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="823f1-120">Within the Web Site Administration Tool, you create new users and roles by selecting the Security tab. Click the **Create user** link to create a new user named Stephen (see Figure 2).</span></span> <span data-ttu-id="823f1-121">Stephen 사용자에 게 원하는 암호를 제공 합니다 (예: *secret*).</span><span class="sxs-lookup"><span data-stu-id="823f1-121">Provide the Stephen user with any password that you want (for example, *secret*).</span></span>

<span data-ttu-id="823f1-122">**그림 2-새 사용자 만들기**</span><span class="sxs-lookup"><span data-stu-id="823f1-122">**Figure 2 – Creating a new user**</span></span>

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

<span data-ttu-id="823f1-124">먼저 역할을 사용 하도록 설정 하 고 하나 이상의 역할을 정의 하 여 새 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-124">You create new roles by first enabling roles and defining one or more roles.</span></span> <span data-ttu-id="823f1-125">**역할 사용** 링크를 클릭 하 여 역할을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-125">Enable roles by clicking the **Enable roles** link.</span></span> <span data-ttu-id="823f1-126">그런 다음 **역할 만들기 또는 관리** 링크를 클릭 하 여 *관리자* 라는 역할을 만듭니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="823f1-126">Next, create a role named *Administrators* by clicking the **Create or Manage roles** link (see Figure 3).</span></span>

<span data-ttu-id="823f1-127">**그림 3-새 역할 만들기**</span><span class="sxs-lookup"><span data-stu-id="823f1-127">**Figure 3 – Creating a new role**</span></span>

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

<span data-ttu-id="823f1-129">마지막으로 Sally 이라는 새 사용자를 만들고 사용자 만들기 링크를 클릭 하 고 Sally를 만들 때 관리자를 선택 하 여 Sally를 관리자 역할에 연결 합니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="823f1-129">Finally, create a new user named Sally and associate Sally with the Administrators role by clicking the Create User link and selecting Administrators when creating Sally (see Figure 4).</span></span>

<span data-ttu-id="823f1-130">**그림 4-역할에 사용자 추가**</span><span class="sxs-lookup"><span data-stu-id="823f1-130">**Figure 4 – Adding a user to a role**</span></span>

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

<span data-ttu-id="823f1-132">모든 작업이 완료 되 면 Stephen 및 Sally 라는 두 명의 새 사용자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-132">When all is said and done, you should have two new users named Stephen and Sally.</span></span> <span data-ttu-id="823f1-133">또한 관리자 라는 새 역할이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-133">You should also have a new role named Administrators.</span></span> <span data-ttu-id="823f1-134">Sally는 Administrators 역할의 멤버이 고 Stephen는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-134">Sally is a member of the Administrators role and Stephen is not.</span></span>

#### <a name="requiring-authorization"></a><span data-ttu-id="823f1-135">권한 부여 필요</span><span class="sxs-lookup"><span data-stu-id="823f1-135">Requiring Authorization</span></span>

<span data-ttu-id="823f1-136">사용자가 작업에 [권한 부여] 특성을 추가 하 여 사용자가 컨트롤러 작업을 호출 하기 전에 사용자를 인증 하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-136">You can require a user to be authenticated before the user invokes a controller action by adding the [Authorize] attribute to the action.</span></span> <span data-ttu-id="823f1-137">[권한 부여] 특성을 개별 컨트롤러 작업에 적용 하거나, 전체 컨트롤러 클래스에이 특성을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-137">You can apply the [Authorize] attribute to an individual controller action or you can apply this attribute to an entire controller class.</span></span>

<span data-ttu-id="823f1-138">예를 들어 목록 1의 컨트롤러는 CompanySecrets () 이라는 동작을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-138">For example, the controller in Listing 1 exposes an action named CompanySecrets().</span></span> <span data-ttu-id="823f1-139">이 동작은 [권한 부여] 특성으로 데코레이팅 되므로 사용자를 인증 하지 않으면이 작업을 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-139">Because this action is decorated with the [Authorize] attribute, this action cannot be invoked unless a user is authenticated.</span></span>

<span data-ttu-id="823f1-140">**목록 1 – Controllers\ homecontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="823f1-140">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

<span data-ttu-id="823f1-141">브라우저의 주소 표시줄에 URL/Home/CompanySecrets을 입력 하 여 CompanySecrets () 작업을 호출 하 고 사용자가 인증 된 사용자가 아닌 경우에는 로그인 뷰로 자동으로 리디렉션됩니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="823f1-141">If you invoke the CompanySecrets() action by entering the URL /Home/CompanySecrets in the address bar of your browser, and you are not an authenticated user, then you will be redirected to the Login view automatically (see Figure 5).</span></span>

<span data-ttu-id="823f1-142">**그림 5-로그인 보기**</span><span class="sxs-lookup"><span data-stu-id="823f1-142">**Figure 5 – The Login view**</span></span>

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

<span data-ttu-id="823f1-144">로그인 보기를 사용 하 여 사용자 이름 및 암호를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-144">You can use the Login view to enter your user name and password.</span></span> <span data-ttu-id="823f1-145">등록 된 사용자가 아닌 경우 **등록 링크를 클릭 하 여 등록** 보기로 이동할 수 있습니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="823f1-145">If you are not a registered user then you can click the **register** link to navigate to the Register view (see Figure 6).</span></span> <span data-ttu-id="823f1-146">등록 보기를 사용 하 여 새 사용자 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-146">You can use the Register view to create a new user account.</span></span>

<span data-ttu-id="823f1-147">**그림 6-레지스터 보기**</span><span class="sxs-lookup"><span data-stu-id="823f1-147">**Figure 6 – The Register view**</span></span>

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

<span data-ttu-id="823f1-149">성공적으로 로그인 하면 CompanySecrets 보기를 볼 수 있습니다 (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="823f1-149">After you successfully log in, you can see the CompanySecrets view (see Figure 7).</span></span> <span data-ttu-id="823f1-150">기본적으로 브라우저 창을 닫을 때까지 계속 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-150">By default, you will continue to be logged in until you close your browser window.</span></span>

<span data-ttu-id="823f1-151">**그림 7-CompanySecrets 뷰**</span><span class="sxs-lookup"><span data-stu-id="823f1-151">**Figure 7 – The CompanySecrets view**</span></span>

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a><span data-ttu-id="823f1-153">사용자 이름 또는 사용자 역할에의 한 권한 부여</span><span class="sxs-lookup"><span data-stu-id="823f1-153">Authorizing by User Name or User Role</span></span>

<span data-ttu-id="823f1-154">[권한 부여] 특성을 사용 하 여 특정 사용자나 특정 사용자 역할 집합에 대 한 컨트롤러 작업에 대 한 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-154">You can use the [Authorize] attribute to restrict access to a controller action to a particular set of users or a particular set of user roles.</span></span> <span data-ttu-id="823f1-155">예를 들어 목록 2의 수정 된 홈 컨트롤러에는 StephenSecrets () 및 관리자 암호 () 라는 두 개의 새로운 동작이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-155">For example, the modified Home controller in Listing 2 contains two new actions named StephenSecrets() and AdministratorSecrets().</span></span>

<span data-ttu-id="823f1-156">**목록 2 – Controllers\ homecontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="823f1-156">**Listing 2 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

<span data-ttu-id="823f1-157">사용자 이름이 Stephen 인 사용자만 StephenSecrets () 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-157">Only a user with the user name Stephen can invoke the StephenSecrets() action.</span></span> <span data-ttu-id="823f1-158">다른 모든 사용자는 로그인 뷰로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-158">All other users get redirected to the Login view.</span></span> <span data-ttu-id="823f1-159">사용자 속성은 쉼표로 구분 된 사용자 계정 이름 목록을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-159">The Users property accepts a comma separated list of user account names.</span></span>

<span data-ttu-id="823f1-160">관리자 역할의 사용자만 관리자 암호 () 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-160">Only users in the Administrators role can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="823f1-161">예를 들어 Sally가 Administrators 그룹의 멤버 이기 때문에 관리자 암호 () 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-161">For example, because Sally is a member of the Administrators group, she can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="823f1-162">다른 모든 사용자는 로그인 뷰로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-162">All other users get redirected to the Login view.</span></span> <span data-ttu-id="823f1-163">Roles 속성은 쉼표로 구분 된 역할 이름 목록을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-163">The Roles property accepts a comma separated list of role names.</span></span>

#### <a name="configuring-authentication"></a><span data-ttu-id="823f1-164">인증 구성</span><span class="sxs-lookup"><span data-stu-id="823f1-164">Configuring Authentication</span></span>

<span data-ttu-id="823f1-165">이 시점에서 사용자 계정 및 역할 정보가 저장 되는 위치를 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-165">At this point, you might be wondering where the user account and role information is being stored.</span></span> <span data-ttu-id="823f1-166">기본적으로이 정보는 MVC 응용 프로그램의 App\_Data 폴더에 있는 ASPNETDB.MDF 라는 SQL Express 데이터베이스 (RANU)에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-166">By default, the information is stored in a (RANU) SQL Express database named ASPNETDB.mdf located in your MVC application's App\_Data folder.</span></span> <span data-ttu-id="823f1-167">이 데이터베이스는 멤버 자격 사용을 시작할 때 자동으로 ASP.NET 프레임 워크에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-167">This database is generated by the ASP.NET framework automatically when you start using membership.</span></span>

<span data-ttu-id="823f1-168">솔루션 탐색기 창에서 ASPNETDB.MDF 데이터베이스를 보려면 먼저 메뉴 옵션 프로젝트, 모든 파일 표시를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-168">In order to see the ASPNETDB.mdf database in the Solution Explorer window, you first need to select the menu option Project, Show All Files.</span></span>

<span data-ttu-id="823f1-169">응용 프로그램을 개발할 때 기본 SQL Express 데이터베이스를 사용 하는 것은 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-169">Using the default SQL Express database is fine when developing an application.</span></span> <span data-ttu-id="823f1-170">그러나 프로덕션 응용 프로그램에 대해 기본 ASPNETDB.MDF 데이터베이스를 사용 하지 않을 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-170">Most likely, however, you won't want to use the default ASPNETDB.mdf database for a production application.</span></span> <span data-ttu-id="823f1-171">이 경우 다음 두 단계를 완료 하 여 사용자 계정 정보가 저장 되는 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-171">In that case, you can change where user account information is stored by completing the following two steps:</span></span>

1. <span data-ttu-id="823f1-172">프로덕션 데이터베이스에 애플리케이션 서비스 데이터베이스 개체 추가-프로덕션 데이터베이스를 가리키도록 응용 프로그램 연결 문자열 변경</span><span class="sxs-lookup"><span data-stu-id="823f1-172">Add the Application Services database objects to your production database - Change your application connection string to point to your production database</span></span>

<span data-ttu-id="823f1-173">첫 번째 단계는 필요한 모든 데이터베이스 개체 (테이블 및 저장 프로시저)를 프로덕션 데이터베이스에 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-173">The first step is to add all of the necessary database objects (tables and stored procedures) to your production database.</span></span> <span data-ttu-id="823f1-174">이러한 개체를 새 데이터베이스에 추가 하는 가장 쉬운 방법은 ASP.NET SQL Server 설치 마법사를 사용 하는 것입니다 (그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="823f1-174">The easiest way to add these objects to a new database is to take advantage of the ASP.NET SQL Server Setup Wizard (see Figure 8).</span></span> <span data-ttu-id="823f1-175">Microsoft Visual Studio 2008 프로그램 그룹에서 Visual Studio 2008 명령 프롬프트를 열고 명령 프롬프트에서 다음 명령을 실행 하 여이 도구를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-175">You can launch this tool by opening the Visual Studio 2008 Command Prompt from the Microsoft Visual Studio 2008 program group and executing the following command from the command prompt:</span></span>

<span data-ttu-id="823f1-176">aspnet\_regsql</span><span class="sxs-lookup"><span data-stu-id="823f1-176">aspnet\_regsql</span></span>

<span data-ttu-id="823f1-177">**그림 8-ASP.NET SQL Server 설치 마법사**</span><span class="sxs-lookup"><span data-stu-id="823f1-177">**Figure 8 – The ASP.NET SQL Server Setup Wizard**</span></span>

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

<span data-ttu-id="823f1-179">ASP.NET SQL Server 설치 마법사를 사용 하 여 네트워크에서 SQL Server 데이터베이스를 선택 하 고 ASP.NET 응용 프로그램 서비스에 필요한 모든 데이터베이스 개체를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-179">The ASP.NET SQL Server Setup Wizard enables you to select a SQL Server database on your network and install all of the database objects required by the ASP.NET application services.</span></span> <span data-ttu-id="823f1-180">데이터베이스 서버가 로컬 컴퓨터에 있을 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-180">The database server is not required to be located on your local machine.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="823f1-181">ASP.NET SQL Server 설치 마법사를 사용 하지 않으려는 경우 다음 폴더에 응용 프로그램 서비스 데이터베이스 개체를 추가 하는 SQL 스크립트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-181">If you don't want to use the ASP.NET SQL Server Setup Wizard, then you can find SQL scripts for adding the application services database objects in the following folder:</span></span>
> 
> > <span data-ttu-id="823f1-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span><span class="sxs-lookup"><span data-stu-id="823f1-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span></span>

<span data-ttu-id="823f1-183">필요한 데이터베이스 개체를 만든 후에는 MVC 응용 프로그램에서 사용 하는 데이터베이스 연결을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-183">After you create the necessary database objects, you need to modify the database connection used by your MVC application.</span></span> <span data-ttu-id="823f1-184">프로덕션 데이터베이스를 가리키도록 웹 구성 파일 (web.config)에서 ApplicationServices 연결 문자열을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-184">Modify the ApplicationServices connection string in your web configuration (web.config) file so that it points to the production database.</span></span> <span data-ttu-id="823f1-185">예를 들어 목록 3의 수정 된 연결은 MyProductionDB 라는 데이터베이스를 가리킵니다 (원래 ApplicationServices 연결 문자열은 주석 처리 됨).</span><span class="sxs-lookup"><span data-stu-id="823f1-185">For example, the modified connection in Listing 3 points to a database named MyProductionDB (the original ApplicationServices connection string has been commented out).</span></span>

<span data-ttu-id="823f1-186">**목록 3 – web.config**</span><span class="sxs-lookup"><span data-stu-id="823f1-186">**Listing 3 – Web.config**</span></span>

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a><span data-ttu-id="823f1-187">데이터베이스 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="823f1-187">Configuring Database Permissions</span></span>

<span data-ttu-id="823f1-188">통합 보안을 사용 하 여 데이터베이스에 연결 하는 경우 올바른 Windows 사용자 계정을 데이터베이스에 로그인으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-188">If you use Integrated Security to connect to your database then you will need to add the correct Windows user account as a login to your database.</span></span> <span data-ttu-id="823f1-189">올바른 계정은 ASP.NET 개발 서버를 사용 하는지 또는 인터넷 정보 서비스를 웹 서버로 사용 하는지에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-189">The correct account depends on whether you are using the ASP.NET Development Server or Internet Information Services as your web server.</span></span> <span data-ttu-id="823f1-190">또한 올바른 사용자 계정은 운영 체제에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-190">The correct user account also depends on your operating system.</span></span>

<span data-ttu-id="823f1-191">ASP.NET 개발 서버 (Visual Studio에서 사용 하는 기본 웹 서버)를 사용 하는 경우 응용 프로그램은 Windows 사용자 계정의 컨텍스트 내에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-191">If you are using the ASP.NET Development Server (the default web server used by Visual Studio) then your application executes within the context of your Windows user account.</span></span> <span data-ttu-id="823f1-192">이 경우 Windows 사용자 계정을 데이터베이스 서버 로그인으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-192">In that case, you need to add your Windows user account as a database server login.</span></span>

<span data-ttu-id="823f1-193">또는 인터넷 정보 서비스를 사용 하는 경우 ASPNET 계정 또는 NT AUTHORITY/NETWORK 서비스 계정을 데이터베이스 서버 로그인으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-193">Alternatively, if you are using Internet Information Services then you need to add either the ASPNET account or the NT AUTHORITY/NETWORK SERVICE account as a database server login.</span></span> <span data-ttu-id="823f1-194">Windows XP를 사용 하는 경우 ASPNET 계정을 데이터베이스에 로그인으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-194">If you are using Windows XP then add the ASPNET account as a login to your database.</span></span> <span data-ttu-id="823f1-195">Windows Vista 또는 Windows Server 2008와 같은 최신 운영 체제를 사용 하는 경우 NT AUTHORITY/NETWORK 서비스 계정을 데이터베이스 로그인으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-195">If you are using a more recent operating system, such as Windows Vista or Windows Server 2008, then add the NT AUTHORITY/NETWORK SERVICE account as the database login.</span></span>

<span data-ttu-id="823f1-196">Microsoft SQL Server Management Studio를 사용 하 여 데이터베이스에 새 사용자 계정을 추가할 수 있습니다 (그림 9 참조).</span><span class="sxs-lookup"><span data-stu-id="823f1-196">You can add a new user account to your database by using Microsoft SQL Server Management Studio (see Figure 9).</span></span>

<span data-ttu-id="823f1-197">**그림 9-새 Microsoft SQL Server 로그인 만들기**</span><span class="sxs-lookup"><span data-stu-id="823f1-197">**Figure 9 – Creating a new Microsoft SQL Server login**</span></span>

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

<span data-ttu-id="823f1-199">필요한 로그인을 만든 후에는 올바른 데이터베이스 역할을 사용 하 여 로그인을 데이터베이스 사용자에 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-199">After you create the required login, you need to map the login to a database user with the right database roles.</span></span> <span data-ttu-id="823f1-200">로그인을 두 번 클릭 하 고 사용자 매핑 탭을 선택 합니다. 하나 이상의 응용 프로그램 서비스 데이터베이스 역할을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-200">Double-click the login and select the User Mapping tab. Select one or more application services database roles.</span></span> <span data-ttu-id="823f1-201">예를 들어 사용자를 인증 하기 위해 BasicAccess 데이터베이스 역할\_aspnet\_멤버 자격을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-201">For example, in order to authenticate users, you need to enable the aspnet\_Membership\_BasicAccess database role.</span></span> <span data-ttu-id="823f1-202">새 사용자를 만들려면 aspnet\_멤버 자격\_FullAccess 데이터베이스 역할을 사용 하도록 설정 해야 합니다 (그림 10 참조).</span><span class="sxs-lookup"><span data-stu-id="823f1-202">In order to create new users, you need to enable the aspnet\_Membership\_FullAccess database role (see Figure 10).</span></span>

<span data-ttu-id="823f1-203">**그림 10-애플리케이션 서비스 데이터베이스 역할 추가**</span><span class="sxs-lookup"><span data-stu-id="823f1-203">**Figure 10 – Adding Application Services database roles**</span></span>

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a><span data-ttu-id="823f1-205">요약</span><span class="sxs-lookup"><span data-stu-id="823f1-205">Summary</span></span>

<span data-ttu-id="823f1-206">이 자습서에서는 ASP.NET MVC 응용 프로그램을 빌드할 때 폼 인증을 사용 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-206">In this tutorial, you learned how to use Forms authentication when building an ASP.NET MVC application.</span></span> <span data-ttu-id="823f1-207">먼저 웹 사이트 관리 도구를 활용 하 여 새 사용자 및 역할을 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-207">First, you learned how to create new users and roles by taking advantage of the Web Site Administration Tool.</span></span> <span data-ttu-id="823f1-208">다음에는 [권한 부여] 특성을 사용 하 여 권한이 없는 사용자가 컨트롤러 작업을 호출 하지 못하도록 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-208">Next, you learned how to use the [Authorize] attribute to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="823f1-209">마지막으로, 프로덕션 데이터베이스에 사용자 및 역할 정보를 저장 하도록 MVC 응용 프로그램을 구성 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="823f1-209">Finally, you learned how to configure your MVC application to store user and role information in a production database.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="823f1-210">다음</span><span class="sxs-lookup"><span data-stu-id="823f1-210">Next</span></span>](authenticating-users-with-windows-authentication-cs.md)
