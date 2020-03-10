---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: ASP.NET MVC 1.0 응용 프로그램을 ASP.NET MVC 2로 업그레이드 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 ASP.NET MVC 1.0 응용 프로그램을 사용 하 여 수동으로 및 마법사를 사용 하 여 ASP.NET MVC 2로 업그레이드 하는 방법을 설명 합니다. 이 문서는 d ...에도 제공 됩니다.
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517301"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a><span data-ttu-id="52ad9-104">ASP.NET MVC 1.0 애플리케이션을 ASP.NET MVC 2로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="52ad9-104">Upgrading an ASP.NET MVC 1.0 Application to ASP.NET MVC 2</span></span>

> <span data-ttu-id="52ad9-105">이 문서에서는 ASP.NET MVC 1.0 응용 프로그램을 사용 하 여 수동으로 및 마법사를 사용 하 여 ASP.NET MVC 2로 업그레이드 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-105">This document describes both how to upgrade manually and with a wizard an ASP.NET MVC 1.0 Application to ASP.NET MVC 2.</span></span> <span data-ttu-id="52ad9-106">이 문서도 [다운로드할](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-106">This document is also available for [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span></span>

## <a name="introduction"></a><span data-ttu-id="52ad9-107">소개</span><span class="sxs-lookup"><span data-stu-id="52ad9-107">Introduction</span></span>

<span data-ttu-id="52ad9-108">ASP.NET MVC 2는 동일한 서버에 ASP.NET MVC 1.0와 나란히 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-108">ASP.NET MVC 2 can be installed side by side with ASP.NET MVC 1.0 on the same server.</span></span> <span data-ttu-id="52ad9-109">이를 통해 응용 프로그램 개발자는 ASP.NET MVC 1.0 응용 프로그램을 ASP.NET MVC 2로 업그레이드할 시기를 유연 하 게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-109">This gives application developers flexibility in choosing when to upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2.</span></span>

<span data-ttu-id="52ad9-110">Visual Studio 2010에는 Visual Studio 2008로 빌드된 기존 ASP.NET MVC 1.0 프로젝트를 ASP.NET MVC 2로 업그레이드 하는 마법사가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-110">Visual Studio 2010 includes a wizard that upgrades existing ASP.NET MVC 1.0 projects built with Visual Studio 2008 to ASP.NET MVC 2.</span></span> <span data-ttu-id="52ad9-111">업그레이드 마법사는 Visual Studio 2010에서 ASP.NET MVC 1.0 프로젝트를 열어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-111">The upgrade wizard is initiated by opening an ASP.NET MVC 1.0 project in Visual Studio 2010.</span></span>

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a><span data-ttu-id="52ad9-112">ASP.NET MVC 1.0에 대 한 업그레이드 마법사 (Visual Studio 2008 SP1)</span><span class="sxs-lookup"><span data-stu-id="52ad9-112">Upgrade Wizard for ASP.NET MVC 1.0 on Visual Studio 2008 SP1</span></span>

<span data-ttu-id="52ad9-113">Visual Studio 2008 s p 1에서 ASP.NET MVC 1.0 응용 프로그램을 ASP.NET MVC 2로 업그레이드 하려면 지원 되지 않는 (지원 되지 않는) MvcAppConverter 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-113">To upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2 in Visual Studio 2008 SP1, use the (unsupported) MvcAppConverter application.</span></span> <span data-ttu-id="52ad9-114">다음 URL에서이 응용 프로그램을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-114">You can download this application from the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a><span data-ttu-id="52ad9-115">ASP.NET MVC 1.0 프로젝트 수동 업그레이드</span><span class="sxs-lookup"><span data-stu-id="52ad9-115">Manually Upgrading an ASP.NET MVC 1.0 Project</span></span>

<span data-ttu-id="52ad9-116">기존 ASP.NET MVC 1.0 응용 프로그램을 버전 2로 수동으로 업그레이드 하려면 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-116">To manually upgrade an existing ASP.NET MVC 1.0 application to version 2, follow these steps:</span></span>

1. <span data-ttu-id="52ad9-117">기존 프로젝트의 백업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-117">Make a backup of the existing project.</span></span>
2. <span data-ttu-id="52ad9-118">텍스트 편집기에서 프로젝트 파일 (.csproj 또는 .vbproj 파일 확장명을 가진 파일)을 열고 ProjectTypeGuid 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-118">In a text editor, open the project file (the file with the .csproj or .vbproj file extension) and find the ProjectTypeGuid element.</span></span> <span data-ttu-id="52ad9-119">해당 요소의 값으로 GUID {603c0e0b-db56-11dc-be95-000d561079b0}을 {F85E285D-A4E0-4152-9332-AB1D724D3325}로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-119">As the value of that element, replace the GUID {603c0e0b-db56-11dc-be95-000d561079b0} with {F85E285D-A4E0-4152-9332-AB1D724D3325}.</span></span> <span data-ttu-id="52ad9-120">완료 되 면 해당 요소의 값은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-120">When you are done, the value of that element should be as follows:</span></span> 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. <span data-ttu-id="52ad9-121">웹 응용 프로그램 루트 폴더에서 web.config 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-121">In the Web application root folder, edit the Web.config file.</span></span> <span data-ttu-id="52ad9-122">System.web, Version = 1.0.0.0을 검색 하 고 모든 인스턴스를 System.web. Mvc, Version = 2.0.0.0으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-122">Search for System.Web.Mvc, Version=1.0.0.0 and replace all instances with System.Web.Mvc, Version=2.0.0.0.</span></span>
4. <span data-ttu-id="52ad9-123">Views 폴더에 있는 web.config 파일에 대해 이전 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-123">Repeat the previous step for the Web.config file located in the Views folder.</span></span>
5. <span data-ttu-id="52ad9-124">Visual Studio를 사용 하 여 프로젝트를 열고 **솔루션 탐색기**에서 **참조** 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-124">Open the project using Visual Studio, and in **Solution Explorer**, expand the **References** node.</span></span> <span data-ttu-id="52ad9-125">버전 1.0 어셈블리를 가리키는 System.web에 대 한 참조를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-125">Delete the reference to System.Web.Mvc (which points to the version 1.0 assembly).</span></span> <span data-ttu-id="52ad9-126">System.web에 대 한 참조를 추가 합니다 (v 2.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="52ad9-126">Add a reference to System.Web.Mvc (v2.0.0.0).</span></span>
6. <span data-ttu-id="52ad9-127">구성을 섹션의 응용 프로그램 루트에 있는 web.config 파일에 다음 bindingRedirect 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-127">Add the following bindingRedirect element to the Web.config file in the application root under the configuraton section:</span></span>   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. <span data-ttu-id="52ad9-128">비어 있는 새 ASP.NET MVC 2 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-128">Create a new empty ASP.NET MVC 2 application.</span></span> <span data-ttu-id="52ad9-129">새 응용 프로그램의 Scripts 폴더에 있는 파일을 기존 응용 프로그램의 Scripts 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-129">Copy the files from the Scripts folder of the new application into the Scripts folder of the existing application.</span></span>
8. <span data-ttu-id="52ad9-130">기존 applicationâ s CSS 파일을 사이트 .css 파일의 CSS 스타일 정의로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-130">Update the existing applicationâ€™s CSS file with the CSS style definitions in the Site.css file.</span></span>
9. <span data-ttu-id="52ad9-131">응용 프로그램을 컴파일하고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ad9-131">Compile the application and run it.</span></span> <span data-ttu-id="52ad9-132">오류가 발생 하는 경우 [ASP.NET MVC 2의 새로운 기능](https://go.microsoft.com/fwlink/?LinkID=185038) 페이지의 주요 변경 내용 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="52ad9-132">If any errors occur, refer to the Breaking Changes section of the [What's New in ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) page.</span></span>
