---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: '8 부: 최종 페이지, 예외 처리 및 결론 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 8 부에서 연락처 페이지, 정보 페이지 및 예외를 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474341"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="fd06d-104">8 부: 최종 페이지, 예외 처리 및 결론</span><span class="sxs-lookup"><span data-stu-id="fd06d-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>

<span data-ttu-id="fd06d-105">만든 사람 [Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="fd06d-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="fd06d-106">Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="fd06d-107">ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="fd06d-108">이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="fd06d-109">8 부에서는 연락처 페이지, 정보 페이지 및 예외 처리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="fd06d-110">이는 계열의 결론입니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-110">This is the conclusion of the series.</span></span>

## <a id="_Toc260221680"></a><span data-ttu-id="fd06d-111">연락처 페이지 (ASP.NET에서 전자 메일 보내기)</span><span class="sxs-lookup"><span data-stu-id="fd06d-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="fd06d-112">ContactUs 라는 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="fd06d-113">디자이너를 사용 하 여 ToolkitScriptManager 및 AjaxControlToolkit의 편집기 컨트롤을 포함 하는 다음과 같은 특수 노트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxControlToolkit.</span></span> <span data-ttu-id="fd06d-114">.</span><span class="sxs-lookup"><span data-stu-id="fd06d-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="fd06d-115">"제출" 단추를 두 번 클릭 하 여 코드 뒤 파일에서 클릭 이벤트 처리기를 생성 하 고 연락처 정보를 전자 메일로 보내는 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="fd06d-116">이 코드를 사용 하려면 web.config 파일에 메일을 보내는 데 사용할 SMTP 서버를 지정 하는 항목을 구성 섹션에 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a><span data-ttu-id="fd06d-117">정보 페이지</span><span class="sxs-lookup"><span data-stu-id="fd06d-117">About Page</span></span>

<span data-ttu-id="fd06d-118">AboutUs 라는 페이지를 만들고 원하는 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a><span data-ttu-id="fd06d-119">전역 예외 처리기</span><span class="sxs-lookup"><span data-stu-id="fd06d-119">Global Exception Handler</span></span>

<span data-ttu-id="fd06d-120">마지막으로, 응용 프로그램 전체에서 예외가 throw 되 고 콜드에서 웹 응용 프로그램에 처리 되지 않은 예외가 발생 하는 예측할 수 없는 상황이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="fd06d-121">처리 되지 않은 예외가 웹 사이트 방문자에 게 표시 되는 것을 원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="fd06d-122">처리 되지 않은 사용자 환경 외에도 보안 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="fd06d-123">이 문제를 해결 하기 위해 전역 예외 처리기를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="fd06d-124">이렇게 하려면 Global.asax 파일을 열고 미리 생성 된 다음 이벤트 처리기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="fd06d-125">다음과 같이 응용 프로그램\_오류 처리기를 구현 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="fd06d-126">그런 다음, .aspx 이라는 페이지를 솔루션에 추가 하 고이 마크업 코드 조각을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="fd06d-127">이제 페이지\_Load 이벤트 처리기에서 요청 개체의 오류 메시지를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a><span data-ttu-id="fd06d-128">끝낼</span><span class="sxs-lookup"><span data-stu-id="fd06d-128">Conclusion</span></span>

<span data-ttu-id="fd06d-129">ASP.NET WebForms를 사용 하면 데이터베이스 액세스, 멤버 자격, AJAX 등의 복잡 한 웹 사이트를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="fd06d-130">매우 빠르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-130">pretty quickly.</span></span>

<span data-ttu-id="fd06d-131">이 자습서에서는 사용자 고유의 ASP.NET WebForms 응용 프로그램 빌드를 시작 하는 데 필요한 도구를 제공 하는 데 도움을 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="fd06d-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fd06d-132">이전</span><span class="sxs-lookup"><span data-stu-id="fd06d-132">Previous</span></span>](tailspin-spyworks-part-7.md)
