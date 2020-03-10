---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Contact Manager 솔루션 설정 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 개발자 워크스테이션에서 로컬로 실행 되도록 Contact Manager 솔루션을 다운로드 하 고 구성 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511163"
---
# <a name="setting-up-the-contact-manager-solution"></a><span data-ttu-id="10a1a-103">Contact Manager 솔루션 설정</span><span class="sxs-lookup"><span data-stu-id="10a1a-103">Setting Up the Contact Manager Solution</span></span>

<span data-ttu-id="10a1a-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="10a1a-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="10a1a-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="10a1a-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="10a1a-106">이 항목에서는 개발자 워크스테이션에서 로컬로 실행 되도록 Contact Manager 솔루션을 다운로드 하 고 구성 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-106">This topic describes how to download and configure the Contact Manager solution to run locally on a developer workstation.</span></span>

## <a name="system-requirements"></a><span data-ttu-id="10a1a-107">시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="10a1a-107">System Requirements</span></span>

<span data-ttu-id="10a1a-108">이 자습서에 설명 된 다른 작업을 수행 하 고이 자습서에서 설명 하는 다른 작업을 수행 하려면 개발자 워크스테이션에이 소프트웨어를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-108">To run the Contact Manager solution locally and to perform the other tasks described in this tutorial, you'll need to install this software on your developer workstation:</span></span>

- <span data-ttu-id="10a1a-109">Visual Studio 2010 서비스 팩 1, Premium 또는 Ultimate Edition</span><span class="sxs-lookup"><span data-stu-id="10a1a-109">Visual Studio 2010 Service Pack 1, Premium or Ultimate Edition</span></span>
- <span data-ttu-id="10a1a-110">인터넷 정보 서비스(IIS) 7.5 Express</span><span class="sxs-lookup"><span data-stu-id="10a1a-110">Internet Information Services (IIS) 7.5 Express</span></span>
- <span data-ttu-id="10a1a-111">SQL Server Express 2008 R2</span><span class="sxs-lookup"><span data-stu-id="10a1a-111">SQL Server Express 2008 R2</span></span>
- <span data-ttu-id="10a1a-112">IIS 웹 배포 도구 (웹 배포) 2.1 이상</span><span class="sxs-lookup"><span data-stu-id="10a1a-112">IIS Web Deployment Tool (Web Deploy) 2.1 or later</span></span>
- <span data-ttu-id="10a1a-113">ASP.NET 4.0</span><span class="sxs-lookup"><span data-stu-id="10a1a-113">ASP.NET 4.0</span></span>
- <span data-ttu-id="10a1a-114">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="10a1a-114">ASP.NET MVC 3</span></span>
- <span data-ttu-id="10a1a-115">.NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="10a1a-115">.NET Framework 4</span></span>
- <span data-ttu-id="10a1a-116">.NET Framework 3.5 SP1</span><span class="sxs-lookup"><span data-stu-id="10a1a-116">.NET Framework 3.5 SP1</span></span>

<span data-ttu-id="10a1a-117">Visual Studio 2010을 제외 하 고 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)를 통해 이러한 모든 제품 및 구성 요소의 최신 버전을 다운로드 하 여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-117">With the exception of Visual Studio 2010, you can download and install the latest versions of all of these products and components through the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

## <a name="download-and-extract-the-solution"></a><span data-ttu-id="10a1a-118">솔루션 다운로드 및 추출</span><span class="sxs-lookup"><span data-stu-id="10a1a-118">Download and Extract the Solution</span></span>

<span data-ttu-id="10a1a-119">[여기](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)서 MSDN 코드 갤러리에서 Contact Manager 샘플 응용 프로그램을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-119">You can download the Contact Manager sample application from the MSDN Code Gallery [here](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).</span></span>

## <a name="configure-and-run-the-solution"></a><span data-ttu-id="10a1a-120">솔루션 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="10a1a-120">Configure and Run the Solution</span></span>

<span data-ttu-id="10a1a-121">로컬 컴퓨터에서 Contact Manager 솔루션을 구성 하 고 실행 하려면 다음과 같은 개략적인 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-121">To configure and run the Contact Manager solution on your local machine, you'll need to perform these high-level steps:</span></span>

1. <span data-ttu-id="10a1a-122">아직 없는 경우 멤버 자격 및 역할 관리 기능을 사용 하도록 설정 하 여 로컬 ASP.NET 응용 프로그램 서비스 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-122">If you don't have one already, create a local ASP.NET application services database with the membership and role management features enabled.</span></span>
2. <span data-ttu-id="10a1a-123">*Web.config* 파일의 연결 문자열을 편집 하 여 로컬 SQL Server Express 인스턴스를 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-123">Edit connection strings in the *web.config* files to point to your local SQL Server Express instance.</span></span>
3. <span data-ttu-id="10a1a-124">Visual Studio 2010에서 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-124">Run the solution from Visual Studio 2010.</span></span>

<span data-ttu-id="10a1a-125">이 섹션의 나머지 부분에서는 이러한 각 작업을 완료 하는 방법에 대 한 자세한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-125">The remainder of this section provides more guidance on how to complete each of these tasks.</span></span>

<span data-ttu-id="10a1a-126">**응용 프로그램 서비스 데이터베이스를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="10a1a-126">**To create the application services database**</span></span>

1. <span data-ttu-id="10a1a-127">Visual Studio 2010 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-127">Open a Visual Studio 2010 command prompt.</span></span> <span data-ttu-id="10a1a-128">이렇게 하려면 **시작** 메뉴에서 **모든 프로그램**을 가리키고 **Microsoft Visual Studio 2010**, **Visual Studio Tools**를 차례로 클릭 한 다음 **Visual Studio 명령 프롬프트 (2010)** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-128">To do this, on the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, click **Visual Studio Tools**, and then click **Visual Studio Command Prompt (2010)**.</span></span>
2. <span data-ttu-id="10a1a-129">명령 프롬프트에서 다음 명령을 입력 하 고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-129">At the command prompt, type this command, and then press Enter:</span></span>

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. <span data-ttu-id="10a1a-130">**– C** 스위치를 사용 하 여 데이터베이스 서버에 대 한 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-130">Use the **–C** switch to specify the connection string for your database server.</span></span>
    2. <span data-ttu-id="10a1a-131">**– A** 스위치를 사용 하 여 데이터베이스에 추가 하려는 응용 프로그램 서비스 기능을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-131">Use the **–A** switch to specify the application services features you want to add to the database.</span></span> <span data-ttu-id="10a1a-132">이 경우 **m** 은 멤버 자격 공급자에 대 한 지원을 추가 하려고 함을 나타내고 **r** 은 역할 관리자에 대 한 지원을 추가할 것임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-132">In this case, **m** indicates that you want to add support for the membership provider and **r** indicates that you want to add support for the role manager.</span></span>
    3. <span data-ttu-id="10a1a-133">**– D** 스위치를 사용 하 여 응용 프로그램 서비스 데이터베이스의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-133">Use the **–d** switch to specify a name for your application services database.</span></span> <span data-ttu-id="10a1a-134">이 스위치를 생략 하는 경우 유틸리티는 기본 이름인 **aspnetdb.mdf**를 사용 하 여 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-134">If you omit this switch, the utility will create a database with the default name of **aspnetdb**.</span></span>
3. <span data-ttu-id="10a1a-135">데이터베이스가 성공적으로 생성 되 면 명령 프롬프트에 확인 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-135">When the database has been created successfully, the command prompt will show a confirmation.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="10a1a-136">Aspnet\_regsql 유틸리티에 대 한 자세한 내용은 [ASP.NET SQL Server Registration Tool (aspnet\_regsql)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="10a1a-136">For more information on the aspnet\_regsql utility, see [ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span></span>

<span data-ttu-id="10a1a-137">다음 단계는 Contact Manager 솔루션의 연결 문자열이 SQL Server Express의 로컬 인스턴스를 가리키는지 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-137">The next step is to make sure that the connection strings in the Contact Manager solution point to your local instance of SQL Server Express.</span></span>

<span data-ttu-id="10a1a-138">**연결 문자열을 업데이트 하려면**</span><span class="sxs-lookup"><span data-stu-id="10a1a-138">**To update the connection strings**</span></span>

1. <span data-ttu-id="10a1a-139">Visual Studio 2010에서 Contact Manager 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-139">Open the Contact Manager solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="10a1a-140">**솔루션 탐색기** 창에서 프로젝트 **관리자. Mvc** 프로젝트를 확장 한 다음 web.config 노드를 두 번 **클릭 합니다.**</span><span class="sxs-lookup"><span data-stu-id="10a1a-140">In the **Solution Explorer** window, expand the **ContactManager.Mvc** project, and then double-click the **Web.config** node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="10a1a-141">프로젝트 관리자. n e t 프로젝트에는 두 개의 *web.config* 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-141">The ContactManager.Mvc project includes two *web.config* files.</span></span> <span data-ttu-id="10a1a-142">프로젝트 수준 파일을 편집 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-142">You need to edit the project-level file.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. <span data-ttu-id="10a1a-143">**ConnectionStrings** 요소에서 **applicationservices** 라는 연결 문자열이 로컬 ASP.NET 응용 프로그램 서비스 데이터베이스를 가리키는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-143">In the **connectionStrings** element, verify that the connection string named **ApplicationServices** points to your local ASP.NET application services database.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. <span data-ttu-id="10a1a-144">**솔루션 탐색기** 창에서 **연락처** 프로젝트를 확장 한 다음 web.config 노드를 두 번 **클릭 합니다.**</span><span class="sxs-lookup"><span data-stu-id="10a1a-144">In the **Solution Explorer** window, expand the **ContactManager.Service** project, and then double-click the **Web.config** node.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. <span data-ttu-id="10a1a-145">**ConnectionStrings** 요소 **에서 이름이 "." 인 연결**문자열에서 **데이터 원본** 속성이 SQL Server Express의 로컬 인스턴스로 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-145">In the **connectionStrings** element, in the connection string named **ContactManagerContext**, verify that the **Data Source** property is set to your local instance of SQL Server Express.</span></span> <span data-ttu-id="10a1a-146">연결 문자열에서 다른 항목을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-146">You don't need to change anything else in the connection string.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. <span data-ttu-id="10a1a-147">열려 있는 모든 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-147">Save all open files.</span></span>

<span data-ttu-id="10a1a-148">이제 로컬 컴퓨터에서 Contact Manager 솔루션을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-148">You should now be ready to run the Contact Manager solution on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="10a1a-149">응용 프로그램 서비스 데이터베이스를 먼저 만들지 않고 이러한 단계를 수행 하는 경우 ASP.NET는 처음으로 사용자를 만들려고 할 때 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-149">If you follow these steps without first creating an application services database, ASP.NET will create the database the first time you attempt to create a user.</span></span> <span data-ttu-id="10a1a-150">그러나 데이터베이스를 수동으로 만들면 지원 하려는 응용 프로그램 서비스 기능 집합을 훨씬 더 세부적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-150">However, manually creating the database gives you a lot more control over the application services feature set you want to support.</span></span>

<span data-ttu-id="10a1a-151">**Contact Manager 솔루션을 실행 하려면**</span><span class="sxs-lookup"><span data-stu-id="10a1a-151">**To run the Contact Manager solution**</span></span>

1. <span data-ttu-id="10a1a-152">Visual Studio 2010에서 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-152">In Visual Studio 2010, press F5.</span></span>
2. <span data-ttu-id="10a1a-153">Internet Explorer가 시작 되 고 Contact Manager ASP.NET MVC 3 응용 프로그램의 URL을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-153">Internet Explorer starts up and requests the URL of the Contact Manager ASP.NET MVC 3 application.</span></span> <span data-ttu-id="10a1a-154">기본적으로 응용 프로그램은 **모든 연락처** 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-154">By default, the application displays the **All Contacts** page.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. <span data-ttu-id="10a1a-155">몇 가지 연락처를 추가 하 고 응용 프로그램이 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-155">Add a few contacts, and then verify that the application works as expected.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. <span data-ttu-id="10a1a-156">`http://localhost:50114/Account/Register` (다른 포트에서 응용 프로그램을 호스트 하는 경우 URL 조정)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-156">Browse to `http://localhost:50114/Account/Register` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="10a1a-157">사용자 이름, 전자 메일 주소 및 암호를 추가 하 고 계정을 성공적으로 등록할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-157">Add a user name, email address, and password, and verify that you're able to register an account successfully.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. <span data-ttu-id="10a1a-158">`http://localhost:50114/Account/LogOn` (다른 포트에서 응용 프로그램을 호스트 하는 경우 URL 조정)로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-158">Browse to `http://localhost:50114/Account/LogOn` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="10a1a-159">방금 만든 계정을 사용 하 여 로그온 할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-159">Verify that you're able to log on using the account you just created.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. <span data-ttu-id="10a1a-160">Internet Explorer를 닫아 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-160">Close Internet Explorer to stop debugging.</span></span>

## <a name="conclusion"></a><span data-ttu-id="10a1a-161">결론</span><span class="sxs-lookup"><span data-stu-id="10a1a-161">Conclusion</span></span>

<span data-ttu-id="10a1a-162">이 시점에서 로컬 컴퓨터에서 실행 되도록 연락처 관리자 솔루션을 완전히 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-162">At this point, the Contact Manager solution should be fully configured to run on your local machine.</span></span> <span data-ttu-id="10a1a-163">이 자습서의 다른 항목을 수행할 때 솔루션을 참조로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-163">You can use the solution as a reference when you work through the other topics in this tutorial.</span></span>

<span data-ttu-id="10a1a-164">다음 항목인 [프로젝트 파일 이해](understanding-the-project-file.md)에서는 Contact Manager 솔루션 내에서 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="10a1a-164">The next topic, [Understanding the Project File](understanding-the-project-file.md), explains how you can use the custom Microsoft Build Engine (MSBuild) project files within the Contact Manager solution to control the deployment process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="10a1a-165">[이전](the-contact-manager-solution.md)
> [다음](understanding-the-project-file.md)</span><span class="sxs-lookup"><span data-stu-id="10a1a-165">[Previous](the-contact-manager-solution.md)
[Next](understanding-the-project-file.md)</span></span>
