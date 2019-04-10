---
uid: web-api/overview/older-versions/self-host-a-web-api
title: ASP.NET Web API 1 자체 호스팅 (C#)-ASP.NET 4.x
author: MikeWasson
description: 코드를 사용 하 여 자습서에는 콘솔 응용 프로그램 내에서 web API를 호스트 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7c73bf4734f8ed8a1bf93595c0847f611ad9cc15
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59409605"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="1fed8-103">자체 호스팅 ASP.NET Web API 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="1fed8-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="1fed8-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1fed8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="1fed8-105">이 자습서에서는 콘솔 응용 프로그램 내에서 web API를 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="1fed8-106">ASP.NET Web API에 IIS를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="1fed8-107">사용자 고유의 호스트 프로세스에서 web API를 자체 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-107">You can self-host a web API in your own host process.</span></span> 
> 
> **<span data-ttu-id="1fed8-108">새 응용 프로그램 자체 호스트 하는 Web API OWIN을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-108">New applications should use OWIN to self-host Web API.</span></span>** <span data-ttu-id="1fed8-109">참조 [OWIN을 사용 하 여 ASP.NET Web API 2 자체 호스팅에](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1fed8-110">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="1fed8-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="1fed8-111">Web API 1</span><span class="sxs-lookup"><span data-stu-id="1fed8-111">Web API 1</span></span>
> - <span data-ttu-id="1fed8-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1fed8-112">Visual Studio 2012</span></span>


## <a name="create-the-console-application-project"></a><span data-ttu-id="1fed8-113">콘솔 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="1fed8-113">Create the Console Application Project</span></span>

<span data-ttu-id="1fed8-114">Visual Studio를 시작 하 고 선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="1fed8-115">또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="1fed8-116">에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="1fed8-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="1fed8-117">아래 **Visual C#** 를 선택 **Windows**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="1fed8-118">프로젝트 템플릿 목록에서 선택 **콘솔 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="1fed8-119">프로젝트 이름을 &quot;SelfHost&quot; 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="1fed8-120">대상 프레임 워크 (Visual Studio 2010) 설정</span><span class="sxs-lookup"><span data-stu-id="1fed8-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="1fed8-121">Visual Studio 2010을 사용 하는 경우.NET Framework 4.0 대상 프레임 워크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="1fed8-122">(기본적으로 프로젝트 템플릿의 대상 합니다 [.NET Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span><span class="sxs-lookup"><span data-stu-id="1fed8-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="1fed8-123">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="1fed8-124">에 **대상 프레임 워크** 드롭다운 목록에서.NET Framework 4.0 대상 프레임 워크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="1fed8-125">변경 내용을 적용 하 라는 메시지가 표시를 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="1fed8-126">NuGet 패키지 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="1fed8-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="1fed8-127">NuGet 패키지 관리자는 비 ASP.NET 프로젝트에 어셈블리를 웹 API를 추가 하려면 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="1fed8-128">NuGet 패키지 관리자가 설치 되어 있는지를 확인 하려면 클릭 합니다 **도구** Visual Studio의 메뉴.</span><span class="sxs-lookup"><span data-stu-id="1fed8-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="1fed8-129">항목 이라는 메뉴가 나타나면 **NuGet 패키지 관리자**, NuGet 패키지 관리자를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="1fed8-130">NuGet 패키지 관리자를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="1fed8-131">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="1fed8-132">**도구** 메뉴에서 **확장 및 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="1fed8-133">에 **확장 및 업데이트** 대화 상자에서 **Online**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="1fed8-134">"NuGet 패키지 관리자"를 보이지 않으면 검색 상자에 "nuget 패키지 관리자"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="1fed8-135">NuGet 패키지 관리자를 선택 하 고 클릭 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="1fed8-136">다운로드가 완료 되 면 설치를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="1fed8-137">설치가 완료 되 면 Visual Studio를 다시 시작 하 라는 메시지가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="1fed8-138">웹 API NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="1fed8-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="1fed8-139">NuGet 패키지 관리자를 설치한 후 웹 API 여 패키지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="1fed8-140">**도구** 메뉴에서 **NuGet 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="1fed8-141">*참고*: 경우 하면이 메뉴가 표시 되지 않으면이 항목을 해당 NuGet 패키지 관리자를 제대로 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="1fed8-142">선택 **솔루션용 NuGet 패키지 관리**</span><span class="sxs-lookup"><span data-stu-id="1fed8-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="1fed8-143">에 **NugGet 패키지 관리** 대화 상자에서 **Online**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="1fed8-144">검색 상자에 입력 &quot;Microsoft.AspNet.WebApi.SelfHost&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="1fed8-145">ASP.NET 웹 API 자체 호스트 패키지를 선택 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="1fed8-146">패키지를 설치한 후 클릭 **닫습니다** 는 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="1fed8-147">Microsoft.AspNet.WebApi.SelfHost, 없습니다 AspNetWebApi.SelfHost 라는 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="1fed8-148">모델 및 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="1fed8-148">Create the Model and Controller</span></span>

<span data-ttu-id="1fed8-149">이 자습서와 동일한 모델 및 컨트롤러 클래스를 사용 합니다 [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="1fed8-150">라는 공용 클래스를 추가 `Product`합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="1fed8-151">라는 공용 클래스를 추가 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="1fed8-152">이 클래스를 파생 **System.Web.Http.ApiController**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="1fed8-153">이 컨트롤러의 코드에 대 한 자세한 내용은 참조는 [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="1fed8-154">이 컨트롤러 3 개의 가져오기 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="1fed8-155">URI</span><span class="sxs-lookup"><span data-stu-id="1fed8-155">URI</span></span> | <span data-ttu-id="1fed8-156">설명</span><span class="sxs-lookup"><span data-stu-id="1fed8-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1fed8-157">api 제품</span><span class="sxs-lookup"><span data-stu-id="1fed8-157">/api/products</span></span> | <span data-ttu-id="1fed8-158">모든 제품의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-158">Get a list of all products.</span></span> |
| <span data-ttu-id="1fed8-159">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="1fed8-159">/api/products/*id*</span></span> | <span data-ttu-id="1fed8-160">제품 id 가져오기</span><span class="sxs-lookup"><span data-stu-id="1fed8-160">Get a product by ID.</span></span> |
| <span data-ttu-id="1fed8-161">/api/products/?category=*category*</span><span class="sxs-lookup"><span data-stu-id="1fed8-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="1fed8-162">범주별으로 제품의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="1fed8-163">Web API 호스팅</span><span class="sxs-lookup"><span data-stu-id="1fed8-163">Host the Web API</span></span>

<span data-ttu-id="1fed8-164">Program.cs 파일을 열고 다음 코드를 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="1fed8-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="1fed8-165">다음 코드를 추가 합니다 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="1fed8-166">(선택 사항) HTTP URL Namespace 예약을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="1fed8-167">이 응용 프로그램에서 수신 하 `http://localhost:8080/`합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="1fed8-168">기본적으로 특정 HTTP 주소에서 수신 대기 하려면 관리자 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="1fed8-169">따라서이 자습서를 실행 하면이 오류가 발생할 수 있습니다. "HTTP URL을 등록 하지 못했습니다 http://+:8080/" 두 가지 방법으로이 오류를 방지 하려면:</span><span class="sxs-lookup"><span data-stu-id="1fed8-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="1fed8-170">관리자 권한으로 Visual Studio를 실행 하거나</span><span class="sxs-lookup"><span data-stu-id="1fed8-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="1fed8-171">URL 예약에 사용자 계정 권한을 부여 하려면 Netsh.exe를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="1fed8-172">Netsh.exe를 사용 하려면 관리자 권한으로 명령 프롬프트를 열고 및 명령 다음 명령을 입력 합니다.:</span><span class="sxs-lookup"><span data-stu-id="1fed8-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="1fed8-173">여기서 \*컴퓨터 \* 는 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="1fed8-174">자체 호스팅 완료 되 면 예약을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="1fed8-175">클라이언트 응용 프로그램 (C#)에서 웹 API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="1fed8-176">Web API를 호출 하는 간단한 콘솔 응용 프로그램을 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="1fed8-177">새 콘솔 응용 프로그램 프로젝트를 솔루션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="1fed8-178">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **새 프로젝트 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="1fed8-179">라는 새 콘솔 응용 프로그램을 만듭니다 &quot;ClientApp&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="1fed8-180">NuGet 패키지 관리자를 사용 하 여 ASP.NET 웹 API Core 라이브러리 패키지를 추가 하려면:</span><span class="sxs-lookup"><span data-stu-id="1fed8-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="1fed8-181">도구 메뉴에서 선택 **NuGet 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="1fed8-182">선택 **솔루션용 NuGet 패키지 관리**</span><span class="sxs-lookup"><span data-stu-id="1fed8-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="1fed8-183">에 **NuGet 패키지 관리** 대화 상자에서 **Online**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="1fed8-184">검색 상자에 입력 &quot;Microsoft.AspNet.WebApi.Client&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="1fed8-185">Microsoft ASP.NET 웹 API 클라이언트 라이브러리 패키지를 선택 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="1fed8-186">ClientApp에 SelfHost 프로젝트에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="1fed8-187">솔루션 탐색기에서 ClientApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="1fed8-188">**참조 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="1fed8-189">에 **참조 관리자** 대화 상자 아래에 있는 **솔루션**를 선택 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="1fed8-190">SelfHost 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="1fed8-191">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="1fed8-192">Client/Program.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="1fed8-193">다음을 추가 합니다 **를 사용 하 여** 문:</span><span class="sxs-lookup"><span data-stu-id="1fed8-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="1fed8-194">추가 정적 **HttpClient** 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="1fed8-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="1fed8-195">모든 제품 ID 기준으로 제품 목록 및 목록 제품 범주별으로 나열 하려면 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="1fed8-196">이러한 메서드는 각각 동일한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="1fed8-197">호출 **HttpClient.GetAsync** 적합 한 URI에 GET 요청을 보내도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="1fed8-198">호출 **HttpResponseMessage.EnsureSuccessStatusCode**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="1fed8-199">이 메서드는 HTTP 응답 상태 오류 코드 이면 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="1fed8-200">호출 **ReadAsAsync&lt;T&gt;**  를 HTTP 응답에서 CLR 형식을 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="1fed8-201">이 메서드는 확장 메서드를 정의 **System.Net.Http.HttpContentExtensions**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="1fed8-202">합니다 **GetAsync** 하 고 **ReadAsAsync** 메서드는 둘 다 비동기 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="1fed8-203">돌아왔을 **태스크** 비동기 작업을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="1fed8-204">시작 합니다 **결과** 속성 작업이 완료 될 때까지 스레드를 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="1fed8-205">비차단 호출을 수행 하는 방법을 비롯 한 HttpClient를 사용 하는 방법에 대 한 자세한 내용은 참조 [Web API에서는.NET 클라이언트 호출](../advanced/calling-a-web-api-from-a-net-client.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="1fed8-206">이러한 메서드를 호출 하기 전에 HttpClient 인스턴스에서 BaseAddress 속성 설정 "`http://localhost:8080`"입니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="1fed8-207">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="1fed8-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="1fed8-208">다음 출력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fed8-208">This should output the following.</span></span> <span data-ttu-id="1fed8-209">(SelfHost 응용 프로그램을 먼저 실행 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1fed8-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
