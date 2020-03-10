---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 폴더 권한 설정 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: 410525bb2e3f6e5a0be6d7d6b33fb3a40509041a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465065"
---
# <a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a><span data-ttu-id="e5f8d-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 폴더 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="e5f8d-103">ASP.NET Web Deployment using Visual Studio: Setting Folder Permissions</span></span>

<span data-ttu-id="e5f8d-104">만든 사람 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e5f8d-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="e5f8d-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="e5f8d-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="e5f8d-106">이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="e5f8d-107">계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="e5f8d-108">개요</span><span class="sxs-lookup"><span data-stu-id="e5f8d-108">Overview</span></span>

<span data-ttu-id="e5f8d-109">이 자습서에서는 응용 프로그램이 해당 폴더에 로그 파일을 만들 수 있도록 배포 된 웹 사이트의 *Elmah* 폴더에 대 한 폴더 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-109">In this tutorial, you set folder permissions for the *Elmah* folder in the deployed web site so that the application can create log files in that folder.</span></span>

<span data-ttu-id="e5f8d-110">Visual Studio 개발 서버 (Cassini) 또는 IIS Express를 사용 하 여 Visual Studio에서 웹 응용 프로그램을 테스트 하는 경우 응용 프로그램은 사용자의 id로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-110">When you test a web application in Visual Studio using the Visual Studio Development Server (Cassini) or IIS Express, the application runs under your identity.</span></span> <span data-ttu-id="e5f8d-111">사용자는 개발 컴퓨터의 관리자 이며 모든 폴더의 모든 파일에 대해 모든 작업을 수행할 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-111">You are most likely an administrator on your development computer and have full authority to do anything to any file in any folder.</span></span> <span data-ttu-id="e5f8d-112">그러나 응용 프로그램이 IIS에서 실행 되는 경우 사이트에 할당 된 응용 프로그램 풀에 대해 정의 된 id로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-112">But when an application runs under IIS, it runs under the identity defined for the application pool that the site is assigned to.</span></span> <span data-ttu-id="e5f8d-113">이는 일반적으로 권한이 제한 된 시스템 정의 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-113">This is typically a system-defined account that has limited permissions.</span></span> <span data-ttu-id="e5f8d-114">기본적으로 웹 응용 프로그램의 파일 및 폴더에 대 한 읽기 및 실행 권한이 있지만 쓰기 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-114">By default it has read and execute permissions on your web application's files and folders, but it doesn't have write access.</span></span>

<span data-ttu-id="e5f8d-115">응용 프로그램에서 파일을 만들거나 업데이트 하는 경우이 문제가 발생 합니다 .이는 웹 응용 프로그램에서 일반적으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-115">This becomes an issue if your application creates or updates files, which is a common need in web applications.</span></span> <span data-ttu-id="e5f8d-116">Contoso 대학 응용 프로그램에서 Elmah는 오류에 대 한 세부 정보를 저장 하기 위해 *elmah* 폴더에 XML 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-116">In the Contoso University application, Elmah creates XML files in the *Elmah* folder in order to save details about errors.</span></span> <span data-ttu-id="e5f8d-117">Elmah와 같은 항목을 사용 하지 않더라도 사이트에서 사용자가 파일을 업로드 하거나 사이트의 폴더에 데이터를 기록 하는 기타 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-117">Even if you don't use something like Elmah, your site might let users upload files or perform other tasks that write data to a folder in your site.</span></span>

<span data-ttu-id="e5f8d-118">미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 [문제 해결 페이지](troubleshooting.md)를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-118">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="test-error-logging-and-reporting"></a><span data-ttu-id="e5f8d-119">오류 로깅 및 보고 테스트</span><span class="sxs-lookup"><span data-stu-id="e5f8d-119">Test error logging and reporting</span></span>

<span data-ttu-id="e5f8d-120">응용 프로그램이 IIS에서 제대로 작동 하지 않는 방법을 확인 하려면 (Visual Studio에서 테스트 했을 경우에도) 일반적으로 Elmah에서 기록 되는 오류를 발생 시킨 다음 Elmah 오류 로그를 열어 세부 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-120">To see how the application doesn't work correctly in IIS (although it did when you tested it in Visual Studio), you can cause an error that would normally be logged by Elmah, and then open the Elmah error log to see the details.</span></span> <span data-ttu-id="e5f8d-121">Elmah가 XML 파일을 만들고 오류 정보를 저장할 수 없는 경우 빈 오류 보고서가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-121">If Elmah was unable to create an XML file and store the error details, you see an empty error report.</span></span>

<span data-ttu-id="e5f8d-122">브라우저를 열고 `http://localhost/ContosoUniversity`로 이동한 다음 *Studentsxxx*와 같은 잘못 된 URL을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-122">Open a browser and go to `http://localhost/ContosoUniversity`, and then request an invalid URL like *Studentsxxx.aspx*.</span></span> <span data-ttu-id="e5f8d-123">Web.config 파일의 `customErrors` 설정이 "RemoteOnly"이 고 IIS를 로컬로 실행 하므로 *Genericerrorpage .aspx* 페이지 대신 시스템 생성 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-123">You see a system-generated error page instead of the *GenericErrorPage.aspx* page because the `customErrors` setting in the Web.config file is "RemoteOnly" and you are running IIS locally:</span></span>

![HTTP 404 오류 페이지](setting-folder-permissions/_static/image1.png)

<span data-ttu-id="e5f8d-125">이제 *Elmah* 를 실행 하 여 오류 보고서를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-125">Now run *Elmah.axd* to see the error report.</span></span> <span data-ttu-id="e5f8d-126">관리자 계정 자격 증명 (&quot;admin&quot; 및 &quot;devpwd&quot;)을 사용 하 여 로그인 한 후에는 Elmah가 *elmah* 폴더에 XML 파일을 만들 수 없기 때문에 빈 오류 로그 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-126">After you log in with the administrator account credentials (&quot;admin&quot; and &quot;devpwd&quot;), you see an empty error log page because Elmah was unable to create an XML file in the *Elmah* folder:</span></span>

![오류 로그가 비어 있습니다.](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a><span data-ttu-id="e5f8d-128">Elmah 폴더에 대 한 쓰기 권한 설정</span><span class="sxs-lookup"><span data-stu-id="e5f8d-128">Set write permission on the Elmah folder</span></span>

<span data-ttu-id="e5f8d-129">폴더 권한은 수동으로 설정 하거나 배포 프로세스의 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-129">You can set folder permissions manually or you can make it an automatic part of the deployment process.</span></span> <span data-ttu-id="e5f8d-130">이러한 작업을 자동으로 수행 하려면 복잡 한 MSBuild 코드가 필요 합니다 .이 작업은 처음 배포할 때만 수행 하면 됩니다. 다음 단계에서는 수동으로 작업을 수행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-130">Making it automatic requires complex MSBuild code, and since you only have to do this the first time you deploy, the following steps how to do it manually.</span></span> <span data-ttu-id="e5f8d-131">배포 프로세스의이 부분을 만드는 방법에 대 한 자세한 내용은 Sayed Hashimi의 웹 게시에 대 한 [폴더 권한 설정](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) 블로그를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-131">(For information about how to make this part of the deployment process, see [Setting Folder Permissions on Web Publish](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) on Sayed Hashimi's blog.)</span></span>

1. <span data-ttu-id="e5f8d-132">**파일 탐색기**에서 *C:\inetpub\wwwroot\ContosoUniversity*로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-132">In **File Explorer**, navigate to *C:\inetpub\wwwroot\ContosoUniversity*.</span></span> <span data-ttu-id="e5f8d-133">*Elmah* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 **보안** 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-133">Right-click the *Elmah* folder, select **Properties**, and then select the **Security** tab.</span></span>
2. <span data-ttu-id="e5f8d-134">**편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-134">Click **Edit**.</span></span>
3. <span data-ttu-id="e5f8d-135">**Elmah에 대 한 사용 권한** 대화 상자에서 **DefaultAppPool**을 선택 하 고 **허용** 열에서 **쓰기** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-135">In the **Permissions for Elmah** dialog box, select **DefaultAppPool**, and then select the **Write** check box in the **Allow** column.</span></span>

    ![ELMAH 폴더에 대 한 사용 권한](setting-folder-permissions/_static/image3.png)

    <span data-ttu-id="e5f8d-137">**그룹 또는 사용자 이름** 목록에 **DefaultAppPool** 가 표시 되지 않으면이 자습서에 지정 된 것과 다른 방법을 사용 하 여 컴퓨터에서 IIS 및 ASP.NET 4를 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-137">(If you don't see **DefaultAppPool** in the **Group or user names** list, you probably used some other method than the one specified in this tutorial to set up IIS and ASP.NET 4 on your computer.</span></span> <span data-ttu-id="e5f8d-138">이 경우 Contoso 대학 응용 프로그램에 할당 된 응용 프로그램 풀에서 사용 되는 id를 확인 하 고 해당 id에 대 한 쓰기 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-138">In that case, find out what identity is used by the application pool assigned to the Contoso University application, and grant write permission to that identity.</span></span> <span data-ttu-id="e5f8d-139">이 자습서의 끝부분에 있는 응용 프로그램 풀 id에 대 한 링크를 참조 하세요.) 두 대화 상자에서 **확인을** 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-139">See the links about application pool identities at the end of this tutorial.) Click **OK** in both dialog boxes.</span></span>

## <a name="retest-error-logging-and-reporting"></a><span data-ttu-id="e5f8d-140">오류 로깅 및 보고 다시 테스트</span><span class="sxs-lookup"><span data-stu-id="e5f8d-140">Retest error logging and reporting</span></span>

<span data-ttu-id="e5f8d-141">동일한 방식으로 오류를 다시 발생 시켜 테스트 합니다 (잘못 된 URL 요청) 하 고 **오류 로그** 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-141">Test by causing an error again in the same way (request a bad URL) and run the **Error Log** page.</span></span> <span data-ttu-id="e5f8d-142">이번에는 페이지에 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-142">This time the error appears on the page.</span></span>

![ELMAH 오류 로그 페이지](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a><span data-ttu-id="e5f8d-144">요약</span><span class="sxs-lookup"><span data-stu-id="e5f8d-144">Summary</span></span>

<span data-ttu-id="e5f8d-145">이제 Contoso 대학이 로컬 컴퓨터의 IIS에서 올바르게 작동 하는 데 필요한 모든 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-145">You have now completed all of the tasks necessary to get Contoso University working correctly in IIS on your local computer.</span></span> <span data-ttu-id="e5f8d-146">다음 자습서에서는 Azure에 배포 하 여 사이트를 공개적으로 사용할 수 있도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-146">In the next tutorial, you will make the site publicly available by deploying it to Azure.</span></span>

## <a name="more-information"></a><span data-ttu-id="e5f8d-147">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="e5f8d-147">More information</span></span>

<span data-ttu-id="e5f8d-148">이 예제에서 Elmah가 로그 파일을 저장할 수 없는 이유는 매우 명확 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-148">In this example, the reason why Elmah was unable to save log files was fairly obvious.</span></span> <span data-ttu-id="e5f8d-149">문제의 원인이 명확 하지 않은 경우에 IIS 추적을 사용할 수 있습니다. IIS.net 사이트에서 [IIS 7에서 추적을 사용 하 여 실패 한 요청 문제 해결](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-149">You can use IIS tracing in cases where the cause of the problem is not so obvious; see [Troubleshooting Failed Requests Using Tracing in IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) on the IIS.net site.</span></span>

<span data-ttu-id="e5f8d-150">응용 프로그램 풀 id에 대 한 사용 권한을 부여 하는 방법에 대 한 자세한 내용은 IIS.net 사이트의 [파일 시스템 acl을 통해 IIS의](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) [응용 프로그램 풀 Id](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) 및 보안 콘텐츠를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e5f8d-150">For more information about how to grant permissions to application pool identities, see [Application Pool Identities](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) and [Secure Content in IIS Through File System ACLs](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) on the IIS.net site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e5f8d-151">[이전](deploying-to-iis.md)
> [다음](deploying-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="e5f8d-151">[Previous](deploying-to-iis.md)
[Next](deploying-to-production.md)</span></span>
