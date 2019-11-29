---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: '1 부: 개요 및 프로젝트 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600323"
---
# <a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="a55af-102">1 부: 개요 및 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a55af-102">Part 1: Overview and Creating the Project</span></span>

<span data-ttu-id="a55af-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a55af-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="a55af-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="a55af-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="a55af-105">Entity Framework은 개체/관계형 매핑 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="a55af-106">코드의 도메인 개체를 관계형 데이터베이스의 엔터티에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="a55af-107">대부분의 경우에는 Entity Framework는 데이터베이스 계층에 대해 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="a55af-108">코드는 개체를 조작 하 고 변경 내용은 데이터베이스에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="a55af-109">자습서 정보</span><span class="sxs-lookup"><span data-stu-id="a55af-109">About the Tutorial</span></span>

<span data-ttu-id="a55af-110">이 자습서에서는 간단한 스토어 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="a55af-111">응용 프로그램에는 두 가지 주요 부분이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-111">There are two main parts to the application.</span></span> <span data-ttu-id="a55af-112">일반 사용자는 제품을 확인 하 고 주문을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="a55af-113">관리자는 제품을 생성, 삭제 또는 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="a55af-114">배울 기술</span><span class="sxs-lookup"><span data-stu-id="a55af-114">Skills You'll Learn</span></span>

<span data-ttu-id="a55af-115">학습할 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="a55af-116">ASP.NET Web API에서 Entity Framework를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="a55af-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="a55af-117">Node.js를 사용 하 여 동적 클라이언트 UI를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="a55af-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="a55af-118">웹 API에서 폼 인증을 사용 하 여 사용자를 인증 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="a55af-119">이 자습서는 자체 포함 되어 있지만 먼저 다음 자습서를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="a55af-120">첫 번째 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="a55af-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="a55af-121">CRUD 작업을 지 원하는 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="a55af-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="a55af-122">[ASP.NET MVC](../../../../mvc/index.md) 에 대 한 일부 지식이 도움이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="a55af-123">개요</span><span class="sxs-lookup"><span data-stu-id="a55af-123">Overview</span></span>

<span data-ttu-id="a55af-124">개략적인 수준에서 응용 프로그램의 아키텍처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="a55af-125">ASP.NET MVC는 클라이언트에 대 한 HTML 페이지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="a55af-126">ASP.NET Web API는 데이터에 대 한 CRUD 작업 (제품 및 주문)을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="a55af-127">Entity Framework는 Web C# API에 사용 되는 모델을 데이터베이스 엔터티로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="a55af-128">다음 다이어그램은 응용 프로그램의 다양 한 계층에서 도메인 개체를 표시 하는 방법을 보여 줍니다. 데이터베이스 계층, 개체 모델 및 마지막으로 HTTP를 통해 클라이언트에 데이터를 전송 하는 데 사용 되는 통신 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="a55af-129">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a55af-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="a55af-130">Visual Web Developer Express 또는 전체 버전의 Visual Studio를 사용 하 여 tutorial 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="a55af-131">**시작** 페이지에서 **새 프로젝트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="a55af-132">**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="a55af-133">**시각적 개체 C#** 에서 **웹**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="a55af-134">프로젝트 템플릿 목록에서 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="a55af-135">프로젝트 이름을 "제품 저장소"로 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="a55af-136">**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 을 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="a55af-137">"인터넷 응용 프로그램" 템플릿은 폼 인증을 지 원하는 ASP.NET MVC 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="a55af-138">지금 응용 프로그램을 실행 하는 경우 다음과 같은 몇 가지 기능이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="a55af-139">새 사용자는 오른쪽 위 모퉁이에 있는 "등록" 링크를 클릭 하 여 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="a55af-140">등록 된 사용자는 "로그인" 링크를 클릭 하 여 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="a55af-141">멤버 자격 정보는 자동으로 생성 되는 데이터베이스에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="a55af-142">ASP.NET MVC의 폼 인증에 대 한 자세한 내용은 [연습: ASP.NET mvc에서 폼 인증 사용](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a55af-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="a55af-143">CSS 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="a55af-143">Update the CSS File</span></span>

<span data-ttu-id="a55af-144">이 단계는 외관상 이지만 페이지를 이전 스크린샷 처럼 렌더링 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="a55af-145">솔루션 탐색기에서 Content 폴더를 확장 하 고 이름이 Site .css 인 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="a55af-146">다음 CSS 스타일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a55af-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="a55af-147">다음</span><span class="sxs-lookup"><span data-stu-id="a55af-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)
