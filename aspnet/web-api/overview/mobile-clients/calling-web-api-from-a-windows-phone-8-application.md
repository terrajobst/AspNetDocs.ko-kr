---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: Windows Phone 8 응용 프로그램에서 Web API 호출 (C#)-ASP.NET 4.x
author: rmcmurray
description: '코드를 사용한 자습서: Windows Phone 8 응용 프로그램에 책 카탈로그를 제공 하는 ASP.NET 4.x에 ASP.NET Web API 응용 프로그램을 만듭니다.'
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498215"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="6098b-103">Windows Phone 8 애플리케이션에서 Web API 호출(C#)</span><span class="sxs-lookup"><span data-stu-id="6098b-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>

<span data-ttu-id="6098b-104">[Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="6098b-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="6098b-105">이 자습서에서는 Windows Phone 8 응용 프로그램에 책 카탈로그를 제공 하는 ASP.NET Web API 응용 프로그램으로 구성 되는 완전 한 종단 간 시나리오를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="6098b-106">개요</span><span class="sxs-lookup"><span data-stu-id="6098b-106">Overview</span></span>

<span data-ttu-id="6098b-107">ASP.NET Web API와 같은 RESTful 서비스는 서버 쪽 및 클라이언트 쪽 응용 프로그램에 대 한 아키텍처를 추상화 하 여 개발자를 위한 HTTP 기반 응용 프로그램 만들기를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="6098b-108">통신을 위한 전용 소켓 기반 프로토콜을 만드는 대신 웹 API 개발자는 응용 프로그램에 대 한 필수 HTTP 메서드 (예: GET, POST, PUT, DELETE)를 게시 하 고 클라이언트 응용 프로그램 개발자만을 사용 해야 합니다. 응용 프로그램에 필요한 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="6098b-109">이 종단 간 자습서에서는 Web API를 사용 하 여 다음 프로젝트를 만드는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="6098b-110">[이 자습서의 첫 번째 부분](#STEP1)에서는 책 카탈로그를 관리 하기 위한 모든 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업을 지 원하는 ASP.NET Web API 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="6098b-111">이 응용 프로그램은 MSDN의 [샘플 Xml 파일 (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) 을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="6098b-112">[이 자습서의 두 번째 부분](#STEP2)에서는 Web API 응용 프로그램에서 데이터를 검색 하는 대화형 Windows Phone 8 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="6098b-113">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="6098b-113">Prerequisites</span></span>

- <span data-ttu-id="6098b-114">Windows Phone 8 SDK가 설치 된 Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="6098b-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="6098b-115">Hyper-v가 설치 된 64 비트 시스템의 Windows 8 이상</span><span class="sxs-lookup"><span data-stu-id="6098b-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="6098b-116">추가 요구 사항 목록은 [WINDOWS PHONE SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) 다운로드 페이지의 *시스템 요구 사항* 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6098b-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="6098b-117">Web API와 로컬 시스템의 Windows Phone 8 프로젝트 간의 연결을 테스트 하려는 경우 테스트 환경을 설정 하려면 *[Windows Phone 8 에뮬레이터를 로컬 컴퓨터의 웹 Api 응용 프로그램에 연결](https://go.microsoft.com/fwlink/?LinkId=324014)* 문서의 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="6098b-118">1 단계: Web API 서 점 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6098b-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="6098b-119">이 종단 간 자습서의 첫 번째 단계는 모든 CRUD 작업을 지 원하는 Web API 프로젝트를 만드는 것입니다. 이 자습서의 [2 단계](#STEP2) 에서는이 솔루션에 Windows Phone 응용 프로그램 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="6098b-120">**Visual Studio 2013**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="6098b-121">**파일**, **새로 만들기**, **프로젝트**를 차례로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="6098b-122">**새 프로젝트** 대화 상자가 표시 되 면 **설치 됨**, **템플릿**, **C#시각적 개체**, **웹**을 차례로 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="6098b-123">확장 하려면 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-123">Click image to expand</span></span>                                                                |

4. <span data-ttu-id="6098b-124">**ASP.NET 웹 응용 프로그램**을 강조 표시 하 고 프로젝트 이름으로 서 **점** 을 입력 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="6098b-125">**새 ASP.NET 프로젝트** 대화 상자가 표시 되 면 **Web API** 템플릿을 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="6098b-126">확장 하려면 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-126">Click image to expand</span></span>                                                                |

6. <span data-ttu-id="6098b-127">Web API 프로젝트가 열리면 프로젝트에서 샘플 컨트롤러를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="6098b-128">솔루션 탐색기에서 **컨트롤러** 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="6098b-129">**ValuesController.cs** 파일을 마우스 오른쪽 단추로 클릭 한 다음 **삭제**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="6098b-130">삭제를 확인 하는 메시지가 표시 되 면 **확인** 을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="6098b-131">Web API 프로젝트에 XML 데이터 파일을 추가 합니다. 이 파일에는 서 점 카탈로그의 내용이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

   1. <span data-ttu-id="6098b-132">솔루션 탐색기에서 **App\_Data** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 항목**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
   2. <span data-ttu-id="6098b-133">**새 항목 추가** 대화 상자가 표시 되 면 **XML 파일** 템플릿을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
   3. <span data-ttu-id="6098b-134">**Books.xml**파일의 이름을 지정한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-134">Name the file **Books.xml**, and then click **Add**.</span></span>
   4. <span data-ttu-id="6098b-135">**Books.xml** 파일을 열면 파일의 코드를 MSDN의 sample **.xml** 파일에 있는 xml로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. <span data-ttu-id="6098b-136">XML 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-136">Save and close the XML file.</span></span>

8. <span data-ttu-id="6098b-137">웹 API 프로젝트에 서 점 모델을 추가 합니다. 이 모델은 응용 프로그램 응용 프로그램에 대 한 CRUD (만들기, 읽기, 업데이트 및 삭제) 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

   1. <span data-ttu-id="6098b-138">솔루션 탐색기에서 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **클래스**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   2. <span data-ttu-id="6098b-139">**새 항목 추가** 대화 상자가 표시 되 면 클래스 파일의 이름을 **BookDetails.cs**로 지정한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   3. <span data-ttu-id="6098b-140">**BookDetails.cs** 파일이 열리면 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. <span data-ttu-id="6098b-141">**BookDetails.cs** 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-141">Save and close the **BookDetails.cs** file.</span></span>

9. <span data-ttu-id="6098b-142">웹 작업 컨트롤러를 웹 API 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-142">Add the bookstore controller to the Web API project:</span></span>

   1. <span data-ttu-id="6098b-143">솔루션 탐색기에서 **컨트롤러** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **컨트롤러**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
   2. <span data-ttu-id="6098b-144">**스 캐 폴드 추가** 대화 상자가 표시 되 면 **Web API 2 컨트롤러-비어 있음**을 강조 표시 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
   3. <span data-ttu-id="6098b-145">**컨트롤러 추가** 대화 상자가 표시 되 면 컨트롤러 이름을 **bookscontroller**로 지정한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
   4. <span data-ttu-id="6098b-146">**BooksController.cs** 파일이 열리면 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. <span data-ttu-id="6098b-147">**BooksController.cs** 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-147">Save and close the **BooksController.cs** file.</span></span>

10. <span data-ttu-id="6098b-148">웹 API 응용 프로그램을 빌드하여 오류를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="6098b-149">2 단계: Windows Phone 8 서 점 카탈로그 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="6098b-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="6098b-150">이 종단 간 시나리오의 다음 단계는 Windows Phone 8 용 카탈로그 응용 프로그램을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="6098b-151">이 응용 프로그램은 기본 사용자 인터페이스에 대 한 *Windows Phone 데이터 바인딩된 앱* 템플릿을 사용 하며,이 자습서의 [1 단계](#STEP1) 에서 만든 웹 API 응용 프로그램을 데이터 원본으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="6098b-152">솔루션 탐색기에서의 서 **점** 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 프로젝트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="6098b-153">**새 프로젝트** 대화 상자가 표시 되 면 **설치 됨**, **C#시각적 개체**를 차례로 확장 한 다음 **Windows Phone**합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="6098b-154">**데이터 바인딩된 앱 Windows Phone**강조 표시 하 고 이름으로 **bookcatalog** 를 입력 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="6098b-155">Json.NET NuGet 패키지를 **Bookcatalog** 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="6098b-156">솔루션 탐색기에서 **Bookcatalog** 프로젝트에 대 한 **참조** 를 마우스 오른쪽 단추로 클릭 한 다음 **NuGet 패키지 관리**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="6098b-157">**NuGet 패키지 관리** 대화 상자가 표시 되 면 **온라인** 섹션을 확장 하 고 **nuget.org**를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="6098b-158">검색 필드에 **Json.NET** 를 입력 하 고 검색 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="6098b-159">검색 결과에서 **Json.NET** 를 강조 표시 하 고 **설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="6098b-160">설치가 완료 되 면 **닫기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="6098b-161">Bookdetails 프로젝트에 **Bookdetails** 모델 을 추가 합니다. 여기에는 클래스의 일반 모델 (:)이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

   1. <span data-ttu-id="6098b-162">솔루션 탐색기에서 **Bookcatalog** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **새 폴더**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
   2. <span data-ttu-id="6098b-163">새 폴더의 이름을 **모델**로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-163">Name the new folder **Models**.</span></span>
   3. <span data-ttu-id="6098b-164">솔루션 탐색기에서 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 클릭 한 다음 **클래스**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   4. <span data-ttu-id="6098b-165">**새 항목 추가** 대화 상자가 표시 되 면 클래스 파일의 이름을 **BookDetails.cs**로 지정한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   5. <span data-ttu-id="6098b-166">**BookDetails.cs** 파일이 열리면 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. <span data-ttu-id="6098b-167">**BookDetails.cs** 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-167">Save and close the **BookDetails.cs** file.</span></span>

6. <span data-ttu-id="6098b-168">**MainViewModel.cs** 클래스를 업데이트 하 여 서 점 웹 API 응용 프로그램과 통신 하는 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

   1. <span data-ttu-id="6098b-169">솔루션 탐색기에서 **Viewmodels** 폴더를 확장 한 다음 **MainViewModel.cs** 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
   2. <span data-ttu-id="6098b-170">**MainViewModel.cs** 파일이 열리면 파일의 코드를 다음으로 바꿉니다. `apiUrl` 상수 값을 Web API의 실제 URL로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. <span data-ttu-id="6098b-171">**MainViewModel.cs** 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-171">Save and close the **MainViewModel.cs** file.</span></span>

7. <span data-ttu-id="6098b-172">**Mainpage** 파일을 업데이트 하 여 응용 프로그램 이름을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

   1. <span data-ttu-id="6098b-173">솔루션 탐색기에서 **Mainpage .xaml** 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="6098b-174">**Mainpage .xaml** 파일을 열면 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. <span data-ttu-id="6098b-175">해당 줄을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-175">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. <span data-ttu-id="6098b-176">**Mainpage .xaml** 파일을 저장 한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-176">Save and close the **MainPage.xaml** file.</span></span>

8. <span data-ttu-id="6098b-177">**DetailsPage** 파일을 업데이트 하 여 표시 된 항목을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

   1. <span data-ttu-id="6098b-178">솔루션 탐색기에서 **DetailsPage** 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="6098b-179">**DetailsPage** 파일이 열리면 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. <span data-ttu-id="6098b-180">해당 줄을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-180">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. <span data-ttu-id="6098b-181">**DetailsPage** 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-181">Save and close the **DetailsPage.xaml** file.</span></span>

9. <span data-ttu-id="6098b-182">오류를 확인 하는 Windows Phone 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="6098b-183">3 단계: 종단 간 솔루션 테스트</span><span class="sxs-lookup"><span data-stu-id="6098b-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="6098b-184">이 자습서의 *전제 조건* 섹션에서 설명한 것 처럼 로컬 시스템에서 web api와 Windows Phone 8 프로젝트 간의 연결을 테스트할 때 테스트 환경을 설정 하려면 *[로컬 컴퓨터에서 Web api 응용 프로그램에 Windows Phone 8 에뮬레이터 연결](https://go.microsoft.com/fwlink/?LinkId=324014)* 문서에 설명 된 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="6098b-185">테스트 환경을 구성한 후에는 Windows Phone 응용 프로그램을 시작 프로젝트로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="6098b-186">이렇게 하려면 솔루션 탐색기에서 **Bookcatalog** 응용 프로그램을 강조 표시 하 고 **시작 프로젝트로 설정**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="6098b-187">확장 하려면 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-187">Click image to expand</span></span> |

<span data-ttu-id="6098b-188">F5 키를 누르면 Visual Studio에서 Windows Phone 에뮬레이터를 모두 시작 합니다 .이 에뮬레이터는 웹 API에서 응용 프로그램 데이터를 검색 하는 동안&quot; &quot;를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="6098b-189">확장 하려면 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-189">Click image to expand</span></span> |

<span data-ttu-id="6098b-190">모든 작업이 성공 하면 카탈로그가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="6098b-191">확장 하려면 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-191">Click image to expand</span></span> |

<span data-ttu-id="6098b-192">책 제목을 누르면 응용 프로그램에 책 설명이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="6098b-193">확장 하려면 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-193">Click image to expand</span></span> |

<span data-ttu-id="6098b-194">응용 프로그램이 Web API와 통신할 수 없는 경우 다음과 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="6098b-195">확장 하려면 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-195">Click image to expand</span></span> |

<span data-ttu-id="6098b-196">오류 메시지를 탭 하면 오류에 대 한 추가 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 <span data-ttu-id="6098b-197">확장 하려면 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6098b-197">Click image to expand</span></span>                                                                 |
