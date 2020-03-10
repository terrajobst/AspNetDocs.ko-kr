---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: AJAX 컨트롤 도구 키트 시작 (VB) | Microsoft Docs
author: microsoft
description: AJAX 컨트롤 도구 키트 사용을 시작 하기 위해 알아야 하는 모든 내용을 알아보세요.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: ff614308555b31710b11f408e12e9a6fadbf98d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497141"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a><span data-ttu-id="c7549-103">AJAX 컨트롤 도구 키트 시작(VB)</span><span class="sxs-lookup"><span data-stu-id="c7549-103">Get Started with the AJAX Control Toolkit (VB)</span></span>

<span data-ttu-id="c7549-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="c7549-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c7549-105">AJAX 컨트롤 도구 키트 사용을 시작 하기 위해 알아야 하는 모든 내용을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="c7549-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="c7549-106">AJAX 컨트롤 도구 키트에는 ASP.NET 응용 프로그램에서 사용할 수 있는 30 개 이상의 무료 컨트롤이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="c7549-107">이 자습서에서는 AJAX 컨트롤 도구 키트를 다운로드 하 고 Visual Studio/Visual Web Developer Express 도구 상자에 toolkit 컨트롤을 추가 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="c7549-108">AJAX 컨트롤 도구 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="c7549-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="c7549-109">[AJAX 컨트롤 도구 키트](http://devexpress.com/act) 는 ASP.NET 커뮤니티와 ASP.NET 팀의 구성원이 개발한 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span>

<span data-ttu-id="c7549-110">[AJAX 컨트롤 도구 키트 다운로드 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c7549-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span></span>

<span data-ttu-id="c7549-111">**그림 01**: AJAX 컨트롤 도구 키트 다운로드 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="c7549-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span></span>

<span data-ttu-id="c7549-112">파일을 다운로드 한 후 파일의 차단을 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="c7549-113">파일을 마우스 오른쪽 단추로 클릭 하 고 속성을 선택한 다음 **차단 해제** 단추를 클릭 합니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="c7549-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="c7549-114">[AJAX 컨트롤 도구 키트 ZIP 파일 차단 해제 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c7549-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span></span>

<span data-ttu-id="c7549-115">**그림 02**: AJAX 컨트롤 도구 키트 ZIP 파일 차단 해제 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="c7549-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span></span>

<span data-ttu-id="c7549-116">파일의 차단을 해제 한 후 파일의 압축을 풀 수 있습니다. 파일을 마우스 오른쪽 단추로 클릭 하 고 **모두 추출** 메뉴 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="c7549-117">이제 도구 키트를 Visual Studio/Visual Web Developer 도구 상자에 추가할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="c7549-118">도구 상자에 AJAX 컨트롤 도구 키트 추가</span><span class="sxs-lookup"><span data-stu-id="c7549-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="c7549-119">AJAX 컨트롤 도구 키트를 사용 하는 가장 쉬운 방법은 Visual Studio/Visual Web Developer 도구 상자에 도구 키트를 추가 하는 것입니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="c7549-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="c7549-120">이렇게 하면 도구 키트 컨트롤을 사용 하려고 할 때 페이지로 끌어 놓기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="c7549-121">[![AJAX 컨트롤 도구 키트가 도구 상자에 표시 됩니다.](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c7549-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span></span>

<span data-ttu-id="c7549-122">**그림 03**: AJAX 컨트롤 도구 키트가 도구 상자에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="c7549-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span></span>

<span data-ttu-id="c7549-123">먼저 AJAX 컨트롤 도구 키트 탭을 도구 상자에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="c7549-124">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-124">Follow these steps.</span></span>

1. <span data-ttu-id="c7549-125">메뉴 옵션 파일, 새 웹 사이트를 선택 하 여 새 ASP.NET 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="c7549-126">솔루션 탐색기 창에서 default.aspx를 두 번 클릭 하 여 편집기에서 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="c7549-127">일반 탭 아래의 도구 상자를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가 탭** 을 선택 합니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="c7549-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="c7549-128">AJAX Control Toolkit 이라는 새 탭을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="c7549-129">[새 탭을 추가 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c7549-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span></span>

<span data-ttu-id="c7549-130">**그림 04**: 새 탭 추가 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="c7549-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span></span>

<span data-ttu-id="c7549-131">그런 다음 새 탭에 AJAX 컨트롤 도구 키트 컨트롤을 추가 해야 합니다. 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c7549-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="c7549-132">AJAX 컨트롤 도구 키트 탭 아래를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 항목 선택을 선택 합니다 **(그림 5 참조)** .</span><span class="sxs-lookup"><span data-stu-id="c7549-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="c7549-133">AJAX 컨트롤 도구 키트의 압축을 푼 위치로 이동 하 여 AjaxControlToolkit 어셈블리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="c7549-134">[도구 상자에 추가할 항목을 선택 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="c7549-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span></span>

<span data-ttu-id="c7549-135">**그림 05**: 도구 상자에 추가할 항목 선택 ([전체 크기 이미지를 보려면 클릭](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="c7549-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span></span>

<span data-ttu-id="c7549-136">이러한 단계를 완료 한 후 도구 상자에 모든 도구 키트 컨트롤이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="c7549-137">새 버전의 Toolkit로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="c7549-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="c7549-138">이전 버전의 도구 키트를 사용 중이 고 이제 이후 버전으로 이동 해야 하는 경우 권장 되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="c7549-139">이진 파일-AjaxControlToolkit 어셈블리의 이전 버전을 웹 사이트 Bin 폴더에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="c7549-140">도구 상자 항목-AJAX 컨트롤 도구 키트 탭을 삭제 하 고 위의 단계에 따라 AjaxControlToolkit 어셈블리의 새 버전으로 탭을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7549-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c7549-141">[이전](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [다음](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c7549-141">[Previous](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
[Next](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span></span>
