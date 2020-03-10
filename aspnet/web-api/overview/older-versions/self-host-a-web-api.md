---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 셀프 호스트 ASP.NET Web API 1 (C#)-ASP.NET 4.x
author: MikeWasson
description: 코드를 사용한 자습서 콘솔 응용 프로그램 내에서 web API를 호스트 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421373"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="4053a-103">셀프 호스트 ASP.NET Web API 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="4053a-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="4053a-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4053a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="4053a-105">이 자습서에서는 콘솔 응용 프로그램 내에서 web API를 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="4053a-106">ASP.NET Web API에는 IIS가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="4053a-107">자체 호스트 프로세스에서 web API를 자체 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-107">You can self-host a web API in your own host process.</span></span> 
> 
> <span data-ttu-id="4053a-108">**새 응용 프로그램은 OWIN를 사용 하 여 웹 API를 자체 호스트 해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4053a-108">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="4053a-109">[OWIN를 사용 하 여 자체 호스트 ASP.NET Web API 2를](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4053a-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4053a-110">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="4053a-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4053a-111">Web API 1</span><span class="sxs-lookup"><span data-stu-id="4053a-111">Web API 1</span></span>
> - <span data-ttu-id="4053a-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="4053a-112">Visual Studio 2012</span></span>

## <a name="create-the-console-application-project"></a><span data-ttu-id="4053a-113">콘솔 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="4053a-113">Create the Console Application Project</span></span>

<span data-ttu-id="4053a-114">Visual Studio를 시작 하 고 **시작** 페이지에서 **새 프로젝트** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="4053a-115">또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="4053a-116">**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="4053a-117">**시각적 개체 C#** 에서 **Windows**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="4053a-118">프로젝트 템플릿 목록에서 **콘솔 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="4053a-119">프로젝트 이름을 SelfHost&quot;로 &quot;하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="4053a-120">대상 프레임 워크 설정 (Visual Studio 2010)</span><span class="sxs-lookup"><span data-stu-id="4053a-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="4053a-121">Visual Studio 2010을 사용 하는 경우 대상 프레임 워크를 .NET Framework 4.0로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="4053a-122">기본적으로 프로젝트 템플릿은 [.Net Framework 클라이언트 프로필](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="4053a-123">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="4053a-124">**대상 프레임 워크** 드롭다운 목록에서 대상 프레임 워크를 .NET Framework 4.0로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="4053a-125">변경 내용을 적용 하 라는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="4053a-126">NuGet 패키지 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="4053a-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="4053a-127">NuGet 패키지 관리자는 non-ASP.NET 프로젝트에 웹 API 어셈블리를 추가 하는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="4053a-128">NuGet 패키지 관리자가 설치 되어 있는지 확인 하려면 Visual Studio에서 **도구** 메뉴를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="4053a-129">**Nuget 패키지 관리자**라는 메뉴 항목이 표시 되 면 Nuget 패키지 관리자가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="4053a-130">NuGet 패키지 관리자를 설치 하려면:</span><span class="sxs-lookup"><span data-stu-id="4053a-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="4053a-131">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="4053a-132">**도구** 메뉴에서 **확장 및 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="4053a-133">**확장 및 업데이트** 대화 상자에서 **온라인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="4053a-134">"NuGet 패키지 관리자"가 표시 되지 않으면 검색 상자에 "nuget 패키지 관리자"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="4053a-135">NuGet 패키지 관리자를 선택 하 고 **다운로드**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="4053a-136">다운로드가 완료 되 면을 설치 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="4053a-137">설치가 완료 되 면 Visual Studio를 다시 시작 하 라는 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="4053a-138">Web API NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="4053a-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="4053a-139">NuGet 패키지 관리자를 설치한 후 프로젝트에 웹 API 자체 호스트 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="4053a-140">**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="4053a-141">*참고*:이 메뉴 항목이 표시 되지 않으면 NuGet 패키지 관리자가 올바르게 설치 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="4053a-142">**솔루션용 NuGet 패키지 관리를 선택 합니다** .</span><span class="sxs-lookup"><span data-stu-id="4053a-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="4053a-143">**NugGet 패키지 관리** 대화 상자에서 **온라인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="4053a-144">검색 상자에 &quot;WebApi. SelfHost&quot;를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="4053a-145">ASP.NET Web API 셀프 호스트 패키지를 선택 하 고 **설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="4053a-146">패키지가 설치 된 후 **닫기** 를 클릭 하 여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="4053a-147">AspNetWebApi가 아닌 SelfHost 라는 패키지를 설치 해야 합니다. WebApi.</span><span class="sxs-lookup"><span data-stu-id="4053a-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="4053a-148">모델 및 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="4053a-148">Create the Model and Controller</span></span>

<span data-ttu-id="4053a-149">이 자습서에서는 [시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 자습서와 동일한 모델 및 컨트롤러 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="4053a-150">`Product`이라는 public 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="4053a-151">`ProductsController`이라는 public 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="4053a-152">**ApiController**에서이 클래스를 파생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="4053a-153">이 컨트롤러의 코드에 대 한 자세한 내용은 [초보자](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 를 위한 자습서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4053a-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="4053a-154">이 컨트롤러는 다음과 같은 세 가지 GET 작업을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="4053a-155">URI</span><span class="sxs-lookup"><span data-stu-id="4053a-155">URI</span></span> | <span data-ttu-id="4053a-156">Description</span><span class="sxs-lookup"><span data-stu-id="4053a-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4053a-157">/api/제품</span><span class="sxs-lookup"><span data-stu-id="4053a-157">/api/products</span></span> | <span data-ttu-id="4053a-158">모든 제품의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-158">Get a list of all products.</span></span> |
| <span data-ttu-id="4053a-159">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="4053a-159">/api/products/*id*</span></span> | <span data-ttu-id="4053a-160">ID로 제품을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-160">Get a product by ID.</span></span> |
| <span data-ttu-id="4053a-161">/api/products/? category =*category*</span><span class="sxs-lookup"><span data-stu-id="4053a-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="4053a-162">범주별로 제품 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="4053a-163">Web API 호스트</span><span class="sxs-lookup"><span data-stu-id="4053a-163">Host the Web API</span></span>

<span data-ttu-id="4053a-164">Program.cs 파일을 열고 다음 using 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="4053a-165">**Program** 클래스에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="4053a-166">필드 HTTP URL 네임 스페이스 예약 추가</span><span class="sxs-lookup"><span data-stu-id="4053a-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="4053a-167">이 응용 프로그램은 `http://localhost:8080/`를 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="4053a-168">기본적으로 특정 HTTP 주소를 수신 하려면 관리자 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="4053a-169">따라서 자습서를 실행할 때이 오류가 발생할 수 있습니다. "HTTP에서 URL http://+:8080/등록할 수 없습니다." 라는 두 가지 방법으로이 오류를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="4053a-170">관리자 권한으로 Visual Studio를 실행 하거나</span><span class="sxs-lookup"><span data-stu-id="4053a-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="4053a-171">Netsh.exe를 사용 하 여 계정에 URL을 예약할 수 있는 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="4053a-172">Netsh.exe를 사용 하려면 관리자 권한으로 명령 프롬프트를 열고 다음 명령을 입력 합니다. 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="4053a-173">여기서 *machine\username* 는 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="4053a-174">자체 호스팅을 완료 한 후에는 예약을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="4053a-175">클라이언트 응용 프로그램에서 Web API 호출 (C#)</span><span class="sxs-lookup"><span data-stu-id="4053a-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="4053a-176">Web API를 호출 하는 간단한 콘솔 응용 프로그램을 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="4053a-177">새 콘솔 응용 프로그램 프로젝트를 솔루션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="4053a-178">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **새 프로젝트 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="4053a-179">&quot;ClientApp&quot;라는 새 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="4053a-180">NuGet 패키지 관리자를 사용 하 여 ASP.NET Web API Core 라이브러리 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="4053a-181">도구 메뉴에서 **NuGet 패키지 관리자**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="4053a-182">**솔루션용 NuGet 패키지 관리를 선택 합니다** .</span><span class="sxs-lookup"><span data-stu-id="4053a-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="4053a-183">**NuGet 패키지 관리** 대화 상자에서 **온라인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="4053a-184">검색 상자에 &quot;WebApi&quot;을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="4053a-185">Microsoft ASP.NET Web API 클라이언트 라이브러리 패키지를 선택 하 고 **설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="4053a-186">SelfHost 프로젝트에 ClientApp에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="4053a-187">솔루션 탐색기에서 ClientApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="4053a-188">**참조 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="4053a-189">**참조 관리자** 대화 상자의 **솔루션**에서 **프로젝트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="4053a-190">SelfHost 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="4053a-191">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="4053a-192">클라이언트/프로그램 .cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="4053a-193">다음 **using** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="4053a-194">정적 **Httpclient** 인스턴스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="4053a-195">모든 제품을 나열 하 고, ID로 제품을 나열 하 고, 범주별로 제품을 나열 하려면 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="4053a-196">이러한 각 메서드는 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="4053a-197">**Httpclient. GetAsync** 를 호출 하 여 GET 요청을 적절 한 URI로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="4053a-198">**HttpResponseMessage. EnsureSuccessStatusCode**를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="4053a-199">HTTP 응답 상태가 오류 코드 인 경우이 메서드는 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="4053a-200">**Readasasync&lt;t&gt;** 를 호출 하 여 HTTP 응답에서 CLR 형식을 deserialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="4053a-201">이 메서드는 **시스템 .net. Http. HttpContentExtensions**에 정의 된 확장 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="4053a-202">**Getasync** 및 **readasasync** 메서드는 모두 비동기 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="4053a-203">비동기 작업을 나타내는 **작업** 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="4053a-204">**Result** 속성을 가져오면 작업이 완료 될 때까지 스레드가 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="4053a-205">비차단 호출을 수행 하는 방법을 비롯 하 여 HttpClient를 사용 하는 방법에 대 한 자세한 내용은 [.Net 클라이언트에서 WEB API 호출](../advanced/calling-a-web-api-from-a-net-client.md)을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4053a-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="4053a-206">이러한 메서드를 호출 하기 전에 HttpClient 인스턴스의 BaseAddress 속성을 "`http://localhost:8080`"로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="4053a-207">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="4053a-208">그러면 다음과 같이 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-208">This should output the following.</span></span> <span data-ttu-id="4053a-209">SelfHost 응용 프로그램을 먼저 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4053a-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
