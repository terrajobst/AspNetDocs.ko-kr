---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWIN을 사용 하 여 자체 호스트 하는 ASP.NET Web API-ASP.NET 4.x
author: rick-anderson
description: 콘솔 응용 프로그램에서 ASP.NET Web API를 호스트 하는 방법을 보여 주는 코드를 사용 하 여 자습서입니다.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: a67db0bd061846af2db3599e0843ed7c6a22db1e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59386517"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="eccaa-103">OWIN을 사용 하 여 자체 호스트 하는 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="eccaa-103">Use OWIN to Self-Host ASP.NET Web API</span></span> 


> <span data-ttu-id="eccaa-104">이 자습서에는 OWIN 자체 호스트 하는 Web API 프레임 워크를 사용 하 여 콘솔 응용 프로그램에서 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-104">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="eccaa-105">[Open Web Interface for.NET](http://owin.org) (OWIN).NET 웹 서버 및 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-105">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="eccaa-106">OWIN 이상적인 OWIN 자체 IIS 외부에서 사용자 고유의 프로세스에서 웹 응용 프로그램을 호스팅하는 서버에서 웹 응용 프로그램을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-106">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="eccaa-107">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="eccaa-107">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="eccaa-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="eccaa-108">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="eccaa-109">웹 API 5.2.7</span><span class="sxs-lookup"><span data-stu-id="eccaa-109">Web API 5.2.7</span></span>


> [!NOTE]
> <span data-ttu-id="eccaa-110">이 자습서에 대 한 전체 소스 코드를 찾을 수 있습니다 [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-110">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>


## <a name="create-a-console-application"></a><span data-ttu-id="eccaa-111">콘솔 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="eccaa-111">Create a console application</span></span>

<span data-ttu-id="eccaa-112">에 **파일** 메뉴에서 **새로 만들기**을 선택한 후 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-112">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="eccaa-113">**설치 됨**아래에 있는 **Visual C#** 선택 **Windows Desktop** 선택한 후 **콘솔 앱 (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="eccaa-113">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="eccaa-114">"OwinSelfhostSample" 프로젝트 이름을 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-114">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="eccaa-115">Web API 및 OWIN 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="eccaa-115">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="eccaa-116">**도구** 메뉴에서 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-116">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="eccaa-117">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-117">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="eccaa-118">이 WebAPI OWIN selfhost 패키지 및 모든 필수 OWIN 패키지가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-118">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="eccaa-119">Web API를 구성에 대 한 자체 호스트</span><span class="sxs-lookup"><span data-stu-id="eccaa-119">Configure Web API for self-host</span></span>

<span data-ttu-id="eccaa-120">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-120">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="eccaa-121">클래스 이름을 `Startup`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-121">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="eccaa-122">모두이 파일의 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-122">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="eccaa-123">Web API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="eccaa-123">Add a Web API controller</span></span>

<span data-ttu-id="eccaa-124">다음으로, Web API 컨트롤러 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-124">Next, add a Web API controller class.</span></span> <span data-ttu-id="eccaa-125">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-125">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="eccaa-126">클래스 이름을 `ValuesController`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-126">Name the class `ValuesController`.</span></span>

<span data-ttu-id="eccaa-127">모두이 파일의 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-127">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="eccaa-128">OWIN 호스트를 시작 하 고 HttpClient 사용 하 여 요청을 만듭니다</span><span class="sxs-lookup"><span data-stu-id="eccaa-128">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="eccaa-129">다음을 사용 하 여 모든 Program.cs 파일의 상용구 코드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-129">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="eccaa-130">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="eccaa-130">Run the application</span></span>

<span data-ttu-id="eccaa-131">Visual Studio에서 F5 키를 눌러 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-131">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="eccaa-132">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eccaa-132">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="eccaa-133">추가 자료</span><span class="sxs-lookup"><span data-stu-id="eccaa-133">Additional resources</span></span>

[<span data-ttu-id="eccaa-134">프로젝트 Katana 개요</span><span class="sxs-lookup"><span data-stu-id="eccaa-134">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="eccaa-135">Azure 작업자 역할에서 ASP.NET Web API 호스팅</span><span class="sxs-lookup"><span data-stu-id="eccaa-135">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
