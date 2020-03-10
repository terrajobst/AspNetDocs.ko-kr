---
uid: web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-using-web-services
title: '[방법:] 웹 서비스를 사용 하 여 지속적인 통신 패턴 구현 | Microsoft Docs'
author: JoeStagner
description: 기존 웹 사이트에서 브라우저 및 서버는 진행 중인 통신을 유지 하지 않고 동작을 수행 하는 사용자에 대 한 응답 으로만 통신 합니다.
ms.author: riande
ms.date: 08/22/2007
ms.assetid: 424c06cd-6d61-43cd-a1f2-d1a6b62e47b1
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-using-web-services
msc.type: video
ms.openlocfilehash: de2eb281cd4bab46635af480ac2e8f07f60f1591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510215"
---
# <a name="how-do-i-implement-the-persistent-communications-pattern-using-web-services"></a><span data-ttu-id="ce1fd-104">[방법:] 웹 서비스를 사용 하 여 지속적인 통신 패턴 구현</span><span class="sxs-lookup"><span data-stu-id="ce1fd-104">[How Do I:] Implement the Persistent Communications Pattern using Web Services?</span></span>

<span data-ttu-id="ce1fd-105">만든 사람 [Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="ce1fd-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="ce1fd-106">기존 웹 사이트에서 브라우저 및 서버는 진행 중인 통신을 유지 하지 않고 동작을 수행 하는 사용자에 대 한 응답 으로만 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1fd-106">In a traditional Web site the browser and the server do not maintain an ongoing communication, but communicate only in response to the user performing an action.</span></span> <span data-ttu-id="ce1fd-107">페이지가 응용 프로그램 컨테이너가 되는 최신 웹 사이트에서 사용자가 작업을 수행 하지 않고도 페이지 업데이트를 수행할 수 있도록 브라우저 및 서버에서 지속적인 통신을 유지 하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce1fd-107">In a modern Web site where the page becomes an application container, it can be advantageous for the browser and the server to maintain an ongoing communication so that page updates can occur without the user performing an action.</span></span> <span data-ttu-id="ce1fd-108">이를 AJAX에 대 한 영구 통신 패턴 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1fd-108">This is known as the Persistent Communications Pattern for AJAX.</span></span> <span data-ttu-id="ce1fd-109">ASP.NET AJAX는 웹 개발자가 지속적인 통신 패턴을 구현 하는 두 가지 주요 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1fd-109">ASP.NET AJAX provides two main ways for Web developers to implement the Persistent Communications Pattern.</span></span> <span data-ttu-id="ce1fd-110">이전 비디오에서는 ASP.NET AJAX UpdatePanel을 구현의 기반으로 사용 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ce1fd-110">In an earlier video we saw how to use the ASP.NET AJAX UpdatePanel as the basis of the implementation.</span></span> <span data-ttu-id="ce1fd-111">이 비디오에서는 웹 서비스에 대 한 JavaScrpt 호출을 사용 하 여 동일한 패턴을 구현 하는 방법에 대해 설명 합니다 .이를 통해 ASP.NET AJAX UpdatePanel이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce1fd-111">In this video we learn how to implement the same pattern using a JavaScrpt call to a Web service, which removes the need for an ASP.NET AJAX UpdatePanel.</span></span>

[<span data-ttu-id="ce1fd-112">&#9654;비디오 보기 (16 분)</span><span class="sxs-lookup"><span data-stu-id="ce1fd-112">&#9654; Watch video (16 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-the-persistent-communications-pattern-using-web-services)

> [!div class="step-by-step"]
> <span data-ttu-id="ce1fd-113">[이전](how-do-i-localize-an-aspnet-ajax-application.md)
> [다음](how-do-i-trigger-an-updatepanel-refresh-from-a-dropdownlist-control.md)</span><span class="sxs-lookup"><span data-stu-id="ce1fd-113">[Previous](how-do-i-localize-an-aspnet-ajax-application.md)
[Next](how-do-i-trigger-an-updatepanel-refresh-from-a-dropdownlist-control.md)</span></span>
