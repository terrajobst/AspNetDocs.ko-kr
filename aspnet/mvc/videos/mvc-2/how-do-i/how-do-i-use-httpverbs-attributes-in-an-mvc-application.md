---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-use-httpverbs-attributes-in-an-mvc-application
title: '방법: MVC 응용 프로그램에서 HttpVerbs 특성 사용 | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서 Chris Pel는 HttpVerbs 특성을 사용 하 여 MVC 동작에 대 한 액세스를 제어 하는 방법을 보여 줍니다. 먼저 기본 co를 사용 하 여 샘플 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 12/30/2009
ms.assetid: d2488a1d-0f3f-4994-8fbe-4f59b8c9503e
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-use-httpverbs-attributes-in-an-mvc-application
msc.type: video
ms.openlocfilehash: bda3b122aaf2970b9238d7120ad15fb06672c85b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432005"
---
# <a name="how-do-i-use-httpverbs-attributes-in-an-mvc-application"></a><span data-ttu-id="acf6f-105">방법: MVC 응용 프로그램에서 HttpVerbs 특성 사용</span><span class="sxs-lookup"><span data-stu-id="acf6f-105">How Do I: Use HttpVerbs Attributes in an MVC Application?</span></span>

<span data-ttu-id="acf6f-106">사람- [Chris pel](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="acf6f-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="acf6f-107">이 비디오에서 Chris Pel는 HttpVerbs 특성을 사용 하 여 MVC 동작에 대 한 액세스를 제어 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="acf6f-107">In this video Chris Pels shows how to use the HttpVerbs attributes to control access to MVC actions.</span></span> <span data-ttu-id="acf6f-108">먼저 기본 컨트롤러와 정보를 편집 하기 위한 뷰를 사용 하 여 샘플 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acf6f-108">First, a sample application is created with a default controller and view for editing the information.</span></span> <span data-ttu-id="acf6f-109">그런 다음 HTTP POST를 사용 하는 경우에만 호출 되도록 제한 하는 HttpPost 특성이 있는 컨트롤러에 두 번째 인덱스 작업이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acf6f-109">Next, a second Index action is added to the controller which has an HttpPost attribute which restricts it to being called only when an HTTP POST is used.</span></span> <span data-ttu-id="acf6f-110">추가 작업으로 AcceptVerbs () 특성은 Visual Studio 2008에 대 한 대체 구문으로 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acf6f-110">As a follow-up, the AcceptVerbs() attribute is implemented as an alternative syntax for Visual Studio 2008.</span></span> <span data-ttu-id="acf6f-111">HTTP GET을 사용 하 여 링크에서 삭제를 수행 하는 것과 관련 된 보안 위험을 방지 하기 위해 HttpVerbs를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="acf6f-111">A use of the HttpVerbs for preventing the security risk associated with using an HTTP GET to perform a delete from a link is then discussed.</span></span>

[<span data-ttu-id="acf6f-112">&#9654;비디오 보기 (16 분)</span><span class="sxs-lookup"><span data-stu-id="acf6f-112">&#9654; Watch video (16 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-httpverbs-attributes-in-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="acf6f-113">[이전](how-do-i-work-with-model-binders-in-an-mvc-application.md)
> [다음](mvc2-html-encoding.md)</span><span class="sxs-lookup"><span data-stu-id="acf6f-113">[Previous](how-do-i-work-with-model-binders-in-an-mvc-application.md)
[Next](mvc2-html-encoding.md)</span></span>
