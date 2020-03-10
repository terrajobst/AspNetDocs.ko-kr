---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: '방법: MVC 응용 프로그램에 대 한 사용자 지정 HTML 도우미 만들기 | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서 Chris Pel는 MVC 응용 프로그램의 표준 집합에서 사용할 수 없는 사용자 지정 HtmlHelper를 만드는 방법을 보여 줍니다. 먼저 샘플 MVC의
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450479"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="6480f-105">방법: MVC 응용 프로그램에 대 한 사용자 지정 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="6480f-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>

<span data-ttu-id="6480f-106">사람- [Chris pel](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="6480f-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="6480f-107">이 비디오에서 Chris Pel는 MVC 응용 프로그램의 표준 집합에서 사용할 수 없는 사용자 지정 HtmlHelper를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6480f-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="6480f-108">먼저 샘플 MVC 응용 프로그램을 데모 컨트롤러 및 뷰를 사용 하 여 만들어 사용자 지정 HtmlHelper를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6480f-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="6480f-109">그런 다음 사용자 지정 HtmlHelper의 구현을 나타내는 확장 메서드인 public 함수를 사용 하 여 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6480f-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="6480f-110">사용자 지정 도우미는 페이지에서 `<img>` 태그를 만드는 데 사용할 수 있으며, 이미지 태그의 id, url 및 대체 텍스트를 비롯 한 여러 인바운드 매개 변수를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6480f-110">The custom helper is for creating `<img>` tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="6480f-111">그런 다음 지정 된 정보를 사용 하 여 완료 된 `<img>` 태그를 반환 하기 위해 논리를 함수에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6480f-111">The logic is then added to the function for returning the completed `<img>` tag with the specified information.</span></span> <span data-ttu-id="6480f-112">그런 다음 데모 페이지에서 사용자 지정 HtmlHelper를 사용 하 여 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6480f-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="6480f-113">마지막으로, 다양 한 `<img>` 태그를 보다 쉽게 만들 수 있도록 유연성을 제공 하는 여러 생성자 재정의를 포함 하도록 사용자 지정 HtmlHelper가 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6480f-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different `<img>` tags.</span></span>

[<span data-ttu-id="6480f-114">&#9654;비디오 보기 (18 분)</span><span class="sxs-lookup"><span data-stu-id="6480f-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="6480f-115">[이전](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [다음](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="6480f-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>
