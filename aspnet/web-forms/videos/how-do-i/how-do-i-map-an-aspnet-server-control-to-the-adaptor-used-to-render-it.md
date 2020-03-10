---
uid: web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
title: '[방법:] ASP.NET 서버 컨트롤을 렌더링 하는 데 사용 되는 어댑터에 매핑 | Microsoft Docs'
author: rick-anderson
description: 이 비디오에서 Chris Pel는 컨트롤 어댑터를 사용 하 여 실제로 c ...를 변경 하지 않고 ASP.NET 서버 컨트롤에 대해 다른 렌더링을 제공 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/19/2008
ms.assetid: d4b498ef-8e1c-4fa2-9c35-1f32f20bb9b7
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
msc.type: video
ms.openlocfilehash: 757c90fac3345b448513fb4c7cd946a3d10f3f89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473423"
---
# <a name="how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it"></a><span data-ttu-id="1f16e-103">[방법:] ASP.NET 서버 컨트롤을 렌더링 하는 데 사용 되는 어댑터에 매핑</span><span class="sxs-lookup"><span data-stu-id="1f16e-103">[How Do I:] Map an ASP.NET Server Control to the Adaptor Used to Render It</span></span>

<span data-ttu-id="1f16e-104">사람- [Chris pel](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="1f16e-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="1f16e-105">이 비디오에서 Chris Pel는 컨트롤 어댑터를 사용 하 여 실제로 컨트롤 자체를 변경 하지 않고 ASP.NET 서버 컨트롤에 대해 다른 렌더링을 제공 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f16e-105">In this video Chris Pels will show how to use a control adaptor to provide different renderings for an ASP.NET server control without actually changing the control itself.</span></span> <span data-ttu-id="1f16e-106">이 비디오에서는 기존 UL 요소 대신 DIV 요소를 사용 하 여 각 목록 항목을 가로로 표시 하도록 ASP.NET BulletList 컨트롤을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f16e-106">In this video, an ASP.NET BulletList control will be adapted to display each list item horizontally using DIV elements instead of the traditional UL elements.</span></span> <span data-ttu-id="1f16e-107">먼저 WebControlAdaptor를 상속 하는 클래스를 만드는 방법을 참조 한 다음 새 목록 형식을 렌더링 하는 코드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f16e-107">First, see how to create a class that inherits WebControlAdaptor and then implements the code to render the new list format.</span></span> <span data-ttu-id="1f16e-108">다음으로, .browser 정의 파일의 ASP.NET 서버 컨트롤에 새 컨트롤 어댑터를 매핑하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f16e-108">Next, learn how to map the new control adaptor to the ASP.NET server control in the .browser definition file.</span></span> <span data-ttu-id="1f16e-109">그런 다음 웹 사이트의 페이지에서 새 컨트롤 어댑터를 사용 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1f16e-109">Then see how to use the new control adaptor on pages in a web site.</span></span> <span data-ttu-id="1f16e-110">마지막으로, 컨트롤 어댑터를 모든 브라우저나 특정 유형의 브라우저와 연결 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f16e-110">Finally, learn how a control adaptor can be associated with either all browsers or specific types of browsers.</span></span>

[<span data-ttu-id="1f16e-111">&#9654;비디오 보기 (23 분)</span><span class="sxs-lookup"><span data-stu-id="1f16e-111">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it)
