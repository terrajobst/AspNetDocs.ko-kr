---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 인증 및 권한 부여를 사용 하 여 응용 프로그램 보호 | Microsoft Docs
author: microsoft
description: 9 단계에서는 사용자가 사이트에 등록 하 고 로그인 하 여 만들 수 있도록 하는 인증 및 권한 부여를 추가 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8d509c5f15bb4d5014e53b8dc2a736454238e72c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486425"
---
# <a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="f6484-103">인증 및 권한 부여를 사용하여 애플리케이션 보호</span><span class="sxs-lookup"><span data-stu-id="f6484-103">Secure Applications Using Authentication and Authorization</span></span>

<span data-ttu-id="f6484-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="f6484-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f6484-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="f6484-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f6484-106">ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 9 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="f6484-107">9 단계에서는 사용자가 새 dinners를 만들기 위해 사이트에 등록 하 고 로그인 해야 하며 dinner a를 호스트 하는 사용자만 나중에 편집할 수 있도록 사용자가 사이트를 등록 하 고 로그인 해야 하는 경우에 인증 및 권한 부여를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="f6484-108">ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="f6484-109">NerdDinner Step 9: 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="f6484-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="f6484-110">이제, microsoft의 사용자가 사이트를 방문 하는 모든 사용자에 게 저녁의 세부 정보를 만들고 편집할 수 있는 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="f6484-111">사용자가 새 dinners를 만들기 위해 사이트에 등록 하 고 로그인 해야 하 고 저녁을 호스트 하는 사용자만 나중에 편집할 수 있도록 제한을 추가 하 여이를 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="f6484-112">이를 사용 하도록 설정 하려면 인증 및 권한 부여를 사용 하 여 응용 프로그램을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="f6484-113">인증 및 권한 부여 이해</span><span class="sxs-lookup"><span data-stu-id="f6484-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="f6484-114">*인증은* 응용 프로그램에 액세스 하는 클라이언트의 id를 식별 하 고 유효성을 검사 하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="f6484-115">좀 더 간단 하 게 말해 최종 사용자가 웹 사이트를 방문할 때 사용자를 식별 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="f6484-116">ASP.NET는 브라우저 사용자를 인증 하는 여러 방법을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="f6484-117">인터넷 웹 응용 프로그램의 경우 사용 되는 가장 일반적인 인증 방법을 "폼 인증" 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="f6484-118">폼 인증을 통해 개발자는 응용 프로그램 내에서 HTML 로그인 양식을 작성 한 후 데이터베이스 또는 다른 암호 자격 증명 저장소에 대해 최종 사용자가 제출한 사용자 이름/암호의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="f6484-119">사용자 이름/암호 조합이 올바르면 개발자가 ASP.NET에 게 암호화 된 HTTP 쿠키를 발급 하 여 향후 요청에서 사용자를 식별 하도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="f6484-120">Microsoft는 동료 Ddinner 응용 프로그램에서 폼 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="f6484-121">*권한 부여* 는 인증 된 사용자에 게 특정 URL/리소스에 대 한 액세스 권한이 있는지 또는 일부 동작을 수행할 권한이 있는지를 확인 하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="f6484-122">예를 들어, 내 동료 Ddinner 응용 프로그램 내에서 로그인 한 사용자만 */Dinners/Create* URL에 액세스 하 고 새 Dinners을 만들 수 있도록 권한을 부여 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="f6484-123">또한 식사를 호스트 하는 사용자만 편집할 수 있도록 권한 부여 논리를 추가 하 고 다른 모든 사용자에 대 한 편집 액세스를 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="f6484-124">폼 인증 및 AccountController</span><span class="sxs-lookup"><span data-stu-id="f6484-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="f6484-125">ASP.NET MVC에 대 한 기본 Visual Studio 프로젝트 템플릿은 새 ASP.NET MVC 응용 프로그램을 만들 때 폼 인증을 자동으로 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="f6484-126">또한 미리 작성 된 계정 로그인 페이지 구현을 프로젝트에 자동으로 추가 하 여 사이트 내에서 보안을 매우 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="f6484-127">기본 site.master 마스터 페이지는 사이트에 액세스 하는 사용자가 인증 되지 않은 경우 사이트의 오른쪽 위에 "로그온" 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="f6484-128">"로그온" 링크를 클릭 하면 사용자가 */Srvlogon* URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="f6484-129">등록 하지 않은 방문자는 "등록" 링크를 클릭 하 여이 작업을 수행할 수 있습니다 .이 링크를 선택 하면 */Dl/dlurl* 로 이동 하 여 계정 세부 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="f6484-130">"등록" 단추를 클릭 하면 ASP.NET 멤버 자격 시스템 내에 새 사용자가 생성 되 고 폼 인증을 사용 하 여 사이트에 대해 사용자가 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="f6484-131">사용자가 로그인 하면 site.master는 페이지의 오른쪽 위를 변경 하 여 "시작 [사용자 이름]!"을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="f6484-132">"로그온" 하는 대신 "로그 오프" 링크를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="f6484-133">"로그 오프" 링크를 클릭 하면 사용자가 로그 아웃 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="f6484-134">위의 로그인, 로그 아웃 및 등록 기능은 프로젝트를 만들 때 Visual Studio에서 프로젝트에 추가한 AccountController 클래스 내에서 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="f6484-135">AccountController의 UI는 \Views\Account 디렉터리 내에서 뷰 템플릿을 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="f6484-136">AccountController 클래스는 ASP.NET Forms 인증 시스템을 사용 하 여 암호화 된 인증 쿠키를 발급 하 고 ASP.NET Membership API를 사용 하 여 사용자 이름/암호를 저장 하 고 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="f6484-137">ASP.NET Membership API는 확장 가능 하며 모든 암호 자격 증명 저장소를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="f6484-138">ASP.NET는 SQL database 내에 사용자 이름/암호를 저장 하거나 Active Directory 내에 저장 하는 기본 제공 멤버 자격 공급자 구현 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="f6484-139">프로젝트의 루트에 있는 "web.config" 파일을 열고 그 안에 있는 &lt;멤버 자격&gt; 섹션을 검색 하 여 팀에서 사용 해야 하는 멤버 자격 공급자를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="f6484-140">프로젝트를 만들 때 추가 된 기본 web.config는 SQL 멤버 자격 공급자를 등록 하 고 "ApplicationServices" 라는 연결 문자열을 사용 하 여 데이터베이스 위치를 지정 하도록 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="f6484-141">Web.config 파일의 &lt;connectionStrings&gt; 섹션에 지정 된 기본 "ApplicationServices" 연결 문자열은 SQL Express를 사용 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="f6484-142">이름이 "ASPNETDB.MDF" 인 SQL Express 데이터베이스를 가리킵니다. MDF "응용 프로그램의" App\_Data "디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="f6484-143">응용 프로그램 내에서 멤버 자격 API를 처음 사용 하는 경우이 데이터베이스가 존재 하지 않는 경우 ASP.NET는 자동으로 데이터베이스를 만들고 해당 데이터베이스 내에서 적절 한 멤버 자격 데이터베이스 스키마를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="f6484-144">SQL Express를 사용 하는 대신 전체 SQL Server 인스턴스를 사용 하거나 원격 데이터베이스에 연결 하려는 경우 web.config 파일 내에서 "ApplicationServices" 연결 문자열을 업데이트 하 고 적절 한 멤버 자격 스키마를 확인 해야 합니다. 가 가리키는 데이터베이스에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="f6484-145">\Windows\Microsoft.NET\Framework\v2.0.50727\ 디렉터리 내에서 "aspnet\_regsql" 유틸리티를 실행 하 여 멤버 자격 및 기타 ASP.NET 응용 프로그램 서비스에 대 한 적절 한 스키마를 데이터베이스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="f6484-146">[권한 부여] 필터를 사용 하 여/Dinners/Create URL 권한 부여</span><span class="sxs-lookup"><span data-stu-id="f6484-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="f6484-147">이제는 코드를 작성 하 여 지 어 Ddinner 응용 프로그램에 대 한 보안 인증 및 계정 관리 구현을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="f6484-148">사용자는 응용 프로그램에 새 계정을 등록 하 고 사이트의 로그인/로그 아웃을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="f6484-149">이제 응용 프로그램에 권한 부여 논리를 추가 하 고 방문자의 인증 상태 및 사용자 이름을 사용 하 여 사이트 내에서 수행할 수 있는 작업을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="f6484-150">먼저 DinnersController 클래스의 "만들기" 작업 메서드에 권한 부여 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="f6484-151">특히 */Dinners/Create* URL에 액세스 하는 사용자가 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="f6484-152">로그인 하지 않은 경우 로그인 페이지로 리디렉션하여 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="f6484-153">이 논리를 구현 하는 것은 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="f6484-154">다음과 같이 만들기 작업 메서드에 [권한 부여] 필터 특성을 추가 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="f6484-155">ASP.NET MVC는 작업 메서드에 선언적으로 적용할 수 있는 재사용 가능한 논리를 구현 하는 데 사용할 수 있는 "작업 필터"를 만드는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="f6484-156">[권한 부여] 필터는 ASP.NET MVC에서 제공 하는 기본 제공 작업 필터 중 하나 이며 개발자가 작업 메서드 및 컨트롤러 클래스에 권한 부여 규칙을 선언적으로 적용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="f6484-157">위와 같이 매개 변수 없이 적용 하는 경우 [권한 부여] 필터는 동작 메서드 요청을 만드는 사용자에 게 로그인 해야 하는 것을 적용 하 고 브라우저를 로그인 URL로 자동으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="f6484-158">이 리디렉션 작업을 수행할 때 원래 요청 된 URL은 querystring 인수로 전달 됩니다 (예:/Account/dv? ReturnUrl =% 2fDinners% 2fCreate).</span><span class="sxs-lookup"><span data-stu-id="f6484-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="f6484-159">그러면 AccountController가 로그인 한 후 사용자를 원래 요청 된 URL로 다시 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="f6484-160">[권한 부여] 필터는 선택적으로 사용자를 로그인 하 고 허용 된 사용자 목록 또는 허용 된 보안 역할의 멤버에 로그인 하도록 요구 하는 데 사용할 수 있는 "사용자" 또는 "역할" 속성을 지정 하는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="f6484-161">예를 들어 아래 코드에서는 두 개의 특정 사용자 "scottgu" 및 "billg"를 사용 하 여/Dinners/Create URL에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="f6484-162">코드 내에 특정 사용자 이름을 포함 하는 것은 유지 관리 하기가 매우 용이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="f6484-163">더 나은 방법은 코드에서 확인 하는 상위 수준 "역할"을 정의한 다음 데이터베이스 또는 active directory 시스템을 사용 하 여 사용자를 역할에 매핑하는 것입니다 (실제 사용자 매핑 목록을 코드에서 외부에 저장할 수 있도록 함).</span><span class="sxs-lookup"><span data-stu-id="f6484-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="f6484-164">ASP.NET에는 기본 제공 역할 관리 API 뿐만 아니라이 사용자/역할 매핑을 수행 하는 데 도움이 되는 역할 공급자의 기본 제공 집합 (SQL 및 Active Directory 포함)이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="f6484-165">그런 다음 특정 "관리자" 역할 내의 사용자만/Dinners/Create URL에 액세스할 수 있도록 코드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="f6484-166">Dinners를 만들 때 User.Identity.Name 속성 사용</span><span class="sxs-lookup"><span data-stu-id="f6484-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="f6484-167">컨트롤러 기본 클래스에 노출 된 User.Identity.Name 속성을 사용 하 여 요청에 대해 현재 로그인 한 사용자의 사용자 이름을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="f6484-168">이전에는 Create () 작업 메서드의 HTTP POST 버전을 구현 했을 때 Dinner a의 "HostedBy" 속성을 정적 문자열로 하드 코딩 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="f6484-169">이제이 코드를 업데이트 하 여 User.Identity.Name 속성을 대신 사용 하 고, Dinner a를 만드는 호스트에 대해 RSVP를 자동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="f6484-170">[권한 부여] 특성을 Create () 메서드에 추가 했으므로 ASP.NET MVC는/Dinners/Create URL을 방문 하는 사용자가 사이트에 로그인 한 경우에만 동작 메서드가 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="f6484-171">이와 같이 User.Identity.Name 속성 값에는 항상 유효한 사용자 이름이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="f6484-172">Dinners를 편집할 때 User.Identity.Name 속성 사용</span><span class="sxs-lookup"><span data-stu-id="f6484-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="f6484-173">이제 자신이 호스트 하는 dinners 속성만 편집할 수 있도록 사용자를 제한 하는 권한 부여 논리를 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="f6484-174">이를 지원 하기 위해 먼저 "IsHostedBy (사용자 이름)" 도우미 메서드를 Dinner object (이전에 빌드한 Dinner.cs partial 클래스 내)에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="f6484-175">이 도우미 메서드는 제공 된 사용자 이름이 Dinner HostedBy 속성과 일치 하는지 여부에 따라 true 또는 false를 반환 하 고, 대/소문자를 구분 하지 않는 문자열 비교를 수행 하는 데 필요한 논리를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="f6484-176">그런 다음, DinnersController 클래스 내의 Edit () 작업 메서드에 [권한 부여] 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="f6484-177">이렇게 하면 */Dinners/Edit/[id]* URL을 요청 하는 사용자가 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="f6484-178">그런 다음 IsHostedBy (username) 도우미 메서드를 사용 하 여 로그인 한 사용자가 Dinner host와 일치 하는지 확인 하는 코드를 편집 메서드에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="f6484-179">사용자가 호스트가 아닌 경우 "InvalidOwner" 보기를 표시 하 고 요청을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="f6484-180">이 작업을 수행 하는 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="f6484-181">그런 다음 \Views\Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가&gt;보기 메뉴 명령을 선택 하 여 새 "InvalidOwner" 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="f6484-182">다음 오류 메시지로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="f6484-183">사용자가 자신이 소유 하지 않은 저녁을 편집 하려고 하면 다음과 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="f6484-184">컨트롤러 내의 Delete () 작업 메서드에 대해 동일한 단계를 반복 하 여 Dinners 삭제 권한도 잠글 수 있으며 저녁의 호스트만 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="f6484-185">편집 및 삭제 링크 표시/숨기기</span><span class="sxs-lookup"><span data-stu-id="f6484-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="f6484-186">세부 정보 URL에서 DinnersController 클래스의 편집 및 삭제 작업 메서드에 연결 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="f6484-187">현재 세부 정보 URL의 방문자가 저녁의 호스트 인지 여부에 관계 없이 편집 및 삭제 작업 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="f6484-188">이를 변경해 보겠습니다. 그러면 방문한 사용자가 저녁의 소유자 인 경우에만 링크가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="f6484-189">DinnersController 내의 Details () 작업 메서드는 Dinner object를 검색 한 다음이를 모델 개체로 모델 개체로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="f6484-190">아래와 같이 IsHostedBy () 도우미 메서드를 사용 하 여 편집 및 삭제 링크를 조건부로 표시/숨기기 위해 뷰 템플릿을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="f6484-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6484-191">Next Steps</span></span>

<span data-ttu-id="f6484-192">이제 AJAX를 사용 하 여 인증 된 사용자에 게 RSVP for dinners를 사용 하도록 설정할 수 있는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f6484-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f6484-193">[이전](implement-efficient-data-paging.md)
> [다음](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="f6484-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>
